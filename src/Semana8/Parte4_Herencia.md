# Parte 4: Aplicando Herencia - Jerarquía de Productos

Hasta ahora hemos estado manejando pizzas y bebidas como simples Strings en arrays. Pero pizzas y bebidas tienen características comunes (precio, nombre) y características únicas (ingredientes para pizzas, tamaño para bebidas). La herencia nos permite modelar esto de forma elegante.

## ¿Por Qué Usar Herencia?

Imagina que tienes código repetido: tanto Pizza como Bebida necesitan nombre y precio. En lugar de escribir el mismo código dos veces, creamos una clase padre `Producto` con lo común, y las clases hijas heredan eso y agregan sus propias características.

Ventajas:
- Evitamos duplicar código
- Organizamos mejor las relaciones entre clases
- Facilitamos el mantenimiento y la expansión

## Paso 1: Crear la Clase Base Producto

Primero creamos la clase padre que tendrá todo lo que comparten todos los productos.

En NetBeans:
1. Clic derecho en `sistemapizzeria`
2. New → Java Class
3. Nombre: `Producto`

```java
package sistemapizzeria;

public class Producto {

    // Estos son los atributos comunes a todos los productos de la pizzeria.
    // Tanto pizzas como bebidas tienen un nombre y un precio.
    // Los hacemos protected en lugar de private.
    // protected significa que las clases hijas pueden acceder directamente a estos atributos.
    // Si fueran private, las clases hijas no podrian verlos directamente.
    protected String nombre;
    protected int precio;

    // Constructor de la clase padre.
    // Este constructor sera llamado por las clases hijas para inicializar los atributos comunes.
    public Producto(String nombre, int precio) {

        // Validamos que el nombre no este vacio.
        // Esta validacion beneficia a todas las clases hijas automaticamente.
        if (nombre == null || nombre.trim().isEmpty()) {
            System.out.println("Advertencia: El nombre no puede estar vacio. Se usara 'Sin Nombre'.");
            this.nombre = "Sin Nombre";
        } else {
            this.nombre = nombre;
        }

        // Validamos que el precio sea razonable.
        if (precio < 0) {
            System.out.println("Advertencia: El precio no puede ser negativo. Se ajustara a 0.");
            this.precio = 0;
        } else {
            this.precio = precio;
        }
    }

    // Getters para acceder a los atributos.
    // Estos metodos seran heredados por las clases hijas.
    public String getNombre() {
        return nombre;
    }

    public int getPrecio() {
        return precio;
    }

    // Setters con validacion.
    public void setNombre(String nombre) {
        if (nombre != null && !nombre.trim().isEmpty()) {
            this.nombre = nombre;
        } else {
            System.out.println("Error: El nombre no puede estar vacio.");
        }
    }

    public void setPrecio(int precio) {
        if (precio >= 0) {
            this.precio = precio;
        } else {
            System.out.println("Error: El precio no puede ser negativo.");
        }
    }

    // Este metodo sera sobrescrito por las clases hijas.
    // Cada tipo de producto mostrara su informacion de forma diferente.
    // Por ahora damos una implementacion basica.
    public void mostrarInformacion() {
        System.out.println("Producto: " + nombre);
        System.out.println("Precio: $" + precio);
    }

    // Metodo para aplicar un descuento.
    // Este metodo es util para todas las clases hijas.
    public void aplicarDescuento(int porcentaje) {

        // Validamos que el porcentaje sea razonable.
        if (porcentaje < 0 || porcentaje > 100) {
            System.out.println("Error: El porcentaje debe estar entre 0 y 100.");
            return;
        }

        // Calculamos el nuevo precio con el descuento.
        int descuento = (precio * porcentaje) / 100;
        precio = precio - descuento;

        System.out.println("Descuento de " + porcentaje + "% aplicado. Nuevo precio: $" + precio);
    }

    @Override
    public String toString() {
        return nombre + " - $" + precio;
    }
}
```

## Paso 2: Crear la Clase Pizza que Hereda de Producto

Ahora creamos Pizza que extiende de Producto y agrega características específicas.

En NetBeans:
1. Clic derecho en `sistemapizzeria`
2. New → Java Class
3. Nombre: `Pizza`

```java
package sistemapizzeria;

import java.util.ArrayList;

public class Pizza extends Producto {

    // La palabra extends indica que Pizza hereda de Producto.
    // Pizza automaticamente tiene nombre y precio porque los hereda.
    // Ahora agregamos atributos especificos de una pizza.

    // El tamaño de la pizza: Personal, Mediana, Familiar.
    private String tamanio;

    // Los ingredientes que lleva la pizza.
    // Usamos ArrayList porque la cantidad de ingredientes puede variar.
    private ArrayList<String> ingredientes;

    // Indica si la pizza es de masa delgada o gruesa.
    private String tipoMasa;

    // Constructor de Pizza.
    // Recibe los parametros comunes (nombre y precio) mas los especificos de pizza.
    public Pizza(String nombre, int precio, String tamanio, String tipoMasa) {

        // super() llama al constructor de la clase padre (Producto).
        // Esto inicializa nombre y precio usando la logica que ya definimos en Producto.
        // super() DEBE ser la primera linea del constructor de la clase hija.
        super(nombre, precio);

        // Ahora inicializamos los atributos especificos de Pizza.
        this.tamanio = tamanio;
        this.tipoMasa = tipoMasa;

        // Creamos el ArrayList vacio para los ingredientes.
        // Los ingredientes se agregaran despues con el metodo agregarIngrediente().
        this.ingredientes = new ArrayList<>();
    }

    // Getters para los atributos especificos de Pizza.
    public String getTamanio() {
        return tamanio;
    }

    public String getTipoMasa() {
        return tipoMasa;
    }

    public ArrayList<String> getIngredientes() {
        return ingredientes;
    }

    // Setters con validacion.
    public void setTamanio(String tamanio) {
        // Solo permitimos ciertos tamaños.
        String[] tamaniosValidos = {"Personal", "Mediana", "Familiar"};
        boolean esValido = false;

        for (String t : tamaniosValidos) {
            if (t.equalsIgnoreCase(tamanio)) {
                esValido = true;
                break;
            }
        }

        if (esValido) {
            this.tamanio = tamanio;
        } else {
            System.out.println("Error: Tamanio invalido. Use: Personal, Mediana o Familiar");
        }
    }

    public void setTipoMasa(String tipoMasa) {
        this.tipoMasa = tipoMasa;
    }

    // Metodo para agregar un ingrediente a la pizza.
    public void agregarIngrediente(String ingrediente) {
        if (ingrediente != null && !ingrediente.trim().isEmpty()) {
            ingredientes.add(ingrediente);
            System.out.println("Ingrediente agregado: " + ingrediente);
        } else {
            System.out.println("Error: El ingrediente no puede estar vacio.");
        }
    }

    // Metodo para quitar un ingrediente.
    // Util para clientes con alergias o preferencias.
    public boolean quitarIngrediente(String ingrediente) {
        if (ingredientes.remove(ingrediente)) {
            System.out.println("Ingrediente quitado: " + ingrediente);
            return true;
        } else {
            System.out.println("El ingrediente no se encontro en la pizza.");
            return false;
        }
    }

    // Aqui sobrescribimos el metodo mostrarInformacion() del padre.
    // @Override es una anotacion que indica que estamos reemplazando un metodo del padre.
    // Esto nos da una version especializada para Pizza.
    @Override
    public void mostrarInformacion() {
        System.out.println("\n========== PIZZA ==========");
        System.out.println("Nombre: " + nombre);
        System.out.println("Precio: $" + precio);
        System.out.println("Tamanio: " + tamanio);
        System.out.println("Tipo de Masa: " + tipoMasa);

        // Mostramos los ingredientes.
        if (ingredientes.isEmpty()) {
            System.out.println("Ingredientes: Sin ingredientes");
        } else {
            System.out.println("Ingredientes:");
            for (String ing : ingredientes) {
                System.out.println("  - " + ing);
            }
        }

        System.out.println("===========================\n");
    }

    // Sobrescribimos toString tambien para dar mas informacion.
    @Override
    public String toString() {
        return String.format("Pizza %s (%s) - %s - $%d - %d ingredientes",
            nombre,
            tamanio,
            tipoMasa,
            precio,
            ingredientes.size()
        );
    }
}
```

## Paso 3: Crear la Clase Bebida que Hereda de Producto

Ahora creamos Bebida, otra clase hija de Producto con sus propias características.

En NetBeans:
1. Clic derecho en `sistemapizzeria`
2. New → Java Class
3. Nombre: `Bebida`

```java
package sistemapizzeria;

public class Bebida extends Producto {

    // Bebida tambien extiende de Producto.
    // Hereda nombre y precio automaticamente.
    // Agregamos atributos especificos de bebidas.

    // El tamaño de la bebida en mililitros.
    private int mililitros;

    // Si la bebida tiene gas o no.
    private boolean esGaseosa;

    // La marca de la bebida.
    private String marca;

    // Constructor de Bebida.
    public Bebida(String nombre, int precio, int mililitros, boolean esGaseosa, String marca) {

        // Llamamos al constructor del padre para inicializar nombre y precio.
        // super() usa la validacion que ya definimos en Producto.
        super(nombre, precio);

        // Inicializamos los atributos especificos de Bebida.
        this.mililitros = mililitros;
        this.esGaseosa = esGaseosa;
        this.marca = marca;
    }

    // Getters para los atributos especificos.
    public int getMililitros() {
        return mililitros;
    }

    public boolean isEsGaseosa() {
        // Para booleanos se usa is en lugar de get.
        return esGaseosa;
    }

    public String getMarca() {
        return marca;
    }

    // Setters con validacion.
    public void setMililitros(int mililitros) {
        if (mililitros > 0) {
            this.mililitros = mililitros;
        } else {
            System.out.println("Error: Los mililitros deben ser positivos.");
        }
    }

    public void setEsGaseosa(boolean esGaseosa) {
        this.esGaseosa = esGaseosa;
    }

    public void setMarca(String marca) {
        if (marca != null && !marca.trim().isEmpty()) {
            this.marca = marca;
        } else {
            System.out.println("Error: La marca no puede estar vacia.");
        }
    }

    // Sobrescribimos mostrarInformacion() con una version para Bebida.
    @Override
    public void mostrarInformacion() {
        System.out.println("\n========== BEBIDA ==========");
        System.out.println("Nombre: " + nombre);
        System.out.println("Marca: " + marca);
        System.out.println("Precio: $" + precio);
        System.out.println("Tamanio: " + mililitros + "ml");
        System.out.println("Tipo: " + (esGaseosa ? "Gaseosa" : "Sin Gas"));
        System.out.println("============================\n");
    }

    // Sobrescribimos toString.
    @Override
    public String toString() {
        return String.format("Bebida %s %s (%dml) - $%d - %s",
            marca,
            nombre,
            mililitros,
            precio,
            (esGaseosa ? "Gaseosa" : "Sin Gas")
        );
    }
}
```

## Paso 4: Usar la Jerarquía en el Sistema

Ahora modificamos `SistemaPizzeria.java` para usar estas clases con herencia:

```java
package sistemapizzeria;

import java.util.Scanner;
import java.util.ArrayList;

public class SistemaPizzeria {

    // Ahora usamos ArrayList de tipo Producto.
    // Aqui esta la magia del polimorfismo: un ArrayList<Producto> puede contener
    // tanto objetos Pizza como objetos Bebida, porque ambos son hijos de Producto.
    private static ArrayList<Producto> menuProductos = new ArrayList<>();

    private static ArrayList<Pedido> historialPedidos = new ArrayList<>();
    private static int contadorPedidos = 1;

    public static void main(String[] args) {

        // Inicializamos el menu con productos.
        // Vamos a crear algunos objetos de ejemplo.
        inicializarMenu();

        Scanner scanner = new Scanner(System.in);
        boolean sistemaActivo = true;

        while (sistemaActivo) {

            System.out.println("\n////////////////////////////////////////");
            System.out.println("///   PIZZERIA BELLA NAPOLI         ///");
            System.out.println("////////////////////////////////////////");
            System.out.println("1. Ver Todos los Productos");
            System.out.println("2. Ver Solo Pizzas");
            System.out.println("3. Ver Solo Bebidas");
            System.out.println("4. Ver Detalle de un Producto");
            System.out.println("5. Crear Nueva Pizza");
            System.out.println("6. Crear Nueva Bebida");
            System.out.println("7. Aplicar Descuento a Producto");
            System.out.println("8. Salir");
            System.out.println("////////////////////////////////////////");
            System.out.print("Seleccione una opcion: ");

            int opcion = scanner.nextInt();
            scanner.nextLine();

            switch (opcion) {
                case 1:
                    mostrarTodosLosProductos();
                    break;

                case 2:
                    mostrarSoloPizzas();
                    break;

                case 3:
                    mostrarSoloBebidas();
                    break;

                case 4:
                    verDetalleProducto(scanner);
                    break;

                case 5:
                    crearNuevaPizza(scanner);
                    break;

                case 6:
                    crearNuevaBebida(scanner);
                    break;

                case 7:
                    aplicarDescuentoProducto(scanner);
                    break;

                case 8:
                    System.out.println("\nGracias por usar el Sistema Pizzeria Bella Napoli!");
                    System.out.println("Hasta pronto!");
                    sistemaActivo = false;
                    break;

                default:
                    System.out.println("\nOpcion invalida.");
            }
        }

        scanner.close();
    }

    // Metodo para inicializar algunos productos de ejemplo.
    public static void inicializarMenu() {

        // Creamos algunas pizzas.
        // Usamos el constructor de Pizza que llama a super() internamente.
        Pizza margarita = new Pizza("Margarita", 5990, "Mediana", "Delgada");
        margarita.agregarIngrediente("Tomate");
        margarita.agregarIngrediente("Queso Mozzarella");
        margarita.agregarIngrediente("Albahaca");
        menuProductos.add(margarita);

        Pizza pepperoni = new Pizza("Pepperoni", 6990, "Familiar", "Gruesa");
        pepperoni.agregarIngrediente("Tomate");
        pepperoni.agregarIngrediente("Queso");
        pepperoni.agregarIngrediente("Pepperoni");
        menuProductos.add(pepperoni);

        // Creamos algunas bebidas.
        // Usamos el constructor de Bebida que tambien llama a super().
        Bebida cocaCola = new Bebida("Coca-Cola", 1500, 500, true, "Coca-Cola");
        menuProductos.add(cocaCola);

        Bebida agua = new Bebida("Agua Mineral", 1000, 500, false, "Vital");
        menuProductos.add(agua);

        System.out.println("Menu inicializado con " + menuProductos.size() + " productos.");
    }

    // Metodo para mostrar todos los productos.
    public static void mostrarTodosLosProductos() {

        System.out.println("\n////////////////////////////////////////");
        System.out.println("///      TODOS LOS PRODUCTOS        ///");
        System.out.println("////////////////////////////////////////");

        if (menuProductos.isEmpty()) {
            System.out.println("No hay productos en el menu.");
            return;
        }

        // Recorremos todos los productos.
        // Algunos seran Pizza, otros Bebida, pero todos son Producto.
        for (int i = 0; i < menuProductos.size(); i++) {
            System.out.println((i + 1) + ". " + menuProductos.get(i));
        }
    }

    // Metodo para mostrar solo las pizzas.
    // Aqui usamos instanceof para verificar el tipo real del objeto.
    public static void mostrarSoloPizzas() {

        System.out.println("\n////////////////////////////////////////");
        System.out.println("///         SOLO PIZZAS             ///");
        System.out.println("////////////////////////////////////////");

        int contador = 0;

        // Recorremos todos los productos.
        for (Producto p : menuProductos) {

            // instanceof verifica si un objeto es de un tipo especifico.
            // Si p es realmente una Pizza, entramos al if.
            if (p instanceof Pizza) {
                contador++;
                System.out.println(contador + ". " + p);
            }
        }

        if (contador == 0) {
            System.out.println("No hay pizzas en el menu.");
        }
    }

    // Metodo para mostrar solo las bebidas.
    public static void mostrarSoloBebidas() {

        System.out.println("\n////////////////////////////////////////");
        System.out.println("///        SOLO BEBIDAS             ///");
        System.out.println("////////////////////////////////////////");

        int contador = 0;

        for (Producto p : menuProductos) {
            // Verificamos si el producto es una Bebida.
            if (p instanceof Bebida) {
                contador++;
                System.out.println(contador + ". " + p);
            }
        }

        if (contador == 0) {
            System.out.println("No hay bebidas en el menu.");
        }
    }

    // Metodo para ver el detalle completo de un producto.
    public static void verDetalleProducto(Scanner scanner) {

        mostrarTodosLosProductos();

        if (menuProductos.isEmpty()) {
            return;
        }

        System.out.print("\nIngrese el numero del producto: ");
        int numero = scanner.nextInt();
        scanner.nextLine();

        if (numero < 1 || numero > menuProductos.size()) {
            System.out.println("Numero invalido.");
            return;
        }

        // Obtenemos el producto y llamamos a mostrarInformacion().
        // Aunque menuProductos es de tipo Producto, si el objeto real es Pizza,
        // se ejecutara mostrarInformacion() de Pizza gracias al polimorfismo.
        Producto producto = menuProductos.get(numero - 1);
        producto.mostrarInformacion();
    }

    // Metodo para crear una nueva pizza.
    public static void crearNuevaPizza(Scanner scanner) {

        System.out.println("\n////////////////////////////////////////");
        System.out.println("///      CREAR NUEVA PIZZA          ///");
        System.out.println("////////////////////////////////////////");

        System.out.print("Nombre de la pizza: ");
        String nombre = scanner.nextLine();

        System.out.print("Precio: ");
        int precio = scanner.nextInt();
        scanner.nextLine();

        System.out.print("Tamanio (Personal/Mediana/Familiar): ");
        String tamanio = scanner.nextLine();

        System.out.print("Tipo de masa (Delgada/Gruesa): ");
        String tipoMasa = scanner.nextLine();

        // Creamos la nueva pizza.
        Pizza nuevaPizza = new Pizza(nombre, precio, tamanio, tipoMasa);

        // Agregamos ingredientes.
        System.out.println("\nAgregar ingredientes (deje vacio para terminar):");
        boolean agregando = true;

        while (agregando) {
            System.out.print("Ingrediente: ");
            String ingrediente = scanner.nextLine();

            if (ingrediente.trim().isEmpty()) {
                agregando = false;
            } else {
                nuevaPizza.agregarIngrediente(ingrediente);
            }
        }

        // Agregamos la pizza al menu.
        menuProductos.add(nuevaPizza);
        System.out.println("\nPizza creada exitosamente!");
        nuevaPizza.mostrarInformacion();
    }

    // Metodo para crear una nueva bebida.
    public static void crearNuevaBebida(Scanner scanner) {

        System.out.println("\n////////////////////////////////////////");
        System.out.println("///      CREAR NUEVA BEBIDA         ///");
        System.out.println("////////////////////////////////////////");

        System.out.print("Nombre de la bebida: ");
        String nombre = scanner.nextLine();

        System.out.print("Marca: ");
        String marca = scanner.nextLine();

        System.out.print("Precio: ");
        int precio = scanner.nextInt();

        System.out.print("Mililitros: ");
        int ml = scanner.nextInt();

        System.out.print("Es gaseosa? (true/false): ");
        boolean esGaseosa = scanner.nextBoolean();
        scanner.nextLine();

        // Creamos la nueva bebida.
        Bebida nuevaBebida = new Bebida(nombre, precio, ml, esGaseosa, marca);

        // Agregamos al menu.
        menuProductos.add(nuevaBebida);
        System.out.println("\nBebida creada exitosamente!");
        nuevaBebida.mostrarInformacion();
    }

    // Metodo para aplicar descuento a un producto.
    // Funciona tanto para pizzas como para bebidas porque heredan el metodo.
    public static void aplicarDescuentoProducto(Scanner scanner) {

        mostrarTodosLosProductos();

        if (menuProductos.isEmpty()) {
            return;
        }

        System.out.print("\nIngrese el numero del producto: ");
        int numero = scanner.nextInt();

        System.out.print("Ingrese el porcentaje de descuento: ");
        int porcentaje = scanner.nextInt();
        scanner.nextLine();

        if (numero < 1 || numero > menuProductos.size()) {
            System.out.println("Numero invalido.");
            return;
        }

        // Aplicamos el descuento.
        // El metodo aplicarDescuento() esta definido en Producto,
        // entonces funciona para cualquier hijo.
        Producto producto = menuProductos.get(numero - 1);
        System.out.println("\nAplicando descuento a: " + producto.getNombre());
        producto.aplicarDescuento(porcentaje);
    }
}
```

## Conceptos Clave de Herencia

### 1. Extends
La palabra clave `extends` establece la relación de herencia entre clases.

### 2. Super()
`super()` llama al constructor de la clase padre y debe ser la primera línea del constructor hijo.

### 3. Protected
Los atributos `protected` son visibles para las clases hijas, a diferencia de `private`.

### 4. @Override
Indica que estamos reemplazando un método del padre con una versión especializada.

### 5. instanceof
Permite verificar el tipo real de un objeto en tiempo de ejecución.

### 6. Polimorfismo Básico
Un ArrayList<Producto> puede contener tanto Pizza como Bebida, ambas hijas de Producto.

## Probando la Herencia

Ejecuta y prueba:
1. Ver todos los productos (mezcla de pizzas y bebidas)
2. Filtrar solo pizzas o solo bebidas
3. Ver el detalle completo de diferentes productos
4. Crear nuevas pizzas y bebidas
5. Aplicar descuentos a diferentes tipos de productos

## Lo que Viene

En la siguiente y última parte, vamos a aplicar polimorfismo avanzado:
- Convertir `Producto` en una clase abstracta
- Crear interfaces `Personalizable` y `Promocionable`
- Implementar métodos abstractos en las clases hijas
- Sistema completo con todas las características POO

Ya tenemos ciclos, encapsulación, colecciones y herencia. Solo falta el polimorfismo avanzado para completar todos los conceptos.

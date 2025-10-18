# Parte 5: Polimorfismo Avanzado - Clases Abstractas e Interfaces

Esta es la última parte de nuestro tutorial. Vamos a transformar nuestra jerarquía de productos aplicando polimorfismo avanzado. Convertiremos `Producto` en una clase abstracta y crearemos interfaces que definan comportamientos específicos.

## ¿Qué es una Clase Abstracta?

Hasta ahora Producto era una clase normal que podíamos instanciar directamente. Pero en la realidad, nunca vendemos un "Producto" genérico, siempre vendemos Pizza o Bebida específicas. Una clase abstracta nos permite:
- Definir métodos que DEBEN ser implementados por las clases hijas
- Prohibir la creación directa de objetos de la clase padre
- Compartir código común entre clases hijas

## ¿Qué es una Interfaz?

Una interfaz es como un contrato. Define QUÉ debe hacer una clase, pero no CÓMO lo hace. Por ejemplo:
- `Personalizable`: Cualquier producto que pueda ser personalizado debe implementar estos métodos
- `Promocionable`: Cualquier producto que pueda tener promociones debe implementar estos métodos

## Paso 1: Convertir Producto en Clase Abstracta

Modificamos la clase `Producto.java` existente:

```java
package sistemapizzeria;

// Agregamos la palabra abstract antes de class.
// Esto convierte a Producto en una clase abstracta.
// Ya no podremos hacer: new Producto("algo", 100)
// Solo podremos crear objetos de las clases hijas: Pizza y Bebida.
public abstract class Producto {

    protected String nombre;
    protected int precio;

    // Constructor de la clase abstracta.
    // No se puede llamar directamente, pero las clases hijas lo usan con super().
    public Producto(String nombre, int precio) {
        if (nombre == null || nombre.trim().isEmpty()) {
            System.out.println("Advertencia: El nombre no puede estar vacio. Se usara 'Sin Nombre'.");
            this.nombre = "Sin Nombre";
        } else {
            this.nombre = nombre;
        }

        if (precio < 0) {
            System.out.println("Advertencia: El precio no puede ser negativo. Se ajustara a 0.");
            this.precio = 0;
        } else {
            this.precio = precio;
        }
    }

    public String getNombre() {
        return nombre;
    }

    public int getPrecio() {
        return precio;
    }

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

    // Este es un metodo abstracto.
    // No tiene cuerpo (no tiene llaves con codigo).
    // Solo define la firma del metodo.
    // Todas las clases hijas DEBEN implementar este metodo.
    // Si una clase hija no lo implementa, dara error de compilacion.
    public abstract void mostrarInformacion();

    // Este es otro metodo abstracto.
    // Cada tipo de producto calculara su tiempo de preparacion de forma diferente.
    // Pizza podria depender de la cantidad de ingredientes.
    // Bebida podria ser siempre un tiempo fijo.
    public abstract int calcularTiempoPreparacion();

    // Este metodo NO es abstracto, tiene implementacion.
    // Las clases hijas lo heredan y pueden usarlo directamente.
    // Pero tambien pueden sobrescribirlo si quieren una version diferente.
    public void aplicarDescuento(int porcentaje) {
        if (porcentaje < 0 || porcentaje > 100) {
            System.out.println("Error: El porcentaje debe estar entre 0 y 100.");
            return;
        }

        int descuento = (precio * porcentaje) / 100;
        precio = precio - descuento;

        System.out.println("Descuento de " + porcentaje + "% aplicado. Nuevo precio: $" + precio);
    }

    // toString no es abstracto, pero las clases hijas lo sobrescriben.
    @Override
    public String toString() {
        return nombre + " - $" + precio;
    }
}
```

## Paso 2: Crear la Interfaz Personalizable

Las interfaces se crean igual que las clases, pero usando la palabra `interface`.

En NetBeans:
1. Clic derecho en `sistemapizzeria`
2. New → Java Interface (no Java Class)
3. Nombre: `Personalizable`

```java
package sistemapizzeria;

import java.util.ArrayList;

// Una interfaz define metodos que las clases deben implementar.
// Todos los metodos en una interfaz son automaticamente public y abstract.
// No necesitamos escribir esas palabras, Java las asume.
public interface Personalizable {

    // Este metodo debe permitir agregar personalizaciones al producto.
    // Por ejemplo, ingredientes extra en una pizza o hielo en una bebida.
    void agregarPersonalizacion(String personalizacion);

    // Este metodo debe quitar una personalizacion.
    boolean quitarPersonalizacion(String personalizacion);

    // Este metodo debe devolver todas las personalizaciones.
    ArrayList<String> obtenerPersonalizaciones();

    // Este metodo calcula el costo adicional de las personalizaciones.
    int calcularCostoPersonalizacion();
}
```

## Paso 3: Crear la Interfaz Promocionable

En NetBeans:
1. Clic derecho en `sistemapizzeria`
2. New → Java Interface
3. Nombre: `Promocionable`

```java
package sistemapizzeria;

// Esta interfaz define comportamientos para productos que pueden tener promociones.
public interface Promocionable {

    // Aplicar una promocion especial al producto.
    // Por ejemplo: "2x1", "50% descuento", etc.
    void aplicarPromocion(String tipoPromocion);

    // Verificar si el producto actualmente tiene alguna promocion activa.
    boolean tienePromocionActiva();

    // Obtener la descripcion de la promocion actual.
    String obtenerDescripcionPromocion();

    // Remover la promocion activa.
    void removerPromocion();
}
```

## Paso 4: Modificar Pizza para Implementar las Interfaces

Ahora modificamos `Pizza.java` para que implemente ambas interfaces:

```java
package sistemapizzeria;

import java.util.ArrayList;

// Pizza extiende de Producto e implementa dos interfaces.
// extends va primero, implements despues.
// Podemos implementar multiples interfaces separadas por comas.
// Pero solo podemos extender de una clase.
public class Pizza extends Producto implements Personalizable, Promocionable {

    private String tamanio;
    private ArrayList<String> ingredientes;
    private String tipoMasa;

    // Nuevos atributos para las interfaces.
    // Para Personalizable necesitamos guardar las personalizaciones.
    private ArrayList<String> personalizaciones;

    // Para Promocionable necesitamos guardar la promocion actual.
    private String promocionActiva;
    private boolean tienePromocion;

    public Pizza(String nombre, int precio, String tamanio, String tipoMasa) {
        super(nombre, precio);
        this.tamanio = tamanio;
        this.tipoMasa = tipoMasa;
        this.ingredientes = new ArrayList<>();

        // Inicializamos los atributos de las interfaces.
        this.personalizaciones = new ArrayList<>();
        this.promocionActiva = null;
        this.tienePromocion = false;
    }

    public String getTamanio() {
        return tamanio;
    }

    public String getTipoMasa() {
        return tipoMasa;
    }

    public ArrayList<String> getIngredientes() {
        return ingredientes;
    }

    public void setTamanio(String tamanio) {
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

    public void agregarIngrediente(String ingrediente) {
        if (ingrediente != null && !ingrediente.trim().isEmpty()) {
            ingredientes.add(ingrediente);
        }
    }

    public boolean quitarIngrediente(String ingrediente) {
        return ingredientes.remove(ingrediente);
    }

    // Implementamos el metodo abstracto de Producto.
    // Esto es obligatorio porque Producto lo define como abstract.
    @Override
    public void mostrarInformacion() {
        System.out.println("\n========== PIZZA ==========");
        System.out.println("Nombre: " + nombre);
        System.out.println("Precio Base: $" + precio);

        // Mostramos el costo adicional de personalizaciones si hay.
        if (!personalizaciones.isEmpty()) {
            System.out.println("Costo Personalizacion: $" + calcularCostoPersonalizacion());
            System.out.println("Precio Total: $" + (precio + calcularCostoPersonalizacion()));
        }

        System.out.println("Tamanio: " + tamanio);
        System.out.println("Tipo de Masa: " + tipoMasa);

        if (ingredientes.isEmpty()) {
            System.out.println("Ingredientes: Sin ingredientes");
        } else {
            System.out.println("Ingredientes:");
            for (String ing : ingredientes) {
                System.out.println("  - " + ing);
            }
        }

        // Mostramos las personalizaciones si hay.
        if (!personalizaciones.isEmpty()) {
            System.out.println("Personalizaciones:");
            for (String p : personalizaciones) {
                System.out.println("  + " + p);
            }
        }

        // Mostramos la promocion si hay.
        if (tienePromocion) {
            System.out.println("PROMOCION ACTIVA: " + promocionActiva);
        }

        System.out.println("Tiempo de Preparacion: " + calcularTiempoPreparacion() + " minutos");
        System.out.println("===========================\n");
    }

    // Implementamos el otro metodo abstracto de Producto.
    // Para una pizza, el tiempo depende de cuantos ingredientes tiene.
    @Override
    public int calcularTiempoPreparacion() {
        // Tiempo base de 15 minutos.
        int tiempoBase = 15;

        // Agregamos 1 minuto por cada ingrediente.
        int tiempoPorIngredientes = ingredientes.size();

        // Si tiene muchas personalizaciones, toma mas tiempo.
        int tiempoPorPersonalizaciones = personalizaciones.size() * 2;

        return tiempoBase + tiempoPorIngredientes + tiempoPorPersonalizaciones;
    }

    // Ahora implementamos los metodos de la interfaz Personalizable.
    // Esto es obligatorio porque declaramos que Pizza implements Personalizable.
    @Override
    public void agregarPersonalizacion(String personalizacion) {
        if (personalizacion != null && !personalizacion.trim().isEmpty()) {
            personalizaciones.add(personalizacion);
            System.out.println("Personalizacion agregada: " + personalizacion);
        } else {
            System.out.println("Error: La personalizacion no puede estar vacia.");
        }
    }

    @Override
    public boolean quitarPersonalizacion(String personalizacion) {
        if (personalizaciones.remove(personalizacion)) {
            System.out.println("Personalizacion quitada: " + personalizacion);
            return true;
        } else {
            System.out.println("No se encontro esa personalizacion.");
            return false;
        }
    }

    @Override
    public ArrayList<String> obtenerPersonalizaciones() {
        return personalizaciones;
    }

    @Override
    public int calcularCostoPersonalizacion() {
        // Cada personalizacion cuesta 500 pesos adicionales.
        return personalizaciones.size() * 500;
    }

    // Ahora implementamos los metodos de la interfaz Promocionable.
    @Override
    public void aplicarPromocion(String tipoPromocion) {
        if (tipoPromocion == null || tipoPromocion.trim().isEmpty()) {
            System.out.println("Error: Debe especificar el tipo de promocion.");
            return;
        }

        this.promocionActiva = tipoPromocion;
        this.tienePromocion = true;

        System.out.println("Promocion aplicada: " + tipoPromocion);

        // Podriamos aplicar logica adicional segun el tipo de promocion.
        // Por ejemplo, si es "2x1" podriamos ajustar el precio.
        if (tipoPromocion.equalsIgnoreCase("2x1")) {
            System.out.println("Lleve 2 pizzas y pague 1!");
        } else if (tipoPromocion.equalsIgnoreCase("Happy Hour")) {
            aplicarDescuento(30);
        }
    }

    @Override
    public boolean tienePromocionActiva() {
        return tienePromocion;
    }

    @Override
    public String obtenerDescripcionPromocion() {
        if (tienePromocion) {
            return promocionActiva;
        } else {
            return "Sin promocion";
        }
    }

    @Override
    public void removerPromocion() {
        if (tienePromocion) {
            System.out.println("Promocion removida: " + promocionActiva);
            this.promocionActiva = null;
            this.tienePromocion = false;
        } else {
            System.out.println("No hay promocion activa para remover.");
        }
    }

    @Override
    public String toString() {
        String promo = tienePromocion ? " [PROMO: " + promocionActiva + "]" : "";
        return String.format("Pizza %s (%s) - %s - $%d%s",
            nombre,
            tamanio,
            tipoMasa,
            precio,
            promo
        );
    }
}
```

## Paso 5: Modificar Bebida para Implementar las Interfaces

Ahora modificamos `Bebida.java`:

```java
package sistemapizzeria;

import java.util.ArrayList;

// Bebida tambien implementa ambas interfaces.
public class Bebida extends Producto implements Personalizable, Promocionable {

    private int mililitros;
    private boolean esGaseosa;
    private String marca;

    // Atributos para las interfaces.
    private ArrayList<String> personalizaciones;
    private String promocionActiva;
    private boolean tienePromocion;

    public Bebida(String nombre, int precio, int mililitros, boolean esGaseosa, String marca) {
        super(nombre, precio);
        this.mililitros = mililitros;
        this.esGaseosa = esGaseosa;
        this.marca = marca;

        this.personalizaciones = new ArrayList<>();
        this.promocionActiva = null;
        this.tienePromocion = false;
    }

    public int getMililitros() {
        return mililitros;
    }

    public boolean isEsGaseosa() {
        return esGaseosa;
    }

    public String getMarca() {
        return marca;
    }

    public void setMililitros(int mililitros) {
        if (mililitros > 0) {
            this.mililitros = mililitros;
        }
    }

    public void setEsGaseosa(boolean esGaseosa) {
        this.esGaseosa = esGaseosa;
    }

    public void setMarca(String marca) {
        if (marca != null && !marca.trim().isEmpty()) {
            this.marca = marca;
        }
    }

    // Implementamos el metodo abstracto mostrarInformacion.
    @Override
    public void mostrarInformacion() {
        System.out.println("\n========== BEBIDA ==========");
        System.out.println("Nombre: " + nombre);
        System.out.println("Marca: " + marca);
        System.out.println("Precio Base: $" + precio);

        if (!personalizaciones.isEmpty()) {
            System.out.println("Costo Personalizacion: $" + calcularCostoPersonalizacion());
            System.out.println("Precio Total: $" + (precio + calcularCostoPersonalizacion()));
        }

        System.out.println("Tamanio: " + mililitros + "ml");
        System.out.println("Tipo: " + (esGaseosa ? "Gaseosa" : "Sin Gas"));

        if (!personalizaciones.isEmpty()) {
            System.out.println("Personalizaciones:");
            for (String p : personalizaciones) {
                System.out.println("  + " + p);
            }
        }

        if (tienePromocion) {
            System.out.println("PROMOCION ACTIVA: " + promocionActiva);
        }

        System.out.println("Tiempo de Preparacion: " + calcularTiempoPreparacion() + " minutos");
        System.out.println("============================\n");
    }

    // Implementamos calcularTiempoPreparacion.
    // Para bebidas es mas simple, casi siempre toma poco tiempo.
    @Override
    public int calcularTiempoPreparacion() {
        // Tiempo base de 2 minutos para servir.
        int tiempoBase = 2;

        // Si tiene personalizaciones (hielo, limon, etc), agrega tiempo.
        int tiempoPorPersonalizaciones = personalizaciones.size();

        return tiempoBase + tiempoPorPersonalizaciones;
    }

    // Implementamos los metodos de Personalizable.
    @Override
    public void agregarPersonalizacion(String personalizacion) {
        if (personalizacion != null && !personalizacion.trim().isEmpty()) {
            personalizaciones.add(personalizacion);
            System.out.println("Personalizacion agregada: " + personalizacion);
        }
    }

    @Override
    public boolean quitarPersonalizacion(String personalizacion) {
        return personalizaciones.remove(personalizacion);
    }

    @Override
    public ArrayList<String> obtenerPersonalizaciones() {
        return personalizaciones;
    }

    @Override
    public int calcularCostoPersonalizacion() {
        // Para bebidas, cada personalizacion cuesta 200 pesos.
        return personalizaciones.size() * 200;
    }

    // Implementamos los metodos de Promocionable.
    @Override
    public void aplicarPromocion(String tipoPromocion) {
        if (tipoPromocion == null || tipoPromocion.trim().isEmpty()) {
            System.out.println("Error: Debe especificar el tipo de promocion.");
            return;
        }

        this.promocionActiva = tipoPromocion;
        this.tienePromocion = true;

        System.out.println("Promocion aplicada: " + tipoPromocion);

        if (tipoPromocion.equalsIgnoreCase("Happy Hour")) {
            aplicarDescuento(20);
        }
    }

    @Override
    public boolean tienePromocionActiva() {
        return tienePromocion;
    }

    @Override
    public String obtenerDescripcionPromocion() {
        return tienePromocion ? promocionActiva : "Sin promocion";
    }

    @Override
    public void removerPromocion() {
        if (tienePromocion) {
            System.out.println("Promocion removida: " + promocionActiva);
            this.promocionActiva = null;
            this.tienePromocion = false;
        }
    }

    @Override
    public String toString() {
        String promo = tienePromocion ? " [PROMO: " + promocionActiva + "]" : "";
        return String.format("Bebida %s %s (%dml) - $%d%s",
            marca,
            nombre,
            mililitros,
            precio,
            promo
        );
    }
}
```

## Paso 6: Sistema Completo con Polimorfismo

Ahora modificamos `SistemaPizzeria.java` para aprovechar todo el polimorfismo:

```java
package sistemapizzeria;

import java.util.Scanner;
import java.util.ArrayList;

public class SistemaPizzeria {

    // ArrayList de Producto puede contener Pizza y Bebida.
    // Esto es polimorfismo: una referencia del padre puede apuntar a objetos hijos.
    private static ArrayList<Producto> menuProductos = new ArrayList<>();

    public static void main(String[] args) {

        inicializarMenu();

        Scanner scanner = new Scanner(System.in);
        boolean sistemaActivo = true;

        while (sistemaActivo) {

            System.out.println("\n////////////////////////////////////////");
            System.out.println("///   PIZZERIA BELLA NAPOLI         ///");
            System.out.println("////////////////////////////////////////");
            System.out.println("1. Ver Todos los Productos");
            System.out.println("2. Ver Detalle de Producto");
            System.out.println("3. Crear Nueva Pizza");
            System.out.println("4. Crear Nueva Bebida");
            System.out.println("5. Personalizar Producto");
            System.out.println("6. Aplicar Promocion a Producto");
            System.out.println("7. Ver Productos con Promocion");
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
                    verDetalleProducto(scanner);
                    break;

                case 3:
                    crearNuevaPizza(scanner);
                    break;

                case 4:
                    crearNuevaBebida(scanner);
                    break;

                case 5:
                    personalizarProducto(scanner);
                    break;

                case 6:
                    aplicarPromocionProducto(scanner);
                    break;

                case 7:
                    verProductosConPromocion();
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

    public static void inicializarMenu() {

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

        Bebida cocaCola = new Bebida("Coca-Cola", 1500, 500, true, "Coca-Cola");
        menuProductos.add(cocaCola);

        Bebida agua = new Bebida("Agua Mineral", 1000, 500, false, "Vital");
        menuProductos.add(agua);

        System.out.println("Menu inicializado con " + menuProductos.size() + " productos.");
    }

    public static void mostrarTodosLosProductos() {

        System.out.println("\n////////////////////////////////////////");
        System.out.println("///      TODOS LOS PRODUCTOS        ///");
        System.out.println("////////////////////////////////////////");

        if (menuProductos.isEmpty()) {
            System.out.println("No hay productos en el menu.");
            return;
        }

        for (int i = 0; i < menuProductos.size(); i++) {
            System.out.println((i + 1) + ". " + menuProductos.get(i));
        }
    }

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

        // Aqui vemos polimorfismo en accion.
        // Aunque producto es de tipo Producto, el objeto real puede ser Pizza o Bebida.
        // Cuando llamamos a mostrarInformacion(), Java ejecuta la version correcta
        // segun el tipo real del objeto (Pizza o Bebida).
        Producto producto = menuProductos.get(numero - 1);
        producto.mostrarInformacion();
    }

    public static void crearNuevaPizza(Scanner scanner) {

        System.out.println("\n////////////////////////////////////////");
        System.out.println("///      CREAR NUEVA PIZZA          ///");
        System.out.println("////////////////////////////////////////");

        System.out.print("Nombre: ");
        String nombre = scanner.nextLine();

        System.out.print("Precio: ");
        int precio = scanner.nextInt();
        scanner.nextLine();

        System.out.print("Tamanio (Personal/Mediana/Familiar): ");
        String tamanio = scanner.nextLine();

        System.out.print("Tipo de masa: ");
        String tipoMasa = scanner.nextLine();

        Pizza nuevaPizza = new Pizza(nombre, precio, tamanio, tipoMasa);

        System.out.println("\nAgregar ingredientes (vacio para terminar):");
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

        menuProductos.add(nuevaPizza);
        System.out.println("\nPizza creada exitosamente!");
        nuevaPizza.mostrarInformacion();
    }

    public static void crearNuevaBebida(Scanner scanner) {

        System.out.println("\n////////////////////////////////////////");
        System.out.println("///      CREAR NUEVA BEBIDA         ///");
        System.out.println("////////////////////////////////////////");

        System.out.print("Nombre: ");
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

        Bebida nuevaBebida = new Bebida(nombre, precio, ml, esGaseosa, marca);
        menuProductos.add(nuevaBebida);

        System.out.println("\nBebida creada exitosamente!");
        nuevaBebida.mostrarInformacion();
    }

    public static void personalizarProducto(Scanner scanner) {

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

        // Obtenemos el producto.
        Producto producto = menuProductos.get(numero - 1);

        // Aqui usamos instanceof para verificar si implementa la interfaz.
        // Sabemos que Pizza y Bebida implementan Personalizable, pero podriamos
        // tener otros productos en el futuro que no lo implementen.
        if (producto instanceof Personalizable) {

            // Hacemos un cast a Personalizable para acceder a los metodos de la interfaz.
            // El cast es seguro porque ya verificamos con instanceof.
            Personalizable personalizable = (Personalizable) producto;

            System.out.println("\nPersonalizando: " + producto.getNombre());
            System.out.println("Agregar personalizaciones (vacio para terminar):");

            boolean agregando = true;

            while (agregando) {
                System.out.print("Personalizacion: ");
                String personalizacion = scanner.nextLine();

                if (personalizacion.trim().isEmpty()) {
                    agregando = false;
                } else {
                    personalizable.agregarPersonalizacion(personalizacion);
                }
            }

            System.out.println("\nCosto adicional por personalizaciones: $" +
                personalizable.calcularCostoPersonalizacion());

        } else {
            System.out.println("Este producto no admite personalizaciones.");
        }
    }

    public static void aplicarPromocionProducto(Scanner scanner) {

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

        Producto producto = menuProductos.get(numero - 1);

        // Verificamos si implementa Promocionable.
        if (producto instanceof Promocionable) {

            Promocionable promocionable = (Promocionable) producto;

            System.out.println("\nTipos de promocion disponibles:");
            System.out.println("1. Happy Hour (descuento)");
            System.out.println("2. 2x1");
            System.out.println("3. Personalizada");

            System.out.print("Seleccione tipo de promocion: ");
            int tipo = scanner.nextInt();
            scanner.nextLine();

            String tipoPromocion = "";

            switch (tipo) {
                case 1:
                    tipoPromocion = "Happy Hour";
                    break;
                case 2:
                    tipoPromocion = "2x1";
                    break;
                case 3:
                    System.out.print("Ingrese el nombre de la promocion: ");
                    tipoPromocion = scanner.nextLine();
                    break;
                default:
                    System.out.println("Opcion invalida.");
                    return;
            }

            promocionable.aplicarPromocion(tipoPromocion);

        } else {
            System.out.println("Este producto no admite promociones.");
        }
    }

    public static void verProductosConPromocion() {

        System.out.println("\n////////////////////////////////////////");
        System.out.println("///   PRODUCTOS CON PROMOCION       ///");
        System.out.println("////////////////////////////////////////");

        int contador = 0;

        // Recorremos todos los productos.
        for (Producto p : menuProductos) {

            // Verificamos si implementa Promocionable.
            if (p instanceof Promocionable) {

                Promocionable promo = (Promocionable) p;

                // Verificamos si tiene promocion activa.
                if (promo.tienePromocionActiva()) {
                    contador++;
                    System.out.println(contador + ". " + p);
                    System.out.println("   Promocion: " + promo.obtenerDescripcionPromocion());
                }
            }
        }

        if (contador == 0) {
            System.out.println("No hay productos con promocion activa.");
        }
    }
}
```

## Conceptos Clave de Polimorfismo

### 1. Clase Abstracta
- Se declara con `abstract class`
- No se puede instanciar directamente
- Puede tener métodos abstractos y métodos normales

### 2. Método Abstracto
- Se declara con `abstract` sin cuerpo
- Las clases hijas DEBEN implementarlo
- Define el "qué" pero no el "cómo"

### 3. Interfaz
- Se declara con `interface`
- Todos los métodos son public y abstract por defecto
- Una clase puede implementar múltiples interfaces

### 4. Implements vs Extends
- `extends`: Herencia de una clase (solo una)
- `implements`: Implementación de interfaces (múltiples)

### 5. Polimorfismo en Acción
- Una variable de tipo Producto puede contener Pizza o Bebida
- Java ejecuta el método correcto según el tipo real del objeto
- Permite escribir código genérico que funciona con diferentes tipos

### 6. Instanceof y Casting
- `instanceof`: Verificar el tipo real de un objeto
- Cast: Convertir una referencia para acceder a métodos específicos

## Probando el Sistema Completo

Ejecuta y prueba todas las características:
1. Crear pizzas y bebidas
2. Personalizar productos agregando extras
3. Aplicar promociones a productos
4. Ver solo productos con promoción activa
5. Ver detalles completos con tiempos de preparación

## Resumen de Todo el Tutorial

Has completado un sistema completo que incluye:

**Parte 1 - Ciclos**: Menú con while, recorrido de arrays con for, búsqueda con break

**Parte 2 - Encapsulación**: Clase Ingrediente con atributos privados, getters/setters, validación

**Parte 3 - Colecciones**: Clase Pedido con ArrayList, operaciones CRUD, manejo dinámico de datos

**Parte 4 - Herencia**: Jerarquía Producto → Pizza/Bebida, uso de super(), @Override

**Parte 5 - Polimorfismo**: Clase abstracta, interfaces Personalizable y Promocionable, polimorfismo completo

Ahora tienes una aplicación completa de pizzería que demuestra todos los conceptos fundamentales de POO en Java.

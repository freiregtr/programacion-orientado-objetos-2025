# Parte 2: Agregando Encapsulación con la Clase Ingrediente

En la parte anterior creamos un sistema de menú funcional con arrays. Ahora vamos a mejorar nuestro código creando una clase `Ingrediente` que nos permitirá almacenar información de manera más organizada y segura.

## ¿Por Qué Necesitamos Una Clase?

En la Parte 1, usamos arrays separados para nombres y precios. Esto funciona, pero tiene problemas:
- Si agregamos un nuevo dato (por ejemplo, cantidad en stock), necesitamos otro array
- Es fácil que los arrays se desincronicen
- No podemos validar que los datos sean correctos

Una clase nos permite agrupar datos relacionados y controlar cómo se accede a ellos.

## Paso 1: Crear la Clase Ingrediente

En NetBeans:
1. Haz clic derecho en el paquete `sistemapizzeria`
2. Selecciona New → Java Class
3. Nombra la clase `Ingrediente`
4. Haz clic en Finish

NetBeans creará un archivo nuevo. Ahí escribiremos:

```java
package sistemapizzeria;

public class Ingrediente {

    // Vamos a almacenar tres datos sobre cada ingrediente: nombre, precio y cantidad disponible.
    // Estos son los atributos de nuestra clase.
    // Los declaramos como private porque queremos controlar como se accede a ellos.
    // Private significa que solo codigo dentro de esta clase puede ver y modificar estos valores.
    // Esto se llama encapsulacion y nos protege de errores.
    private String nombre;
    private int precio;
    private int cantidadDisponible;

    // Ahora necesitamos una forma de crear ingredientes.
    // El constructor es un metodo especial que se ejecuta cuando creamos un nuevo objeto.
    // Tiene el mismo nombre que la clase y no tiene tipo de retorno.
    // Recibe los valores iniciales que queremos asignar al ingrediente.
    public Ingrediente(String nombre, int precio, int cantidadDisponible) {

        // Antes de guardar los valores, vamos a validarlos.
        // No tiene sentido tener un precio negativo, seria regalar dinero.
        // Usamos if para verificar que el precio sea mayor o igual a cero.
        if (precio < 0) {
            // Si el precio es negativo, mostramos un error y lo ajustamos a cero.
            System.out.println("Advertencia: El precio no puede ser negativo. Se ajustara a 0.");
            precio = 0;
        }

        // Lo mismo con la cantidad disponible.
        // No podemos tener cantidades negativas de un ingrediente.
        if (cantidadDisponible < 0) {
            System.out.println("Advertencia: La cantidad no puede ser negativa. Se ajustara a 0.");
            cantidadDisponible = 0;
        }

        // Ahora guardamos los valores en los atributos del objeto.
        // this.nombre se refiere al atributo de la clase.
        // nombre (sin this) se refiere al parametro que recibimos.
        // Usamos this para distinguir entre ambos.
        this.nombre = nombre;
        this.precio = precio;
        this.cantidadDisponible = cantidadDisponible;
    }

    // Como los atributos son privados, necesitamos metodos publicos para leerlos.
    // Estos metodos se llaman getters (obtener).
    // Son metodos simples que solo devuelven el valor del atributo.
    public String getNombre() {
        return nombre;
    }

    public int getPrecio() {
        return precio;
    }

    public int getCantidadDisponible() {
        return cantidadDisponible;
    }

    // Tambien necesitamos metodos para modificar los valores.
    // Estos se llaman setters (establecer).
    // La ventaja de usar setters en lugar de atributos publicos es que podemos validar.
    public void setNombre(String nombre) {
        // Verificamos que el nombre no este vacio.
        // Un ingrediente sin nombre no tiene sentido.
        if (nombre != null && !nombre.trim().isEmpty()) {
            this.nombre = nombre;
        } else {
            System.out.println("Error: El nombre no puede estar vacio.");
        }
    }

    public void setPrecio(int precio) {
        // Validamos que el precio sea razonable.
        if (precio >= 0) {
            this.precio = precio;
        } else {
            System.out.println("Error: El precio no puede ser negativo.");
        }
    }

    public void setCantidadDisponible(int cantidadDisponible) {
        // Validamos que la cantidad sea valida.
        if (cantidadDisponible >= 0) {
            this.cantidadDisponible = cantidadDisponible;
        } else {
            System.out.println("Error: La cantidad no puede ser negativa.");
        }
    }

    // Vamos a crear un metodo que reduzca la cantidad disponible.
    // Esto sera util cuando usemos un ingrediente para hacer una pizza.
    // Lo hacemos private porque es un detalle interno de como funciona la clase.
    // Solo esta clase necesita saber como se reduce el stock.
    public boolean reducirCantidad(int cantidad) {

        // Primero verificamos si tenemos suficiente stock.
        // No podemos usar mas ingrediente del que tenemos disponible.
        if (cantidad > cantidadDisponible) {
            System.out.println("Error: No hay suficiente " + nombre + " disponible.");
            return false;
        }

        // Si hay suficiente, reducimos la cantidad.
        cantidadDisponible -= cantidad;
        return true;
    }

    // Este metodo permite aumentar el stock.
    // Seria util cuando recibimos nuevos ingredientes.
    public void aumentarCantidad(int cantidad) {

        // Validamos que no esten tratando de agregar una cantidad negativa.
        if (cantidad > 0) {
            cantidadDisponible += cantidad;
            System.out.println("Se agregaron " + cantidad + " unidades de " + nombre);
        } else {
            System.out.println("Error: La cantidad a agregar debe ser positiva.");
        }
    }

    // Este metodo nos permite mostrar la informacion del ingrediente de forma legible.
    // toString es un metodo especial que Java llama automaticamente cuando
    // intentamos imprimir un objeto o convertirlo a texto.
    @Override
    public String toString() {
        return String.format("%-20s | Precio: $%-6d | Stock: %d unidades",
            nombre, precio, cantidadDisponible);
    }
}
```

## Paso 2: Usar la Clase Ingrediente en el Sistema

Ahora vamos a modificar nuestra clase principal para usar `Ingrediente` en lugar de arrays simples. Abre `SistemaPizzeria.java` y agrega este código:

```java
package sistemapizzeria;

import java.util.Scanner;

public class SistemaPizzeria {

    public static void main(String[] args) {

        Scanner scanner = new Scanner(System.in);
        boolean sistemaActivo = true;

        // En lugar de usar arrays simples de String e int, ahora vamos a crear objetos Ingrediente.
        // Primero creamos un array que puede contener objetos de tipo Ingrediente.
        // Cada posicion del array guardara un objeto completo con nombre, precio y cantidad.
        Ingrediente[] ingredientes = new Ingrediente[5];

        // Ahora creamos cada ingrediente usando el constructor.
        // Usamos new Ingrediente() para crear un nuevo objeto.
        // Entre parentesis pasamos los tres valores que el constructor necesita.
        ingredientes[0] = new Ingrediente("Tomate", 500, 100);
        ingredientes[1] = new Ingrediente("Queso Mozzarella", 1200, 50);
        ingredientes[2] = new Ingrediente("Pepperoni", 800, 75);
        ingredientes[3] = new Ingrediente("Champinones", 600, 40);
        ingredientes[4] = new Ingrediente("Aceitunas", 400, 60);

        while (sistemaActivo) {

            // Ahora nuestro menu incluye opciones para gestionar ingredientes.
            System.out.println("\n////////////////////////////////////////");
            System.out.println("///   PIZZERIA BELLA NAPOLI         ///");
            System.out.println("////////////////////////////////////////");
            System.out.println("1. Ver Menu de Pizzas");
            System.out.println("2. Ver Menu de Bebidas");
            System.out.println("3. Buscar Pizza por Nombre");
            System.out.println("4. Ver Inventario de Ingredientes");
            System.out.println("5. Buscar Ingrediente");
            System.out.println("6. Actualizar Stock de Ingrediente");
            System.out.println("7. Salir");
            System.out.println("////////////////////////////////////////");
            System.out.print("Seleccione una opcion: ");

            int opcion = scanner.nextInt();
            scanner.nextLine();

            switch (opcion) {
                case 1:
                    mostrarMenuPizzas();
                    break;

                case 2:
                    mostrarMenuBebidas();
                    break;

                case 3:
                    System.out.print("Ingrese el nombre de la pizza: ");
                    String nombreBuscar = scanner.nextLine();
                    buscarPizza(nombreBuscar);
                    break;

                case 4:
                    // El usuario quiere ver el inventario completo de ingredientes.
                    // Llamamos al nuevo metodo que muestra todos los ingredientes.
                    mostrarInventarioIngredientes(ingredientes);
                    break;

                case 5:
                    // El usuario quiere buscar un ingrediente especifico.
                    System.out.print("Ingrese el nombre del ingrediente: ");
                    String nombreIngrediente = scanner.nextLine();
                    buscarIngrediente(ingredientes, nombreIngrediente);
                    break;

                case 6:
                    // El usuario quiere actualizar la cantidad de un ingrediente.
                    // Esto simula recibir nuevos ingredientes o usar algunos.
                    actualizarStockIngrediente(scanner, ingredientes);
                    break;

                case 7:
                    System.out.println("\nGracias por usar el Sistema Pizzeria Bella Napoli!");
                    System.out.println("Hasta pronto!");
                    sistemaActivo = false;
                    break;

                default:
                    System.out.println("\nOpcion invalida. Por favor seleccione una opcion valida.");
            }
        }

        scanner.close();
    }

    // Mantenemos los metodos anteriores sin cambios.
    public static void mostrarMenuPizzas() {
        String[] nombresPizzas = {
            "Margarita",
            "Pepperoni",
            "Hawaiana",
            "Cuatro Quesos",
            "Vegetariana"
        };

        int[] preciosPizzas = {
            5990,
            6990,
            7490,
            7990,
            6490
        };

        System.out.println("\n////////////////////////////////////////");
        System.out.println("///       MENU DE PIZZAS            ///");
        System.out.println("////////////////////////////////////////");

        for (int i = 0; i < nombresPizzas.length; i++) {
            System.out.printf("%d. %-20s $%d%n",
                (i + 1),
                nombresPizzas[i],
                preciosPizzas[i]
            );
        }

        System.out.println();
    }

    public static void mostrarMenuBebidas() {
        String[] nombresBebidas = {
            "Coca-Cola",
            "Fanta",
            "Sprite",
            "Agua Mineral",
            "Jugo Natural"
        };

        int[] preciosBebidas = {
            1500,
            1500,
            1500,
            1000,
            2000
        };

        System.out.println("\n////////////////////////////////////////");
        System.out.println("///       MENU DE BEBIDAS           ///");
        System.out.println("////////////////////////////////////////");

        for (int i = 0; i < nombresBebidas.length; i++) {
            System.out.printf("%d. %-20s $%d%n",
                (i + 1),
                nombresBebidas[i],
                preciosBebidas[i]
            );
        }

        System.out.println();
    }

    public static void buscarPizza(String nombreBuscar) {
        String[] nombresPizzas = {
            "Margarita",
            "Pepperoni",
            "Hawaiana",
            "Cuatro Quesos",
            "Vegetariana"
        };

        int[] preciosPizzas = {
            5990,
            6990,
            7490,
            7990,
            6490
        };

        boolean encontrada = false;

        System.out.println("\nBuscando: " + nombreBuscar);
        System.out.println("---------------------------------------");

        for (int i = 0; i < nombresPizzas.length; i++) {
            if (nombresPizzas[i].equalsIgnoreCase(nombreBuscar)) {
                System.out.println("Encontrada: " + nombresPizzas[i]);
                System.out.println("Precio: $" + preciosPizzas[i]);
                encontrada = true;
                break;
            }
        }

        if (!encontrada) {
            System.out.println("No se encontro una pizza con ese nombre.");
        }

        System.out.println();
    }

    // Nuevo metodo que muestra todos los ingredientes disponibles.
    // Recibe el array de ingredientes como parametro.
    public static void mostrarInventarioIngredientes(Ingrediente[] ingredientes) {

        System.out.println("\n////////////////////////////////////////");
        System.out.println("///   INVENTARIO DE INGREDIENTES    ///");
        System.out.println("////////////////////////////////////////");

        // Recorremos el array de ingredientes.
        // Esto es igual que recorrer un array de int o String.
        for (int i = 0; i < ingredientes.length; i++) {

            // Mostramos el numero del ingrediente.
            System.out.print((i + 1) + ". ");

            // Aqui usamos el metodo toString() del ingrediente.
            // Cuando hacemos println de un objeto, Java llama automaticamente a toString().
            System.out.println(ingredientes[i]);
        }

        System.out.println();
    }

    // Metodo para buscar un ingrediente especifico.
    // Necesitamos recibir tanto el array como el nombre a buscar.
    public static void buscarIngrediente(Ingrediente[] ingredientes, String nombreBuscar) {

        boolean encontrado = false;

        System.out.println("\nBuscando ingrediente: " + nombreBuscar);
        System.out.println("---------------------------------------");

        // Recorremos todos los ingredientes buscando coincidencias.
        for (int i = 0; i < ingredientes.length; i++) {

            // Obtenemos el nombre del ingrediente actual usando el getter.
            // Como nombre es private, no podemos acceder directamente.
            // Tenemos que usar getNombre().
            if (ingredientes[i].getNombre().equalsIgnoreCase(nombreBuscar)) {

                System.out.println("Encontrado:");
                System.out.println(ingredientes[i]);
                encontrado = true;
                break;
            }
        }

        if (!encontrado) {
            System.out.println("No se encontro un ingrediente con ese nombre.");
        }

        System.out.println();
    }

    // Metodo para actualizar el stock de un ingrediente.
    // Esto simula cuando recibimos mas ingredientes o cuando los usamos.
    public static void actualizarStockIngrediente(Scanner scanner, Ingrediente[] ingredientes) {

        System.out.println("\n////////////////////////////////////////");
        System.out.println("///   ACTUALIZAR STOCK              ///");
        System.out.println("////////////////////////////////////////");

        // Primero mostramos los ingredientes disponibles para que el usuario sepa que numeros puede elegir.
        for (int i = 0; i < ingredientes.length; i++) {
            System.out.println((i + 1) + ". " + ingredientes[i].getNombre());
        }

        System.out.print("\nSeleccione el numero del ingrediente: ");
        int indice = scanner.nextInt();
        scanner.nextLine();

        // Validamos que el usuario haya ingresado un numero valido.
        // El numero debe estar entre 1 y la cantidad de ingredientes.
        if (indice < 1 || indice > ingredientes.length) {
            System.out.println("Numero invalido.");
            return;
        }

        // Ajustamos el indice porque los arrays comienzan en 0 pero mostramos desde 1.
        int indiceArray = indice - 1;

        System.out.println("Ingrediente seleccionado: " + ingredientes[indiceArray].getNombre());
        System.out.println("Stock actual: " + ingredientes[indiceArray].getCantidadDisponible());

        System.out.print("Ingrese cantidad a agregar (use numeros negativos para reducir): ");
        int cantidad = scanner.nextInt();
        scanner.nextLine();

        // Si la cantidad es positiva, agregamos stock.
        // Si es negativa, reducimos stock.
        if (cantidad > 0) {
            ingredientes[indiceArray].aumentarCantidad(cantidad);
        } else if (cantidad < 0) {
            // Para reducir, necesitamos pasar un valor positivo al metodo.
            // Por eso multiplicamos por -1.
            ingredientes[indiceArray].reducirCantidad(cantidad * -1);
        } else {
            System.out.println("No se realizo ningun cambio.");
        }

        System.out.println("Nuevo stock: " + ingredientes[indiceArray].getCantidadDisponible());
        System.out.println();
    }
}
```

## Conceptos Clave de Encapsulación

### 1. Atributos Privados
Los datos importantes se declaran `private` para protegerlos del acceso directo.

### 2. Getters y Setters
Métodos públicos que controlan el acceso a los atributos privados y permiten validación.

### 3. Validación en el Constructor
El constructor verifica que los datos iniciales sean válidos antes de crear el objeto.

### 4. Métodos de Negocio
Métodos como `reducirCantidad()` y `aumentarCantidad()` encapsulan la lógica de negocio.

### 5. toString()
Permite que el objeto se represente como texto de forma legible.

## Probando la Nueva Funcionalidad

Ejecuta el programa y prueba:
1. Ver el inventario de ingredientes (opción 4)
2. Buscar un ingrediente específico (opción 5)
3. Actualizar el stock de un ingrediente (opción 6)
4. Intenta ingresar valores negativos para ver la validación

## Lo que Viene

En la siguiente parte, vamos a usar `ArrayList` para manejar colecciones dinámicas. Crearemos una clase `Pedido` que permitirá:
- Agregar y eliminar productos sin límite fijo
- Gestionar un historial de pedidos
- Aplicar operaciones CRUD completas

Ya tenemos encapsulación, ahora necesitamos estructuras de datos más flexibles.

# Parte 3: Trabajando con Colecciones - La Clase Pedido

Hasta ahora hemos usado arrays que tienen un tamaño fijo. Si queremos agregar más elementos, tenemos que crear un array más grande y copiar todo. Esto es tedioso e ineficiente. Java nos proporciona `ArrayList`, una colección que crece automáticamente según necesitemos.

## ¿Por Qué ArrayList en Lugar de Arrays?

Los arrays tienen limitaciones:
- Tamaño fijo desde el inicio
- No podemos agregar o eliminar elementos fácilmente
- Tenemos que gestionar manualmente el tamaño

ArrayList soluciona todo esto:
- Tamaño dinámico que crece automáticamente
- Métodos para agregar, eliminar y buscar elementos
- Gestión automática de la memoria

## Paso 1: Crear la Clase Pedido

Vamos a crear una clase que represente un pedido de la pizzería. Un pedido puede tener múltiples productos y debe poder crecer o reducirse según el cliente agregue o quite items.

En NetBeans:
1. Clic derecho en el paquete `sistemapizzeria`
2. New → Java Class
3. Nombre: `Pedido`

```java
package sistemapizzeria;

import java.util.ArrayList;
import java.time.LocalDateTime;
import java.time.format.DateTimeFormatter;

public class Pedido {

    // Vamos a necesitar varios datos para cada pedido.
    // Un numero unico que identifique el pedido.
    private int numeroPedido;

    // El nombre del cliente que hizo el pedido.
    private String nombreCliente;

    // Aqui viene la parte importante: la lista de productos.
    // En lugar de usar un array, usamos ArrayList.
    // ArrayList<String> significa que es una lista que solo puede contener Strings.
    // Esto nos da flexibilidad para agregar o quitar productos sin limite.
    private ArrayList<String> productos;

    // Tambien guardamos los precios de cada producto.
    // Usamos ArrayList<Integer> para una lista de numeros enteros.
    private ArrayList<Integer> precios;

    // Guardamos cuando se creo el pedido.
    // LocalDateTime almacena fecha y hora exacta.
    private LocalDateTime fechaHora;

    // El estado del pedido puede ser: Pendiente, En Preparacion, Listo, Entregado.
    private String estado;

    // Necesitamos un constructor para crear nuevos pedidos.
    // El numero de pedido y el nombre del cliente se reciben como parametros.
    // Los productos empiezan vacios porque el cliente los va agregando.
    public Ingrediente(int numeroPedido, String nombreCliente) {

        this.numeroPedido = numeroPedido;
        this.nombreCliente = nombreCliente;

        // Aqui creamos los ArrayList vacios.
        // Usamos new ArrayList<>() para crear una nueva lista.
        // Empieza sin elementos, pero puede crecer cuando agregemos productos.
        this.productos = new ArrayList<>();
        this.precios = new ArrayList<>();

        // Guardamos la fecha y hora actual del sistema.
        // LocalDateTime.now() obtiene el momento exacto en que se crea el pedido.
        this.fechaHora = LocalDateTime.now();

        // Todo pedido nuevo comienza en estado Pendiente.
        this.estado = "Pendiente";
    }

    // Getters para acceder a la informacion del pedido.
    public int getNumeroPedido() {
        return numeroPedido;
    }

    public String getNombreCliente() {
        return nombreCliente;
    }

    public String getEstado() {
        return estado;
    }

    public ArrayList<String> getProductos() {
        return productos;
    }

    public ArrayList<Integer> getPrecios() {
        return precios;
    }

    // Metodo para cambiar el estado del pedido.
    // Solo permitimos estados validos.
    public void setEstado(String nuevoEstado) {

        // Creamos un array con los estados validos.
        // Solo estos valores estan permitidos.
        String[] estadosValidos = {"Pendiente", "En Preparacion", "Listo", "Entregado", "Cancelado"};

        // Verificamos si el estado que quieren poner es valido.
        // Usamos un ciclo para revisar cada estado permitido.
        boolean esValido = false;
        for (int i = 0; i < estadosValidos.length; i++) {
            if (estadosValidos[i].equalsIgnoreCase(nuevoEstado)) {
                esValido = true;
                break;
            }
        }

        // Si el estado es valido, lo actualizamos.
        // Si no, mostramos un error.
        if (esValido) {
            this.estado = nuevoEstado;
            System.out.println("Estado del pedido actualizado a: " + nuevoEstado);
        } else {
            System.out.println("Error: Estado invalido. Use: Pendiente, En Preparacion, Listo, Entregado o Cancelado");
        }
    }

    // Este metodo agrega un producto al pedido.
    // Recibe el nombre del producto y su precio.
    // Aqui vemos la ventaja de ArrayList: podemos agregar sin preocuparnos por el tamaño.
    public void agregarProducto(String nombreProducto, int precio) {

        // Validamos que el nombre no este vacio.
        if (nombreProducto == null || nombreProducto.trim().isEmpty()) {
            System.out.println("Error: El nombre del producto no puede estar vacio.");
            return;
        }

        // Validamos que el precio sea razonable.
        if (precio < 0) {
            System.out.println("Error: El precio no puede ser negativo.");
            return;
        }

        // Usamos add() para agregar elementos al ArrayList.
        // add() aumenta automaticamente el tamaño de la lista.
        // No necesitamos preocuparnos por crear espacio.
        productos.add(nombreProducto);
        precios.add(precio);

        System.out.println("Producto agregado: " + nombreProducto + " - $" + precio);
    }

    // Metodo para eliminar un producto del pedido.
    // El cliente podria cambiar de opinion y querer quitar algo.
    public boolean eliminarProducto(String nombreProducto) {

        // Buscamos el producto en la lista.
        // Usamos un ciclo for con indices porque necesitamos eliminar de ambas listas.
        for (int i = 0; i < productos.size(); i++) {

            // size() nos da la cantidad de elementos en el ArrayList.
            // Es como length para arrays, pero se llama con parentesis porque es un metodo.

            // Si encontramos el producto, lo eliminamos.
            if (productos.get(i).equalsIgnoreCase(nombreProducto)) {

                // get(i) obtiene el elemento en la posicion i.
                // Es como productos[i] en un array, pero usamos el metodo get().

                // remove(i) elimina el elemento en la posicion i.
                // Automaticamente todos los elementos siguientes se recorren hacia atras.
                String productoEliminado = productos.remove(i);
                int precioEliminado = precios.remove(i);

                System.out.println("Producto eliminado: " + productoEliminado + " - $" + precioEliminado);
                return true;
            }
        }

        // Si llegamos aqui es porque no encontramos el producto.
        System.out.println("No se encontro el producto: " + nombreProducto);
        return false;
    }

    // Metodo para calcular el total del pedido.
    // Sumamos todos los precios de los productos.
    public int calcularTotal() {

        // Empezamos con un total de cero.
        int total = 0;

        // Recorremos todos los precios y los vamos sumando.
        // Podemos usar un for tradicional o un for-each.
        // Usamos for-each porque solo necesitamos el valor, no el indice.
        for (int precio : precios) {
            // En cada iteracion, precio toma el valor del siguiente elemento.
            total += precio;
        }

        return total;
    }

    // Metodo para obtener la cantidad de productos en el pedido.
    public int cantidadProductos() {
        // size() nos da directamente cuantos elementos hay.
        return productos.size();
    }

    // Metodo para mostrar el detalle completo del pedido.
    public void mostrarDetalle() {

        System.out.println("\n========================================");
        System.out.println("DETALLE DEL PEDIDO #" + numeroPedido);
        System.out.println("========================================");
        System.out.println("Cliente: " + nombreCliente);

        // Formateamos la fecha para que se vea bonita.
        // DateTimeFormatter nos permite elegir como mostrar fecha y hora.
        DateTimeFormatter formato = DateTimeFormatter.ofPattern("dd/MM/yyyy HH:mm:ss");
        System.out.println("Fecha: " + fechaHora.format(formato));

        System.out.println("Estado: " + estado);
        System.out.println("----------------------------------------");

        // Verificamos si hay productos en el pedido.
        // isEmpty() devuelve true si el ArrayList esta vacio.
        if (productos.isEmpty()) {
            System.out.println("No hay productos en este pedido.");
        } else {
            System.out.println("Productos:");

            // Mostramos cada producto con su precio.
            // Usamos un for tradicional porque necesitamos el indice para acceder a ambas listas.
            for (int i = 0; i < productos.size(); i++) {
                System.out.printf("  %d. %-25s $%d%n",
                    (i + 1),
                    productos.get(i),
                    precios.get(i)
                );
            }

            System.out.println("----------------------------------------");
            System.out.printf("TOTAL: $%d%n", calcularTotal());
        }

        System.out.println("========================================\n");
    }

    @Override
    public String toString() {
        return String.format("Pedido #%d - %s - %d productos - $%d - %s",
            numeroPedido,
            nombreCliente,
            cantidadProductos(),
            calcularTotal(),
            estado
        );
    }
}
```

## Paso 2: Gestionar Múltiples Pedidos en el Sistema

Ahora modificamos `SistemaPizzeria.java` para manejar múltiples pedidos usando ArrayList:

```java
package sistemapizzeria;

import java.util.Scanner;
import java.util.ArrayList;

public class SistemaPizzeria {

    // Vamos a hacer estos ArrayLists globales dentro de la clase.
    // static significa que pertenecen a la clase, no a instancias individuales.
    // Los declaramos aqui para que todos los metodos puedan acceder a ellos.
    // Esto simula una "base de datos" temporal de nuestros pedidos.
    private static ArrayList<Pedido> historialPedidos = new ArrayList<>();

    // Contador para asignar numeros unicos a cada pedido.
    // Cada vez que creamos un pedido nuevo, incrementamos este numero.
    private static int contadorPedidos = 1;

    public static void main(String[] args) {

        Scanner scanner = new Scanner(System.in);
        boolean sistemaActivo = true;

        Ingrediente[] ingredientes = new Ingrediente[5];
        ingredientes[0] = new Ingrediente("Tomate", 500, 100);
        ingredientes[1] = new Ingrediente("Queso Mozzarella", 1200, 50);
        ingredientes[2] = new Ingrediente("Pepperoni", 800, 75);
        ingredientes[3] = new Ingrediente("Champinones", 600, 40);
        ingredientes[4] = new Ingrediente("Aceitunas", 400, 60);

        while (sistemaActivo) {

            // Expandimos el menu para incluir gestion de pedidos.
            System.out.println("\n////////////////////////////////////////");
            System.out.println("///   PIZZERIA BELLA NAPOLI         ///");
            System.out.println("////////////////////////////////////////");
            System.out.println("1. Ver Menu de Pizzas");
            System.out.println("2. Ver Menu de Bebidas");
            System.out.println("3. Crear Nuevo Pedido");
            System.out.println("4. Ver Todos los Pedidos");
            System.out.println("5. Buscar Pedido por Numero");
            System.out.println("6. Actualizar Estado de Pedido");
            System.out.println("7. Ver Inventario de Ingredientes");
            System.out.println("8. Salir");
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
                    // El usuario quiere crear un nuevo pedido.
                    // Llamamos al metodo que maneja todo el proceso de creacion.
                    crearNuevoPedido(scanner);
                    break;

                case 4:
                    // Mostrar todos los pedidos que se han realizado.
                    mostrarTodosPedidos();
                    break;

                case 5:
                    // Buscar un pedido especifico por su numero.
                    System.out.print("Ingrese el numero de pedido: ");
                    int numeroBuscar = scanner.nextInt();
                    scanner.nextLine();
                    buscarPedido(numeroBuscar);
                    break;

                case 6:
                    // Actualizar el estado de un pedido existente.
                    actualizarEstadoPedido(scanner);
                    break;

                case 7:
                    mostrarInventarioIngredientes(ingredientes);
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

    // Metodo para crear un nuevo pedido.
    // Este metodo guia al usuario paso a paso en la creacion del pedido.
    public static void crearNuevoPedido(Scanner scanner) {

        System.out.println("\n////////////////////////////////////////");
        System.out.println("///      CREAR NUEVO PEDIDO         ///");
        System.out.println("////////////////////////////////////////");

        // Pedimos el nombre del cliente.
        System.out.print("Nombre del cliente: ");
        String nombreCliente = scanner.nextLine();

        // Validamos que el cliente haya ingresado un nombre.
        if (nombreCliente.trim().isEmpty()) {
            System.out.println("Error: Debe ingresar un nombre.");
            return;
        }

        // Creamos el pedido usando el constructor.
        // contadorPedidos se incrementa automaticamente para el siguiente pedido.
        Pedido nuevoPedido = new Pedido(contadorPedidos++, nombreCliente);

        // Mostramos los menus para que el cliente pueda elegir.
        mostrarMenuPizzas();
        mostrarMenuBebidas();

        // Ahora el cliente puede agregar productos al pedido.
        // Usamos un ciclo para que pueda agregar multiples productos.
        boolean agregandoProductos = true;

        while (agregandoProductos) {
            System.out.println("\nOpciones:");
            System.out.println("1. Agregar producto al pedido");
            System.out.println("2. Finalizar pedido");
            System.out.print("Seleccione una opcion: ");

            int opcion = scanner.nextInt();
            scanner.nextLine();

            if (opcion == 1) {
                // El cliente quiere agregar un producto.
                System.out.print("Nombre del producto: ");
                String nombreProducto = scanner.nextLine();

                System.out.print("Precio del producto: ");
                int precio = scanner.nextInt();
                scanner.nextLine();

                // Usamos el metodo agregarProducto del pedido.
                nuevoPedido.agregarProducto(nombreProducto, precio);

            } else if (opcion == 2) {
                // El cliente termino de agregar productos.

                // Verificamos que haya al menos un producto.
                if (nuevoPedido.cantidadProductos() == 0) {
                    System.out.println("Error: Debe agregar al menos un producto.");
                } else {
                    // El pedido esta completo, lo agregamos al historial.
                    // Usamos add() para agregar el pedido al ArrayList.
                    historialPedidos.add(nuevoPedido);

                    System.out.println("\nPedido creado exitosamente!");
                    nuevoPedido.mostrarDetalle();

                    agregandoProductos = false;
                }
            } else {
                System.out.println("Opcion invalida.");
            }
        }
    }

    // Metodo para mostrar todos los pedidos registrados.
    public static void mostrarTodosPedidos() {

        System.out.println("\n////////////////////////////////////////");
        System.out.println("///     HISTORIAL DE PEDIDOS        ///");
        System.out.println("////////////////////////////////////////");

        // Verificamos si hay pedidos registrados.
        if (historialPedidos.isEmpty()) {
            System.out.println("No hay pedidos registrados.");
            return;
        }

        // Recorremos todos los pedidos y los mostramos.
        // Usamos for-each porque solo necesitamos ver cada pedido.
        for (Pedido pedido : historialPedidos) {
            // Esto llama automaticamente al toString() del pedido.
            System.out.println(pedido);
        }

        System.out.println("\nTotal de pedidos: " + historialPedidos.size());
    }

    // Metodo para buscar un pedido especifico por su numero.
    public static void buscarPedido(int numeroPedido) {

        // Recorremos el historial buscando el pedido con ese numero.
        for (Pedido pedido : historialPedidos) {
            if (pedido.getNumeroPedido() == numeroPedido) {
                // Encontramos el pedido, mostramos su detalle completo.
                pedido.mostrarDetalle();
                return;
            }
        }

        // Si llegamos aqui es porque no encontramos el pedido.
        System.out.println("No se encontro un pedido con el numero: " + numeroPedido);
    }

    // Metodo para actualizar el estado de un pedido.
    public static void actualizarEstadoPedido(Scanner scanner) {

        System.out.println("\n////////////////////////////////////////");
        System.out.println("///   ACTUALIZAR ESTADO PEDIDO      ///");
        System.out.println("////////////////////////////////////////");

        // Primero mostramos todos los pedidos.
        if (historialPedidos.isEmpty()) {
            System.out.println("No hay pedidos registrados.");
            return;
        }

        for (Pedido pedido : historialPedidos) {
            System.out.println(pedido);
        }

        System.out.print("\nIngrese el numero de pedido: ");
        int numeroPedido = scanner.nextInt();
        scanner.nextLine();

        // Buscamos el pedido.
        Pedido pedidoEncontrado = null;

        for (Pedido pedido : historialPedidos) {
            if (pedido.getNumeroPedido() == numeroPedido) {
                pedidoEncontrado = pedido;
                break;
            }
        }

        // Si no encontramos el pedido, terminamos.
        if (pedidoEncontrado == null) {
            System.out.println("No se encontro el pedido.");
            return;
        }

        // Mostramos los estados disponibles.
        System.out.println("\nEstados disponibles:");
        System.out.println("1. Pendiente");
        System.out.println("2. En Preparacion");
        System.out.println("3. Listo");
        System.out.println("4. Entregado");
        System.out.println("5. Cancelado");

        System.out.print("Ingrese el nuevo estado: ");
        String nuevoEstado = scanner.nextLine();

        // Usamos el setter que valida el estado.
        pedidoEncontrado.setEstado(nuevoEstado);
    }

    // Mantenemos los metodos anteriores.
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

    public static void mostrarInventarioIngredientes(Ingrediente[] ingredientes) {
        System.out.println("\n////////////////////////////////////////");
        System.out.println("///   INVENTARIO DE INGREDIENTES    ///");
        System.out.println("////////////////////////////////////////");

        for (int i = 0; i < ingredientes.length; i++) {
            System.out.print((i + 1) + ". ");
            System.out.println(ingredientes[i]);
        }

        System.out.println();
    }
}
```

## Conceptos Clave de Colecciones

### 1. ArrayList vs Array
- Array: Tamaño fijo, acceso con corchetes `arr[i]`
- ArrayList: Tamaño dinámico, acceso con métodos `list.get(i)`

### 2. Métodos Principales de ArrayList
- `add()`: Agregar elementos
- `remove()`: Eliminar elementos
- `get()`: Obtener elemento en posición
- `size()`: Cantidad de elementos
- `isEmpty()`: Verificar si está vacío

### 3. Operaciones CRUD
- Create: `add()` para agregar nuevos pedidos
- Read: `get()` y ciclos para leer pedidos
- Update: Modificar objetos existentes con setters
- Delete: `remove()` para eliminar pedidos

### 4. For-Each vs For Tradicional
- For-each: Cuando solo necesitas el valor
- For tradicional: Cuando necesitas el índice

## Probando el Sistema

Ejecuta y prueba:
1. Crear varios pedidos con diferentes productos
2. Ver el historial completo
3. Buscar pedidos específicos
4. Actualizar estados de pedidos
5. Intentar crear pedidos sin productos

## Lo que Viene

En la siguiente parte, vamos a aplicar herencia. Crearemos:
- Una clase base `Producto`
- Subclases `Pizza` y `Bebida`
- Uso de `super()` y `@Override`
- Polimorfismo básico

Ya tenemos ciclos, encapsulación y colecciones. Ahora necesitamos jerarquías de clases para organizar mejor nuestro código.

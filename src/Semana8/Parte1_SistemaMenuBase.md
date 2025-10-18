# Parte 1: Sistema de Menú Base

En esta primera parte vamos a construir el sistema base de nuestra pizzería. Crearemos un menú interactivo que permite al usuario navegar entre diferentes opciones usando la consola de NetBeans.

## Configuración Inicial en NetBeans

Antes de escribir código, necesitamos preparar nuestro proyecto:

1. Abre NetBeans y crea un nuevo proyecto Java
2. Ve a File → New Project → Java Application
3. Nombra el proyecto "SistemaPizzeria"
4. Asegúrate de marcar "Create Main Class"
5. Haz clic en Finish

NetBeans creará automáticamente una clase Main con el método `public static void main(String[] args)`. Ahí es donde escribiremos nuestro código.

## El Código Completo

```java
package sistemapizzeria;

import java.util.Scanner;

public class SistemaPizzeria {

    public static void main(String[] args) {

        // Vamos a crear una aplicacion que muestre un menu al usuario.
        // Para que el usuario pueda elegir opciones, necesitamos una forma de leer lo que escribe.
        // Java nos proporciona la clase Scanner que hace exactamente eso.
        // La creamos al inicio porque la vamos a usar durante toda la ejecucion del programa.
        Scanner scanner = new Scanner(System.in);

        // Nuestro programa debe seguir mostrando el menu hasta que el usuario decida salir.
        // Para controlar esto, usamos una variable booleana que actua como un interruptor.
        // Mientras esta variable sea true, el menu seguira apareciendo.
        // Cuando el usuario elija salir, la cambiaremos a false y el programa terminara.
        boolean sistemaActivo = true;

        // Aqui empieza el ciclo principal de nuestra aplicacion.
        // Un ciclo while repite todo lo que esta dentro de las llaves mientras la condicion sea verdadera.
        // Esto es perfecto para un menu porque queremos que el usuario pueda hacer varias acciones.
        // Solo cuando el usuario elija "Salir" es que sistemaActivo se volvera false y saldremos del ciclo.
        while (sistemaActivo) {

            // Mostramos el menu principal.
            // Usamos println para imprimir cada linea en la consola.
            // Las barras diagonales ayudan a que el menu se vea organizado y facil de leer.
            System.out.println("\n////////////////////////////////////////");
            System.out.println("///   PIZZERIA BELLA NAPOLI         ///");
            System.out.println("////////////////////////////////////////");
            System.out.println("1. Ver Menu de Pizzas");
            System.out.println("2. Ver Menu de Bebidas");
            System.out.println("3. Buscar Pizza por Nombre");
            System.out.println("4. Salir");
            System.out.println("////////////////////////////////////////");
            System.out.print("Seleccione una opcion: ");

            // Ahora leemos el numero que el usuario escriba.
            // nextInt() lee un numero entero desde el teclado.
            // Este numero lo guardamos en la variable opcion para poder evaluarlo despues.
            int opcion = scanner.nextInt();

            // Tenemos que hacer esta limpieza del buffer.
            // Cuando el usuario presiona Enter despues de escribir el numero, queda un salto de linea.
            // nextInt() lee el numero pero NO consume ese salto de linea.
            // Si no lo limpiamos, puede causar problemas cuando queramos leer texto mas adelante.
            scanner.nextLine();

            // Ahora necesitamos hacer algo diferente dependiendo de que opcion eligio el usuario.
            // Podriamos usar varios if, pero switch es mas claro cuando tenemos varias opciones especificas.
            // El switch evalua la variable opcion y ejecuta el bloque de codigo que coincida con el case.
            switch (opcion) {
                case 1:
                    // El usuario quiere ver las pizzas disponibles.
                    // En lugar de escribir todo el codigo aqui, lo organizamos en un metodo separado.
                    // Esto hace que nuestro codigo sea mas facil de leer y mantener.
                    mostrarMenuPizzas();
                    break;

                case 2:
                    // El usuario quiere ver las bebidas disponibles.
                    // Igual que con las pizzas, usamos un metodo separado.
                    mostrarMenuBebidas();
                    break;

                case 3:
                    // El usuario quiere buscar una pizza especifica por nombre.
                    // Primero necesitamos pedirle que escriba el nombre que quiere buscar.
                    System.out.print("Ingrese el nombre de la pizza: ");
                    String nombreBuscar = scanner.nextLine();

                    // Ahora llamamos al metodo de busqueda pasandole el nombre que el usuario escribio.
                    buscarPizza(nombreBuscar);
                    break;

                case 4:
                    // El usuario decidio salir del sistema.
                    // Mostramos un mensaje de despedida amable.
                    System.out.println("\nGracias por usar el Sistema Pizzeria Bella Napoli!");
                    System.out.println("Hasta pronto!");

                    // Cambiamos sistemaActivo a false.
                    // Esto hara que en la proxima evaluacion del while, la condicion sea falsa.
                    // El ciclo terminara y el programa finalizara.
                    sistemaActivo = false;
                    break;

                default:
                    // Si el usuario escribe un numero que no esta en las opciones (por ejemplo 5 o 99),
                    // caemos en este bloque default.
                    // Es importante dar retroalimentacion al usuario cuando comete un error.
                    System.out.println("\nOpcion invalida. Por favor seleccione 1, 2, 3 o 4.");
            }
        }

        // Cuando salimos del ciclo while significa que el programa va a terminar.
        // Es una buena practica cerrar el Scanner para liberar los recursos del sistema.
        scanner.close();
    }

    // Vamos a crear un metodo que muestre todas las pizzas disponibles.
    // Los metodos nos permiten organizar nuestro codigo en bloques reutilizables.
    // static significa que este metodo pertenece a la clase, no a un objeto especifico.
    // void significa que no devuelve ningun valor, solo ejecuta acciones.
    public static void mostrarMenuPizzas() {

        // Necesitamos almacenar los nombres de las pizzas.
        // Un array es perfecto para esto porque es una lista ordenada de elementos del mismo tipo.
        // Cada pizza tendra un indice: la primera es 0, la segunda es 1, y asi sucesivamente.
        String[] nombresPizzas = {
            "Margarita",
            "Pepperoni",
            "Hawaiana",
            "Cuatro Quesos",
            "Vegetariana"
        };

        // Necesitamos tambien los precios de cada pizza.
        // Creamos otro array de numeros enteros donde la posicion coincide con el array de nombres.
        // Esto significa que preciosPizzas[0] es el precio de nombresPizzas[0].
        int[] preciosPizzas = {
            5990,
            6990,
            7490,
            7990,
            6490
        };

        // Mostramos un encabezado para que el usuario sepa que esta viendo.
        System.out.println("\n////////////////////////////////////////");
        System.out.println("///       MENU DE PIZZAS            ///");
        System.out.println("////////////////////////////////////////");

        // Ahora necesitamos mostrar todas las pizzas.
        // Podriamos escribir System.out.println 5 veces, pero si mañana agregamos mas pizzas tendriamos que modificar mucho codigo.
        // En su lugar, usamos un ciclo for que recorre automaticamente todo el array.
        // El ciclo empieza en i=0 (primera pizza), continua mientras i sea menor que la cantidad de pizzas,
        // y en cada vuelta aumenta i en 1 para pasar a la siguiente pizza.
        for (int i = 0; i < nombresPizzas.length; i++) {

            // Mostramos cada pizza con su informacion.
            // i+1 porque queremos mostrar al usuario "1. Margarita" no "0. Margarita".
            // Los humanos preferimos contar desde 1, pero Java cuenta desde 0.
            System.out.printf("%d. %-20s $%d%n",
                (i + 1),
                nombresPizzas[i],
                preciosPizzas[i]
            );
        }

        // Agregamos una linea en blanco para separar visualmente el menu del resto.
        System.out.println();
    }

    // Creamos un metodo similar para mostrar las bebidas.
    // La logica es identica a mostrarMenuPizzas, solo cambian los datos.
    public static void mostrarMenuBebidas() {

        // Array con los nombres de las bebidas que vendemos.
        String[] nombresBebidas = {
            "Coca-Cola",
            "Fanta",
            "Sprite",
            "Agua Mineral",
            "Jugo Natural"
        };

        // Array con los precios correspondientes a cada bebida.
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

        // Usamos el mismo patron de ciclo for para recorrer todas las bebidas.
        for (int i = 0; i < nombresBebidas.length; i++) {
            System.out.printf("%d. %-20s $%d%n",
                (i + 1),
                nombresBebidas[i],
                preciosBebidas[i]
            );
        }

        System.out.println();
    }

    // Este metodo permite buscar una pizza especifica por su nombre.
    // Recibe como parametro el texto que el usuario quiere buscar.
    public static void buscarPizza(String nombreBuscar) {

        // Necesitamos nuevamente los datos de las pizzas.
        // En esta primera version tenemos que repetir estos arrays.
        // Mas adelante aprenderemos una forma mejor de almacenar estos datos
        // para no tener que escribirlos multiples veces.
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

        // Necesitamos una forma de saber si encontramos la pizza o no.
        // Usamos un boolean que empieza como false (no encontrada).
        // Si durante la busqueda la encontramos, lo cambiaremos a true.
        boolean encontrada = false;

        // Informamos al usuario que estamos procesando su busqueda.
        System.out.println("\nBuscando: " + nombreBuscar);
        System.out.println("---------------------------------------");

        // Ahora recorremos todas las pizzas buscando una coincidencia.
        // Usamos un ciclo for porque queremos revisar cada elemento del array.
        for (int i = 0; i < nombresPizzas.length; i++) {

            // Comparamos el nombre que el usuario busca con el nombre de la pizza actual.
            // equalsIgnoreCase compara textos sin importar mayusculas o minusculas.
            // Esto significa que si el usuario escribe "margarita", "MARGARITA" o "Margarita",
            // todas se consideraran iguales y encontraremos la pizza.
            if (nombresPizzas[i].equalsIgnoreCase(nombreBuscar)) {

                // Encontramos una coincidencia.
                // Mostramos la informacion de la pizza al usuario.
                System.out.println("Encontrada: " + nombresPizzas[i]);
                System.out.println("Precio: $" + preciosPizzas[i]);

                // Cambiamos la bandera a true para indicar que si la encontramos.
                encontrada = true;

                // Usamos break para salir del ciclo inmediatamente.
                // No tiene sentido seguir buscando si ya encontramos lo que queriamos.
                // Esto tambien hace nuestro programa mas eficiente.
                break;
            }
        }

        // Despues del ciclo, verificamos si encontramos algo.
        // Si encontrada sigue siendo false, significa que revisamos todas las pizzas
        // y ninguna coincidio con lo que el usuario buscaba.
        if (!encontrada) {
            System.out.println("No se encontro una pizza con ese nombre.");
            System.out.println("Por favor verifique el nombre e intente nuevamente.");
        }

        System.out.println();
    }
}
```

## Conceptos Clave Aplicados

### 1. Ciclo While para el Menú Principal

El ciclo `while` es perfecto para menús porque:
- Se ejecuta mientras una condición sea verdadera
- Permite que el usuario realice múltiples acciones
- Solo termina cuando el usuario decide salir

### 2. Ciclo For para Recorrer Arrays

El ciclo `for` es ideal cuando sabemos cuántas veces necesitamos iterar:
- Controlamos la posición actual con un índice
- Verificamos que no nos salgamos del array con la condición
- Avanzamos automáticamente al siguiente elemento

### 3. Switch para Múltiples Opciones

El `switch` hace el código más legible que múltiples `if-else`:
- Cada `case` representa una opción del menú
- `break` evita que se ejecuten los siguientes casos
- `default` maneja opciones inválidas

## Probando el Sistema

Para probar tu aplicación en NetBeans:

1. Haz clic derecho en el proyecto → Run
2. Prueba cada opción del menú
3. Intenta ingresar opciones inválidas para ver el manejo de errores
4. Busca pizzas que existen y que no existen
5. Finalmente, usa la opción 4 para salir correctamente

## Lo que Viene

En la siguiente parte, vamos a mejorar este sistema creando una clase `Ingrediente` que nos permitirá:
- Almacenar información de manera más organizada
- Aplicar encapsulación para proteger los datos
- Validar la información que ingresamos

Por ahora, tenemos un sistema funcional con un menú interactivo que demuestra el uso de ciclos en Java.

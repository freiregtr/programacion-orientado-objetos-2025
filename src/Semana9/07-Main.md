# Main - El Programa Principal

## ¿Qué vamos a crear?

Finalmente creamos la clase `Main`, que es el punto de entrada de nuestra aplicación. Esta clase contiene el menú interactivo que permite al usuario usar todas las funcionalidades del sistema: ingresar mascotas, buscarlas, aplicar ajustes y calcular descuentos.

Aquí integramos todo lo que hemos construido: creamos objetos `Perro` y `Gato`, los gestionamos con la clase `Clinica`, y permitimos la interacción mediante un menú con ciclos y decisiones.

## Conceptos POO Aplicados

- **Ciclos**: while para el menú, for para procesar múltiples mascotas
- **Decisiones**: switch-case para el menú, if-else para validaciones
- **Entrada de datos**: Scanner para leer desde consola
- **Integración**: Uso de todas las clases creadas trabajando juntas

## Código Completo

```java
// Importamos Scanner para leer entrada del usuario desde consola
import java.util.Scanner;

// Clase Main: punto de entrada del programa
public class Main {

    // Método main: aquí comienza la ejecución del programa
    public static void main(String[] args) {

        // Creamos un Scanner para leer datos ingresados por el usuario
        Scanner scanner = new Scanner(System.in);

        // Creamos el objeto Clinica que gestionará todas las mascotas
        Clinica clinica = new Clinica();

        // Variable de control para el ciclo del menú
        boolean continuar = true;

        // Ciclo principal: se ejecuta hasta que el usuario elija salir
        while (continuar) {

            // Mostramos el menú de opciones
            System.out.println("\n════════════════════════════════════════");
            System.out.println("   CLÍNICA VETERINARIA PATITASFELICES");
            System.out.println("════════════════════════════════════════");
            System.out.println("1. Ingresar Mascota");
            System.out.println("2. Mostrar Información de Mascota");
            System.out.println("3. Aplicar Ajuste de Costo");
            System.out.println("4. Calcular Descuento Total por Vacunación");
            System.out.println("5. Salir");
            System.out.print("\nSeleccione una opción: ");

            // Leemos la opción seleccionada
            int opcion = scanner.nextInt();

            // Limpiamos el buffer del scanner
            // Esto es necesario después de nextInt() para evitar problemas con nextLine()
            scanner.nextLine();

            // Procesamos la opción usando switch-case
            switch (opcion) {

                case 1:
                    // OPCIÓN 1: Ingresar Mascota
                    // Mostramos submenú para elegir tipo de mascota
                    System.out.println("\n¿Qué tipo de mascota desea ingresar?");
                    System.out.println("1. Perro");
                    System.out.println("2. Gato");
                    System.out.print("Opción: ");
                    int tipo = scanner.nextInt();
                    scanner.nextLine();

                    // Solicitamos los datos comunes a todas las mascotas
                    System.out.print("Código: ");
                    String codigo = scanner.nextLine();

                    System.out.print("Nombre: ");
                    String nombre = scanner.nextLine();

                    System.out.print("Especie: ");
                    String especie = scanner.nextLine();

                    System.out.print("Costo de consulta: ");
                    double costo = scanner.nextDouble();

                    System.out.print("Edad: ");
                    int edad = scanner.nextInt();
                    scanner.nextLine();

                    // Según el tipo elegido, creamos Perro o Gato
                    if (tipo == 1) {
                        // Es un perro: solicitamos datos específicos

                        System.out.print("Raza: ");
                        String raza = scanner.nextLine();

                        System.out.print("Tamaño (pequeño/grande): ");
                        String tamanio = scanner.nextLine();

                        // Creamos el objeto Perro con todos los datos
                        Perro perro = new Perro(codigo, nombre, especie, costo, edad, raza, tamanio);

                        // Intentamos ingresar el perro a la clínica
                        clinica.ingresarMascota(perro);

                    } else if (tipo == 2) {
                        // Es un gato: solicitamos datos específicos

                        System.out.print("Tipo de pelaje (corto/largo): ");
                        String pelaje = scanner.nextLine();

                        System.out.print("¿Es exótico? (true/false): ");
                        boolean exotico = scanner.nextBoolean();
                        scanner.nextLine();

                        // Creamos el objeto Gato con todos los datos
                        Gato gato = new Gato(codigo, nombre, especie, costo, edad, pelaje, exotico);

                        // Intentamos ingresar el gato a la clínica
                        clinica.ingresarMascota(gato);

                    } else {
                        // Opción inválida
                        System.out.println("Opción inválida");
                    }
                    break;

                case 2:
                    // OPCIÓN 2: Mostrar Información de Mascota
                    // Solicitamos el código de la mascota a buscar
                    System.out.print("Ingrese el código de la mascota: ");
                    String codigoBuscar = scanner.nextLine();

                    // Buscamos la mascota en la clínica
                    Mascota encontrada = clinica.buscarMascota(codigoBuscar);

                    // Verificamos si se encontró
                    if (encontrada != null) {
                        // Si existe, mostramos su información usando toString()
                        System.out.println("\n--- Información de la Mascota ---");
                        System.out.println(encontrada.toString());
                    }
                    // Si es null, buscarMascota() ya mostró el mensaje de error
                    break;

                case 3:
                    // OPCIÓN 3: Aplicar Ajuste de Costo
                    // Ejecutamos el método que aplica ajuste a todos los gatos con pelaje corto
                    int cantidadAjustada = clinica.aplicarAjusteATodos();

                    // Mostramos cuántas mascotas fueron ajustadas
                    System.out.println("Se aplicó ajuste de costo a " + cantidadAjustada +
                                     " gatos con pelaje corto");
                    break;

                case 4:
                    // OPCIÓN 4: Calcular Descuento Total por Vacunación
                    // Ejecutamos el método que calcula el total de descuentos
                    double totalDescuento = clinica.calcularDescuentoTotal();

                    // Mostramos el resultado con formato de 2 decimales
                    System.out.printf("Total de descuentos por vacunación: $%.2f\n", totalDescuento);
                    break;

                case 5:
                    // OPCIÓN 5: Salir
                    // Mostramos mensaje de despedida
                    System.out.println("\n¡Gracias por usar el sistema PatitasFelices!");
                    System.out.println("¡Hasta pronto!");

                    // Cambiamos la variable de control para salir del ciclo
                    continuar = false;
                    break;

                default:
                    // Opción inválida (no está entre 1 y 5)
                    System.out.println("Opción inválida. Por favor seleccione una opción del 1 al 5");
                    break;
            }
        }

        // Cerramos el scanner para liberar recursos
        scanner.close();
    }
}
```

## Explicación Paso a Paso

**Scanner:**
Creamos un objeto `Scanner` conectado a `System.in` (entrada estándar = teclado). Esto nos permite leer datos que el usuario escribe en la consola.

**El objeto Clinica:**
Creamos una instancia de `Clinica` que se mantendrá viva durante toda la ejecución del programa. Todas las mascotas que ingresemos se almacenarán en este objeto.

**El ciclo while:**
`while (continuar)` ejecuta el menú repetidamente mientras `continuar` sea `true`. Solo cuando el usuario elija la opción 5 (Salir), cambiamos `continuar` a `false` y el programa termina.

**scanner.nextLine() después de nextInt():**
Este es un detalle técnico importante. Cuando usamos `nextInt()`, lee el número pero deja el "Enter" en el buffer. Si después usamos `nextLine()`, leerá ese "Enter" vacío. Por eso siempre llamamos `scanner.nextLine()` después de `nextInt()` para limpiar el buffer.

**switch-case:**
Procesamos cada opción del menú. Cada `case` maneja una funcionalidad diferente. El `default` captura opciones inválidas.

**Opción 1 - Ingresar Mascota:**
Primero preguntamos si es perro o gato. Luego pedimos los datos comunes (código, nombre, especie, costo, edad). Según el tipo, pedimos datos específicos (raza y tamaño para perros, pelaje y exótico para gatos). Creamos el objeto correspondiente y lo ingresamos a la clínica.

**Opción 2 - Mostrar Información:**
Pedimos el código, buscamos la mascota con `clinica.buscarMascota()`, y si retorna algo diferente de `null`, mostramos su información usando `toString()`.

**Opción 3 - Aplicar Ajuste:**
Simplemente llamamos a `clinica.aplicarAjusteATodos()`, guardamos el valor retornado (cantidad de mascotas ajustadas) y lo mostramos.

**Opción 4 - Calcular Descuento:**
Llamamos a `clinica.calcularDescuentoTotal()`, guardamos el total y lo mostramos con formato de 2 decimales usando `printf()`.

**Opción 5 - Salir:**
Mostramos mensaje de despedida y cambiamos `continuar` a `false` para terminar el ciclo.

## Ejemplo de Ejecución

```
════════════════════════════════════════
   CLÍNICA VETERINARIA PATITASFELICES
════════════════════════════════════════
1. Ingresar Mascota
2. Mostrar Información de Mascota
3. Aplicar Ajuste de Costo
4. Calcular Descuento Total por Vacunación
5. Salir

Seleccione una opción: 1

¿Qué tipo de mascota desea ingresar?
1. Perro
2. Gato
Opción: 1
Código: P001
Nombre: Firulais
Especie: Canino
Costo de consulta: 20000
Edad: 3
Raza: Labrador
Tamaño (pequeño/grande): pequeño
Mascota ingresada exitosamente
```

## Pruebas Recomendadas

1. Ingresar varios perros pequeños y grandes
2. Ingresar varios gatos con pelaje corto y largo, algunos exóticos
3. Intentar ingresar una mascota con código duplicado (debe rechazarse)
4. Buscar mascotas existentes y no existentes
5. Aplicar ajuste y verificar que cuenta solo gatos con pelaje corto
6. Calcular descuento y verificar que suma solo perros pequeños
7. Probar todas las validaciones del menú

## ¡Felicidades!

Has completado todo el sistema de gestión de la clínica veterinaria PatitasFelices. Has aplicado todos los conceptos clave de POO:

✅ **Herencia**: Perro y Gato heredan de Mascota
✅ **Abstracción**: Clase abstracta Mascota con métodos abstractos
✅ **Polimorfismo**: Colección de Mascota que contiene Perro y Gato
✅ **Interfaces**: PlanPrevencion implementada por Perro
✅ **Encapsulación**: Atributos privados con getters y setters
✅ **Colecciones**: ArrayList para gestionar múltiples mascotas
✅ **Ciclos**: for-each, while para procesar datos

El sistema está listo para ser compilado, ejecutado y entregado. ¡Éxito en tu evaluación!

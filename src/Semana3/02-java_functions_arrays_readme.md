# Java Fundamentals - README 2
## Funciones, Arrays y Estructuras de Control

> **Requisitos**: Java JDK 11 o superior (usa `.repeat()` y otras caracteristicas modernas)
> 
> **IDE Sugerido**: NetBeans con configuracion de autocompletado
>
> **Configuracion**: Ver `netbeans_setup.md` para templates y shortcuts utiles

### Objetivos de Aprendizajee
Al completar esta guia, seras capaz de:
- Crear y usar funciones (metodos) en Java
- Manejar arrays (arreglos) de datos
- Implementar estructuras de control (if/else, switch)
- Usar ciclos (for, while) correctammente
- Combinar todos estos conceptos en programas mas complejos

---

## 1. Funciones (Metodos) en Java

### 1.1 Que es una Funcion?

Una **funcion** (llamada metodo en Java) es un bloque de codigo que realiza una tarea especifica y puede ser reutilizzado multiples veces.

**Sintaxis basica:**
```java
modificadorAcceso tipoRetorno nombreMetodo(parametros) {
    // codigo del metodo
    return valor; // opcional
}
```

### 1.2 Funciones sin Retorno (void)

```java
public class FuncionesBasicas {
    
    // Función que solo imprime un mensaje
    public static void saludar() {
        System.out.println("¡Hola! Bienvenido a Java");
        System.out.println("Este es mi primer método");
    }
    
    // Función que recibe un parámetro
    public static void saludarPersona(String nombre) {
        System.out.println("¡Hola " + nombre + "!");
        System.out.println("Es un placer conocerte");
    }
    
    // Función que recibe múltiples parámetros
    public static void mostrarInformacion(String nombre, int edad, String ciudad) {
        System.out.println("=== INFORMACIÓN PERSONAL ===");
        System.out.println("Nombre: " + nombre);           // Parámetro tipo String
        System.out.println("Edad: " + edad + " años");     // Parámetro tipo int
        System.out.println("Ciudad: " + ciudad);           // Parámetro tipo String
        System.out.println("===========================");
    }
    
    public static void main(String[] args) {
        // Llamando a la función simple
        saludar();
        
        System.out.println(); // Línea en blanco para separar
        
        // Llamando a la función con un parámetro
        saludarPersona("María");
        saludarPersona("Juan");
        
        System.out.println(); // Línea en blanco para separar
        
        // Llamando a la función con múltiples parámetros
        mostrarInformacion("Ana García", 22, "Santiago");
        mostrarInformacion("Carlos López", 19, "Valparaíso");
    }
}
```

### 1.3 Funciones con Retorno

```java
public class FuncionesConRetorno {
    
    // Función que suma dos números y retorna el resultado
    public static int sumar(int numero1, int numero2) {
        int resultado = numero1 + numero2;  // Calculamos la suma
        return resultado;                    // Devolvemos el resultado
    }
    
    // Función que calcula el área de un rectángulo
    public static double calcularAreaRectangulo(double largo, double ancho) {
        double area = largo * ancho;        // Fórmula: largo × ancho
        return area;                        // Retornamos el área calculada
    }
    
    // Función que determina si un número es par
    public static boolean esPar(int numero) {
        boolean resultado = (numero % 2 == 0);  // Si el residuo es 0, es par
        return resultado;                        // Retorna true si es par, false si es impar
    }
    
    // Función que crea un saludo personalizado
    public static String crearSaludo(String nombre, String apellido) {
        String saludoCompleto = "¡Hola " + nombre + " " + apellido + "! ¿Cómo estás?";
        return saludoCompleto;              // Retorna el saludo como String
    }
    
    // Función que calcula el promedio de tres notas
    public static double calcularPromedio(double nota1, double nota2, double nota3) {
        double suma = nota1 + nota2 + nota3;    // Sumamos las tres notas
        double promedio = suma / 3;             // Dividimos entre 3 para obtener el promedio
        return promedio;                        // Retornamos el promedio
    }
    
    public static void main(String[] args) {
        // Usando función que retorna int
        int resultadoSuma = sumar(15, 25);
        System.out.println("La suma de 15 + 25 = " + resultadoSuma);
        
        // Podemos usar directamente el resultado de la función
        System.out.println("La suma de 8 + 12 = " + sumar(8, 12));
        
        System.out.println(); // Línea en blanco
        
        // Usando función que retorna double
        double area = calcularAreaRectangulo(5.5, 3.2);
        System.out.println("El área del rectángulo es: " + area + " metros cuadrados");
        
        System.out.println(); // Línea en blanco
        
        // Usando función que retorna boolean
        int numeroParaPrueba = 24;
        boolean esNumeroPar = esPar(numeroParaPrueba);
        System.out.println("¿El número " + numeroParaPrueba + " es par? " + esNumeroPar);
        
        // Probando con un número impar
        System.out.println("¿El número 17 es par? " + esPar(17));
        
        System.out.println(); // Línea en blanco
        
        // Usando función que retorna String
        String mensaje = crearSaludo("Ana", "Martínez");
        System.out.println(mensaje);
        
        System.out.println(); // Línea en blanco
        
        // Usando función para calcular promedio
        double nota1 = 8.5, nota2 = 7.2, nota3 = 9.1;
        double promedioFinal = calcularPromedio(nota1, nota2, nota3);
        System.out.println("Las notas son: " + nota1 + ", " + nota2 + ", " + nota3);
        System.out.println("El promedio es: " + promedioFinal);
    }
}
```

---

## 2. Arrays (Arreglos)

### 2.1 Que es un Array?

Un **array** es una estructura de datos que puede almacenar multiples valores del mismo tipo en una solla variable.

### 2.2 Declaracion e Inicializacion de Arrays

```java
public class ArraysBasicos {
    
    public static void main(String[] args) {
        // Forma 1: Declarar y luego asignar valores
        int[] numeros = new int[5];         // Array de 5 enteros (inicializado con 0s)
        numeros[0] = 10;                    // Primer elemento (índice 0)
        numeros[1] = 20;                    // Segundo elemento (índice 1)
        numeros[2] = 30;                    // Tercer elemento (índice 2)
        numeros[3] = 40;                    // Cuarto elemento (índice 3)
        numeros[4] = 50;                    // Quinto elemento (índice 4)
        
        System.out.println("=== ARRAY DE NÚMEROS ===");
        System.out.println("Primer número: " + numeros[0]);
        System.out.println("Tercer número: " + numeros[2]);
        System.out.println("Último número: " + numeros[4]);
        
        System.out.println(); // Línea en blanco
        
        // Forma 2: Declarar e inicializar al mismo tiempo
        String[] nombres = {"Juan", "María", "Carlos", "Ana", "Luis"};
        
        System.out.println("=== ARRAY DE NOMBRES ===");
        System.out.println("Primer nombre: " + nombres[0]);
        System.out.println("Segundo nombre: " + nombres[1]);
        System.out.println("Cantidad de nombres: " + nombres.length); // .length nos da el tamaño
        
        System.out.println(); // Línea en blanco
        
        // Array de números decimales
        double[] precios = {19.99, 25.50, 12.75, 8.30, 45.20};
        
        System.out.println("=== ARRAY DE PRECIOS ===");
        for (int i = 0; i < precios.length; i++) {  // Recorremos todo el array
            System.out.println("Precio " + (i + 1) + ": $" + precios[i]);
        }
        
        System.out.println(); // Línea en blanco
        
        // Array de valores booleanos
        boolean[] respuestas = {true, false, true, true, false};
        
        System.out.println("=== ARRAY DE RESPUESTAS ===");
        for (int i = 0; i < respuestas.length; i++) {
            System.out.println("Pregunta " + (i + 1) + ": " + respuestas[i]);
        }
    }
}
```

### 2.3 Funciones que Trabajan con Arrays

```java
public class FuncionesConArrays {
    
    // Función que muestra todos los elementos de un array de enteros
    public static void mostrarArray(int[] array) {
        System.out.print("Array: [");
        for (int i = 0; i < array.length; i++) {
            System.out.print(array[i]);
            if (i < array.length - 1) {    // Si no es el último elemento
                System.out.print(", ");    // Agregamos coma y espacio
            }
        }
        System.out.println("]");
    }
    
    // Función que encuentra el número más grande en un array
    public static int encontrarMaximo(int[] array) {
        int maximo = array[0];             // Asumimos que el primero es el más grande
        
        for (int i = 1; i < array.length; i++) {   // Empezamos desde el índice 1
            if (array[i] > maximo) {               // Si encontramos uno más grande
                maximo = array[i];                 // Lo guardamos como nuevo máximo
            }
        }
        
        return maximo;                     // Retornamos el número más grande
    }
    
    // Función que calcula el promedio de un array de números
    public static double calcularPromedioArray(int[] array) {
        int suma = 0;                      // Variable para acumular la suma
        
        for (int i = 0; i < array.length; i++) {
            suma = suma + array[i];        // Sumamos cada elemento
        }
        
        double promedio = (double) suma / array.length;  // Convertimos a double para decimales
        return promedio;
    }
    
    // Función que cuenta cuántos números son mayores a un valor dado
    public static int contarMayoresA(int[] array, int valor) {
        int contador = 0;                  // Contador inicializado en 0
        
        for (int i = 0; i < array.length; i++) {
            if (array[i] > valor) {        // Si el elemento es mayor al valor
                contador++;                // Incrementamos el contador
            }
        }
        
        return contador;                   // Retornamos cuántos encontramos
    }
    
    // Función que busca un nombre específico en un array de strings
    public static boolean buscarNombre(String[] nombres, String nombreBuscado) {
        for (int i = 0; i < nombres.length; i++) {
            if (nombres[i].equals(nombreBuscado)) {    // Usamos .equals() para comparar strings
                return true;                            // Si lo encontramos, retornamos true
            }
        }
        return false;                      // Si no lo encontramos, retornamos false
    }
    
    public static void main(String[] args) {
        // Creamos un array de números para probar nuestras funciones
        int[] numeros = {15, 8, 23, 4, 16, 42, 11, 7};
        
        System.out.println("=== TRABAJANDO CON ARRAYS ===");
        
        // Mostramos el array completo
        mostrarArray(numeros);
        
        // Encontramos el número más grande
        int numeroMaximo = encontrarMaximo(numeros);
        System.out.println("El número más grande es: " + numeroMaximo);
        
        // Calculamos el promedio
        double promedio = calcularPromedioArray(numeros);
        System.out.println("El promedio es: " + promedio);
        
        // Contamos cuántos son mayores a 15
        int mayoresA15 = contarMayoresA(numeros, 15);
        System.out.println("Números mayores a 15: " + mayoresA15);
        
        System.out.println(); // Línea en blanco
        
        // Probamos con un array de nombres
        String[] estudiantes = {"Juan", "María", "Carlos", "Ana", "Luis", "Carmen"};
        
        System.out.println("=== BUSCANDO ESTUDIANTES ===");
        System.out.println("¿Está María en la lista? " + buscarNombre(estudiantes, "María"));
        System.out.println("¿Está Pedro en la lista? " + buscarNombre(estudiantes, "Pedro"));
    }
}
```

---

## 3. Estructuras de Control

### 3.1 Condicionales (if/else)

```java
public class EstructurasCondicionales {
    
    // Función que determina si una persona puede votar
    public static void verificarEdadVotar(int edad) {
        if (edad >= 18) {                          // Si la edad es mayor o igual a 18
            System.out.println("Puedes votar");
        } else {                                   // Si no cumple la condición anterior
            System.out.println("No puedes votar todavia");
            int añosFaltantes = 18 - edad;
            System.out.println("Te faltan " + añosFaltantes + " años");
        }
    }
    
    // Función que clasifica una calificación
    public static void clasificarNota(double nota) {
        if (nota >= 9.0) {                         // Excelente
            System.out.println("Excelente - Nota: " + nota);
        } else if (nota >= 8.0) {                  // Muy bueno
            System.out.println("Muy Bueno - Nota: " + nota);
        } else if (nota >= 7.0) {                  // Bueno
            System.out.println("Bueno - Nota: " + nota);
        } else if (nota >= 6.0) {                  // Regular
            System.out.println("Regular - Nota: " + nota);
        } else {                                   // Insuficiente
            System.out.println("Insuficiente - Nota: " + nota);
        }
    }
    
    // Función que determina el precio con descuento
    public static double calcularPrecioConDescuento(double precio, boolean esEstudiante, int edad) {
        double descuento = 0.0;                    // Inicializamos el descuento en 0
        
        if (esEstudiante && edad < 25) {           // Si es estudiante Y menor de 25
            descuento = 0.20;                      // 20% de descuento
            System.out.println("Descuento estudiante joven: 20%");
        } else if (esEstudiante) {                 // Solo si es estudiante
            descuento = 0.10;                      // 10% de descuento
            System.out.println("Descuento estudiante: 10%");
        } else if (edad >= 65) {                   // Si es adulto mayor
            descuento = 0.15;                      // 15% de descuento
            System.out.println("Descuento adulto mayor: 15%");
        } else {                                   // Sin descuento
            System.out.println("Precio regular - Sin descuento");
        }
        
        double precioFinal = precio - (precio * descuento);  // Calculamos el precio final
        return precioFinal;
    }
    
    public static void main(String[] args) {
        System.out.println("=== VERIFICACIÓN DE EDAD PARA VOTAR ===");
        verificarEdadVotar(20);
        verificarEdadVotar(16);
        verificarEdadVotar(18);
        
        System.out.println(); // Línea en blanco
        
        System.out.println("=== CLASIFICACIÓN DE NOTAS ===");
        clasificarNota(9.5);
        clasificarNota(8.2);
        clasificarNota(7.8);
        clasificarNota(6.1);
        clasificarNota(4.5);
        
        System.out.println(); // Línea en blanco
        
        System.out.println("=== CÁLCULO DE PRECIOS CON DESCUENTO ===");
        double precioOriginal = 100.0;
        
        double precio1 = calcularPrecioConDescuento(precioOriginal, true, 22);   // Estudiante joven
        System.out.println("Precio final: $" + precio1);
        System.out.println();
        
        double precio2 = calcularPrecioConDescuento(precioOriginal, true, 30);   // Estudiante adulto
        System.out.println("Precio final: $" + precio2);
        System.out.println();
        
        double precio3 = calcularPrecioConDescuento(precioOriginal, false, 70);  // Adulto mayor
        System.out.println("Precio final: $" + precio3);
        System.out.println();
        
        double precio4 = calcularPrecioConDescuento(precioOriginal, false, 35);  // Sin descuento
        System.out.println("Precio final: $" + precio4);
    }
}
```

### 3.2 Switch

```java
public class EstructuraSwitch {
    
    // Función que convierte un número de día a nombre del día
    public static String obtenerNombreDia(int numeroDia) {
        String nombreDia;
        
        switch (numeroDia) {                       // Evaluamos la variable numeroDia
            case 1:                                // Si es 1
                nombreDia = "Lunes";
                break;                             // Importante: break para salir del switch
            case 2:                                // Si es 2
                nombreDia = "Martes";
                break;
            case 3:                                // Si es 3
                nombreDia = "Miércoles";
                break;
            case 4:                                // Si es 4
                nombreDia = "Jueves";
                break;
            case 5:                                // Si es 5
                nombreDia = "Viernes";
                break;
            case 6:                                // Si es 6
                nombreDia = "Sábado";
                break;
            case 7:                                // Si es 7
                nombreDia = "Domingo";
                break;
            default:                               // Si no coincide con ningún caso
                nombreDia = "Día inválido";
                break;
        }
        
        return nombreDia;
    }
    
    // Función que determina el tipo de día (laborable o fin de semana)
    public static void analizarTipoDia(int numeroDia) {
        switch (numeroDia) {
            case 1:                                // Lunes
            case 2:                                // Martes
            case 3:                                // Miércoles
            case 4:                                // Jueves
            case 5:                                // Viernes
                System.out.println("Es un día laborable");
                System.out.println("¡A trabajar o estudiar!");
                break;
            case 6:                                // Sábado
            case 7:                                // Domingo
                System.out.println("Es fin de semana");
                System.out.println("¡Tiempo de descansar!");
                break;
            default:
                System.out.println("Número de día inválido");
                break;
        }
    }
    
    // Función calculadora simple usando switch
    public static double calculadora(double num1, double num2, char operacion) {
        double resultado = 0;
        
        switch (operacion) {
            case '+':                              // Suma
                resultado = num1 + num2;
                System.out.println(num1 + " + " + num2 + " = " + resultado);
                break;
            case '-':                              // Resta
                resultado = num1 - num2;
                System.out.println(num1 + " - " + num2 + " = " + resultado);
                break;
            case '*':                              // Multiplicación
                resultado = num1 * num2;
                System.out.println(num1 + " * " + num2 + " = " + resultado);
                break;
            case '/':                              // División
                if (num2 != 0) {                   // Verificamos que no sea división por cero
                    resultado = num1 / num2;
                    System.out.println(num1 + " / " + num2 + " = " + resultado);
                } else {
                    System.out.println("Error: No se puede dividir por cero");
                    resultado = 0;
                }
                break;
            default:
                System.out.println("Operación no válida");
                break;
        }
        
        return resultado;
    }
    
    public static void main(String[] args) {
        System.out.println("=== DÍAS DE LA SEMANA ===");
        
        // Probamos diferentes días
        for (int dia = 1; dia <= 7; dia++) {
            String nombre = obtenerNombreDia(dia);
            System.out.println("Día " + dia + ": " + nombre);
        }
        
        // Probamos con un día inválido
        System.out.println("Día 10: " + obtenerNombreDia(10));
        
        System.out.println(); // Línea en blanco
        
        System.out.println("=== ANÁLISIS DE TIPO DE DÍA ===");
        analizarTipoDia(3);  // Miércoles
        System.out.println();
        analizarTipoDia(7);  // Domingo
        
        System.out.println(); // Línea en blanco
        
        System.out.println("=== CALCULADORA CON SWITCH ===");
        calculadora(10, 5, '+');     // Suma
        calculadora(10, 5, '-');     // Resta
        calculadora(10, 5, '*');     // Multiplicación
        calculadora(10, 5, '/');     // División
        calculadora(10, 0, '/');     // División por cero
        calculadora(10, 5, '%');     // Operación inválida
    }
}
```

---

## 4. Ciclos (Loops)

### 4.1 Ciclo for

```java
public class CiclosFor {
    
    // Función que cuenta del 1 al número dado
    public static void contarHasta(int numero) {
        System.out.println("Contando del 1 al " + numero + ":");
        
        for (int i = 1; i <= numero; i++) {        // i empieza en 1, mientras sea <= numero, i++
            System.out.print(i + " ");
        }
        System.out.println(); // Nueva línea al final
    }
    
    // Función que cuenta hacia atrás
    public static void contarHaciaAtras(int desde, int hasta) {
        System.out.println("Contando desde " + desde + " hasta " + hasta + ":");
        
        for (int i = desde; i >= hasta; i--) {     // i empieza en 'desde', mientras sea >= hasta, i--
            System.out.print(i + " ");
        }
        System.out.println(); // Nueva línea al final
    }
    
    // Función que muestra la tabla de multiplicar
    public static void mostrarTablaMultiplicar(int numero) {
        System.out.println("=== TABLA DEL " + numero + " ===");
        
        for (int i = 1; i <= 10; i++) {            // Del 1 al 10
            int resultado = numero * i;             // Calculamos el resultado
            System.out.println(numero + " × " + i + " = " + resultado);
        }
    }
    
    // Función que suma todos los números pares del 1 al límite dado
    public static int sumarNumerosPares(int limite) {
        int suma = 0;                              // Acumulador para la suma
        
        System.out.print("Números pares del 2 al " + limite + ": ");
        
        for (int i = 2; i <= limite; i += 2) {    // Empezamos en 2, incrementamos de 2 en 2
            suma += i;                             // suma = suma + i
            System.out.print(i + " ");
        }
        System.out.println();
        
        return suma;                               // Retornamos la suma total
    }
    
    public static void main(String[] args) {
        System.out.println("=== EJEMPLOS DE CICLO FOR ===");
        
        // Contar del 1 al 5
        contarHasta(5);
        System.out.println();
        
        // Contar hacia atrás del 10 al 1
        contarHaciaAtras(10, 1);
        System.out.println();
        
        // Mostrar tabla del 7
        mostrarTablaMultiplicar(7);
        System.out.println();
        
        // Sumar números pares
        int sumaPares = sumarNumerosPares(20);
        System.out.println("La suma de todos los pares es: " + sumaPares);
    }
}
```

### 4.2 Ciclo while

```java
public class CiclosWhile {
    
    // Función que adivina un número (simulación)
    public static void juegoAdivinanza(int numeroSecreto) {
        int intento = 1;                           // Número de intento
        int numeroAdivinado = 0;                   // Número que "adivinamos"
        
        System.out.println("Juego de adivinanza - Número secreto: " + numeroSecreto);
        
        while (numeroAdivinado != numeroSecreto) { // Mientras no adivinemos el número
            numeroAdivinado = intento * 3;         // Estrategia simple de adivinanza
            
            System.out.println("Intento " + intento + ": ¿Es " + numeroAdivinado + "?");
            
            if (numeroAdivinado < numeroSecreto) {
                System.out.println("Demasiado bajo");
            } else if (numeroAdivinado > numeroSecreto) {
                System.out.println("Demasiado alto");
            } else {
                System.out.println("¡Correcto! Lo adiviné en " + intento + " intentos");
            }
            
            intento++;                             // Incrementamos el número de intento
            
            // Medida de seguridad para evitar bucle infinito
            if (intento > 20) {
                System.out.println("Me rindo después de 20 intentos");
                break;
            }
        }
    }
    
    // Función que cuenta dígitos de un número
    public static int contarDigitos(int numero) {
        int contador = 0;                          // Contador de dígitos
        int temp = Math.abs(numero);               // Usamos valor absoluto (sin signo)
        
        if (numero == 0) {                         // Caso especial: el 0 tiene 1 dígito
            return 1;
        }
        
        while (temp > 0) {                         // Mientras queden dígitos
            temp = temp / 10;                      // Dividimos por 10 para "quitar" el último dígito
            contador++;                            // Incrementamos el contador
        }
        
        return contador;                           // Retornamos el total de dígitos
    }
    
    // Función que simula un contador hacia atrás
    public static void contadorRegresivo(int inicio) {
        int contador = inicio;                     // Empezamos desde el número dado
        
        System.out.println("Contador regresivo desde " + inicio + ":");
        
        while (contador > 0) {                     // Mientras el contador sea mayor a 0
            System.out.println("" + contador);
            contador--;                            // Decrementamos el contador
            
            // Simulamos una pausa (en un programa real usarías Thread.sleep())
            try {
                Thread.sleep(500);                 // Pausa de 500 milisegundos
            } catch (InterruptedException e) {
                System.out.println("Contador interrumpido");
                Thread.currentThread().interrupt(); // Restaurar estado de interrupción
                break;                               // Salir del bucle
            }
        }
        
        System.out.println("¡DESPEGUE!");
    }
    
    public static void main(String[] args) {
        System.out.println("=== EJEMPLOS DE CICLO WHILE ===");
        
        // Juego de adivinanza
        juegoAdivinanza(15);
        System.out.println();
        
        // Contar dígitos
        int[] numeros = {123, 7, 0, -456, 99999};
        System.out.println("=== CONTAR DÍGITOS ===");
        for (int numero : numeros) {               // For-each loop (forma simplificada)
            int digitos = contarDigitos(numero);
            System.out.println("El número " + numero + " tiene " + digitos + " dígito(s)");
        }
        System.out.println();
        
        // Contador regresivo (comentado para no hacer esperar mucho)
        // contadorRegresivo(5);
        System.out.println("Contador regresivo omitido para ahorrar tiempo");
    }
}
```

---

## 5. Proyecto Integrador - Sistema de Notas

```java
public class SistemaNotas {
    
    // Función para mostrar el menú principal
    public static void mostrarMenu() {
        System.out.println("\n=== SISTEMA DE GESTIÓN DE NOTAS ===");
        System.out.println("1. Mostrar todas las notas");
        System.out.println("2. Calcular promedio");
        System.out.println("3. Encontrar nota más alta");
        System.out.println("4. Encontrar nota más baja");
        System.out.println("5. Contar notas por rango");
        System.out.println("6. Mostrar estadísticas completas");
        System.out.println("=====================================");
    }
    
    // Función para mostrar todas las notas con sus índices
    public static void mostrarNotas(double[] notas, String[] estudiantes) {
        System.out.println("\nLISTA DE NOTAS:");
        for (int i = 0; i < notas.length; i++) {
            System.out.println((i + 1) + ". " + estudiantes[i] + ": " + notas[i]);
        }
    }
    
    // Función para calcular el promedio de las notas
    public static double calcularPromedio(double[] notas) {
        double suma = 0.0;                         // Acumulador para la suma
        
        for (int i = 0; i < notas.length; i++) {
            suma += notas[i];                      // Sumamos cada nota
        }
        
        double promedio = suma / notas.length;     // Dividimos la suma entre el total de notas
        return promedio;
    }
    
    // Función para encontrar la nota más alta y el estudiante
    public static void encontrarNotaMasAlta(double[] notas, String[] estudiantes) {
        double notaMaxima = notas[0];              // Asumimos que la primera es la más alta
        int indiceMaximo = 0;                      // Guardamos el índice de la nota más alta
        
        for (int i = 1; i < notas.length; i++) {
            if (notas[i] > notaMaxima) {           // Si encontramos una nota más alta
                notaMaxima = notas[i];             // La guardamos como nueva máxima
                indiceMaximo = i;                  // Guardamos su índice
            }
        }
        
        System.out.println("\nNOTA MÁS ALTA:");
        System.out.println("Estudiante: " + estudiantes[indiceMaximo]);
        System.out.println("Nota: " + notaMaxima);
    }
    
    // Función para encontrar la nota más baja y el estudiante
    public static void encontrarNotaMasBaja(double[] notas, String[] estudiantes) {
        double notaMinima = notas[0];              // Asumimos que la primera es la más baja
        int indiceMinimo = 0;                      // Guardamos el índice de la nota más baja
        
        for (int i = 1; i < notas.length; i++) {
            if (notas[i] < notaMinima) {           // Si encontramos una nota más baja
                notaMinima = notas[i];             // La guardamos como nueva mínima
                indiceMinimo = i;                  // Guardamos su índice
            }
        }
        
        System.out.println("\nNOTA MÁS BAJA:");
        System.out.println("Estudiante: " + estudiantes[indiceMinimo]);
        System.out.println("Nota: " + notaMinima);
    }
    
    // Función para contar notas por rangos
    public static void contarNotasPorRango(double[] notas) {
        int excelentes = 0;    // 9.0 - 10.0
        int muyBuenas = 0;     // 8.0 - 8.9
        int buenas = 0;        // 7.0 - 7.9
        int regulares = 0;     // 6.0 - 6.9
        int insuficientes = 0; // < 6.0
        
        for (int i = 0; i < notas.length; i++) {
            if (notas[i] >= 9.0) {
                excelentes++;
            } else if (notas[i] >= 8.0) {
                muyBuenas++;
            } else if (notas[i] >= 7.0) {
                buenas++;
            } else if (notas[i] >= 6.0) {
                regulares++;
            } else {
                insuficientes++;
            }
        }
        
        System.out.println("\nDISTRIBUCIÓN DE NOTAS:");
        System.out.println("Excelentes (9.0-10.0): " + excelentes);
        System.out.println("Muy Buenas (8.0-8.9): " + muyBuenas);
        System.out.println("Buenas (7.0-7.9): " + buenas);
        System.out.println("Regulares (6.0-6.9): " + regulares);
        System.out.println("Insuficientes (<6.0): " + insuficientes);
    }
    
    // Función que muestra estadísticas completas
    public static void mostrarEstadisticasCompletas(double[] notas, String[] estudiantes) {
        System.out.println("\nESTADÍSTICAS COMPLETAS:");
        System.out.println("Total de estudiantes: " + notas.length);
        
        double promedio = calcularPromedio(notas);
        System.out.println("Promedio general: " + String.format("%.2f", promedio));
        
        // Calculamos cuántos están por encima del promedio
        int arribaPromedio = 0;
        for (int i = 0; i < notas.length; i++) {
            if (notas[i] > promedio) {
                arribaPromedio++;
            }
        }
        
        System.out.println("Estudiantes sobre el promedio: " + arribaPromedio);
        System.out.println("Estudiantes bajo el promedio: " + (notas.length - arribaPromedio));
        
        // Mostramos las notas extremas
        encontrarNotaMasAlta(notas, estudiantes);
        encontrarNotaMasBaja(notas, estudiantes);
        
        // Mostramos la distribución
        contarNotasPorRango(notas);
    }
    
    public static void main(String[] args) {
        // Datos de ejemplo: notas y estudiantes
        String[] estudiantes = {
            "Ana García", "Juan Pérez", "María López", "Carlos Silva", 
            "Luis Martín", "Carmen Ruiz", "Pedro Sánchez", "Laura Torres"
        };
        
        double[] notas = {8.5, 7.2, 9.1, 6.8, 5.9, 8.8, 7.5, 9.3};
        
        // Simulamos un menú (en un programa real usarías Scanner para input del usuario)
        System.out.println("Bienvenido al Sistema de Gestión de Notas");
        
        // Ejecutamos todas las funciones para demostrar el sistema
        mostrarNotas(notas, estudiantes);
        
        double promedio = calcularPromedio(notas);
        System.out.println("\nPromedio del curso: " + String.format("%.2f", promedio));
        
        encontrarNotaMasAlta(notas, estudiantes);
        encontrarNotaMasBaja(notas, estudiantes);
        contarNotasPorRango(notas);
        
        System.out.println("\n" + "=".repeat(50)); // Nota: .repeat() requiere Java 11 o superior
        mostrarEstadisticasCompletas(notas, estudiantes);
        
        System.out.println("\nSistema ejecutado correctamente");
    }
}
```

---

## 6. Ejercicios Prácticos

### Ejercicio 1: Gestión de Inventario
Crea un programa que:
- Tenga arrays para nombres de productos, precios y cantidades
- Implemente funciones para:
  - Mostrar todo el inventario
  - Calcular el valor total del inventario
  - Encontrar el producto más caro
  - Contar productos con stock bajo (cantidad < 10)

### Ejercicio 2: Análisis de Temperaturas
Crea un programa que:
- Tenga un array con temperaturas de una semana
- Implemente funciones para:
  - Calcular temperatura promedio
  - Encontrar el día más caluroso y más frío
  - Contar días con temperatura sobre 25°C
  - Mostrar un reporte completo

### Ejercicio 3: Sistema de Votación
Crea un programa que:
- Tenga arrays con candidatos y sus votos
- Implemente funciones para:
  - Mostrar resultados parciales
  - Determinar el ganador
  - Calcular porcentajes de votación
  - Verificar si hay empate

---

## 7. Consejos y Buenas Practicas

### 7.1 Funciones
- **Una función, una responsabilidad**: Cada función debe hacer solo una cosa
- **Nombres descriptivos**: `calcularPromedio()` es mejor que `calcular()`
- **Parámetros claros**: No uses demasiados parámetros (máximo 4-5)
- **Comentarios**: Explica qué hace la función, no cómo lo hace

### 7.2 Arrays
- **Inicialización**: Siempre inicializa tus arrays antes de usarlos
- **Índices**: Recuerda que empiezan en 0 y terminan en `length - 1`
- **Verificación de límites**: Asegúrate de no acceder a índices inválidos
- **Uso de `.length`**: Usa `array.length` en lugar de números fijos

### 7.3 Estructuras de Control
- **if/else**: Usa llaves `{}` incluso para una sola línea
- **switch**: No olvides los `break;` statements
- **Ciclos**: Ten cuidado con los bucles infinitos
- **Condiciones claras**: Escribe condiciones fáciles de entender

---

## Siguiente Paso

Excelente trabajo! Has completado el segundo README sobre funciones, arrays y estructuras de control. En el proximo README exploraremmos:
- Programacion Orientada a Objetos (clases, objetos)
- Constructores y metodos
- Encapsulacion y modificadores de acceso
- Herencia basica
- Manejo basico de excepciones

Sigue practicando con los ejercicios y nos vemos en el README 3!
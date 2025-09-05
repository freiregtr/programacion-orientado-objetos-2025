# Java Fundamentals - README 1
## Variables y Conceptos Basicos

> **Requisitos**: Java JDK 8 o superior. Recomendado: Java 11 LTS o Java 17 LTS
> 
> **IDE Sugerido**: NetBeans, Eclipse, o IntelliJ IDEA
>
> **Para configurar NetBeans**: Ver `netbeans_setup.md`

### Objetivos de Aprendiazje
Al completar esta guia, seras capaz de:
- Entender que son las variables en Java
- Conocer los tipos de datos basicos
- Crear y usar variables correctammente
- Aplicar operadores basicos
- Entender el flujo basico de un programa Java

---

## 1. Que es Java?

Java es un lenguaje de programacion **orientado a objetos** que se ejecuta en cualquier dispositivo que tenga instalada la **Maquina Virtual de Java (JVM)**. 

**Caracteristicas principales:**
- **Write Once, Run Anywhere (WORA)** - Escribe una vez, ejecuta en cualquier lugar
- **Fuertemente tipado** - Debes declarar el tipo de cada variable
- **Orientado a obejtos** - Todo gira en torno a clases y objetos

---

## 2. Estructura Basica de un Programa Java

```java
public class MiPrimerPrograma {
    public static void main(String[] args) {
        System.out.println("Hola Mundo!");
    }
}
```

**Explicacion paso a paso:**
1. `public class MiPrimerPrograma` - Define una clase publica
2. `public static void main(String[] args)` - Metodo principal donde inicia el programa
3. `System.out.println()` - Imprime texto en la consola

---

## 3. Variables y Tipos de Datos

### 3.1 Que es una Variable?

Una variable es un **contenedor** que almacena datos que pueden cambiar durannte la ejecucion del programa.

**Sintaxis:**
```java
tipoDeVariable nombreVariable = valor;
```

### 3.2 Tipos de Datos Primitivos

#### **Números Enteros**
```java
public class TiposEnteros {
    public static void main(String[] args) {
        // byte: -128 a 127
        byte edad = 25;
        
        // short: -32,768 a 32,767
        short año = 2024;
        
        // int: -2,147,483,648 a 2,147,483,647 (más usado)
        int poblacion = 1000000;
        
        // long: números muy grandes
        long distanciaEspacio = 9460730472580800L; // Nota la 'L' al final
        
        System.out.println("Edad: " + edad);
        System.out.println("Año: " + año);
        System.out.println("Población: " + poblacion);
        System.out.println("Distancia: " + distanciaEspacio);
    }
}
```

#### **Números Decimales**
```java
public class TiposDecimales {
    public static void main(String[] args) {
        // float: precisión simple
        float temperatura = 36.5f; // Nota la 'f' al final
        
        // double: precisión doble (más usado)
        double precio = 199.99;
        double pi = 3.141592653589793;
        
        System.out.println("Temperatura: " + temperatura + "°C");
        System.out.println("Precio: $" + precio);
        System.out.println("Pi: " + pi);
    }
}
```

#### **Caracteres y Texto**
```java
public class TiposTexto {
    public static void main(String[] args) {
        // char: un solo carácter
        char inicial = 'A';
        char simbolo = '@';
        
        // String: cadena de texto
        String nombre = "Juan Pérez";
        String mensaje = "¡Bienvenido a Java!";
        
        System.out.println("Inicial: " + inicial);
        System.out.println("Símbolo: " + simbolo);
        System.out.println("Nombre: " + nombre);
        System.out.println("Mensaje: " + mensaje);
    }
}
```

#### **Valores Lógicos**
```java
public class TipoBoolean {
    public static void main(String[] args) {
        // boolean: true o false
        boolean esMayorDeEdad = true;
        boolean tieneDescuento = false;
        boolean esVerdadero = 5 > 3; // true
        
        System.out.println("¿Es mayor de edad? " + esMayorDeEdad);
        System.out.println("¿Tiene descuento? " + tieneDescuento);
        System.out.println("¿5 > 3? " + esVerdadero);
    }
}
```

### 3.3 Ejercicio Práctico - Mi Perfil
```java
public class MiPerfil {
    public static void main(String[] args) {
        // Información personal
        String nombre = "Ana García";
        int edad = 20;
        double altura = 1.65;
        char genero = 'F';
        boolean esEstudiante = true;
        
        // Información adicional
        String carrera = "Ingeniería en Sistemas";
        int semestre = 4;
        double promedio = 8.7;
        
        // Mostrar información
        System.out.println("=== MI PERFIL ===");
        System.out.println("Nombre: " + nombre);
        System.out.println("Edad: " + edad + " años");
        System.out.println("Altura: " + altura + " metros");
        System.out.println("Género: " + genero);
        System.out.println("¿Es estudiante? " + esEstudiante);
        System.out.println("Carrera: " + carrera);
        System.out.println("Semestre: " + semestre);
        System.out.println("Promedio: " + promedio);
    }
}
```

---

## 4. Operadores

### 4.1 Operadores Aritméticos
```java
public class OperadoresAritmeticos {
    public static void main(String[] args) {
        int a = 15;
        int b = 4;
        
        System.out.println("a = " + a + ", b = " + b);
        System.out.println("Suma: " + a + " + " + b + " = " + (a + b));
        System.out.println("Resta: " + a + " - " + b + " = " + (a - b));
        System.out.println("Multiplicación: " + a + " * " + b + " = " + (a * b));
        System.out.println("División: " + a + " / " + b + " = " + (a / b));
        System.out.println("Módulo: " + a + " % " + b + " = " + (a % b));
        
        // Incremento y decremento
        System.out.println("\n--- Incremento y Decremento ---");
        int contador = 10;
        System.out.println("Contador inicial: " + contador);
        contador++; // contador = contador + 1
        System.out.println("Después de contador++: " + contador);
        contador--; // contador = contador - 1
        System.out.println("Después de contador--: " + contador);
    }
}
```

### 4.2 Operadores de Comparación
```java
public class OperadoresComparacion {
    public static void main(String[] args) {
        int x = 10;
        int y = 5;
        
        System.out.println("x = " + x + ", y = " + y);
        System.out.println("x > y: " + (x > y));   // true
        System.out.println("x < y: " + (x < y));   // false
        System.out.println("x >= y: " + (x >= y)); // true
        System.out.println("x <= y: " + (x <= y)); // false
        System.out.println("x == y: " + (x == y)); // false
        System.out.println("x != y: " + (x != y)); // true
    }
}
```

### 4.3 Operadores Lógicos
```java
public class OperadoresLogicos {
    public static void main(String[] args) {
        boolean tienePermiso = true;
        boolean esMayorEdad = true;
        boolean tieneExperiencia = false;
        
        // AND (&&) - Ambas condiciones deben ser true
        boolean puedeTrabajar = tienePermiso && esMayorEdad;
        System.out.println("¿Puede trabajar? " + puedeTrabajar);
        
        // OR (||) - Al menos una condición debe ser true
        boolean esContratado = esMayorEdad || tieneExperiencia;
        System.out.println("¿Es contratado? " + esContratado);
        
        // NOT (!) - Invierte el valor
        boolean noTieneExperiencia = !tieneExperiencia;
        System.out.println("¿No tiene experiencia? " + noTieneExperiencia);
    }
}
```

---

## 5. Ejercicio Integrador - Calculadora Simple

```java
public class CalculadoraSimple {
    public static void main(String[] args) {
        // Datos de entrada
        double numero1 = 25.5;
        double numero2 = 10.2;
        
        System.out.println("=== CALCULADORA SIMPLE ===");
        System.out.println("Número 1: " + numero1);
        System.out.println("Número 2: " + numero2);
        System.out.println();
        
        // Operaciones
        double suma = numero1 + numero2;
        double resta = numero1 - numero2;
        double multiplicacion = numero1 * numero2;
        double division = numero1 / numero2;
        
        // Mostrar resultados
        System.out.println("RESULTADOS:");
        System.out.println("Suma: " + suma);
        System.out.println("Resta: " + resta);
        System.out.println("Multiplicación: " + multiplicacion);
        System.out.println("División: " + division);
        
        // Comparaciones
        System.out.println("\nCOMPARACIONES:");
        System.out.println("¿" + numero1 + " es mayor que " + numero2 + "? " + (numero1 > numero2));
        System.out.println("¿Son iguales? " + (numero1 == numero2));
        
        // Operaciones lógicas
        boolean ambosSonPositivos = (numero1 > 0) && (numero2 > 0);
        System.out.println("¿Ambos números son positivos? " + ambosSonPositivos);
    }
}
```

---

## 6. Buenas Practicas

### 6.1 Nomenclatura de Variables
```java
public class BuenasPracticas {
    public static void main(String[] args) {
        // CORRECTO - camelCase
        String nombreCompleto = "Maria Rodriguez";
        int edadActual = 22;
        boolean estaActivo = true;
        double salarioMensual = 15000.50;
        
        // INCORRECTO
        // String nombre_completo;  // No usar guiones bajos
        // int EdadActual;          // No empezar con mayuscula
        // boolean esta_activo;     // No usar guiones bajos
    }
}
```

### 6.2 Inicialización de Variables
```java
public class InicializacionVariables {
    public static void main(String[] args) {
        // CORRECTO - Inicializar al declarar
        int contador = 0;
        String mensaje = "";
        boolean activo = false;
        
        // INCORRECTO - Variables sin inicializar
        // int numero; // Error: variable not initialized
        // System.out.println(numero);
        
        System.out.println("Contador: " + contador);
        System.out.println("Mensaje: '" + mensaje + "'");
        System.out.println("Activo: " + activo);
    }
}
```

---

## 7. Retos Practicos

### Reto 1: Informacion Personal
Crea un programa que declare variables para almacenar:
- Tu nombre completo
- Tu edad
- Tu altura en metros
- Si eres estudiante (true/false)
- Tu materia favorita

Imprime toda la información de forma organizada.

### Reto 2: Calculadora de IMC
Crea un programa que:
- Declare variables para peso (kg) y altura (m)
- Calcule el IMC usando la fórmula: IMC = peso / (altura * altura)
- Muestre el resultado

### Reto 3: Tienda de Descuentos
Crea un programa que:
- Declare el precio original de un producto
- Declare el porcentaje de descuento
- Calcule el descuento en pesos
- Calcule el precio final
- Muestre todos los valores

---

## 8. Conceptos Clave para Recordar

1. **Variables**: Contenedores que almacenan datos
2. **Tipos primitivos**: int, double, boolean, char, etc.
3. **String**: No es primitivo, es una clase
4. **Operadores**: Aritméticos (+, -, *, /, %), comparación (>, <, ==), lógicos (&&, ||, !)
5. **camelCase**: Convención para nombrar variables
6. **Inicialización**: Siempre asignar un valor inicial a las variables
7. **System.out.println()**: Para mostrar información en consola

---

## Siguiente Paso

Felicidades! Has completado el primer README sobre fundamentos de Java. En el proximo README exploraremos:
- Estructuras de control (if, else, switch)
- Ciclos (for, while)
- Arrays basicos
- Metodos simples

Sigue practiciando y nos vemos en el README 2!
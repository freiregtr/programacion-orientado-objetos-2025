# NetBeans IDE Setup Guide - Configuracion para Java

## Guia Completa de Configuracion de NetBeans para Programacion Java

### Objetivos de esta Guiia
Al completar esta guia, seras capaz de:
- Instalar y configurar NetBeans IDE correctammente
- Crear y gestionar proyectos Java
- Utilizar las herramientas de desarrollo mas importantes
- Configurar el entorno para programacion orientada a objetos
- Aplicar shortcuts y buenas practicas de desarrollo

---

## 1. Instalacion de NetBeans

### 1.1 Requisitos del Sistema
- **Java JDK**: Versión 11 o superior (recomendado JDK 17 LTS)
- **Memoria RAM**: Mínimo 4GB, recomendado 8GB
- **Espacio en disco**: Al menos 1GB libres
- **Sistema operativo**: Windows 10+, macOS 10.14+, o Linux

### 1.2 Descarga e Instalación

**Paso 1: Instalar JDK**
```bash
# Verificar si ya tienes Java instalado
java -version
javac -version

# Si no lo tienes, descarga desde:
# https://www.oracle.com/java/technologies/downloads/
# o usa OpenJDK: https://openjdk.org/
```

**Paso 2: Descargar NetBeans**
- Visita: https://netbeans.apache.org/download/
- Descarga la versión LTS más reciente
- Elige "Apache NetBeans IDE" (incluye soporte completo para Java)

**Paso 3: Instalar NetBeans**
- **Windows**: Ejecuta el `.exe` descargado
- **macOS**: Monta el `.dmg` y arrastra NetBeans a Applications
- **Linux**: Extrae el `.zip` y ejecuta `./bin/netbeans`

---

## 2. Configuracion Inicial

### 2.1 Primera Ejecución
1. **Abre NetBeans**
2. **Configurar JDK**: Ve a `Tools → Java Platforms`
   - Verifica que tu JDK esté listado
   - Si no aparece, haz clic en "Add Platform" y navega a tu instalación JDK

3. **Configurar Encoding**:
   - `Tools → Options → Editor → General`
   - Cambia encoding a `UTF-8` para soporte completo de caracteres

### 2.2 Configuración Recomendada

**Apariencia y Tema:**
```
Tools → Options → Appearance
- Tema: Dark Metal (para mejor experiencia visual)
- Font Size: 12 (ajustar según preferencia)
```

**Editor de Código:**
```
Tools → Options → Editor → Formatting
- Language: Java
- Tabs vs Spaces: Spaces
- Number of Spaces per Indent: 4
- Text Limit Column: 120
```

**Plugins Útiles:**
```
Tools → Plugins → Available Plugins
- GitHub Issues (para integración con GitHub)
- Markdown Support (para archivos .md)
- PlantUML (para diagramas UML)
```

---

## 3. Creación de Proyectos Java

### 3.1 Crear un Nuevo Proyecto

**Método 1: Desde el Menú**
1. `File → New Project`
2. **Categories**: Java with Ant
3. **Projects**: Java Application
4. **Next**

**Método 2: Atajo de Teclado**
```
Ctrl + Shift + N (Windows/Linux)
Cmd + Shift + N (macOS)
```

### 3.2 Configuración del Proyecto

```
Project Name: MiProyectoJava
Project Location: C:\Users\TuUsuario\Documents\NetBeansProjects\
Create Main Class
Main Class: com.micompania.MiProyectoJava
```

**Estructura del Proyecto Creado:**
```
MiProyectoJava/
├── src/
│   └── com/micompania/
│       └── MiProyectoJava.java
├── test/
├── build/
├── dist/
└── nbproject/
```

### 3.3 Ejemplo de Proyecto para Prácticas de POO

**Crear Proyecto "GestionEstudiantes":**
```java
// Archivo: src/main/GestionEstudiantes.java
public class GestionEstudiantes {
    public static void main(String[] args) {
        System.out.println("=== SISTEMA DE GESTIÓN DE ESTUDIANTES ===");
        
        // Aquí irán las clases de los READMEs
    }
}
```

---

## 4. Herramientas Esenciales de NetBeans

### 4.1 Navegación de Código

**Projects Window (Ctrl+1)**
- Muestra la estructura de archivos
- Haz clic derecho para crear nuevas clases
- Drag & drop para mover archivos

**Navigator Window (Ctrl+7)**
- Muestra métodos y variables de la clase actual
- Click para saltar rápidamente a definiciones

**Output Window (Ctrl+4)**
- Muestra la salida del programa
- Errores de compilación
- Logs del debugger

### 4.2 Creación Rápida de Clases

**Para crear una nueva clase:**
1. Click derecho en el paquete (en Projects)
2. `New → Java Class`
3. Nombre: `Estudiante`
4. **Finish**

**Ejemplo de clase generada:**
```java
package com.micompania;

/**
 * Clase que representa un estudiante
 * @author Tu Nombre
 */
public class Estudiante {
    
    // Constructor por defecto
    public Estudiante() {
    }
}
```

### 4.3 Autocompletado y Code Templates

**Autocompletado (Ctrl+Space):**
```java
System.out.println(); // Escribe "sout" + Ctrl+Space
public static void main(String[] args) // Escribe "psvm" + Ctrl+Space
```

**Templates Útiles:**
- `sout` → System.out.println();
- `psvm` → public static void main(String[] args)
- `for` → for (int i = 0; i < ; i++) { }
- `fori` → for (int i = 0; i < args.length; i++) { }
- `fore` → for (Object object : collection) { }

### 4.4 Refactoring Tools

**Renombrar Variables/Métodos:**
```
Click derecho en variable → Refactor → Rename (Ctrl+R)
```

**Extraer Método:**
```
Seleccionar código → Refactor → Extract Method (Ctrl+R, M)
```

**Generar Getters/Setters:**
```
Click derecho en clase → Insert Code (Alt+Insert)
→ Getter and Setter
```

---

## 5. Debugging y Testing

### 5.1 Debugging Básico

**Establecer Breakpoints:**
- Click en el número de línea (aparece un círculo rojo)
- `Ctrl+F8` para toggle breakpoint

**Ejecutar en Debug Mode:**
```
Debug → Debug Main Project (Ctrl+F5)
```

**Controles de Debug:**
- **Step Over (F8)**: Ejecuta línea actual
- **Step Into (F7)**: Entra en métodos
- **Step Out (Ctrl+F7)**: Sale del método actual
- **Continue (F5)**: Continúa ejecución

### 5.2 Ejemplo de Debug Session

```java
public class TestDebug {
    public static void main(String[] args) {
        int numero = 10;          // ← Breakpoint aquí
        int resultado = duplicar(numero);
        System.out.println("Resultado: " + resultado);
    }
    
    public static int duplicar(int n) {
        return n * 2;             // ← Breakpoint aquí también
    }
}
```

---

## 6. Shortcuts Esenciales

### 6.1 Navegación
```
Ctrl + O          → Ir a archivo
Ctrl + Shift + O  → Ir a tipo (clase)
Ctrl + G          → Ir a línea
Ctrl + F          → Buscar en archivo actual
Ctrl + H          → Buscar y reemplazar
Ctrl + Shift + F  → Buscar en proyecto
Alt + ←/→         → Navegar tabs
```

### 6.2 Edición de Código
```
Ctrl + Space      → Autocompletado
Ctrl + Shift + I  → Organizar imports
Ctrl + L          → Ir a línea
Ctrl + D          → Duplicar línea
Ctrl + Shift + ↑/↓ → Mover línea
Ctrl + /          → Comentar/descomentar
Alt + Insert      → Generar código
```

### 6.3 Compilación y Ejecución
```
F6                → Compilar proyecto
Shift + F6        → Compilar archivo actual
F9                → Compilar y ejecutar
Ctrl + F5         → Debug
Shift + F5        → Ejecutar sin debug
```

---

## 7. Configuracion para Proyectos de los READMEs

### 7.1 Estructura Recomendada para Prácticas

**Crear el siguiente proyecto:**
```
ProyectosPOO/
├── src/
│   ├── fundamentals/        → Código del README 1
│   │   ├── Variables.java
│   │   └── Operadores.java
│   ├── functions/          → Código del README 2
│   │   ├── MetodosBasicos.java
│   │   ├── Arrays.java
│   │   └── SistemaNotas.java
│   └── oop/               → Código del README 3
│       ├── Persona.java
│       ├── CuentaBancaria.java
│       ├── Empleado.java
│       ├── Desarrollador.java
│       ├── Gerente.java
│       └── TestSistemas.java
└── test/
```

### 7.2 Configurar Paquetes por Tema

**Crear paquetes:**
1. Click derecho en `src`
2. `New → Java Package`
3. Nombres sugeridos:
   - `com.duoc.fundamentals`
   - `com.duoc.functions`
   - `com.duoc.oop.personas`
   - `com.duoc.oop.empleados`
   - `com.duoc.oop.vehiculos`

### 7.3 Template para Clases de Práctica

```java
package com.duoc.oop.personas;

/**
 * Clase de práctica basada en README 3 - POO
 * Tema: [Descripción del tema]
 * @author [Tu Nombre]
 * @version 1.0
 * @since 2024
 */
public class MiClase {
    
    // Atributos privados
    private String atributo;
    
    // Constructor
    public MiClase(String atributo) {
        this.atributo = atributo;
    }
    
    // Getters y Setters
    public String getAtributo() {
        return atributo;
    }
    
    public void setAtributo(String atributo) {
        this.atributo = atributo;
    }
    
    // Método main para pruebas
    public static void main(String[] args) {
        System.out.println("=== PRUEBA DE [NOMBRE_CLASE] ===");
        
        MiClase obj = new MiClase("Valor de prueba");
        System.out.println("Atributo: " + obj.getAtributo());
        
        System.out.println("Prueba completada");
    }
}
```

---

## 8. Troubleshooting Comun

### 8.1 Problemas de JDK

**Error: "No JDK found"**
```
Solución:
1. Tools → Java Platforms
2. Add Platform
3. Seleccionar carpeta de instalación JDK
```

**Error: "Package does not exist"**
```
Solución:
1. Click derecho en proyecto → Properties
2. Libraries → Classpath
3. Verificar que todas las librerías estén presentes
```

### 8.2 Problemas de Encoding

**Caracteres especiales no se muestran correctamente:**
```
Solución:
1. Tools → Options → Editor → General
2. Encoding: UTF-8
3. Reiniciar NetBeans
```

### 8.3 Problemas de Performance

**NetBeans lento:**
```
Solución:
1. Editar netbeans.conf
2. Aumentar -J-Xmx512m a -J-Xmx1024m
3. Cerrar proyectos no utilizados
4. Tools → Options → Java → Maven → Skip Tests
```

---

## 9. Flujo de Trabajo Recomendado

### 9.1 Para Cada Nuevo Concepto

1. **Crear nueva clase**
2. **Escribir comentarios explicativos**
3. **Implementar código paso a paso**
4. **Usar autocompletado y templates**
5. **Compilar frecuentemente (F6)**
6. **Ejecutar y probar (F9)**
7. **Debug si hay errores (Ctrl+F5)**
8. **Refactorizar cuando sea necesario**

### 9.2 Organización de Código

```java
// 1. Comentario de clase
public class MiClase {
    
    // 2. Atributos (siempre private)
    private String atributo1;
    private int atributo2;
    
    // 3. Constructores
    public MiClase() { }
    
    public MiClase(String atributo1, int atributo2) {
        this.atributo1 = atributo1;
        this.atributo2 = atributo2;
    }
    
    // 4. Getters y Setters
    public String getAtributo1() { return atributo1; }
    public void setAtributo1(String atributo1) { this.atributo1 = atributo1; }
    
    // 5. Métodos de negocio
    public void metodoEspecifico() { }
    
    // 6. toString, equals, hashCode si es necesario
    @Override
    public String toString() {
        return "MiClase{" + "atributo1=" + atributo1 + ", atributo2=" + atributo2 + '}';
    }
    
    // 7. Método main para pruebas (opcional)
    public static void main(String[] args) {
        // Código de prueba
    }
}
```

---

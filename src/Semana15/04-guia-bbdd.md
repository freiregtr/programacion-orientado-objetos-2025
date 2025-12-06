# Guia 04: Base de Datos MySQL y Conexion

## Objetivo
Configurar la base de datos en MySQL Workbench y crear la clase de conexion en Java.

## Parte 1: MySQL Workbench

### Paso 1: Abrir MySQL Workbench

1. Abrir MySQL Workbench
2. Conectarse al servidor local (localhost)

### Paso 2: Crear la base de datos

Ejecutar el siguiente script SQL:

```sql
-- Crear la base de datos
CREATE DATABASE IF NOT EXISTS pizzeria_db;

-- Usar la base de datos
USE pizzeria_db;

-- Crear la tabla pizza
CREATE TABLE pizza (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nombre VARCHAR(100) NOT NULL,
    precio DOUBLE NOT NULL,
    tamanio VARCHAR(50) NOT NULL
);

-- Insertar datos de ejemplo
INSERT INTO pizza (nombre, precio, tamanio) VALUES
('Pepperoni', 8500, 'Mediana'),
('Hawaiana', 9000, 'Familiar'),
('Margherita', 7500, 'Personal'),
('Cuatro Quesos', 10000, 'Familiar'),
('Napolitana', 8000, 'Mediana');
```

### Paso 3: Verificar la creacion

Ejecutar:

```sql
SELECT * FROM pizza;
```

Deberia mostrar las 5 pizzas insertadas.

## Parte 2: Conector JDBC

### Paso 1: Descargar el conector

1. Ir a: https://dev.mysql.com/downloads/connector/j/
2. Seleccionar "Platform Independent"
3. Descargar el archivo ZIP
4. Extraer y ubicar el archivo `mysql-connector-j-X.X.XX.jar`

### Paso 2: Agregar al proyecto en NetBeans

1. Click derecho en el proyecto > Properties
2. Seleccionar "Libraries" en el panel izquierdo
3. En la pestana "Compile", click en el "+" junto a "Classpath"
4. Seleccionar "Add JAR/Folder"
5. Buscar y seleccionar el archivo `mysql-connector-j-X.X.XX.jar`
6. Click en "Open" y luego "OK"

## Parte 3: Clase Conexion

### Paso 1: Crear la clase

1. Click derecho en `pizzeria.conexion`
2. New > Java Class
3. Nombre: `Conexion`

### Paso 2: Codigo de la clase

```java
package pizzeria.conexion;

import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.SQLException;

public class Conexion {

    // Datos de conexion
    private static final String URL = "jdbc:mysql://localhost:3306/pizzeria_db";
    private static final String USUARIO = "root";
    private static final String PASSWORD = "tu_password"; // Cambiar por tu password

    // Metodo para obtener conexion
    public static Connection getConexion() throws SQLException {
        return DriverManager.getConnection(URL, USUARIO, PASSWORD);
    }

    // Metodo para cerrar conexion
    public static void cerrarConexion(Connection conn) {
        if (conn != null) {
            try {
                conn.close();
            } catch (SQLException e) {
                System.err.println("Error al cerrar conexion: " + e.getMessage());
            }
        }
    }
}
```

**Importante:** Cambiar `"tu_password"` por la contrasena de tu MySQL.

## Parte 4: Probar la conexion

### Paso 1: Crear clase de prueba (opcional)

Puedes crear una clase para probar que la conexion funciona:

```java
package pizzeria.controlador;

import pizzeria.conexion.Conexion;
import java.sql.Connection;

public class PruebaConexion {

    public static void main(String[] args) {
        try {
            Connection conn = Conexion.getConexion();
            if (conn != null) {
                System.out.println("Conexion exitosa!");
                Conexion.cerrarConexion(conn);
            }
        } catch (Exception e) {
            System.err.println("Error de conexion: " + e.getMessage());
        }
    }
}
```

### Paso 2: Ejecutar la prueba

1. Click derecho en `PruebaConexion.java`
2. Run File
3. Si muestra "Conexion exitosa!" todo esta correcto

## Resumen de archivos

Al finalizar deberias tener:

```
PizzeriaSistema/
└── src/
    └── pizzeria/
        ├── modelo/
        │   └── Pizza.java
        ├── vista/
        │   └── VentanaPrincipal.java
        ├── controlador/
        │   ├── PizzaController.java
        │   └── PruebaConexion.java (opcional)
        └── conexion/
            └── Conexion.java
```

---

## Siguiente: 05-guia-eventos.md

En la siguiente guia conectaremos los botones de la vista con los metodos del controlador.

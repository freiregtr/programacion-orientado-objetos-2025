# Guia 03: Controlador - Logica CRUD

## Objetivo
Crear el controlador con los metodos para insertar, actualizar, eliminar, buscar y listar pizzas.

## Paso 1: Crear la clase PizzaController

1. Click derecho en `pizzeria.controlador`
2. New > Java Class
3. Nombre: `PizzaController`

## Paso 2: Estructura basica

```java
package pizzeria.controlador;

import pizzeria.conexion.Conexion;
import pizzeria.modelo.Pizza;
import java.sql.*;
import java.util.ArrayList;

public class PizzaController {

}
```

## Paso 3: Metodo insertar

Este metodo recibe una Pizza y la guarda en la base de datos.

```java
public boolean insertar(Pizza pizza) {
    Connection conn = null;
    try {
        conn = Conexion.getConexion();

        String sql = "INSERT INTO pizza (nombre, precio, tamanio) VALUES (?, ?, ?)";
        PreparedStatement ps = conn.prepareStatement(sql);
        ps.setString(1, pizza.getNombre());
        ps.setDouble(2, pizza.getPrecio());
        ps.setString(3, pizza.getTamanio());
        ps.executeUpdate();

        return true;
    } catch (SQLException e) {
        System.err.println("Error al insertar: " + e.getMessage());
        return false;
    } finally {
        Conexion.cerrarConexion(conn);
    }
}
```

## Paso 4: Metodo buscarPorId

Este metodo busca una pizza por su ID y la retorna.

```java
public Pizza buscarPorId(int id) {
    Connection conn = null;
    try {
        conn = Conexion.getConexion();

        String sql = "SELECT * FROM pizza WHERE id = ?";
        PreparedStatement ps = conn.prepareStatement(sql);
        ps.setInt(1, id);
        ResultSet rs = ps.executeQuery();

        if (rs.next()) {
            String nombre = rs.getString("nombre");
            double precio = rs.getDouble("precio");
            String tamanio = rs.getString("tamanio");
            return new Pizza(id, nombre, precio, tamanio);
        }

        return null;
    } catch (SQLException e) {
        System.err.println("Error al buscar: " + e.getMessage());
        return null;
    } finally {
        Conexion.cerrarConexion(conn);
    }
}
```

## Paso 5: Metodo actualizar

Este metodo actualiza los datos de una pizza existente.

```java
public boolean actualizar(Pizza pizza) {
    Connection conn = null;
    try {
        conn = Conexion.getConexion();

        String sql = "UPDATE pizza SET nombre = ?, precio = ?, tamanio = ? WHERE id = ?";
        PreparedStatement ps = conn.prepareStatement(sql);
        ps.setString(1, pizza.getNombre());
        ps.setDouble(2, pizza.getPrecio());
        ps.setString(3, pizza.getTamanio());
        ps.setInt(4, pizza.getId());

        return ps.executeUpdate() > 0;
    } catch (SQLException e) {
        System.err.println("Error al actualizar: " + e.getMessage());
        return false;
    } finally {
        Conexion.cerrarConexion(conn);
    }
}
```

## Paso 6: Metodo eliminar

Este metodo elimina una pizza por su ID.

```java
public boolean eliminar(int id) {
    Connection conn = null;
    try {
        conn = Conexion.getConexion();

        String sql = "DELETE FROM pizza WHERE id = ?";
        PreparedStatement ps = conn.prepareStatement(sql);
        ps.setInt(1, id);

        return ps.executeUpdate() > 0;
    } catch (SQLException e) {
        System.err.println("Error al eliminar: " + e.getMessage());
        return false;
    } finally {
        Conexion.cerrarConexion(conn);
    }
}
```

## Paso 7: Metodo listarTodos

Este metodo retorna todas las pizzas en un ArrayList.

```java
public ArrayList<Pizza> listarTodos() {
    ArrayList<Pizza> pizzas = new ArrayList<>();
    Connection conn = null;

    try {
        conn = Conexion.getConexion();

        String sql = "SELECT * FROM pizza";
        PreparedStatement ps = conn.prepareStatement(sql);
        ResultSet rs = ps.executeQuery();

        while (rs.next()) {
            int id = rs.getInt("id");
            String nombre = rs.getString("nombre");
            double precio = rs.getDouble("precio");
            String tamanio = rs.getString("tamanio");

            Pizza pizza = new Pizza(id, nombre, precio, tamanio);
            pizzas.add(pizza);
        }
    } catch (SQLException e) {
        System.err.println("Error al listar: " + e.getMessage());
    } finally {
        Conexion.cerrarConexion(conn);
    }

    return pizzas;
}
```

## Codigo completo

```java
package pizzeria.controlador;

import pizzeria.conexion.Conexion;
import pizzeria.modelo.Pizza;
import java.sql.*;
import java.util.ArrayList;

public class PizzaController {

    // Insertar nueva pizza
    public boolean insertar(Pizza pizza) {
        Connection conn = null;
        try {
            conn = Conexion.getConexion();

            String sql = "INSERT INTO pizza (nombre, precio, tamanio) VALUES (?, ?, ?)";
            PreparedStatement ps = conn.prepareStatement(sql);
            ps.setString(1, pizza.getNombre());
            ps.setDouble(2, pizza.getPrecio());
            ps.setString(3, pizza.getTamanio());
            ps.executeUpdate();

            return true;
        } catch (SQLException e) {
            System.err.println("Error al insertar: " + e.getMessage());
            return false;
        } finally {
            Conexion.cerrarConexion(conn);
        }
    }

    // Buscar pizza por ID
    public Pizza buscarPorId(int id) {
        Connection conn = null;
        try {
            conn = Conexion.getConexion();

            String sql = "SELECT * FROM pizza WHERE id = ?";
            PreparedStatement ps = conn.prepareStatement(sql);
            ps.setInt(1, id);
            ResultSet rs = ps.executeQuery();

            if (rs.next()) {
                String nombre = rs.getString("nombre");
                double precio = rs.getDouble("precio");
                String tamanio = rs.getString("tamanio");
                return new Pizza(id, nombre, precio, tamanio);
            }

            return null;
        } catch (SQLException e) {
            System.err.println("Error al buscar: " + e.getMessage());
            return null;
        } finally {
            Conexion.cerrarConexion(conn);
        }
    }

    // Actualizar pizza
    public boolean actualizar(Pizza pizza) {
        Connection conn = null;
        try {
            conn = Conexion.getConexion();

            String sql = "UPDATE pizza SET nombre = ?, precio = ?, tamanio = ? WHERE id = ?";
            PreparedStatement ps = conn.prepareStatement(sql);
            ps.setString(1, pizza.getNombre());
            ps.setDouble(2, pizza.getPrecio());
            ps.setString(3, pizza.getTamanio());
            ps.setInt(4, pizza.getId());

            return ps.executeUpdate() > 0;
        } catch (SQLException e) {
            System.err.println("Error al actualizar: " + e.getMessage());
            return false;
        } finally {
            Conexion.cerrarConexion(conn);
        }
    }

    // Eliminar pizza por ID
    public boolean eliminar(int id) {
        Connection conn = null;
        try {
            conn = Conexion.getConexion();

            String sql = "DELETE FROM pizza WHERE id = ?";
            PreparedStatement ps = conn.prepareStatement(sql);
            ps.setInt(1, id);

            return ps.executeUpdate() > 0;
        } catch (SQLException e) {
            System.err.println("Error al eliminar: " + e.getMessage());
            return false;
        } finally {
            Conexion.cerrarConexion(conn);
        }
    }

    // Listar todas las pizzas
    public ArrayList<Pizza> listarTodos() {
        ArrayList<Pizza> pizzas = new ArrayList<>();
        Connection conn = null;

        try {
            conn = Conexion.getConexion();

            String sql = "SELECT * FROM pizza";
            PreparedStatement ps = conn.prepareStatement(sql);
            ResultSet rs = ps.executeQuery();

            while (rs.next()) {
                int id = rs.getInt("id");
                String nombre = rs.getString("nombre");
                double precio = rs.getDouble("precio");
                String tamanio = rs.getString("tamanio");

                Pizza pizza = new Pizza(id, nombre, precio, tamanio);
                pizzas.add(pizza);
            }
        } catch (SQLException e) {
            System.err.println("Error al listar: " + e.getMessage());
        } finally {
            Conexion.cerrarConexion(conn);
        }

        return pizzas;
    }
}
```

## Siguiente: 04-guia-bbdd.md

# Guia 02: Modelo - Clase Pizza

## Objetivo
Crear la clase Pizza que representa la entidad del sistema.

## Paso 1: Crear la clase Pizza

1. Click derecho en `pizzeria.modelo`
2. New > Java Class
3. Nombre: `Pizza`

## Paso 2: Definir los atributos

La clase Pizza debe tener los mismos atributos que la tabla en la base de datos:

```java
package pizzeria.modelo;

public class Pizza {

    private int id;
    private String nombre;
    private double precio;
    private String tamanio;
}
```

## Paso 3: Crear los constructores

Necesitamos dos constructores:
- Uno sin ID (para insertar, porque el ID es autoincremental)
- Uno con ID (para cuando traemos datos de la BD)

```java
// Constructor sin ID (para insertar)
public Pizza(String nombre, double precio, String tamanio) {
    this.nombre = nombre;
    this.precio = precio;
    this.tamanio = tamanio;
}

// Constructor con ID (para consultas)
public Pizza(int id, String nombre, double precio, String tamanio) {
    this.id = id;
    this.nombre = nombre;
    this.precio = precio;
    this.tamanio = tamanio;
}
```

## Paso 4: Crear getters y setters

En NetBeans puedes generarlos automaticamente:
1. Click derecho dentro de la clase
2. Insert Code > Getter and Setter
3. Seleccionar todos los atributos

```java
public int getId() {
    return id;
}

public void setId(int id) {
    this.id = id;
}

public String getNombre() {
    return nombre;
}

public void setNombre(String nombre) {
    this.nombre = nombre;
}

public double getPrecio() {
    return precio;
}

public void setPrecio(double precio) {
    this.precio = precio;
}

public String getTamanio() {
    return tamanio;
}

public void setTamanio(String tamanio) {
    this.tamanio = tamanio;
}
```

## Paso 5: Crear metodo toString (opcional)

Util para debuggear:

```java
@Override
public String toString() {
    return "Pizza{" + "id=" + id + ", nombre=" + nombre + ", precio=" + precio + ", tamanio=" + tamanio + '}';
}
```

## Codigo completo

```java
package pizzeria.modelo;

public class Pizza {

    private int id;
    private String nombre;
    private double precio;
    private String tamanio;

    // Constructor sin ID (para insertar)
    public Pizza(String nombre, double precio, String tamanio) {
        this.nombre = nombre;
        this.precio = precio;
        this.tamanio = tamanio;
    }

    // Constructor con ID (para consultas)
    public Pizza(int id, String nombre, double precio, String tamanio) {
        this.id = id;
        this.nombre = nombre;
        this.precio = precio;
        this.tamanio = tamanio;
    }

    // Getters y Setters
    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    public String getNombre() {
        return nombre;
    }

    public void setNombre(String nombre) {
        this.nombre = nombre;
    }

    public double getPrecio() {
        return precio;
    }

    public void setPrecio(double precio) {
        this.precio = precio;
    }

    public String getTamanio() {
        return tamanio;
    }

    public void setTamanio(String tamanio) {
        this.tamanio = tamanio;
    }

    @Override
    public String toString() {
        return "Pizza{" + "id=" + id + ", nombre=" + nombre + ", precio=" + precio + ", tamanio=" + tamanio + '}';
    }
}
```

## Siguiente: 03-guia-controladores.md

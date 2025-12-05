# Mascota - La Clase Abstracta Base

## ¿Qué vamos a crear?

Ahora creamos la clase `Mascota`, que es la base de toda nuestra jerarquía. Esta clase es **abstracta** porque representa el concepto general de "mascota", pero nunca crearemos una mascota genérica. Siempre crearemos perros o gatos específicos.

La clase `Mascota` contiene todos los atributos y comportamientos comunes que comparten perros y gatos: código, nombre, especie, costo de consulta y edad.

## Conceptos POO Aplicados

- **Abstracción**: Clase abstracta que no puede ser instanciada directamente
- **Herencia**: Será la clase padre de Perro y Gato
- **Encapsulación**: Atributos privados con getters y setters
- **Métodos abstractos**: Definen comportamientos que las clases hijas deben implementar

## Código Completo

```java
// Clase abstracta: no se pueden crear objetos de tipo Mascota directamente
// Solo se pueden crear objetos de sus clases hijas (Perro, Gato)
public abstract class Mascota {

    // Atributos privados (encapsulación)
    // Estos datos son comunes a todas las mascotas
    private String codigo;
    private String nombre;
    private String especie;
    private double costoConsulta;
    private int edad;

    // Constructor: inicializa todos los atributos cuando se crea una mascota
    // Las clases hijas llamarán a este constructor usando super()
    public Mascota(String codigo, String nombre, String especie, double costoConsulta, int edad) {
        this.codigo = codigo;
        this.nombre = nombre;
        this.especie = especie;
        this.costoConsulta = costoConsulta;
        this.edad = edad;
    }

    // Getter: permite obtener el código de la mascota desde fuera de la clase
    public String getCodigo() {
        return codigo;
    }

    // Setter: permite modificar el código desde fuera de la clase
    public void setCodigo(String codigo) {
        this.codigo = codigo;
    }

    // Getter para nombre
    public String getNombre() {
        return nombre;
    }

    // Setter para nombre
    public void setNombre(String nombre) {
        this.nombre = nombre;
    }

    // Getter para especie
    public String getEspecie() {
        return especie;
    }

    // Setter para especie
    public void setEspecie(String especie) {
        this.especie = especie;
    }

    // Getter para costo de consulta
    // Este valor puede ser modificado por los métodos ajusteCosto() y aplicarRecargo()
    public double getCostoConsulta() {
        return costoConsulta;
    }

    // Setter para costo de consulta
    // Protected permite que las clases hijas lo modifiquen directamente
    protected void setCostoConsulta(double costoConsulta) {
        this.costoConsulta = costoConsulta;
    }

    // Getter para edad
    public int getEdad() {
        return edad;
    }

    // Setter para edad
    public void setEdad(int edad) {
        this.edad = edad;
    }

    // Método abstracto: cada tipo de mascota implementa su propia lógica
    // Los gatos con pelaje corto tendrán -20% de descuento
    // Los perros no tienen este ajuste
    public abstract void ajusteCosto();

    // Método abstracto: cada tipo de mascota implementa su propia lógica
    // Perros grandes tendrán recargo
    // Gatos exóticos tendrán recargo
    public abstract void aplicarRecargo(double porcentaje);

    // toString: retorna una representación en texto de la mascota
    // Las clases hijas pueden sobrescribir este método para agregar más información
    @Override
    public String toString() {
        return "Código: " + codigo +
               "\nNombre: " + nombre +
               "\nEspecie: " + especie +
               "\nCosto Consulta: $" + costoConsulta +
               "\nEdad: " + edad + " años";
    }
}
```

## Explicación Paso a Paso

**¿Por qué abstract?**
Usamos `abstract class` porque "Mascota" es un concepto general. En la clínica nunca dirán "ingresé una mascota", siempre será "ingresé un perro" o "ingresé un gato". Las clases abstractas no pueden ser instanciadas, solo heredadas.

**Los atributos privados:**
Todos los atributos son `private` para aplicar encapsulación. Nadie desde fuera de la clase puede acceder directamente a ellos. Solo a través de getters y setters.

**El constructor:**
Recibe los 5 parámetros básicos y los asigna a los atributos usando `this`. Las clases hijas (Perro y Gato) llamarán a este constructor desde su propio constructor usando `super()`.

**Getters y Setters:**
Cada atributo privado necesita métodos públicos para leer (get) y modificar (set) su valor. Nota que `setCostoConsulta` es `protected`, no `public`, porque solo las clases hijas deberían modificar directamente el costo.

**Métodos abstractos:**
`ajusteCosto()` y `aplicarRecargo()` están declarados pero no implementados (no tienen cuerpo). Cada clase hija debe implementar su propia versión. Por ejemplo, los gatos verificarán el tipo de pelaje en ajusteCosto(), mientras que los perros pueden dejarlo vacío.

**El método toString():**
Sobrescribe el método heredado de Object. Retorna una cadena de texto con todos los datos básicos de la mascota. Esto es útil para mostrar información en consola de forma legible.

## ¿Qué sigue?

Ahora que tenemos la clase base, crearemos la clase `Perro` que hereda de `Mascota` e implementa la interfaz `PlanPrevencion`.

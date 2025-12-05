# Gato - Segunda Clase Concreta

## ¿Qué vamos a crear?

Ahora creamos la clase `Gato`, nuestra segunda clase concreta. Esta clase **hereda** de `Mascota` pero **NO implementa** `PlanPrevencion` porque los gatos no participan en el plan de descuento de vacunación de la clínica.

Los gatos tienen atributos adicionales (tipoPelaje y esExotico) y deben implementar los métodos abstractos heredados de Mascota, pero con lógica diferente a la de los perros.

## Conceptos POO Aplicados

- **Herencia**: Gato extiende de Mascota
- **Polimorfismo**: Un objeto Gato puede ser tratado como Mascota
- **Sobrescritura de métodos**: Implementa los métodos abstractos con lógica específica para gatos
- **Encapsulación**: Atributos privados con getters y setters

## Código Completo

```java
// Clase Gato: hereda de Mascota pero NO implementa PlanPrevencion
// Los gatos no participan en el plan de descuento de vacunación
public class Gato extends Mascota {

    // Atributos específicos de los gatos
    // Adicionales a los heredados de Mascota
    private String tipoPelaje;
    private boolean esExotico;

    // Constructor: recibe TODOS los parámetros (heredados + propios)
    // codigo, nombre, especie, costoConsulta, edad vienen de Mascota
    // tipoPelaje y esExotico son específicos de Gato
    public Gato(String codigo, String nombre, String especie, double costoConsulta, int edad,
                String tipoPelaje, boolean esExotico) {

        // super() llama al constructor de la clase padre (Mascota)
        // Le pasamos los 5 parámetros que necesita
        super(codigo, nombre, especie, costoConsulta, edad);

        // Inicializamos los atributos propios de Gato
        this.tipoPelaje = tipoPelaje;
        this.esExotico = esExotico;
    }

    // Getter para tipo de pelaje
    public String getTipoPelaje() {
        return tipoPelaje;
    }

    // Setter para tipo de pelaje
    public void setTipoPelaje(String tipoPelaje) {
        this.tipoPelaje = tipoPelaje;
    }

    // Getter para esExotico
    // Nota: para booleanos, el getter se llama "is" en vez de "get"
    public boolean isEsExotico() {
        return esExotico;
    }

    // Setter para esExotico
    public void setEsExotico(boolean esExotico) {
        this.esExotico = esExotico;
    }

    // Implementación del método abstracto heredado de Mascota
    // Para gatos, aplicamos un descuento si el pelaje es corto
    // Los gatos de pelaje corto requieren menos tiempo de atención
    @Override
    public void ajusteCosto() {

        // Verificamos si el tipo de pelaje es "corto"
        // equals() compara el contenido de los strings
        if (this.tipoPelaje.equals("corto")) {

            // Si es pelaje corto, reducimos el costo en 20%
            // Multiplicamos por 0.8 que es equivalente a reducir 20%
            // Por ejemplo: si costo es 15000, nuevo costo = 15000 * 0.8 = 12000
            this.setCostoConsulta(this.getCostoConsulta() * 0.8);
        }
    }

    // Implementación del método abstracto heredado de Mascota
    // Aplica un recargo si el gato es de raza exótica
    // Los gatos exóticos requieren atención especializada
    @Override
    public void aplicarRecargo(double porcentaje) {

        // Verificamos si el gato es exótico
        if (this.esExotico) {

            // Calculamos el recargo sobre el costo actual
            // Por ejemplo: si costo es 15000 y porcentaje es 10
            // recargo = 15000 * 10 / 100 = 1500
            double recargo = this.getCostoConsulta() * porcentaje / 100;

            // Actualizamos el costo sumando el recargo
            this.setCostoConsulta(this.getCostoConsulta() + recargo);
        }
    }

    // Sobrescribimos toString() para incluir información específica de Gato
    // Llamamos al toString() de la clase padre y agregamos más datos
    @Override
    public String toString() {

        // super.toString() obtiene la información básica de Mascota
        // Luego agregamos la información específica de Gato
        return super.toString() +
               "\nTipo de Pelaje: " + tipoPelaje +
               "\nEs Exótico: " + (esExotico ? "Sí" : "No");
    }
}
```

## Explicación Paso a Paso

**La declaración de la clase:**
`extends Mascota` significa que Gato hereda todo de Mascota. Nota que NO implementa `PlanPrevencion` porque los gatos no califican para el descuento de vacunación según las reglas de negocio de la clínica.

**El constructor:**
Similar al de Perro, recibe 7 parámetros: 5 heredados + 2 propios. La primera línea DEBE ser `super()` para inicializar los atributos de Mascota. Luego inicializamos tipoPelaje y esExotico.

**Los getters y setters:**
Creamos getters y setters solo para los atributos propios. Nota que el getter de un boolean se llama `isEsExotico()` en vez de `getEsExotico()`, esto es una convención de Java.

**ajusteCosto():**
Aquí está la diferencia clave con Perro. Para gatos, este método SÍ hace algo: si el pelaje es "corto", reduce el costo en 20%. Usamos `* 0.8` que es lo mismo que reducir un 20% (100% - 20% = 80% = 0.8).

**aplicarRecargo():**
Si el gato es exótico (esExotico == true), calculamos el recargo y lo sumamos al costo. La lógica es similar a la de Perro, pero la condición es diferente: aquí verificamos si es exótico, en Perro verificábamos si era grande.

**toString():**
Llamamos a `super.toString()` para obtener la información básica y agregamos tipoPelaje y esExotico. Para el booleano usamos el operador ternario `? :` para mostrar "Sí" o "No" en vez de "true" o "false".

## Diferencias Clave con Perro

- **Gato NO implementa PlanPrevencion**: No tiene el método descuentoVacunacion()
- **ajusteCosto() hace algo**: En Perro estaba vacío, en Gato aplica el descuento de -20%
- **aplicarRecargo() verifica otra condición**: En Perro verifica tamaño, en Gato verifica si es exótico
- **Usa un atributo boolean**: esExotico es boolean, mientras que tamaño en Perro es String

## ¿Qué sigue?

Ahora que tenemos nuestras dos clases concretas (Perro y Gato), crearemos la clase `Clinica` que será la manejadora de la colección de mascotas. Esta clase permitirá ingresar, buscar, aplicar ajustes y calcular descuentos.

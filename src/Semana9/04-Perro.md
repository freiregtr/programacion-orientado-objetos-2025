# Perro - Primera Clase Concreta

## ¿Qué vamos a crear?

Ahora creamos la clase `Perro`, que es nuestra primera clase concreta. Esta clase **hereda** de `Mascota` e **implementa** la interfaz `PlanPrevencion`.

Los perros tienen atributos adicionales (raza y tamaño) y deben implementar los métodos abstractos de la clase padre. Además, como implementan `PlanPrevencion`, deben definir la lógica del descuento de vacunación.

## Conceptos POO Aplicados

- **Herencia**: Perro extiende de Mascota, heredando sus atributos y métodos
- **Implementación de Interfaces**: Perro implementa PlanPrevencion
- **Polimorfismo**: Un objeto Perro puede ser tratado como Mascota o como PlanPrevencion
- **Sobrescritura de métodos**: Implementa los métodos abstractos heredados

## Código Completo

```java
// Clase Perro: hereda de Mascota e implementa PlanPrevencion
// La palabra extends indica herencia, implements indica interfaz
public class Perro extends Mascota implements PlanPrevencion {

    // Atributos específicos de los perros
    // Estos son adicionales a los heredados de Mascota
    private String raza;
    private String tamanio;

    // Constructor: recibe TODOS los parámetros (los heredados + los propios)
    // codigo, nombre, especie, costoConsulta, edad vienen de Mascota
    // raza y tamanio son específicos de Perro
    public Perro(String codigo, String nombre, String especie, double costoConsulta, int edad,
                 String raza, String tamanio) {

        // super() llama al constructor de la clase padre (Mascota)
        // Le pasamos los 5 parámetros que necesita
        super(codigo, nombre, especie, costoConsulta, edad);

        // Ahora inicializamos los atributos propios de Perro
        this.raza = raza;
        this.tamanio = tamanio;
    }

    // Getter para raza
    public String getRaza() {
        return raza;
    }

    // Setter para raza
    public void setRaza(String raza) {
        this.raza = raza;
    }

    // Getter para tamaño
    public String getTamanio() {
        return tamanio;
    }

    // Setter para tamaño
    public void setTamanio(String tamanio) {
        this.tamanio = tamanio;
    }

    // Implementación del método abstracto heredado de Mascota
    // Para los perros, este método no hace nada
    // El ajuste de -20% solo aplica a gatos con pelaje corto
    @Override
    public void ajusteCosto() {
        // No aplicamos ningún ajuste para perros
        // Este método existe porque Mascota lo definió como abstracto
        // Podríamos dejarlo vacío o agregar un mensaje
    }

    // Implementación del método abstracto heredado de Mascota
    // Aplica un recargo si el perro es de tamaño grande
    @Override
    public void aplicarRecargo(double porcentaje) {

        // Verificamos si el tamaño es "grande"
        // equals() compara el contenido de los strings
        if (this.tamanio.equals("grande")) {

            // Calculamos el recargo sobre el costo actual
            // Por ejemplo: si costo es 20000 y porcentaje es 10
            // recargo = 20000 * 10 / 100 = 2000
            double recargo = this.getCostoConsulta() * porcentaje / 100;

            // Actualizamos el costo sumando el recargo
            // Usamos setCostoConsulta heredado de Mascota
            this.setCostoConsulta(this.getCostoConsulta() + recargo);
        }
    }

    // Implementación del método de la interfaz PlanPrevencion
    // Este método calcula el descuento por vacunación
    // Solo aplica a perros pequeños
    @Override
    public double descuentoVacunacion() {

        // Verificamos si el tamaño es "pequeño"
        if (this.tamanio.equals("pequeño")) {

            // Si es pequeño, calculamos el 15% del costo de consulta
            // DESCUENTO_VACUNA viene de la interfaz PlanPrevencion (0.15)
            // Por ejemplo: si costo es 20000, descuento = 20000 * 0.15 = 3000
            return this.getCostoConsulta() * DESCUENTO_VACUNA;
        }

        // Si no es pequeño, no hay descuento
        return 0;
    }

    // Sobrescribimos toString() para incluir la información específica de Perro
    // Llamamos al toString() de la clase padre y agregamos más datos
    @Override
    public String toString() {

        // super.toString() obtiene la información básica de Mascota
        // Luego agregamos la información específica de Perro
        return super.toString() +
               "\nRaza: " + raza +
               "\nTamaño: " + tamanio;
    }
}
```

## Explicación Paso a Paso

**La declaración de la clase:**
`extends Mascota` significa que Perro hereda todo de Mascota (atributos y métodos). `implements PlanPrevencion` significa que Perro se compromete a implementar el método `descuentoVacunacion()`.

**El constructor:**
Recibe 7 parámetros en total: 5 heredados de Mascota + 2 propios. La primera línea DEBE ser `super()` para inicializar los atributos heredados. Luego inicializamos los propios con `this`.

**Los getters y setters:**
Solo necesitamos crear getters y setters para los atributos propios (raza y tamanio). Los de los atributos heredados ya existen en Mascota.

**ajusteCosto():**
Este método está vacío porque según las reglas de negocio, el ajuste de -20% solo aplica a gatos con pelaje corto. Los perros no tienen este ajuste. Pero como el método es abstracto en Mascota, estamos obligados a implementarlo.

**aplicarRecargo():**
Aquí implementamos la lógica: si el tamaño es "grande", calculamos el recargo y lo sumamos al costo actual. Usamos `getCostoConsulta()` para leer el costo y `setCostoConsulta()` para actualizarlo.

**descuentoVacunacion():**
Este método viene de la interfaz. Si el perro es pequeño, retornamos el 15% del costo de consulta. Si no, retornamos 0. Este método será usado por la clase Clinica para calcular el total de descuentos.

**toString():**
Llamamos a `super.toString()` para obtener la información básica (código, nombre, especie, costo, edad) y le agregamos la información específica de perro (raza y tamaño).

## ¿Qué sigue?

Ahora crearemos la clase `Gato`, que también hereda de `Mascota` pero NO implementa `PlanPrevencion` porque los gatos no participan en el plan de vacunación.

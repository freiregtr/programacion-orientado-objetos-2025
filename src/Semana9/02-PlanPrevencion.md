# PlanPrevencion - La Interfaz

## ¿Qué vamos a crear?

Empezamos con lo más simple: una interfaz. Las interfaces en Java son como contratos que definen qué métodos debe tener una clase, pero sin implementarlos. En nuestro caso, la interfaz `PlanPrevencion` define el comportamiento para aplicar descuentos en el plan de vacunación de la clínica.

Solo los perros pequeños participan en este plan, pero por ahora solo definimos el "contrato". Más adelante, la clase `Perro` implementará este contrato.

## Conceptos POO Aplicados

- **Abstracción**: Definimos QUÉ se debe hacer (calcular descuento), no CÓMO hacerlo
- **Interfaces**: Contrato que obliga a las clases a implementar ciertos métodos
- **Constantes**: El descuento es fijo (15%) para todas las clases que implementen la interfaz

## Código Completo

```java
// Esta es una interfaz, no una clase
// Las interfaces definen comportamientos que otras clases deben implementar
public interface PlanPrevencion {

    // Constante: descuento del 15% para vacunación
    // En interfaces, las variables son automáticamente public, static y final
    double DESCUENTO_VACUNA = 0.15;

    // Método abstracto: debe ser implementado por las clases que usen esta interfaz
    // Retorna el monto de descuento aplicable a la mascota
    // Si la mascota no califica, debe retornar 0
    double descuentoVacunacion();
}
```

## Explicación Paso a Paso

**¿Por qué una interfaz?**
La clínica tiene un plan de prevención que no aplica a todas las mascotas. Solo perros pequeños califican. Usar una interfaz nos permite que solo las clases que realmente participan en este plan lo implementen. Los gatos no lo implementarán.

**La constante DESCUENTO_VACUNA:**
El valor 0.15 representa el 15% de descuento. Es una constante porque este porcentaje no cambia. Al estar en la interfaz, todas las clases que la implementen tienen acceso a este valor.

**El método descuentoVacunacion():**
Este método no tiene cuerpo (no tiene llaves {}). Solo declara que debe existir. Cada clase que implemente esta interfaz debe escribir su propia lógica para calcular el descuento. Por ejemplo, los perros verificarán si son pequeños antes de aplicarlo.

## ¿Qué sigue?

Ahora que tenemos el contrato definido, crearemos la clase abstracta `Mascota` que será la base para todos los animales de la clínica.

# Sistema de Gestión de Clínica Veterinaria "PatitasFelices"

## Descripción del Problema

La clínica veterinaria "PatitasFelices" necesita un sistema para gestionar las mascotas que atiende. Actualmente llevan todo en papel, lo que dificulta el control de costos, la aplicación de descuentos y el seguimiento de sus planes de prevención.

El sistema debe permitir registrar perros y gatos con sus características específicas, aplicar políticas comerciales automáticamente (descuentos y recargos según el tipo de mascota), buscar mascotas rápidamente, y generar reportes sobre los descuentos otorgados.

## Requerimientos del Sistema

Se requiere modelar un sistema para gestionar las mascotas de la clínica. La información a considerar es la siguiente:

### Las Mascotas (clase base)
Todas las mascotas tienen:
- **Código** (String): Identificador único de la mascota
- **Nombre** (String): Nombre del animal
- **Especie** (String): Tipo de especie (ej: "Canino", "Felino")
- **Costo de Consulta** (double): Precio base de la consulta
- **Edad** (int): Edad del animal en años

### Los Perros
Además de los atributos heredados, tienen:
- **Raza** (String): La raza del perro (ej: "Labrador", "Poodle")
- **Tamaño** (String): Puede ser "pequeño" o "grande"

### Los Gatos
Además de los atributos heredados, tienen:
- **Tipo de Pelaje** (String): Puede ser "corto" o "largo"
- **Es Exótico** (boolean): Indica si es una raza exótica

### La Interfaz PlanPrevencion
Contiene el atributo `DESCUENTO_VACUNA` (15%) y el método `descuentoVacunacion()`. Este método aplicará el descuento solo si es un perro pequeño. En cualquier otro caso, el descuento será cero.

### Métodos Requeridos

Además, se necesitan los siguientes métodos:

- **ajusteCosto()**: Disminuirá el costo de consulta en un 20% si el tipo de pelaje es "corto"
- **aplicarRecargo()**: Aumentará el costo de consulta en un X% si el tamaño es "grande" o si es un gato exótico

### Clase Manejadora: Clinica

Crear una clase manejadora llamada `Clinica` que permita gestionar una colección de Mascota. Los métodos que esta clase debe tener son:

- **ingresarMascota()**: Agrega una mascota a la colección. Debe validar que no esté duplicada por su código
- **buscarMascota()**: Busca y devuelve una mascota por su código
- **aplicarAjusteATodos()**: Recorre la colección y aplica el método ajusteCosto a todas las mascotas que cumplan con la condición. Devolverá el total de mascotas a las que se les aplicó el ajuste
- **calcularDescuentoTotal()**: Recorre la colección y calcula el total de dinero ahorrado por concepto de descuentoVacunacion

## Diagrama de Clases

```
         Mascota (abstracta)
              |
      ________|________
     |                 |
   Perro          Gato
     |
     |
implements PlanPrevencion (interface)
```

## Menú de la Aplicación

Implementar el siguiente menú:

```
PATITASFELICES

1. Ingresar Mascota: Permite agregar un Perro o un Gato a la colección
2. Mostrar Información: Muestra toda la información de una mascota dado su código
3. Aplicar Ajuste de Costo: Ejecuta el método aplicarAjusteATodos, mostrando mensaje adecuado
4. Calcular Descuento Total: Ejecuta el método calcularDescuentoTotal
5. Salir
```

## Notas Importantes

- Construya las clases que representen la situación anterior en Java utilizando NetBeans
- Implemente constructores, accesadores (getters) y mutadores (setters)
- Considere el uso de clases y métodos abstractos donde sea necesario para modelar la jerarquía de manera correcta
- La clase `Mascota` debe ser abstracta
- Solo la clase `Perro` implementa la interfaz `PlanPrevencion`
- Use `ArrayList` para la colección de mascotas

# Clinica - La Clase Manejadora

## ¿Qué vamos a crear?

Ahora creamos la clase `Clinica`, que es el corazón del sistema. Esta clase maneja la colección de todas las mascotas registradas y proporciona métodos para realizar operaciones sobre ellas: ingresar, buscar, aplicar ajustes y calcular descuentos.

Esta clase usa **colecciones** (ArrayList) para almacenar las mascotas y demuestra el concepto de **polimorfismo**: la colección es de tipo `Mascota`, pero puede contener tanto `Perro` como `Gato`.

## Conceptos POO Aplicados

- **Colecciones**: Uso de ArrayList para almacenar objetos dinámicamente
- **Polimorfismo**: La lista es de tipo Mascota pero contiene Perro y Gato
- **Encapsulación**: La colección es privada, solo accesible mediante métodos públicos
- **Casting**: Conversión de tipos para acceder a métodos específicos
- **instanceof**: Verificación del tipo real de un objeto

## Código Completo

```java
// Importamos ArrayList para manejar la colección de mascotas
import java.util.ArrayList;

// Clase Clinica: gestiona todas las mascotas registradas en la clínica
public class Clinica {

    // Colección privada que almacena todas las mascotas
    // ArrayList es una lista dinámica que puede crecer según sea necesario
    // Es de tipo Mascota, por lo que puede contener Perro y Gato (polimorfismo)
    private ArrayList<Mascota> mascotas;

    // Constructor: inicializa la colección vacía
    // Cuando creamos una Clinica nueva, comienza sin mascotas
    public Clinica() {
        // Creamos un ArrayList vacío
        this.mascotas = new ArrayList<>();
    }

    // Método para ingresar una nueva mascota a la colección
    // Recibe un objeto de tipo Mascota (puede ser Perro o Gato)
    // Retorna true si se agregó exitosamente, false si ya existía
    public boolean ingresarMascota(Mascota m) {

        // Primero debemos verificar que no exista una mascota con el mismo código
        // Recorremos la colección completa
        for (Mascota mascota : mascotas) {

            // Comparamos el código de cada mascota con el código de la nueva mascota
            // equals() compara el contenido de los strings
            if (mascota.getCodigo().equals(m.getCodigo())) {

                // Si encontramos un código duplicado, mostramos error y retornamos false
                System.out.println("Error: Ya existe una mascota con el código " + m.getCodigo());
                return false;
            }
        }

        // Si llegamos aquí, no hay duplicados
        // Agregamos la mascota a la colección usando add()
        mascotas.add(m);

        // Mostramos mensaje de confirmación
        System.out.println("Mascota ingresada exitosamente");
        return true;
    }

    // Método para buscar una mascota por su código
    // Recibe el código a buscar como String
    // Retorna el objeto Mascota si lo encuentra, null si no existe
    public Mascota buscarMascota(String codigo) {

        // Recorremos toda la colección buscando el código
        for (Mascota mascota : mascotas) {

            // Comparamos el código de cada mascota con el código buscado
            if (mascota.getCodigo().equals(codigo)) {

                // Si encontramos coincidencia, retornamos ese objeto
                return mascota;
            }
        }

        // Si terminamos el ciclo sin encontrar nada, mostramos mensaje y retornamos null
        System.out.println("No se encontró mascota con el código " + codigo);
        return null;
    }

    // Método para aplicar el ajuste de costo a todas las mascotas que califican
    // Recorre la colección y aplica ajusteCosto() donde corresponda
    // Retorna la cantidad de mascotas a las que se les aplicó el ajuste
    public int aplicarAjusteATodos() {

        // Contador: lleva la cuenta de cuántas mascotas fueron ajustadas
        int contador = 0;

        // Recorremos toda la colección
        for (Mascota mascota : mascotas) {

            // Verificamos si la mascota es un Gato usando instanceof
            // instanceof retorna true si el objeto es de ese tipo
            if (mascota instanceof Gato) {

                // Hacemos casting: convertimos Mascota a Gato
                // Esto nos permite acceder a métodos específicos de Gato como getTipoPelaje()
                Gato gato = (Gato) mascota;

                // Verificamos si el pelaje es "corto"
                // Solo los gatos con pelaje corto reciben el ajuste de -20%
                if (gato.getTipoPelaje().equals("corto")) {

                    // Aplicamos el ajuste llamando al método ajusteCosto()
                    gato.ajusteCosto();

                    // Incrementamos el contador
                    contador++;
                }
            }
        }

        // Retornamos cuántas mascotas fueron ajustadas
        return contador;
    }

    // Método para calcular el total de descuentos otorgados por vacunación
    // Recorre la colección y suma los descuentos de todas las mascotas que califican
    // Retorna el total acumulado en pesos
    public double calcularDescuentoTotal() {

        // Acumulador: suma todos los descuentos
        double total = 0;

        // Recorremos toda la colección
        for (Mascota mascota : mascotas) {

            // Verificamos si la mascota implementa la interfaz PlanPrevencion
            // Solo los Perros implementan esta interfaz
            if (mascota instanceof PlanPrevencion) {

                // Hacemos casting a PlanPrevencion para acceder al método descuentoVacunacion()
                PlanPrevencion plan = (PlanPrevencion) mascota;

                // Llamamos al método y acumulamos el resultado
                // Si es un perro pequeño, retornará el 15% del costo, si no, retornará 0
                total += plan.descuentoVacunacion();
            }
        }

        // Retornamos el total acumulado
        return total;
    }

    // Método opcional: retorna la cantidad de mascotas registradas
    // Útil para validaciones o mostrar estadísticas
    public int getCantidadMascotas() {
        return mascotas.size();
    }
}
```

## Explicación Paso a Paso

**El ArrayList:**
`ArrayList<Mascota>` es una lista dinámica que puede crecer automáticamente. Es de tipo `Mascota`, lo que significa que puede almacenar objetos `Perro` y `Gato` porque ambos heredan de `Mascota`. Esto es polimorfismo en acción.

**ingresarMascota():**
Primero recorre toda la colección con un `for-each` verificando si existe alguna mascota con el mismo código. Si encuentra duplicado, retorna `false`. Si no hay duplicados, usa `mascotas.add(m)` para agregar la mascota y retorna `true`.

**buscarMascota():**
Recorre la colección comparando códigos. Cuando encuentra coincidencia, retorna ese objeto. Si termina el ciclo sin encontrar nada, retorna `null`. El que llame a este método debe verificar si el resultado es `null` antes de usarlo.

**aplicarAjusteATodos():**
Este método es más complejo porque usa `instanceof` y casting. Primero verifica si cada mascota es un `Gato`. Si lo es, hace casting para poder llamar a `getTipoPelaje()`. Si el pelaje es "corto", llama a `ajusteCosto()` e incrementa el contador. Al final retorna cuántas mascotas fueron ajustadas.

**calcularDescuentoTotal():**
Similar al anterior, pero verifica si la mascota implementa `PlanPrevencion` (solo los perros). Si la implementa, hace casting a `PlanPrevencion` y llama a `descuentoVacunacion()`. Acumula todos los valores y retorna el total.

## Conceptos Importantes

**¿Por qué instanceof?**
Porque la colección es de tipo `Mascota`, no sabemos si cada objeto es realmente un `Perro` o un `Gato`. `instanceof` nos permite verificar el tipo real del objeto en tiempo de ejecución.

**¿Por qué casting?**
Cuando hacemos `Gato gato = (Gato) mascota`, estamos diciéndole a Java "confía en mí, este objeto es un Gato". Esto nos permite acceder a métodos específicos de `Gato` como `getTipoPelaje()` que no existen en `Mascota`.

**¿Por qué for-each?**
El ciclo `for (Mascota mascota : mascotas)` es más limpio y legible que un for tradicional. Lee "para cada mascota en mascotas". Java automáticamente itera sobre todos los elementos.

## ¿Qué sigue?

Finalmente crearemos la clase `Main` que tendrá el menú interactivo. Esta clase usará todos los métodos de `Clinica` para permitir al usuario interactuar con el sistema.

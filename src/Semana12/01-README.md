# Sistema de Pedidos de Pizza - Análisis y Arquitectura

## Descripción del Problema

Las pizzerías necesitan un sistema digital para gestionar pedidos de manera eficiente. Actualmente, muchos negocios pequeños dependen de sistemas manuales (papel y lápiz) que generan errores, retrasos y dificultan el cálculo de precios cuando los clientes personalizan sus pedidos.

Este proyecto implementa un sistema de pedidos de pizza que permite:
- Seleccionar diferentes tipos de pizzas predefinidas
- Personalizar pizzas con ingredientes adicionales
- Calcular automáticamente el precio según tamaño y extras
- Gestionar un carrito de compras
- Visualizar el total del pedido

## Objetivos de Aprendizaje

Este proyecto demuestra los conceptos fundamentales de Programación Orientada a Objetos (POO):

1. Clases y Objetos
2. Herencia
3. Polimorfismo
4. Interfaces
5. Abstracción
6. Encapsulación
7. Composición
8. Enumeraciones (Enums)

## Casos de Uso

### Caso de Uso 1: Seleccionar Pizza Predefinida
**Actor:** Cliente
**Flujo:**
1. El cliente selecciona un tipo de pizza (Tradicional o Premium)
2. El cliente elige el tamaño (Pequeña, Mediana, Familiar)
3. El sistema calcula el precio automáticamente
4. El cliente agrega la pizza al carrito

### Caso de Uso 2: Crear Pizza Personalizada
**Actor:** Cliente
**Flujo:**
1. El cliente selecciona "Pizza Personalizada"
2. El cliente elige el tamaño
3. El cliente selecciona ingredientes extras (checkbox múltiples)
4. El sistema calcula el precio base + ingredientes
5. El cliente agrega la pizza al carrito

### Caso de Uso 3: Ver Carrito y Total
**Actor:** Cliente
**Flujo:**
1. El cliente visualiza las pizzas agregadas al carrito
2. El sistema muestra el desglose de cada pizza
3. El sistema calcula y muestra el total del pedido

## Requisitos Funcionales

### RF-01: Gestión de Tipos de Pizza
El sistema debe soportar tres tipos de pizzas:
- **Pizza Tradicional:** Precio base fijo, sin personalización
- **Pizza Premium:** Precio base más alto, ingredientes premium incluidos
- **Pizza Personalizada:** Precio base + costo por ingrediente adicional

### RF-02: Gestión de Tamaños
El sistema debe permitir tres tamaños:
- **Pequeña:** Multiplicador 1.0x
- **Mediana:** Multiplicador 1.5x
- **Familiar:** Multiplicador 2.0x

### RF-03: Gestión de Ingredientes
El sistema debe permitir agregar ingredientes extras:
- Jamón (+$1000)
- Champiñones (+$800)
- Aceitunas (+$600)
- Pepperoni (+$1200)
- Piña (+$700)
- Cebolla (+$500)

### RF-04: Cálculo de Precios
El sistema debe calcular automáticamente:
- Precio de pizza según tipo y tamaño
- Precio de ingredientes extras
- Total del pedido sumando todas las pizzas del carrito

### RF-05: Gestión de Carrito
El sistema debe permitir:
- Agregar pizzas al carrito
- Visualizar lista de pizzas en el carrito
- Mostrar total acumulado

## Requisitos No Funcionales

### RNF-01: Usabilidad
La interfaz debe ser intuitiva y fácil de usar, con componentes claramente etiquetados.

### RNF-02: Mantenibilidad
El código debe seguir principios SOLID y estar bien documentado para facilitar futuras modificaciones.

### RNF-03: Escalabilidad
La arquitectura debe permitir agregar nuevos tipos de pizzas e ingredientes sin modificar código existente (Principio Abierto/Cerrado).

## Arquitectura del Sistema

### Patrón de Diseño: MVC (Model-View-Controller)

El sistema se estructura en tres capas:

**Modelo (Backend):**
- Clases de dominio (Pizza, Pedido, Ingrediente, Cliente)
- Lógica de negocio
- Cálculos y validaciones

**Vista (Frontend):**
- Interfaz gráfica con Swing
- Componentes visuales (JFrame, JPanel, JButton, etc.)
- Presentación de datos

**Controlador:**
- Event listeners
- Conexión entre Vista y Modelo
- Flujo de la aplicación

### Diagrama de Clases (Conceptual)

```
                    <<interface>>
                     Calculable
                    +-----------+
                    | calcularPrecio(): double
                    +-----------+
                          ^
                          |
                    <<abstract>>
                       Pizza
            +-------------------------+
            | - nombre: String        |
            | - tamaño: Tamaño        |
            | - precioBase: double    |
            +-------------------------+
            | + calcularPrecio(): double (abstracto)
            | + getTamaño(): Tamaño   |
            | + getNombre(): String   |
            +-------------------------+
                      ^
                      |
        +-------------+---------------+
        |             |               |
  PizzaTradicional  PizzaPremium  PizzaPersonalizada
  +-----------+     +-----------+   +------------------+
  | calcularPrecio() | calcularPrecio() | - ingredientes: List<Ingrediente>
  +-----------+     +-----------+   | + agregarIngrediente()
                                    | + quitarIngrediente()
                                    | + calcularPrecio()
                                    +------------------+
                                            |
                                    implements Customizable


                    <<interface>>
                    Customizable
                    +------------------+
                    | agregarIngrediente(Ingrediente)
                    | quitarIngrediente(Ingrediente)
                    +------------------+


                     Ingrediente
                    +------------------+
                    | - nombre: String |
                    | - precio: double |
                    +------------------+
                    | + getNombre()    |
                    | + getPrecio()    |
                    +------------------+


                       Pedido
            +-------------------------+
            | - cliente: String       |
            | - pizzas: List<Pizza>   |
            | - fecha: LocalDateTime  |
            +-------------------------+
            | + agregarPizza(Pizza)   |
            | + calcularTotal(): double
            | + getPizzas(): List     |
            +-------------------------+


                    <<enum>>
                      Tamaño
            +-------------------------+
            | PEQUEÑA (1.0)           |
            | MEDIANA (1.5)           |
            | FAMILIAR (2.0)          |
            +-------------------------+
            | - multiplicador: double |
            | + getMultiplicador()    |
            +-------------------------+
```

## Decisiones de Arquitectura POO

### 1. Herencia: Jerarquía de Pizzas

**Decisión:** Crear una clase abstracta `Pizza` con tres clases hijas concretas.

**Justificación:**
- Todas las pizzas comparten atributos comunes (nombre, tamaño, precioBase)
- Cada tipo de pizza calcula su precio de manera diferente
- Permite agregar nuevos tipos sin modificar código existente (OCP)

**Aplicación:**
```java
abstract class Pizza {
    // Atributos comunes
    protected String nombre;
    protected Tamaño tamaño;
    protected double precioBase;

    // Método abstracto - cada hijo lo implementa diferente
    public abstract double calcularPrecio();
}
```

### 2. Polimorfismo: Cálculo de Precios

**Decisión:** Usar polimorfismo para calcular el precio de diferentes tipos de pizzas.

**Justificación:**
- Cada tipo de pizza tiene su propia lógica de cálculo
- El cliente (código que usa las pizzas) no necesita saber qué tipo específico es
- Facilita agregar nuevos tipos con diferentes estrategias de cálculo

**Aplicación:**
```java
List<Pizza> pizzas = new ArrayList<>();
pizzas.add(new PizzaTradicional(...));
pizzas.add(new PizzaPremium(...));
pizzas.add(new PizzaPersonalizada(...));

// Polimorfismo en acción
for (Pizza pizza : pizzas) {
    total += pizza.calcularPrecio(); // Llama al método correcto según el tipo
}
```

### 3. Interfaces: Capacidades Específicas

**Decisión:** Crear interfaces `Calculable` y `Customizable`.

**Justificación:**
- No todas las pizzas son customizables (solo PizzaPersonalizada)
- Separa "qué puede hacer" de "qué es" (interface segregation)
- Permite que otras clases implementen estas capacidades

**Aplicación:**
```java
interface Calculable {
    double calcularPrecio();
}

interface Customizable {
    void agregarIngrediente(Ingrediente ingrediente);
    void quitarIngrediente(Ingrediente ingrediente);
}
```

### 4. Abstracción: Clase Pizza Base

**Decisión:** Hacer `Pizza` una clase abstracta en lugar de concreta.

**Justificación:**
- No tiene sentido crear una instancia de "Pizza" genérica
- Fuerza a los desarrolladores a usar tipos específicos
- Centraliza comportamiento común sin permitir instanciación directa

### 5. Encapsulación: Atributos Privados

**Decisión:** Todos los atributos son privados/protected con getters/setters públicos.

**Justificación:**
- Control sobre cómo se accede y modifica el estado
- Validación en setters (ej: precio no puede ser negativo)
- Flexibilidad para cambiar implementación interna

**Aplicación:**
```java
private double precioBase;

public double getPrecioBase() {
    return precioBase;
}

public void setPrecioBase(double precio) {
    if (precio < 0) {
        throw new IllegalArgumentException("Precio no puede ser negativo");
    }
    this.precioBase = precio;
}
```

### 6. Composición: Pedido tiene Pizzas

**Decisión:** Usar composición en lugar de herencia para la relación Pedido-Pizza.

**Justificación:**
- Un Pedido "tiene" pizzas, no "es" una pizza
- Permite múltiples pizzas en un pedido
- Favorece composición sobre herencia (principio de diseño)

**Aplicación:**
```java
class Pedido {
    private List<Pizza> pizzas = new ArrayList<>();

    public void agregarPizza(Pizza pizza) {
        pizzas.add(pizza);
    }
}
```

### 7. Enums: Valores Fijos y Seguros

**Decisión:** Usar enum para Tamaño en lugar de Strings o constantes.

**Justificación:**
- Type-safe: el compilador previene valores inválidos
- Centraliza valores posibles
- Puede contener lógica (multiplicador de precio)

**Aplicación:**
```java
enum Tamaño {
    PEQUEÑA(1.0),
    MEDIANA(1.5),
    FAMILIAR(2.0);

    private final double multiplicador;

    Tamaño(double multiplicador) {
        this.multiplicador = multiplicador;
    }

    public double getMultiplicador() {
        return multiplicador;
    }
}
```

## Patrones de Diseño Aplicados

### 1. Factory Method (Implícito)
Aunque no implementamos un Factory explícito, la creación de diferentes tipos de pizzas sigue este patrón conceptualmente.

### 2. Strategy Pattern
El cálculo de precio es diferente para cada tipo de pizza (estrategia diferente).

### 3. Composite Pattern (Simplificado)
El Pedido contiene una colección de Pizzas y calcula el total agregado.

## Estructura del Proyecto

```
PizzaApp/
├── 01-README.md              (este archivo)
├── 02-interfaz-grafica.md    (diseño visual)
├── 03-backend.md             (implementación)
├── screenshots/
│   ├── gui-principal.png
│   ├── seleccion-pizza.png
│   └── carrito.png
└── src/
    ├── modelo/
    │   ├── Pizza.java
    │   ├── PizzaTradicional.java
    │   ├── PizzaPremium.java
    │   ├── PizzaPersonalizada.java
    │   ├── Ingrediente.java
    │   ├── Pedido.java
    │   └── Tamaño.java
    ├── interfaces/
    │   ├── Calculable.java
    │   └── Customizable.java
    └── vista/
        ├── VentanaPrincipal.java
        └── PanelPedido.java
```

## Tecnologías Utilizadas

- **Lenguaje:** Java 8+
- **GUI Framework:** Swing (javax.swing)
- **IDE:** Apache NetBeans
- **Build Tool:** Ant (incluido en NetBeans)

## Próximos Pasos

1. Revisar este documento de arquitectura
2. Pasar a `02-interfaz-grafica.md` para diseñar la GUI
3. Implementar el backend según `03-backend.md`
4. Integrar frontend y backend
5. Probar la aplicación completa

## Criterios de Evaluación

Este proyecto demuestra:
- [ ] Correcta aplicación de herencia (Pizza y sus hijos)
- [ ] Uso de polimorfismo (calcularPrecio())
- [ ] Implementación de interfaces (Calculable, Customizable)
- [ ] Abstracción (clase abstracta Pizza)
- [ ] Encapsulación (atributos privados)
- [ ] Composición (Pedido contiene Pizzas)
- [ ] Uso de Enums (Tamaño)
- [ ] GUI funcional con Swing
- [ ] Separación de responsabilidades (MVC)
- [ ] Código limpio y bien documentado

## Referencias

- Documentación oficial de Java Swing: https://docs.oracle.com/javase/tutorial/uiswing/
- Principios SOLID
- Patrones de Diseño GOF (Gang of Four)
- Material del curso DSY1102 - Semana 12

# Sistema de Pizzería - Tutorial Progresivo POO

## Descripción General

Este tutorial te guía paso a paso en la construcción de un **Sistema de Gestión de Pizzería** completo, aplicando todos los conceptos de Programación Orientada a Objetos de forma progresiva. Construirás una aplicación funcional desde cero, agregando nuevas características en cada parte.

El sistema permite:
- Gestionar un menú de pizzas y bebidas
- Crear pedidos con múltiples productos
- Personalizar pizzas con ingredientes adicionales
- Aplicar descuentos y promociones
- Calcular totales con lógica de negocio compleja
- Mantener historial de pedidos

## Contexto del Negocio

**"Pizzería Bella Napoli"** es una pizzería que necesita modernizar su sistema de pedidos. Actualmente toman pedidos en papel y calculan precios manualmente, lo que genera errores y pérdida de tiempo. Necesitan un sistema por consola que les permita:

1. Mostrar la carta de productos disponibles
2. Armar pedidos con múltiples productos
3. Personalizar pizzas con ingredientes extra
4. Aplicar descuentos automáticos
5. Calcular el total correctamente
6. Guardar historial de pedidos

## Estructura del Tutorial

Este tutorial está dividido en **5 partes progresivas**. Cada parte construye sobre la anterior, agregando nuevos conceptos y funcionalidades:

| Parte | Título | Conceptos POO | Ponderación | Archivo |
|-------|--------|---------------|-------------|---------|
| **Parte 1** | Sistema de Menú Base | Ciclos (while, for, for-each) | **15%** | [Parte1_SistemaMenuBase.md](Parte1_SistemaMenuBase.md) |
| **Parte 2** | Agregando Encapsulación | Clases, atributos privados, getters/setters | **15%** | [Parte2_Encapsulacion.md](Parte2_Encapsulacion.md) |
| **Parte 3** | Trabajando con Colecciones | ArrayList, CRUD, manejo dinámico | **30%** | [Parte3_Colecciones.md](Parte3_Colecciones.md) |
| **Parte 4** | Aplicando Herencia | extends, super(), @Override, instanceof | **20%** | [Parte4_Herencia.md](Parte4_Herencia.md) |
| **Parte 5** | Polimorfismo Avanzado | abstract, interface, implements | **20%** | [Parte5_Polimorfismo.md](Parte5_Polimorfismo.md) |

## Cómo Usar Este Tutorial

### Opción 1: Construir Paso a Paso (Recomendado)

1. **Lee la Parte 1** y crea el sistema de menú base
2. **Prueba el código** y asegúrate de que funciona
3. **Pasa a la Parte 2** y agrega la clase Ingrediente
4. **Continúa con las partes 3, 4 y 5** en orden
5. Al final tendrás una aplicación completa funcionando

### Opción 2: Revisar Código Completo

Si prefieres ver el código completo de cada etapa:
- Cada archivo `.md` contiene el código completo funcional al final
- Puedes copiar directamente el código de la última parte para tener el sistema completo
- Asegúrate de leer los comentarios para entender cada sección

## Progresión de la Aplicación

### Parte 1: Sistema de Menú Base
- Menú principal interactivo con `while`
- Mostrar pizzas y bebidas con `for`
- Buscar productos por nombre
- Arrays simples para datos

**Al completar**: Tendrás un menú funcional que muestra productos y permite búsquedas.

### Parte 2: Agregando Encapsulación
- Clase `Ingrediente` con atributos privados
- Validación de datos en constructor
- Getters y setters con validación
- Métodos de negocio (aumentar/reducir stock)

**Al completar**: Tendrás un sistema más robusto con datos protegidos y validados.

### Parte 3: Trabajando con Colecciones
- Clase `Pedido` con ArrayList
- Gestión dinámica de productos
- Operaciones CRUD completas
- Historial de pedidos

**Al completar**: Podrás crear y gestionar múltiples pedidos sin límite fijo.

### Parte 4: Aplicando Herencia
- Clase base `Producto`
- Clases hijas `Pizza` y `Bebida`
- Reutilización de código con `super()`
- Especialización con `@Override`

**Al completar**: Tendrás una jerarquía organizada de productos con comportamientos especializados.

### Parte 5: Polimorfismo Avanzado
- Clase abstracta `Producto`
- Interfaces `Personalizable` y `Promocionable`
- Polimorfismo completo
- Sistema profesional completo

**Al completar**: Tendrás un sistema POO completo con todas las características profesionales.

## Conceptos POO Cubiertos

| Concepto | Dónde se Aplica | Parte |
|----------|-----------------|-------|
| **Ciclos while** | Menú principal que se repite | Parte 1 |
| **Ciclos for** | Recorrer arrays de productos | Parte 1 |
| **Clases y Objetos** | Ingrediente, Pedido, Producto | Partes 2-5 |
| **Encapsulación** | Atributos privados con validación | Parte 2 |
| **ArrayList** | Listas dinámicas de productos y pedidos | Parte 3 |
| **Herencia** | Producto → Pizza/Bebida | Parte 4 |
| **Polimorfismo** | Diferentes implementaciones de métodos | Partes 4-5 |
| **Clases Abstractas** | Producto como clase base | Parte 5 |
| **Interfaces** | Personalizable, Promocionable | Parte 5 |

## Estructura Final del Código

Al completar las 5 partes, tendrás estas clases:

```
sistemapizzeria/
├── SistemaPizzeria.java (Clase principal con main)
├── Producto.java (Clase abstracta base)
├── Pizza.java (Hereda de Producto, implementa interfaces)
├── Bebida.java (Hereda de Producto, implementa interfaces)
├── Ingrediente.java (Clase simple con encapsulación)
├── Pedido.java (Clase con ArrayList)
├── Personalizable.java (Interfaz)
└── Promocionable.java (Interfaz)
```

## Requisitos Técnicos

### Software Necesario
- **NetBeans IDE** (versión 12 o superior)
- **JDK** (Java Development Kit 11 o superior)
- Sistema operativo: Windows, macOS o Linux

### Conocimientos Previos
- Sintaxis básica de Java
- Variables y tipos de datos
- Estructuras de control (if, switch)
- Creación de clases simples

## Instrucciones de Ejecución en NetBeans

### Configuración Inicial (Solo Parte 1)

1. Abre NetBeans
2. File → New Project → Java Application
3. Nombre del proyecto: `SistemaPizzeria`
4. Marca "Create Main Class"
5. Click en Finish

### Agregar Nuevas Clases (Partes 2-5)

1. Clic derecho en el paquete `sistemapizzeria`
2. New → Java Class
3. Escribe el nombre de la clase
4. Copia el código del tutorial
5. Run → Run Project para probar

### Crear Interfaces (Parte 5)

1. Clic derecho en el paquete `sistemapizzeria`
2. New → Java Interface (no Java Class)
3. Escribe el nombre de la interfaz
4. Copia el código del tutorial

## Características del Código

### Estilo de Comentarios

El código está comentado siguiendo estas reglas:
- **Comentarios SIEMPRE arriba** del código que explican
- **Nunca comentarios al lado** de las líneas
- **Lectura secuencial** de arriba hacia abajo
- **Explicaciones del POR QUÉ**, no solo del qué

Ejemplo:
```java
// Necesitamos crear un Scanner para leer la entrada del usuario.
// Esto nos permite capturar lo que el usuario escribe en la consola.
Scanner scanner = new Scanner(System.in);
```

### Estilo Visual Simple

- **Menús con barras diagonales**: `///`
- **Sin caracteres especiales complicados**
- **Sin emojis ni símbolos Unicode**
- **Formato simple y claro** para enfocarse en el código

## Ejemplo de Flujo Completo

### Parte 1: Menú Básico
```
////////////////////////////////////////
///   PIZZERIA BELLA NAPOLI         ///
////////////////////////////////////////
1. Ver Menu de Pizzas
2. Ver Menu de Bebidas
3. Buscar Pizza por Nombre
4. Salir
////////////////////////////////////////
```

### Parte 5: Sistema Completo
```
////////////////////////////////////////
///   PIZZERIA BELLA NAPOLI         ///
////////////////////////////////////////
1. Ver Todos los Productos
2. Ver Detalle de Producto
3. Crear Nueva Pizza
4. Crear Nueva Bebida
5. Personalizar Producto
6. Aplicar Promocion a Producto
7. Ver Productos con Promocion
8. Salir
////////////////////////////////////////
```

## Evaluación de Conceptos

### IL 2.1 - Ciclos (15%)
- Ciclo `while` para menú principal
- Ciclo `for` para recorrer arrays
- Ciclo `for-each` para colecciones
- Control de flujo con `break`

### IL 2.2 - Encapsulación (15%)
- Atributos `private`
- Getters y setters con validación
- Métodos helper privados
- Validación en constructores

### IL 2.3 - Colecciones (30%)
- `ArrayList` para gestión dinámica
- Métodos: add, remove, get, size
- Operaciones CRUD completas
- Iteración con diferentes estilos de ciclos

### IL 2.4 - Herencia (20%)
- Clase base `Producto`
- Subclases `Pizza` y `Bebida`
- Uso de `super()` y `extends`
- Sobrescritura con `@Override`

### IL 2.5 - Polimorfismo (20%)
- Clase abstracta con métodos abstractos
- Interfaces para comportamientos
- Implementación múltiple con `implements`
- Polimorfismo en acción con ArrayList

## Consejos para el Estudiante

1. **No saltes partes**: Cada parte construye sobre la anterior
2. **Escribe el código tú mismo**: No solo copies y pegues
3. **Lee los comentarios**: Explican el POR QUÉ de cada decisión
4. **Prueba el código**: Ejecuta después de cada parte
5. **Experimenta**: Agrega tus propias pizzas, bebidas y funcionalidades
6. **Pregunta**: Si algo no tiene sentido, revisa los comentarios o pregunta

## Solución de Problemas Comunes

### Error: "class expected"
- Verifica que hayas creado la clase (no interfaz) cuando corresponde
- Revisa que el nombre del archivo coincida con el nombre de la clase

### Error: "cannot find symbol"
- Asegúrate de haber creado todas las clases necesarias hasta esa parte
- Verifica que los nombres estén escritos correctamente

### El programa no compila
- Lee el mensaje de error completo
- Verifica que hayas copiado todo el código
- Revisa que las llaves `{}` estén balanceadas

### El menú no se repite
- Verifica que la variable `sistemaActivo` se mantenga en `true`
- Asegúrate de que el ciclo `while` esté correctamente cerrado

## Extensiones Posibles

Una vez completado el tutorial, puedes:
1. **Agregar más tipos de productos**: Postres, entradas, etc.
2. **Sistema de clientes**: Con puntos de fidelidad
3. **Guardar en archivos**: Persistencia de datos
4. **Interfaz gráfica**: Migrar de consola a GUI
5. **Base de datos**: Usar MySQL o SQLite

## Recursos Adicionales

- [Documentación oficial de Java](https://docs.oracle.com/javase/)
- [Tutorial de NetBeans](https://netbeans.apache.org/kb/)
- Material de las Semanas 5, 6 y 7 del curso

---

**Autor**: Material educativo POO - Duoc UC
**Versión**: 2.0 (Tutorial Progresivo)
**Fecha**: 2025
**Curso**: Programación Orientada a Objetos

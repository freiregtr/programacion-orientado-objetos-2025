# Guia 01: Interfaz Grafica con Java Swing

## Objetivo
Construir la interfaz grafica del sistema de pizzeria usando Java Swing, aplicando los conceptos de contenedores y componentes.

## Anterior: 00-problema.md
En el documento anterior vimos la problematica del sistema de pizzeria y los requerimientos.

---

## PASO 1: Crear el Proyecto en NetBeans

### 1.1 Nuevo Proyecto

primero que nada, vamos a crear el proyecto en NetBeans, para ello:

1. Abrir NetBeans
2. File > New Project
3. Seleccionar Categories: Java with Ant
4. Seleccionar Projects: Java Application
5. Click en Next

### 1.2 Configurar el Proyecto

en la siguiente ventana, configuramos el nombre del proyecto:

1. Project Name: `PizzeriaSistema`
2. Project Location: donde quieras guardar el proyecto
3. **Importante:** Desmarcar "Create Main Class" porque vamos a crear un JFrame
4. Click en Finish

de esta forma, NetBeans nos crea la estructura basica del proyecto

---

## PASO 2: Crear los Paquetes

### 2.1 Por que usar paquetes?

los paquetes nos permiten organizar nuestro codigo en carpetas logicas, esto es parte del patron MVC que vamos a implementar, donde separamos:
- **modelo** - las clases que representan los datos (Pizza)
- **vista** - las interfaces graficas (JFrame, JDialog)
- **controlador** - la logica de negocio y acceso a datos
- **conexion** - la clase para conectar con la base de datos

### 2.2 Crear los paquetes

1. Click derecho en Source Packages
2. New > Java Package
3. Crear los siguientes paquetes uno por uno:

```
pizzeria.modelo
pizzeria.vista
pizzeria.controlador
pizzeria.conexion
```

una vez creados, veras la estructura en el panel izquierdo de NetBeans

---

## PASO 3: Crear el JFrame Principal

### 3.1 Que es un JFrame?

un JFrame es la ventana principal de nuestra aplicacion, es el contenedor mas grande donde vamos a colocar todos los demas componentes

### 3.2 Crear el JFrame

1. Click derecho en `pizzeria.vista`
2. New > JFrame Form
3. Class Name: `VentanaPrincipal`
4. Click en Finish

NetBeans nos abre el editor visual donde podemos disenar la interfaz arrastrando componentes

### 3.3 Configurar propiedades del JFrame

1. Seleccionar el JFrame (click en el borde de la ventana)
2. En el panel Properties (derecha), configurar:
   - **Title:** `Gestion - Pizza`
   - **defaultCloseOperation:** `EXIT_ON_CLOSE`

el Title es lo que aparece en la barra de titulo de la ventana, y defaultCloseOperation en EXIT_ON_CLOSE hace que al cerrar la ventana se termine la aplicacion

### 3.4 Configurar tamano del JFrame

1. Click derecho en el JFrame
2. Set Size: ancho 800, alto 500 (aproximado)

o puedes arrastrar los bordes para ajustar el tamano

---

## PASO 4: Crear las Islas (Paneles Principales)

antes de agregar los campos y botones, primero vamos a crear la estructura general con paneles, esto nos ayuda a organizar mejor la interfaz

### 4.1 Que son las islas?

las islas son los paneles principales que dividen nuestra interfaz en secciones, en nuestro caso tendremos:
- Panel izquierdo: formularios (insertar, actualizar, eliminar)
- Panel derecho: tabla de registros

### 4.2 Agregar Panel Izquierdo

1. En la Palette (derecha), buscar JPanel en Swing Containers
2. Arrastrar un JPanel al lado izquierdo del JFrame
3. Ajustar el tamano para que ocupe aproximadamente 1/3 del ancho
4. Cambiar nombre de variable a: `pnlIzquierdo`

este panel va a contener los 3 formularios

### 4.3 Agregar Panel Derecho

1. Arrastrar otro JPanel al lado derecho
2. Ajustar para que ocupe los 2/3 restantes
3. Cambiar nombre de variable a: `pnlDerecho`

este panel va a contener la tabla de registros

ahora tenemos las dos islas principales de nuestra interfaz

---

## PASO 5: Crear los Sub-Paneles del Lado Izquierdo

dentro del panel izquierdo, vamos a crear 3 paneles mas pequenos, uno para cada operacion

### 5.1 Panel Insertar

1. Arrastrar un JPanel dentro del panel izquierdo (arriba)
2. Seleccionar el panel
3. Click derecho > Properties
4. Buscar la propiedad **border**
5. Click en los "..." para abrir el editor de bordes
6. Seleccionar TitledBorder
7. En Title escribir: `Insertar nuevo (ID autoincremental)`
8. Click en OK
9. Cambiar nombre de variable a: `pnlInsertar`

ahora el panel tiene un titulo que indica su funcion

### 5.2 Panel Actualizar

1. Arrastrar otro JPanel debajo del anterior
2. Agregar TitledBorder con titulo: `Actualizar`
3. Cambiar nombre de variable a: `pnlActualizar`

### 5.3 Panel Eliminar

1. Arrastrar otro JPanel debajo del anterior
2. Agregar TitledBorder con titulo: `Eliminar`
3. Cambiar nombre de variable a: `pnlEliminar`

ahora tenemos los 3 sub-paneles organizados verticalmente en el lado izquierdo

---

## PASO 6: Crear el Panel de Registros (Lado Derecho)

### 6.1 Configurar el panel derecho

1. Seleccionar el panel derecho
2. Agregar TitledBorder con titulo: `Registros`
3. Cambiar nombre de variable a: `pnlRegistros`

### 6.2 Vista previa de la estructura

en este punto, tu interfaz deberia verse asi:

```
+--------------------------------------------------+
|           Gestion - Pizza                        |
+--------------------------------------------------+
| +------------------+  +------------------------+ |
| | Insertar nuevo   |  | Registros              | |
| | (ID autoincrem.) |  |                        | |
| |                  |  |                        | |
| +------------------+  |                        | |
| +------------------+  |                        | |
| | Actualizar       |  |                        | |
| |                  |  |                        | |
| +------------------+  |                        | |
| +------------------+  |                        | |
| | Eliminar         |  |                        | |
| |                  |  |                        | |
| +------------------+  +------------------------+ |
+--------------------------------------------------+
```

ya tenemos la estructura de islas lista, ahora vamos a agregar los componentes dentro de cada una

---

## PASO 7: Componentes del Panel Insertar

ahora vamos a agregar los campos y botones dentro del panel Insertar

### 7.1 Agregar Labels y TextFields

dentro del panel "Insertar nuevo", agregar:

1. **JLabel** con texto: `Nombre:` - cambiar nombre de variable a `lblNombre`
2. **JTextField** al lado - cambiar nombre de variable a `txtNombre`

3. **JLabel** con texto: `Precio:` - cambiar nombre de variable a `lblPrecio`
4. **JTextField** al lado - cambiar nombre de variable a `txtPrecio`

5. **JLabel** con texto: `Tamanio:` - cambiar nombre de variable a `lblTamanio`
6. **JTextField** al lado - cambiar nombre de variable a `txtTamanio`

para cambiar el nombre de la variable:
1. Click derecho en el componente
2. Change Variable Name
3. Escribir el nuevo nombre

### 7.2 Agregar Boton Insertar

1. Arrastrar un **JButton** debajo de los campos
2. Cambiar el texto a: `Insertar`
3. Cambiar nombre de variable a: `btnInsertar`

### 7.3 Vista previa del panel Insertar

```
+------------------------+
| Insertar nuevo (ID...) |
| Nombre:  [__________]  |
| Precio:  [__________]  |
| Tamanio: [__________]  |
|         [Insertar]     |
+------------------------+
```

---

## PASO 8: Componentes del Panel Actualizar

### 8.1 Agregar campos

dentro del panel "Actualizar", agregar:

1. **JLabel** con texto: `ID a actualizar:` - variable: `lblIdActualizar`
2. **JTextField** al lado - variable: `txtIdActualizar`

### 8.2 Agregar botones

1. **JButton** con texto: `Cargar datos` - variable: `btnCargarDatos`
2. **JButton** con texto: `Actualizar registro` - variable: `btnActualizar`

el boton "Cargar datos" sirve para traer los datos de una pizza por su ID y mostrarlos en los campos del panel Insertar, asi el usuario puede modificarlos y luego presionar "Actualizar registro"

### 8.3 Vista previa del panel Actualizar

```
+---------------------------+
| Actualizar                |
| ID a actualizar: [______] |
| [Cargar datos] [Actualizar registro] |
+---------------------------+
```

---

## PASO 9: Componentes del Panel Eliminar

### 9.1 Agregar campos

dentro del panel "Eliminar", agregar:

1. **JLabel** con texto: `ID a eliminar:` - variable: `lblIdEliminar`
2. **JTextField** al lado - variable: `txtIdEliminar`

### 9.2 Agregar boton

1. **JButton** con texto: `Eliminar` - variable: `btnEliminar`

### 9.3 Vista previa del panel Eliminar

```
+------------------------+
| Eliminar               |
| ID a eliminar: [_____] |
|         [Eliminar]     |
+------------------------+
```

---

## PASO 10: Componentes del Panel Registros

### 10.1 Agregar botones superiores

en la parte superior del panel "Registros", agregar:

1. **JButton** con texto: `Refrescar tabla` - variable: `btnRefrescar`
2. **JButton** con texto: `Listar todo` - variable: `btnListarTodo`

### 10.2 Agregar la tabla

1. En la Palette, buscar **JTable** en Swing Controls
2. Arrastrar al centro del panel Registros
3. NetBeans automaticamente la envuelve en un JScrollPane (para tener scroll)
4. Cambiar nombre de variable a: `tablaPizzas`

### 10.3 Configurar columnas de la tabla

1. Seleccionar la JTable
2. Click derecho > Table Contents
3. En la pestana Columns, veras columnas por defecto
4. Modificar para que queden:
   - Title: `ID`
   - Title: `Nombre`
   - Title: `Precio`
   - Title: `Tamanio`
5. Click en Close

### 10.4 Vista previa del panel Registros

```
+--------------------------------+
| Registros                      |
| [Refrescar tabla] [Listar todo]|
| +----------------------------+ |
| | ID | Nombre | Precio | Tam | |
| |----|--------|--------|-----| |
| | 1  | Pepperoni | 8500 | M  | |
| | 2  | Hawaiana | 9000 | F   | |
| +----------------------------+ |
+--------------------------------+
```

---

## PASO 11: Resumen de Variables

asegurate de que todos los componentes tengan los nombres correctos:

| Componente | Variable | Ubicacion |
|------------|----------|-----------|
| Panel | pnlIzquierdo | JFrame (izquierda) |
| Panel | pnlDerecho | JFrame (derecha) |
| Panel | pnlInsertar | Panel Izquierdo |
| Panel | pnlActualizar | Panel Izquierdo |
| Panel | pnlEliminar | Panel Izquierdo |
| Panel | pnlRegistros | Panel Derecho |
| Label | lblNombre | Panel Insertar |
| TextField | txtNombre | Panel Insertar |
| Label | lblPrecio | Panel Insertar |
| TextField | txtPrecio | Panel Insertar |
| Label | lblTamanio | Panel Insertar |
| TextField | txtTamanio | Panel Insertar |
| Button | btnInsertar | Panel Insertar |
| Label | lblIdActualizar | Panel Actualizar |
| TextField | txtIdActualizar | Panel Actualizar |
| Button | btnCargarDatos | Panel Actualizar |
| Button | btnActualizar | Panel Actualizar |
| Label | lblIdEliminar | Panel Eliminar |
| TextField | txtIdEliminar | Panel Eliminar |
| Button | btnEliminar | Panel Eliminar |
| Button | btnRefrescar | Panel Registros |
| Button | btnListarTodo | Panel Registros |
| Table | tablaPizzas | Panel Registros |

---

## PASO 12: Vista Previa Final

1. Click derecho en el JFrame
2. Preview Design (o presionar Ctrl+Shift+P)

la interfaz completa deberia verse asi:

```
+--------------------------------------------------+
|           Gestion - Pizza                        |
+--------------------------------------------------+
| +------------------+  +------------------------+ |
| | Insertar nuevo   |  | [Refrescar] [Listar]   | |
| | Nombre: [____]   |  | +--------------------+ | |
| | Precio: [____]   |  | | ID|Nombre|Precio|T | | |
| | Tamanio:[____]   |  | | 1 |Pepperoni|8500|M| | |
| | [Insertar]       |  | | 2 |Hawaiana|9000|F | | |
| +------------------+  | +--------------------+ | |
| +------------------+  +------------------------+ |
| | Actualizar       |                            |
| | ID: [____]       |                            |
| | [Cargar][Actual] |                            |
| +------------------+                            |
| +------------------+                            |
| | Eliminar         |                            |
| | ID: [____]       |                            |
| | [Eliminar]       |                            |
| +------------------+                            |
+--------------------------------------------------+
```

---

## Resumen

en esta guia aprendimos a:
- crear un proyecto en NetBeans
- organizar el codigo en paquetes (MVC)
- crear un JFrame principal
- usar JPanel para crear islas/secciones
- agregar TitledBorder para identificar cada seccion
- agregar componentes: JLabel, JTextField, JButton, JTable
- nombrar correctamente las variables

los eventos de los botones los conectaremos con el controlador en la guia 05

---

## Siguiente: 02-guia-modelos.md

# Evaluacion Practica - Pizzeria "La Buona Pizza"

## Objetivo

Desarrollar una aplicacion Java Swing con integracion a un motor de base de datos que permita realizar operaciones CRUD para el correcto funcionamiento del sistema.

## Caso a resolver

La pizzeria "La Buona Pizza" requiere el desarrollo de un sistema basico para la administracion de su menu de pizzas. Cada nueva pizza que ingresa debe ser registrada en una base de datos. Para ello, se solicita construir una aplicacion en Java capaz de insertar, actualizar, eliminar y visualizar la informacion almacenada en una base de datos relacional.

Cada registro posee un ID autoincremental, por lo que dicho valor no debe ser ingresado manualmente por el usuario.

## Entidad a gestionar

**Pizza:** cada pizza del menu cuenta con un registro en la tabla "pizza". Cada registro debe almacenar:
- **id** - identificador (autoincremental)
- **nombre** - nombre de la pizza (ej: "Pepperoni", "Hawaiana", "Margherita")
- **precio** - precio en moneda local
- **tamanio** - tamanio de la pizza (ej: "Personal", "Mediana", "Familiar")

## Requerimientos funcionales

El sistema debe permitir:
1. **Insertar** - agregar nuevas pizzas al menu
2. **Actualizar** - modificar datos de una pizza existente
3. **Eliminar** - quitar una pizza del menu
4. **Listar** - mostrar todas las pizzas registradas
5. **Buscar** - cargar datos de una pizza por su ID

## Requerimientos tecnicos

- Programar en Java utilizando NetBeans
- Interfaz grafica con Java Swing
- Base de datos MySQL
- Patron de arquitectura MVC (Modelo-Vista-Controlador)
- Separacion en paquetes segun funcion

## Estructura de paquetes sugerida

```
PizzeriaSistema/
└── src/
    └── pizzeria/
        ├── modelo/
        │   └── Pizza.java
        ├── vista/
        │   └── VentanaPrincipal.java
        ├── controlador/
        │   └── PizzaController.java
        └── conexion/
            └── Conexion.java
```

## Propuesta de interfaz grafica

La interfaz debe contemplar:

### Seccion Insertar
- Campo: Nombre
- Campo: Precio
- Campo: Tamanio
- Boton: Insertar

### Seccion Actualizar
- Campo: ID a actualizar
- Boton: Cargar datos
- Boton: Actualizar registro

### Seccion Eliminar
- Campo: ID a eliminar
- Boton: Eliminar

### Seccion Listado
- Tabla con columnas: ID, Nombre, Precio, Tamanio
- Boton: Refrescar tabla
- Boton: Listar todo

## Guias de desarrollo

1. [01-guia-gui.md](01-guia-gui.md) - Construccion de la interfaz grafica
2. [02-guia-modelos.md](02-guia-modelos.md) - Creacion de la clase Pizza
3. [03-guia-controladores.md](03-guia-controladores.md) - Logica del controlador y CRUD
4. [04-guia-bbdd.md](04-guia-bbdd.md) - Configuracion de MySQL y conexion

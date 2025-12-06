# Guia 05: Conectar Eventos con el Controlador

## Objetivo
Conectar los botones de la interfaz grafica con los metodos del controlador para que el sistema funcione correctamente.

## Anterior: 04-guia-bbdd.md
En el documento anterior configuramos la base de datos MySQL y la clase de conexion.

---

## PASO 1: Agregar Imports en VentanaPrincipal

### 1.1 Abrir el codigo fuente

1. En NetBeans, abrir `VentanaPrincipal.java`
2. Click en la pestana **Source** (arriba del editor)

veras el codigo Java de tu JFrame

### 1.2 Agregar los imports necesarios

al inicio del archivo, despues de `package pizzeria.vista;`, agregar:

```java
import pizzeria.controlador.PizzaController;
import pizzeria.modelo.Pizza;
import javax.swing.JOptionPane;
import javax.swing.table.DefaultTableModel;
import java.util.ArrayList;
```

---

## PASO 2: Declarar Variables de Instancia

### 2.1 Declarar el controlador y el modelo de tabla

dentro de la clase `VentanaPrincipal`, antes del constructor, agregar:

```java
public class VentanaPrincipal extends javax.swing.JFrame {

    private PizzaController controller;
    private DefaultTableModel modeloTabla;

    public VentanaPrincipal() {
        initComponents();
    }
```

---

## PASO 3: Inicializar en el Constructor

### 3.1 Modificar el constructor

modificar el constructor para inicializar el controlador y configurar la tabla:

```java
public VentanaPrincipal() {
    initComponents();

    controller = new PizzaController();

    modeloTabla = new DefaultTableModel();
    modeloTabla.addColumn("ID");
    modeloTabla.addColumn("Nombre");
    modeloTabla.addColumn("Precio");
    modeloTabla.addColumn("Tamanio");
    tablaPizzas.setModel(modeloTabla);

    cargarTabla();
}
```

### 3.2 Crear metodo auxiliar cargarTabla

despues del constructor, agregar este metodo:

```java
private void cargarTabla() {
    modeloTabla.setRowCount(0);
    ArrayList<Pizza> pizzas = controller.listarTodos();
    for (Pizza pizza : pizzas) {
        Object[] fila = {
            pizza.getId(),
            pizza.getNombre(),
            pizza.getPrecio(),
            pizza.getTamanio()
        };
        modeloTabla.addRow(fila);
    }
}
```

### 3.3 Crear metodo auxiliar limpiarCampos

agregar otro metodo auxiliar:

```java
private void limpiarCampos() {
    txtNombre.setText("");
    txtPrecio.setText("");
    txtTamanio.setText("");
    txtIdActualizar.setText("");
    txtIdEliminar.setText("");
}
```

---

## PASO 4: Evento del Boton Insertar

### 4.1 Crear el evento en NetBeans

1. Volver a la vista **Design**
2. Hacer **doble clic** en el boton `btnInsertar`
3. NetBeans crea el metodo del evento

### 4.2 Agregar el codigo

```java
private void btnInsertarActionPerformed(java.awt.event.ActionEvent evt) {
    String nombre = txtNombre.getText();
    double precio = Double.parseDouble(txtPrecio.getText());
    String tamanio = txtTamanio.getText();

    Pizza pizza = new Pizza();
    pizza.setNombre(nombre);
    pizza.setPrecio(precio);
    pizza.setTamanio(tamanio);

    if (controller.insertar(pizza)) {
        JOptionPane.showMessageDialog(this, "Pizza insertada correctamente");
        limpiarCampos();
        cargarTabla();
    } else {
        JOptionPane.showMessageDialog(this, "Error al insertar");
    }
}
```

---

## PASO 5: Evento del Boton Cargar Datos

### 5.1 Crear el evento

1. Volver a **Design**
2. Hacer **doble clic** en el boton `btnCargarDatos`

### 5.2 Agregar el codigo

```java
private void btnCargarDatosActionPerformed(java.awt.event.ActionEvent evt) {
    int id = Integer.parseInt(txtIdActualizar.getText());
    Pizza pizza = controller.buscarPorId(id);

    if (pizza != null) {
        txtNombre.setText(pizza.getNombre());
        txtPrecio.setText(String.valueOf(pizza.getPrecio()));
        txtTamanio.setText(pizza.getTamanio());
    } else {
        JOptionPane.showMessageDialog(this, "Pizza no encontrada");
    }
}
```

---

## PASO 6: Evento del Boton Actualizar

### 6.1 Crear el evento

1. Volver a **Design**
2. Hacer **doble clic** en el boton `btnActualizar`

### 6.2 Agregar el codigo

```java
private void btnActualizarActionPerformed(java.awt.event.ActionEvent evt) {
    int id = Integer.parseInt(txtIdActualizar.getText());
    String nombre = txtNombre.getText();
    double precio = Double.parseDouble(txtPrecio.getText());
    String tamanio = txtTamanio.getText();

    Pizza pizza = new Pizza(id, nombre, precio, tamanio);

    if (controller.actualizar(pizza)) {
        JOptionPane.showMessageDialog(this, "Pizza actualizada correctamente");
        limpiarCampos();
        cargarTabla();
    } else {
        JOptionPane.showMessageDialog(this, "Error al actualizar");
    }
}
```

---

## PASO 7: Evento del Boton Eliminar

### 7.1 Crear el evento

1. Volver a **Design**
2. Hacer **doble clic** en el boton `btnEliminar`

### 7.2 Agregar el codigo

```java
private void btnEliminarActionPerformed(java.awt.event.ActionEvent evt) {
    int id = Integer.parseInt(txtIdEliminar.getText());

    if (controller.eliminar(id)) {
        JOptionPane.showMessageDialog(this, "Pizza eliminada correctamente");
        limpiarCampos();
        cargarTabla();
    } else {
        JOptionPane.showMessageDialog(this, "Error al eliminar");
    }
}
```

---

## PASO 8: Evento del Boton Refrescar

### 8.1 Crear el evento

1. Volver a **Design**
2. Hacer **doble clic** en el boton `btnRefrescar`

### 8.2 Agregar el codigo

```java
private void btnRefrescarActionPerformed(java.awt.event.ActionEvent evt) {
    cargarTabla();
}
```

---

## PASO 9: Evento del Boton Listar Todo

### 9.1 Crear el evento

1. Volver a **Design**
2. Hacer **doble clic** en el boton `btnListarTodo`

### 9.2 Agregar el codigo

```java
private void btnListarTodoActionPerformed(java.awt.event.ActionEvent evt) {
    cargarTabla();
}
```

---

## PASO 10: Crear el Metodo Main

al final de la clase, agregar:

```java
public static void main(String args[]) {
    java.awt.EventQueue.invokeLater(new Runnable() {
        public void run() {
            new VentanaPrincipal().setVisible(true);
        }
    });
}
```

---

## Resumen

en esta guia aprendimos a:
- agregar imports necesarios
- declarar e inicializar el controlador en la vista
- configurar el DefaultTableModel para la JTable
- crear eventos usando doble clic en NetBeans
- conectar cada boton con su operacion CRUD
- refrescar la tabla despues de cada operacion

---

## Prueba Final

1. Click derecho en `VentanaPrincipal.java`
2. Run File
3. Probar cada operacion:
   - Insertar una pizza nueva
   - Buscar una pizza por ID
   - Actualizar los datos
   - Eliminar una pizza
   - Refrescar la tabla

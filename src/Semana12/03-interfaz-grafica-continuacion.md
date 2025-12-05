# Sistema de Pedidos de Pizza - Interfaz Gráfica (Parte 2)

**Documento anterior:** [02-interfaz-grafica.md](02-interfaz-grafica.md)

Este documento continúa la implementación de la interfaz gráfica con los Módulos 3, 4 y 5.

---

## MÓDULO 3: Módulo de Ingredientes Personalizables

### Objetivo
Agregar panel de ingredientes con checkboxes que aparece solo cuando se selecciona "Pizza Personalizada".

### Paso 3.1: Crear Panel de Ingredientes

1. Arrastrar un **JPanel** dentro de `panelSeleccionPizza`
2. Configurar:
   ```
   Variable Name: panelIngredientes
   border: LineBorder o TitledBorder "Ingredientes Extras"
   background: Color claro
   ```
3. Posición: `x: 20, y: 250`
4. Tamaño: `width: 350, height: 160`

[SCREENSHOT: Panel de ingredientes agregado]

### Paso 3.2: Agregar CheckBoxes para Ingredientes

Crearemos 6 checkboxes en 2 columnas:

**Columna 1:**

**Checkbox 1: Jamón**
```
Variable Name: chkJamon
text: "Jamón (+$1.000)"
```
Posición: `x: 10, y: 10`

**Checkbox 2: Champiñones**
```
Variable Name: chkChampinones
text: "Champiñones (+$800)"
```
Posición: `x: 10, y: 40`

**Checkbox 3: Aceitunas**
```
Variable Name: chkAceitunas
text: "Aceitunas (+$600)"
```
Posición: `x: 10, y: 70`

**Columna 2:**

**Checkbox 4: Pepperoni**
```
Variable Name: chkPepperoni
text: "Pepperoni (+$1.200)"
```
Posición: `x: 180, y: 10`

**Checkbox 5: Piña**
```
Variable Name: chkPina
text: "Piña (+$700)"
```
Posición: `x: 180, y: 40`

**Checkbox 6: Cebolla**
```
Variable Name: chkCebolla
text: "Cebolla (+$500)"
```
Posición: `x: 180, y: 70`

[SCREENSHOT: Panel con los 6 checkboxes organizados]

### Paso 3.3: Configurar Visibilidad del Panel

Por defecto, el panel de ingredientes debe estar visible solo para pizza personalizada.

1. En el constructor de la clase (después de `initComponents()`), agregar:

```java
public VentanaPrincipal() {
    initComponents();

    // Configurar visibilidad inicial del panel de ingredientes
    actualizarVisibilidadIngredientes();
}
```

2. Crear método para controlar visibilidad:

```java
private void actualizarVisibilidadIngredientes() {
    // Mostrar ingredientes solo si Personalizada está seleccionada
    boolean esPersonalizada = optPersonalizada.isSelected();
    panelIngredientes.setVisible(esPersonalizada);
}
```

3. Actualizar los event handlers de los radio buttons:

```java
private void optTradicionalActionPerformed(java.awt.event.ActionEvent evt) {
    System.out.println("Seleccionado: Tradicional");
    actualizarVisibilidadIngredientes();
}

private void optPremiumActionPerformed(java.awt.event.ActionEvent evt) {
    System.out.println("Seleccionado: Premium");
    actualizarVisibilidadIngredientes();
}

private void optPersonalizadaActionPerformed(java.awt.event.ActionEvent evt) {
    System.out.println("Seleccionado: Personalizada");
    actualizarVisibilidadIngredientes();
}
```

[SCREENSHOT: Código del método actualizarVisibilidadIngredientes]

### Paso 3.4: Configurar Eventos de CheckBoxes

Para cada checkbox, configurar evento:

1. Click derecho en `chkJamon`
2. **Events > Action > actionPerformed**
3. Agregar:

```java
private void chkJamonActionPerformed(java.awt.event.ActionEvent evt) {
    System.out.println("Jamón: " + chkJamon.isSelected());
}
```

Repetir para todos los checkboxes.

**Tip:** Puedes crear un método genérico:

```java
private void ingredienteSeleccionado(java.awt.event.ActionEvent evt) {
    JCheckBox checkbox = (JCheckBox) evt.getSource();
    System.out.println(checkbox.getText() + ": " + checkbox.isSelected());
}
```

Y asignar este mismo método a todos los checkboxes.

### Checklist Módulo 3

- [ ] Panel de ingredientes creado
- [ ] 6 checkboxes agregados y configurados
- [ ] Panel se oculta/muestra según tipo de pizza
- [ ] Event listeners configurados para checkboxes
- [ ] Método actualizarVisibilidadIngredientes() implementado

### Probar Módulo 3

1. **Run File**
2. Verificar que:
   - Al seleccionar "Tradicional" o "Premium", el panel de ingredientes desaparece
   - Al seleccionar "Personalizada", el panel aparece
   - Los checkboxes pueden marcarse/desmarcarse
   - Aparecen mensajes en consola al cambiar checkboxes

[SCREENSHOT: Ventana mostrando panel de ingredientes visible]

[SCREENSHOT: Ventana mostrando panel de ingredientes oculto]

---

## MÓDULO 4: Módulo de Carrito

### Objetivo
Crear el panel derecho para visualizar las pizzas agregadas al carrito y el total del pedido.

### Paso 4.1: Crear Panel Derecho

1. Arrastrar un **JPanel** al `panelPrincipal` (no dentro del panel izquierdo)
2. Configurar:
   ```
   Variable Name: panelCarrito
   border: TitledBorder "CARRITO DE COMPRAS"
   background: Color blanco
   ```
3. Posición: `x: 450, y: 20`
4. Tamaño: `width: 420, height: 500`

[SCREENSHOT: Panel derecho agregado al lado del izquierdo]

### Paso 4.2: Agregar Área de Texto para Lista de Pizzas

**JTextArea:**
1. Arrastrar **JTextArea** dentro de `panelCarrito`
2. Configurar:
   ```
   Variable Name: txaCarrito
   editable: false
   lineWrap: true
   wrapStyleWord: true
   font: Monospaced, 11pt
   ```
3. Posición: `x: 10, y: 30`
4. Tamaño: `width: 390, height: 350`

**JScrollPane (importante):**
1. Click derecho en `txaCarrito`
2. **Enclose in > Scroll Pane**

NetBeans automáticamente envuelve el JTextArea en un JScrollPane.

[SCREENSHOT: TextArea con scroll en el panel carrito]

### Paso 4.3: Agregar Panel de Información Total

Crearemos un sub-panel en la parte inferior del carrito para mostrar información del total.

1. Arrastrar **JPanel** dentro de `panelCarrito`
2. Configurar:
   ```
   Variable Name: panelTotal
   border: LineBorder superior
   ```
3. Posición: `x: 10, y: 400`
4. Tamaño: `width: 390, height: 80`

**Label de Cantidad:**
1. Arrastrar **JLabel** a `panelTotal`
2. Configurar:
   ```
   Variable Name: lblCantidad
   text: "Cantidad: 0 pizzas"
   font: 12pt
   ```
3. Posición: `x: 10, y: 10`

**Label de Total:**
1. Arrastrar **JLabel** a `panelTotal`
2. Configurar:
   ```
   Variable Name: lblTotal
   text: "TOTAL: $0"
   font: Bold, 16pt
   foreground: Color verde oscuro
   ```
3. Posición: `x: 10, y: 35`

[SCREENSHOT: Panel total con labels de cantidad y total]

### Paso 4.4: Agregar Botón Limpiar Carrito

1. Arrastrar **JButton** a `panelTotal`
2. Configurar:
   ```
   Variable Name: btnLimpiarCarrito
   text: "Limpiar Carrito"
   font: 11pt
   foreground: Color rojo
   ```
3. Posición: `x: 250, y: 25`
4. Tamaño: `width: 130, height: 30`

[SCREENSHOT: Botón limpiar agregado]

### Paso 4.5: Configurar Evento del Botón Limpiar

1. Click derecho en `btnLimpiarCarrito`
2. **Events > Action > actionPerformed**
3. Agregar:

```java
private void btnLimpiarCarritoActionPerformed(java.awt.event.ActionEvent evt) {
    // Limpiar el área de texto
    txaCarrito.setText("");

    // Resetear labels
    lblCantidad.setText("Cantidad: 0 pizzas");
    lblTotal.setText("TOTAL: $0");

    System.out.println("Carrito limpiado");
}
```

### Paso 4.6: Agregar Texto de Ejemplo al Carrito

Para probar visualmente, agregar texto de ejemplo en el constructor:

```java
public VentanaPrincipal() {
    initComponents();

    // Configurar visibilidad inicial del panel de ingredientes
    actualizarVisibilidadIngredientes();

    // Texto de ejemplo para el carrito (TEMPORAL - para visualizar)
    String ejemploCarrito = "1. Pizza Tradicional\n" +
                           "   Tamaño: Mediana\n" +
                           "   Precio: $12.000\n\n" +
                           "2. Pizza Personalizada\n" +
                           "   Tamaño: Familiar\n" +
                           "   Extras: Jamón, Aceitunas\n" +
                           "   Precio: $22.600\n\n";
    txaCarrito.setText(ejemploCarrito);

    lblCantidad.setText("Cantidad: 2 pizzas");
    lblTotal.setText("TOTAL: $34.600");
}
```

### Checklist Módulo 4

- [ ] Panel carrito creado en el lado derecho
- [ ] JTextArea agregada y configurada como no editable
- [ ] JScrollPane configurado correctamente
- [ ] Panel de total creado
- [ ] Labels de cantidad y total agregados
- [ ] Botón limpiar carrito agregado
- [ ] Evento de limpiar carrito implementado

### Probar Módulo 4

1. **Run File**
2. Verificar que:
   - El panel carrito aparece a la derecha
   - El texto de ejemplo se muestra correctamente
   - El scroll funciona si agregas más texto
   - El botón "Limpiar Carrito" limpia todo y resetea valores

[SCREENSHOT: Ventana completa mostrando ambos paneles con texto de ejemplo]

---

## MÓDULO 5: Módulo de Integración

### Objetivo
Agregar los botones de acción principal (Agregar al Carrito y Finalizar Pedido) y conectar todos los módulos.

### Paso 5.1: Agregar Botón "Agregar al Carrito"

1. Arrastrar **JButton** a `panelSeleccionPizza` (panel izquierdo)
2. Configurar:
   ```
   Variable Name: btnAgregarCarrito
   text: "AGREGAR AL CARRITO"
   font: Bold, 13pt
   background: Color azul
   foreground: Color blanco
   ```
3. Posición: `x: 80, y: 460`
4. Tamaño: `width: 240, height: 35`

[SCREENSHOT: Botón agregar al carrito en panel izquierdo]

### Paso 5.2: Agregar Botón "Finalizar Pedido"

1. Arrastrar **JButton** a `panelPrincipal` (abajo, centrado)
2. Configurar:
   ```
   Variable Name: btnFinalizarPedido
   text: "FINALIZAR PEDIDO"
   font: Bold, 14pt
   background: Color verde
   foreground: Color blanco
   ```
3. Posición: `x: 350, y: 550`
4. Tamaño: `width: 200, height: 40`

[SCREENSHOT: Botón finalizar pedido centrado abajo]

### Paso 5.3: Configurar Evento "Agregar al Carrito"

Por ahora, solo agregaremos lógica de GUI (sin crear objetos del modelo aún).

1. Click derecho en `btnAgregarCarrito`
2. **Events > Action > actionPerformed**
3. Agregar:

```java
private void btnAgregarCarritoActionPerformed(java.awt.event.ActionEvent evt) {
    // VALIDACIÓN 1: Verificar que haya un tipo seleccionado
    if (!optTradicional.isSelected() &&
        !optPremium.isSelected() &&
        !optPersonalizada.isSelected()) {

        JOptionPane.showMessageDialog(this,
            "Debe seleccionar un tipo de pizza",
            "Error",
            JOptionPane.ERROR_MESSAGE);
        return;
    }

    // VALIDACIÓN 2: Verificar que haya un tamaño seleccionado
    if (cboTamano.getSelectedIndex() == -1) {
        JOptionPane.showMessageDialog(this,
            "Debe seleccionar un tamaño",
            "Error",
            JOptionPane.ERROR_MESSAGE);
        return;
    }

    // Obtener información de la selección
    String tipoPizza = "";
    if (optTradicional.isSelected()) tipoPizza = "Tradicional";
    else if (optPremium.isSelected()) tipoPizza = "Premium";
    else if (optPersonalizada.isSelected()) tipoPizza = "Personalizada";

    String tamano = (String) cboTamano.getSelectedItem();

    // Si es personalizada, obtener ingredientes
    String ingredientes = "";
    if (optPersonalizada.isSelected()) {
        StringBuilder sb = new StringBuilder();
        if (chkJamon.isSelected()) sb.append("Jamón, ");
        if (chkChampinones.isSelected()) sb.append("Champiñones, ");
        if (chkAceitunas.isSelected()) sb.append("Aceitunas, ");
        if (chkPepperoni.isSelected()) sb.append("Pepperoni, ");
        if (chkPina.isSelected()) sb.append("Piña, ");
        if (chkCebolla.isSelected()) sb.append("Cebolla, ");

        if (sb.length() > 0) {
            // Remover última coma
            ingredientes = sb.substring(0, sb.length() - 2);
        }
    }

    // Construir texto para el carrito
    String textoActual = txaCarrito.getText();
    int numeroPizza = contarPizzasEnCarrito() + 1;

    StringBuilder nuevaEntrada = new StringBuilder();
    nuevaEntrada.append(numeroPizza).append(". Pizza ").append(tipoPizza).append("\n");
    nuevaEntrada.append("   Tamaño: ").append(tamano).append("\n");

    if (!ingredientes.isEmpty()) {
        nuevaEntrada.append("   Extras: ").append(ingredientes).append("\n");
    }

    // Por ahora, precio simulado (en Módulo 3-backend.md haremos el cálculo real)
    nuevaEntrada.append("   Precio: $15.000\n\n");

    // Agregar al carrito
    txaCarrito.setText(textoActual + nuevaEntrada.toString());

    // Actualizar contador
    lblCantidad.setText("Cantidad: " + numeroPizza + " pizzas");

    // Mostrar mensaje de éxito
    JOptionPane.showMessageDialog(this,
        "Pizza agregada al carrito exitosamente",
        "Éxito",
        JOptionPane.INFORMATION_MESSAGE);

    // Limpiar selección de ingredientes
    limpiarSeleccionIngredientes();
}

// Método auxiliar para contar pizzas en el carrito
private int contarPizzasEnCarrito() {
    String texto = txaCarrito.getText();
    if (texto.isEmpty()) return 0;

    int contador = 0;
    String[] lineas = texto.split("\n");
    for (String linea : lineas) {
        if (linea.matches("^\\d+\\..*")) {
            contador++;
        }
    }
    return contador;
}

// Método auxiliar para limpiar ingredientes
private void limpiarSeleccionIngredientes() {
    chkJamon.setSelected(false);
    chkChampinones.setSelected(false);
    chkAceitunas.setSelected(false);
    chkPepperoni.setSelected(false);
    chkPina.setSelected(false);
    chkCebolla.setSelected(false);
}
```

[SCREENSHOT: Código del método btnAgregarCarritoActionPerformed]

### Paso 5.4: Configurar Evento "Finalizar Pedido"

1. Click derecho en `btnFinalizarPedido`
2. **Events > Action > actionPerformed**
3. Agregar:

```java
private void btnFinalizarPedidoActionPerformed(java.awt.event.ActionEvent evt) {
    // VALIDACIÓN: Verificar que el carrito no esté vacío
    if (txaCarrito.getText().trim().isEmpty()) {
        JOptionPane.showMessageDialog(this,
            "El carrito está vacío.\nAgregue pizzas antes de finalizar.",
            "Carrito Vacío",
            JOptionPane.WARNING_MESSAGE);
        return;
    }

    // Construir resumen del pedido
    String resumen = "=== RESUMEN DEL PEDIDO ===\n\n";
    resumen += txaCarrito.getText();
    resumen += "=============================\n";
    resumen += lblTotal.getText();
    resumen += "\n\n¿Confirmar pedido?";

    // Mostrar diálogo de confirmación
    int respuesta = JOptionPane.showConfirmDialog(this,
        resumen,
        "Confirmar Pedido",
        JOptionPane.YES_NO_OPTION,
        JOptionPane.QUESTION_MESSAGE);

    if (respuesta == JOptionPane.YES_OPTION) {
        // Pedido confirmado
        JOptionPane.showMessageDialog(this,
            "¡Pedido confirmado exitosamente!\n\n" +
            "Su pedido será preparado pronto.\n" +
            lblTotal.getText(),
            "Pedido Confirmado",
            JOptionPane.INFORMATION_MESSAGE);

        // Limpiar carrito después de confirmar
        btnLimpiarCarritoActionPerformed(null);

        System.out.println("Pedido finalizado exitosamente");
    } else {
        System.out.println("Pedido cancelado por el usuario");
    }
}
```

[SCREENSHOT: Código del método btnFinalizarPedidoActionPerformed]

### Paso 5.5: Remover Texto de Ejemplo

Ahora que tenemos la funcionalidad completa, remover el texto de ejemplo del constructor:

```java
public VentanaPrincipal() {
    initComponents();

    // Configurar visibilidad inicial del panel de ingredientes
    actualizarVisibilidadIngredientes();

    // Ya no necesitamos el texto de ejemplo
    // El carrito inicia vacío
}
```

### Paso 5.6: Agregar Método Main

Si no existe, agregar el método main para ejecutar la aplicación:

```java
public static void main(String args[]) {
    /* Set the Nimbus look and feel */
    try {
        for (javax.swing.UIManager.LookAndFeelInfo info : javax.swing.UIManager.getInstalledLookAndFeels()) {
            if ("Nimbus".equals(info.getName())) {
                javax.swing.UIManager.setLookAndFeel(info.getClassName());
                break;
            }
        }
    } catch (Exception ex) {
        java.util.logging.Logger.getLogger(VentanaPrincipal.class.getName()).log(java.util.logging.Level.SEVERE, null, ex);
    }

    /* Create and display the form */
    java.awt.EventQueue.invokeLater(new Runnable() {
        public void run() {
            new VentanaPrincipal().setVisible(true);
        }
    });
}
```

### Checklist Módulo 5

- [ ] Botón "Agregar al Carrito" agregado y configurado
- [ ] Botón "Finalizar Pedido" agregado y configurado
- [ ] Validaciones implementadas (tipo de pizza, tamaño, carrito vacío)
- [ ] Evento agregar al carrito funcional
- [ ] Evento finalizar pedido funcional
- [ ] Métodos auxiliares implementados
- [ ] Método main configurado

### Probar Módulo 5

1. **Run File** (o F6)
2. Flujo completo de prueba:

   **Prueba 1: Agregar Pizza Tradicional**
   - Seleccionar "Tradicional"
   - Elegir tamaño "Mediana"
   - Click "Agregar al Carrito"
   - Verificar que aparece en el carrito

   **Prueba 2: Agregar Pizza Personalizada**
   - Seleccionar "Personalizada"
   - Elegir tamaño "Familiar"
   - Marcar 2-3 ingredientes
   - Click "Agregar al Carrito"
   - Verificar que aparece con ingredientes listados

   **Prueba 3: Validaciones**
   - Intentar agregar sin seleccionar tipo → debe mostrar error
   - Intentar finalizar con carrito vacío → debe mostrar advertencia

   **Prueba 4: Finalizar Pedido**
   - Agregar 2-3 pizzas al carrito
   - Click "Finalizar Pedido"
   - Verificar que muestra resumen
   - Confirmar pedido
   - Verificar que el carrito se limpia

[SCREENSHOT: Diálogo de validación de error]

[SCREENSHOT: Carrito con varias pizzas agregadas]

[SCREENSHOT: Diálogo de confirmación de pedido]

[SCREENSHOT: Mensaje de pedido confirmado exitosamente]

---

## Resumen de la Interfaz Completa

### Componentes Creados

**Panel Izquierdo (Crear Pizza):**
- 3 JRadioButton (Tradicional, Premium, Personalizada)
- 1 ButtonGroup
- 1 JComboBox (Tamaños)
- 6 JCheckBox (Ingredientes)
- 2 JLabel (Precio)
- 1 JButton (Agregar al Carrito)

**Panel Derecho (Carrito):**
- 1 JTextArea (Lista de pizzas)
- 1 JScrollPane
- 2 JLabel (Cantidad, Total)
- 1 JButton (Limpiar Carrito)

**Panel Principal:**
- 1 JButton (Finalizar Pedido)

### Flujo Completo de Usuario

```
1. Usuario abre la aplicación
   ↓
2. Selecciona tipo de pizza (radio button)
   ↓
3. Si es Personalizada → aparece panel de ingredientes
   ↓
4. Selecciona tamaño (combobox)
   ↓
5. Marca ingredientes (si aplica)
   ↓
6. Click "Agregar al Carrito"
   ↓
7. Pizza aparece en el carrito (lado derecho)
   ↓
8. Repite pasos 2-7 para más pizzas
   ↓
9. Click "Finalizar Pedido"
   ↓
10. Revisa resumen y confirma
    ↓
11. Recibe mensaje de éxito
```

## Estructura de Archivos del Proyecto

```
SistemaPizzaPOO/
├── src/
│   └── sistemapizzapoo/
│       ├── vista/
│       │   ├── VentanaPrincipal.java
│       │   └── VentanaPrincipal.form (generado por NetBeans)
│       ├── modelo/
│       │   └── (se llenará en 04-backend.md)
│       └── interfaces/
│           └── (se llenará en 04-backend.md)
├── nbproject/
├── build/
└── dist/
```

## Capturas de Pantalla Finales

A continuación se insertarán las capturas de pantalla tomadas durante la implementación:

[SCREENSHOT: Interfaz completa - vista general]

[SCREENSHOT: Interfaz con pizza Tradicional seleccionada]

[SCREENSHOT: Interfaz con pizza Personalizada e ingredientes visibles]

[SCREENSHOT: Carrito con múltiples pizzas agregadas]

[SCREENSHOT: Proceso de finalización de pedido]

---

## Código Completo de Métodos Importantes

### Método actualizarVisibilidadIngredientes()

```java
private void actualizarVisibilidadIngredientes() {
    boolean esPersonalizada = optPersonalizada.isSelected();
    panelIngredientes.setVisible(esPersonalizada);
}
```

### Método limpiarSeleccionIngredientes()

```java
private void limpiarSeleccionIngredientes() {
    chkJamon.setSelected(false);
    chkChampinones.setSelected(false);
    chkAceitunas.setSelected(false);
    chkPepperoni.setSelected(false);
    chkPina.setSelected(false);
    chkCebolla.setSelected(false);
}
```

### Método contarPizzasEnCarrito()

```java
private int contarPizzasEnCarrito() {
    String texto = txaCarrito.getText();
    if (texto.isEmpty()) return 0;

    int contador = 0;
    String[] lineas = texto.split("\n");
    for (String linea : lineas) {
        if (linea.matches("^\\d+\\..*")) {
            contador++;
        }
    }
    return contador;
}
```

---

## Mejoras Opcionales

Si deseas agregar funcionalidades extra a la interfaz:

### Nivel 1: Estética
- [ ] Cambiar colores de fondo de paneles
- [ ] Agregar iconos a los botones
- [ ] Usar fuentes personalizadas
- [ ] Agregar imágenes de pizzas

### Nivel 2: Funcionalidad
- [ ] Botón para eliminar pizza específica del carrito (no solo limpiar todo)
- [ ] Mostrar precio en tiempo real mientras seleccionas opciones
- [ ] Agregar campo para nombre del cliente
- [ ] Agregar selector de método de pago

### Nivel 3: Avanzado
- [ ] Múltiples ventanas (Login, Historial de Pedidos)
- [ ] Guardar pedidos en archivo
- [ ] Imprimir ticket de compra
- [ ] Animaciones al agregar al carrito

---

## Problemas Comunes y Soluciones

### Problema 1: Radio buttons permiten seleccionar múltiples
**Causa:** No están asignados a un ButtonGroup
**Solución:** Verificar que todos los radio buttons tengan configurado el mismo ButtonGroup en la propiedad `buttonGroup`

### Problema 2: Panel de ingredientes no se oculta/muestra
**Causa:** No se está llamando a `actualizarVisibilidadIngredientes()` en los event handlers
**Solución:** Asegurarse de que cada radio button llame al método

### Problema 3: ComboBox no muestra opciones
**Causa:** El modelo no está configurado correctamente
**Solución:** Click derecho en ComboBox > Edit model > Agregar items

### Problema 4: Carrito no muestra texto
**Causa:** El JTextArea puede estar detrás de otro componente
**Solución:** Verificar el orden de capas (click derecho > Bring to Front)

### Problema 5: Botones no responden
**Causa:** Event handlers no están configurados
**Solución:** Click derecho en botón > Events > Action > actionPerformed

---

## Checklist Final de la Interfaz

Antes de pasar al documento [04-backend.md](04-backend.md), verificar:

### Configuración Visual
- [ ] Ventana de 900x650 píxeles
- [ ] Título "Sistema de Pedidos - Pizzería POO"
- [ ] Dos paneles principales visibles
- [ ] Panel de ingredientes se oculta/muestra correctamente
- [ ] Todos los componentes tienen nombres descriptivos (lbl, btn, opt, etc.)

### Funcionalidad de Selección
- [ ] Solo un radio button puede estar seleccionado
- [ ] ComboBox muestra 3 opciones de tamaño
- [ ] CheckBoxes se pueden marcar/desmarcar
- [ ] Panel de ingredientes solo visible con Personalizada

### Funcionalidad de Carrito
- [ ] Botón "Agregar" agrega pizzas al carrito correctamente
- [ ] El carrito muestra tipo, tamaño e ingredientes
- [ ] Contador de pizzas se actualiza
- [ ] Botón "Limpiar Carrito" funciona

### Validaciones
- [ ] Error si no se selecciona tipo de pizza
- [ ] Error si no se selecciona tamaño
- [ ] Advertencia si carrito está vacío al finalizar

### Finalización
- [ ] Botón "Finalizar Pedido" muestra resumen
- [ ] Diálogo de confirmación aparece
- [ ] Mensaje de éxito se muestra
- [ ] Carrito se limpia después de confirmar

### Calidad del Código
- [ ] Sin errores de compilación
- [ ] Sin warnings importantes
- [ ] Código comentado donde es necesario
- [ ] Nombres de variables descriptivos

---

## Próximos Pasos

Ahora que la interfaz gráfica está completa y funcional, el siguiente paso es implementar el backend (la lógica de negocio con POO).

**Continuar con:** [04-backend.md](04-backend.md)

En ese documento:
1. Crearemos las clases del modelo (Pizza, Ingrediente, Pedido, etc.)
2. Implementaremos herencia, polimorfismo e interfaces
3. Conectaremos la GUI con el modelo
4. Reemplazaremos los precios simulados por cálculos reales
5. Implementaremos validaciones de negocio

La interfaz que acabas de crear será la capa de presentación que interactuará con el modelo de datos que construiremos a continuación.

---

## Referencias

- Documentación oficial Java Swing: https://docs.oracle.com/javase/tutorial/uiswing/
- NetBeans GUI Builder Guide: https://netbeans.apache.org/tutorial/main/kb/docs/java/quickstart-gui/
- Material del curso: `3.1.1 Interfaz Grafica.pdf`
- Documento de arquitectura: [01-README.md](01-README.md)
- Parte 1 de este tutorial: [02-interfaz-grafica.md](02-interfaz-grafica.md)

---

**Nota importante:** Este documento describe la implementación de la interfaz gráfica (frontend). La lógica de negocio (backend) con clases, herencia, polimorfismo e interfaces se implementará en el siguiente documento `04-backend.md`.

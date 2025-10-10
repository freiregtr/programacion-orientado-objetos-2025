# semana 5: colecciones en java

tiempo estimado: 3 horas de practica

## contexto del mundo real

cuando usas spotify y agregas canciones a tu playlist favorita, esa lista crece y decrece dinamicamente. no tiene un limite fijo de 10 o 20 canciones. lo mismo pasa con instagram donde la lista de tus seguidores cambia constantemente, whatsapp donde tus conversaciones se agregan y eliminan, amazon donde tu carrito de compras puede tener 1 o 100 productos, y netflix donde tu lista mi lista crece sin limite fijo.

todas estas empresas usan colecciones en sus sistemas backend. netflix maneja mas de 200 millones de usuarios con listas dinamicas de contenido. imagina intentar hacer eso con arreglos de tamano fijo.

## el problema: arreglos de tamano fijo

imagina que amazon te dice solo puedes tener 5 productos en tu carrito, ni uno mas. seria terrible para el negocio verdad.

### codigo que no funciona para nuestro contexto

```java
public class CarritoCompras {

    private String[] productos = new String[5];
    private int cantidad = 0;

    public void agregarProducto(String producto) {
        if (cantidad < 5) {
            productos[cantidad] = producto;
            cantidad++;
        } else {
            System.out.println("carrito lleno, no puedes agregar mas");
        }
    }

    public void mostrarCarrito() {
        for (int i = 0; i < cantidad; i++) {
            System.out.println(productos[i]);
        }
    }
}
```

### por que este codigo no funciona para nosotros

primero: limite artificial de 5 productos. que pasa si el cliente quiere comprar 10 cosas.

segundo: si el usuario quiere agregar un sexto producto se pierde la venta.

tercero: si solo usa 2 espacios desperdiciamos memoria en los otros 3.

cuarto: codigo fragil que requiere mantener un contador manual llamado cantidad.

quinto: tienes que saber el tamano maximo antes de compilar el programa.

### clase de prueba para ver el problema

```java
public class TestCarritoProblema {

    public static void main(String[] args) {

        CarritoCompras miCarrito = new CarritoCompras();

        miCarrito.agregarProducto("laptop lenovo");
        miCarrito.agregarProducto("mouse logitech");
        miCarrito.agregarProducto("teclado mecanico");
        miCarrito.agregarProducto("monitor samsung");
        miCarrito.agregarProducto("webcam");
        miCarrito.agregarProducto("audifonos");

        System.out.println("productos en el carrito:");
        miCarrito.mostrarCarrito();
    }
}
```

salida en consola:

```
carrito lleno, no puedes agregar mas
productos en el carrito:
laptop lenovo
mouse logitech
teclado mecanico
monitor samsung
webcam
```

### validacion del problema

paso 1: crea un nuevo proyecto en netbeans llamado problemaarreglo

paso 2: copia la clase carritocompras con arreglo fijo

paso 3: copia la clase testcarritoproblema con el metodo main

paso 4: ejecuta testcarritoproblema con f6 como clase principal

paso 5: observa en la consola como el sexto producto audifonos se rechaza

paso 6: observa el mensaje carrito lleno no puedes agregar mas

## la solucion: arraylist

arraylist es una clase de java que te da un arreglo que crece automaticamente. es como tener un cajon magico que se agranda cada vez que necesitas mas espacio.

### codigo que si funciona correctamente

```java
import java.util.ArrayList;

public class CarritoCompras {

    private ArrayList<String> productos = new ArrayList<String>();

    public void agregarProducto(String producto) {
        productos.add(producto);
        System.out.println("producto agregado: " + producto);
    }

    public void eliminarProducto(String producto) {
        if (productos.remove(producto)) {
            System.out.println("producto eliminado: " + producto);
        } else {
            System.out.println("producto no encontrado");
        }
    }

    public void mostrarCarrito() {
        System.out.println("tu carrito tiene " + productos.size() + " productos:");
        for (String producto : productos) {
            System.out.println("- " + producto);
        }
    }

    public boolean buscarProducto(String producto) {
        return productos.contains(producto);
    }

    public void vaciarCarrito() {
        productos.clear();
        System.out.println("carrito vacio");
    }
}
```

### clase de prueba

```java
public class TestCarrito {

    public static void main(String[] args) {

        CarritoCompras miCarrito = new CarritoCompras();

        miCarrito.agregarProducto("laptop lenovo");
        miCarrito.agregarProducto("mouse logitech");
        miCarrito.agregarProducto("teclado mecanico");
        miCarrito.agregarProducto("monitor samsung");
        miCarrito.agregarProducto("webcam");
        miCarrito.agregarProducto("audifonos");

        miCarrito.mostrarCarrito();

        if (miCarrito.buscarProducto("laptop lenovo")) {
            System.out.println("si, tienes una laptop en el carrito");
        }

        miCarrito.eliminarProducto("webcam");

        miCarrito.mostrarCarrito();
    }
}
```

### validacion paso a paso

paso 1: crea un nuevo proyecto en netbeans llamado carritocompras

paso 2: crea la clase carritocompras con el codigo de arriba

paso 3: crea la clase testcarrito con el metodo main

paso 4: ejecuta con f6 y observa la consola

paso 5: debes ver en consola los 6 productos agregados sin error

paso 6: debes ver el producto webcam eliminado

paso 7: debes ver el carrito final con 5 productos

salida esperada en consola:

```
producto agregado: laptop lenovo
producto agregado: mouse logitech
producto agregado: teclado mecanico
producto agregado: monitor samsung
producto agregado: webcam
producto agregado: audifonos
tu carrito tiene 6 productos:
- laptop lenovo
- mouse logitech
- teclado mecanico
- monitor samsung
- webcam
- audifonos
si, tienes una laptop en el carrito
producto eliminado: webcam
tu carrito tiene 5 productos:
- laptop lenovo
- mouse logitech
- teclado mecanico
- monitor samsung
- audifonos
```

## comparacion tecnica entre ambos enfoques

aspecto: lineas de codigo
arreglo tradicional: 15 lineas
arraylist: 8 lineas

aspecto: tamano
arreglo tradicional: fijo en compilacion
arraylist: dinamico en ejecucion

aspecto: agregar elemento
arreglo tradicional: manual con contador
arraylist: productos.add()

aspecto: eliminar elemento
arreglo tradicional: complejo reorganizar manual
arraylist: productos.remove()

aspecto: buscar elemento
arreglo tradicional: bucle manual
arraylist: productos.contains()

aspecto: obtener tamano
arreglo tradicional: variable contador manual
arraylist: productos.size()

aspecto: riesgo de errores
arreglo tradicional: alto
arraylist: bajo

aspecto: mantenibilidad
arreglo tradicional: dificil de mantener
arraylist: facil de mantener

archivos necesarios:
arreglo tradicional: 2 archivos carritocompras.java y testcarrito.java
arraylist: 2 archivos carritocompras.java y testcarrito.java

## como funciona arraylist internamente

cuando creas un arraylist vacio tiene capacidad inicial de 10 espacios en memoria.

```
arraylist<string> productos = new arraylist<string>();
```

estado interno: capacidad 10 tamano 0

cuando agregas 3 elementos:

```
productos.add("laptop");
productos.add("mouse");
productos.add("teclado");
```

estado interno: capacidad 10 tamano 3

cuando agregas el elemento 11 se expande automaticamente a capacidad 15.

esto es transparente para ti como programador. no tienes que preocuparte por nada.

## ejemplo completo del mundo real: sistema de empleados scootin

scootin es una empresa que vende scooters electricos. como las ventas crecieron necesitan un sistema para manejar empleados de forma dinamica.

vamos a construir el sistema completo paso por paso.

### paso 1: crear la clase puesto

archivo puesto.java

```java
public class Puesto {

    private int codigo;
    private String nombrePuesto;

    public Puesto() {
    }

    public Puesto(int codigo, String nombrePuesto) {
        this.codigo = codigo;
        this.nombrePuesto = nombrePuesto;
    }

    public int getCodigo() {
        return codigo;
    }

    public void setCodigo(int codigo) {
        this.codigo = codigo;
    }

    public String getNombrePuesto() {
        return nombrePuesto;
    }

    public void setNombrePuesto(String nombrePuesto) {
        this.nombrePuesto = nombrePuesto;
    }

    @Override
    public String toString() {
        return "puesto codigo=" + codigo + " nombre=" + nombrePuesto;
    }
}
```

validacion paso 1:

crea el archivo puesto.java en netbeans

compila con f9 y verifica que no hay errores

### paso 2: crear la clase empleado

archivo empleado.java

```java
public class Empleado {

    private String rut;
    private String nombreEmpleado;
    private char genero;
    private int acno;
    private int edad;
    private Puesto puesto;

    public Empleado() {
        puesto = new Puesto();
    }

    public Empleado(String rut, String nombreEmpleado, char genero, int acno, int edad, Puesto puesto) {
        this.rut = rut;
        this.nombreEmpleado = nombreEmpleado;
        this.genero = genero;
        this.acno = acno;
        this.edad = edad;
        this.puesto = puesto;
    }

    public String getRut() {
        return rut;
    }

    public void setRut(String rut) {
        this.rut = rut;
    }

    public String getNombreEmpleado() {
        return nombreEmpleado;
    }

    public void setNombreEmpleado(String nombreEmpleado) {
        this.nombreEmpleado = nombreEmpleado;
    }

    public char getGenero() {
        return genero;
    }

    public void setGenero(char genero) {
        this.genero = genero;
    }

    public int getAcno() {
        return acno;
    }

    public void setAcno(int acno) {
        this.acno = acno;
    }

    public int getEdad() {
        return edad;
    }

    public void setEdad(int edad) {
        this.edad = edad;
    }

    public Puesto getPuesto() {
        return puesto;
    }

    public void setPuesto(Puesto puesto) {
        this.puesto = puesto;
    }

    @Override
    public String toString() {
        return "empleado rut=" + rut + " nombre=" + nombreEmpleado + " genero=" + genero + " anos=" + acno + " edad=" + edad + " " + puesto;
    }
}
```

nota importante sobre la linea puesto = new puesto en el constructor vacio.

esta linea inicializa el objeto puesto para evitar nullpointerexception. si no pones esta linea y alguien crea un empleado sin parametros el atributo puesto sera null y al intentar usar puesto.getCodigo() el programa va a crashear.

validacion paso 2:

crea el archivo empleado.java en netbeans

compila con f9 y verifica que no hay errores

nota que empleado tiene una composicion con puesto

### paso 3: crear la clase empresa con arraylist

archivo empresa.java

```java
import java.util.ArrayList;

public class Empresa {

    private ArrayList<Empleado> listaEmpleados;

    public Empresa() {
        listaEmpleados = new ArrayList<Empleado>();
    }

    public boolean agregar(Empleado emple) {
        return listaEmpleados.add(emple);
    }

    public boolean buscarEmpleado(String rut) {
        for (Empleado emple : listaEmpleados) {
            if (emple.getRut().equals(rut)) {
                return true;
            }
        }
        return false;
    }

    public void listarEmpleados() {
        System.out.println("lista de empleados:");
        System.out.println("===================");
        for (Empleado emple : listaEmpleados) {
            System.out.println(emple.toString());
        }
        System.out.println("total empleados: " + listaEmpleados.size());
    }

    public boolean eliminarEmpleado(String rut) {
        for (Empleado emple : listaEmpleados) {
            if (emple.getRut().equals(rut)) {
                listaEmpleados.remove(emple);
                return true;
            }
        }
        return false;
    }
}
```

analisis linea por linea del metodo buscarEmpleado:

linea 1: recibe el rut a buscar como parametro

linea 2: inicia un for each que recorre cada empleado de la lista

linea 3: compara el rut del empleado actual con el rut buscado usando equals

linea 4: si encuentra coincidencia retorna true

linea 7: si termina el bucle sin encontrar nada retorna false

validacion paso 3:

crea el archivo empresa.java en netbeans

asegurate de importar java.util.arraylist

compila con f9 y verifica que no hay errores

### paso 4: crear clase de prueba

archivo testempresa.java

```java
public class TestEmpresa {

    public static void main(String[] args) {

        Puesto pueston = new Puesto(1, "gerente");
        Puesto puestito = new Puesto(2, "ejecutivo");

        Empleado empleado1 = new Empleado("1-9", "john", 'M', 10, 40, pueston);
        Empleado empleado2 = new Empleado("2-7", "juanita", 'F', 2, 25, puestito);

        Empresa empresa = new Empresa();

        if (empresa.buscarEmpleado("1-9") == false) {
            empresa.agregar(empleado1);
            System.out.println("se agrego empleado " + empleado1.getNombreEmpleado());
        } else {
            System.out.println("empleado existe");
        }

        if (empresa.buscarEmpleado("2-7") == false) {
            empresa.agregar(empleado2);
            System.out.println("se agrego empleado " + empleado2.getNombreEmpleado());
        } else {
            System.out.println("empleado existe");
        }

        empresa.listarEmpleados();

        if (empresa.eliminarEmpleado("2-7")) {
            System.out.println("se elimino empleado " + empleado2.getNombreEmpleado());
        } else {
            System.out.println("no se elimino empleado " + empleado2.getNombreEmpleado());
        }

        empresa.listarEmpleados();
    }
}
```

validacion paso 4:

paso 1: crea testempresa.java en netbeans

paso 2: ejecuta con f6

paso 3: observa la consola debe mostrar:

```
se agrego empleado john
se agrego empleado juanita
lista de empleados:
===================
empleado rut=1-9 nombre=john genero=M anos=10 edad=40 puesto codigo=1 nombre=gerente
empleado rut=2-7 nombre=juanita genero=F anos=2 edad=25 puesto codigo=2 nombre=ejecutivo
total empleados: 2
se elimino empleado juanita
lista de empleados:
===================
empleado rut=1-9 nombre=john genero=M anos=10 edad=40 puesto codigo=1 nombre=gerente
total empleados: 1
```

## metodos principales de arraylist

### metodo add agregar elementos

```java
ArrayList<String> lista = new ArrayList<String>();

lista.add("primero");
lista.add("segundo");
lista.add("tercero");
```

resultado: la lista tiene 3 elementos en orden primero segundo tercero

### metodo add con indice

```java
lista.add(1, "insertado");
```

resultado: inserta insertado en la posicion 1 y mueve los demas elementos

### metodo get obtener elemento

```java
String elemento = lista.get(0);
```

resultado: obtiene el elemento en la posicion 0

### metodo size obtener tamano

```java
int tamano = lista.size();
```

resultado: retorna la cantidad de elementos en la lista

### metodo contains verificar existencia

```java
boolean existe = lista.contains("primero");
```

resultado: retorna true si el elemento existe false si no

### metodo remove eliminar elemento

```java
lista.remove("primero");
```

resultado: elimina la primera ocurrencia de primero y reorganiza la lista

### metodo remove con indice

```java
lista.remove(0);
```

resultado: elimina el elemento en la posicion 0

### metodo clear vaciar lista

```java
lista.clear();
```

resultado: elimina todos los elementos lista queda vacia

### metodo isempty verificar si esta vacia

```java
boolean vacia = lista.isEmpty();
```

resultado: retorna true si no hay elementos false si hay al menos uno

### metodo indexof obtener posicion

```java
int posicion = lista.indexOf("segundo");
```

resultado: retorna el indice de la primera ocurrencia o menos 1 si no existe

## tipos de colecciones en java

java tiene varias estructuras de colecciones cada una para diferentes necesidades.

### list mantiene orden permite duplicados

arraylist: implementacion mas usada acceso rapido por indice

linkedlist: insercion y eliminacion rapida en medio de la lista

vector: sincronizado para multithreading codigo antiguo

### set no permite duplicados

hashset: mas rapido sin orden garantizado

linkedhashset: mantiene orden de insercion

treeset: ordenado automaticamente

### queue cola fifo

priorityqueue: ordenada por prioridad

arraydeque: cola de doble extremo

### map pares clave valor

hashmap: mas usado acceso rapido por clave

linkedhashmap: mantiene orden de insercion

treemap: ordenado por claves

hashtable: sincronizado codigo antiguo

## cuando usar arraylist vs otras colecciones

usa arraylist cuando necesitas una lista simple con orden y acceso rapido por indice. este es el 80% de los casos.

usa linkedlist cuando necesitas muchas inserciones y eliminaciones en medio de la lista.

usa hashset cuando necesitas elementos unicos sin duplicados.

usa hashmap cuando necesitas buscar por clave como un diccionario.

## colecciones genericas vs no genericas

### problema: colecciones sin genericos

```java
ArrayList lista = new ArrayList();

lista.add("texto");
lista.add(123);
lista.add(new Empleado());

String texto = (String) lista.get(0);
```

este codigo tiene varios problemas.

primero: puede contener cualquier tipo de objeto mezclado.

segundo: necesitas hacer cast casting cada vez que recuperas un elemento.

tercero: puedes tener errores en tiempo de ejecucion si el cast esta mal.

cuarto: el compilador no puede ayudarte a detectar errores.

### solucion: colecciones con genericos

```java
ArrayList<String> lista = new ArrayList<String>();

lista.add("texto");
lista.add("otro texto");

String texto = lista.get(0);
```

este codigo es mejor.

primero: especifica el tipo entre angulos arraylist de string.

segundo: el compilador solo permite agregar strings.

tercero: no necesitas hacer cast al recuperar elementos.

cuarto: errores se detectan en tiempo de compilacion no en ejecucion.

## problemas comunes y sus soluciones

### problema 1: nullpointerexception

codigo que falla:

```java
public class Empresa {

    private ArrayList<Empleado> listaEmpleados;

    public Empresa() {
    }

    public void agregar(Empleado e) {
        listaEmpleados.add(e);
    }
}
```

por que falla: no inicializamos la lista en el constructor entonces listaempleados es null.

cuando intentas hacer listaempleados.add() java dice nullpointerexception porque estas intentando usar un objeto que no existe.

solucion correcta:

```java
public class Empresa {

    private ArrayList<Empleado> listaEmpleados;

    public Empresa() {
        listaEmpleados = new ArrayList<Empleado>();
    }

    public void agregar(Empleado e) {
        listaEmpleados.add(e);
    }
}
```

regla de oro: siempre inicializa tus colecciones en el constructor.

validacion en consola:

ejecuta el codigo que falla y veras:

```
exception in thread main java.lang.nullpointerexception
```

ejecuta el codigo corregido y funcionara sin errores.

### problema 2: concurrentmodificationexception

codigo que falla:

```java
for (Empleado e : listaEmpleados) {
    if (e.getEdad() < 18) {
        listaEmpleados.remove(e);
    }
}
```

por que falla: no puedes modificar una lista mientras la estas recorriendo con for each.

java lanza concurrentmodificationexception porque el iterador interno se desincroniza.

solucion correcta opcion 1:

```java
import java.util.Iterator;

Iterator<Empleado> iterator = listaEmpleados.iterator();

while (iterator.hasNext()) {
    Empleado e = iterator.next();
    if (e.getEdad() < 18) {
        iterator.remove();
    }
}
```

solucion correcta opcion 2:

```java
for (int i = listaEmpleados.size() - 1; i >= 0; i--) {
    if (listaEmpleados.get(i).getEdad() < 18) {
        listaEmpleados.remove(i);
    }
}
```

la opcion 2 funciona porque recorres de atras hacia adelante entonces los indices no se desincronizan.

### problema 3: comparar strings con doble igual

codigo que falla:

```java
if (emple.getRut() == "1-9") {
    System.out.println("encontrado");
}
```

por que falla: el operador doble igual compara referencias de memoria no contenido.

getrut retorna un objeto string y uno 9 es otro objeto string diferente en memoria.

aunque tengan el mismo contenido uno 9 son objetos diferentes entonces doble igual retorna false.

solucion correcta:

```java
if (emple.getRut().equals("1-9")) {
    System.out.println("encontrado");
}
```

regla de oro: siempre usa equals para comparar strings nunca doble igual.

validacion:

prueba ambos codigos con el sistema de empleados y veras que doble igual nunca encuentra el empleado.

### problema 4: indexoutofboundsexception

codigo que falla:

```java
ArrayList<String> lista = new ArrayList<String>();

lista.add("primero");
lista.add("segundo");

String tercero = lista.get(2);
```

por que falla: la lista tiene solo 2 elementos en indices 0 y 1.

cuando intentas acceder al indice 2 que no existe java lanza indexoutofboundsexception.

solucion correcta:

```java
ArrayList<String> lista = new ArrayList<String>();

lista.add("primero");
lista.add("segundo");

if (lista.size() > 2) {
    String tercero = lista.get(2);
} else {
    System.out.println("no hay elemento en posicion 2");
}
```

regla de oro: siempre valida que el indice exista antes de acceder.

## ejercicio practico completo: tienda de productos

vamos a crear un sistema para una tienda online como mercadolibre.

tiempo estimado: 45 minutos

requisitos del sistema:

1. agregar productos con codigo nombre y precio
2. buscar producto por codigo
3. listar todos los productos
4. eliminar producto por codigo
5. calcular valor total del inventario

### paso 1: crear clase producto

archivo producto.java

```java
public class Producto {

    private String codigo;
    private String nombre;
    private double precio;

    public Producto() {
    }

    public Producto(String codigo, String nombre, double precio) {
        this.codigo = codigo;
        this.nombre = nombre;
        this.precio = precio;
    }

    public String getCodigo() {
        return codigo;
    }

    public void setCodigo(String codigo) {
        this.codigo = codigo;
    }

    public String getNombre() {
        return nombre;
    }

    public void setNombre(String nombre) {
        this.nombre = nombre;
    }

    public double getPrecio() {
        return precio;
    }

    public void setPrecio(double precio) {
        this.precio = precio;
    }

    @Override
    public String toString() {
        return "codigo=" + codigo + " nombre=" + nombre + " precio=" + precio;
    }
}
```

### paso 2: crear clase tienda

archivo tienda.java

```java
import java.util.ArrayList;

public class Tienda {

    private ArrayList<Producto> inventario;

    public Tienda() {
        inventario = new ArrayList<Producto>();
    }

    public boolean agregarProducto(Producto prod) {
        if (buscarProducto(prod.getCodigo()) == false) {
            inventario.add(prod);
            return true;
        }
        return false;
    }

    public boolean buscarProducto(String codigo) {
        for (Producto prod : inventario) {
            if (prod.getCodigo().equals(codigo)) {
                return true;
            }
        }
        return false;
    }

    public void listarProductos() {
        System.out.println("inventario de productos:");
        System.out.println("========================");
        for (Producto prod : inventario) {
            System.out.println(prod.toString());
        }
        System.out.println("total productos: " + inventario.size());
    }

    public boolean eliminarProducto(String codigo) {
        for (Producto prod : inventario) {
            if (prod.getCodigo().equals(codigo)) {
                inventario.remove(prod);
                return true;
            }
        }
        return false;
    }

    public double calcularValorTotal() {
        double total = 0;
        for (Producto prod : inventario) {
            total = total + prod.getPrecio();
        }
        return total;
    }
}
```

### paso 3: crear clase de prueba

archivo testtienda.java

```java
public class TestTienda {

    public static void main(String[] args) {

        Tienda miTienda = new Tienda();

        Producto p1 = new Producto("001", "laptop hp", 599990);
        Producto p2 = new Producto("002", "mouse logitech", 15990);
        Producto p3 = new Producto("003", "teclado mecanico", 45990);
        Producto p4 = new Producto("004", "monitor samsung", 189990);
        Producto p5 = new Producto("005", "webcam logitech", 35990);

        if (miTienda.agregarProducto(p1)) {
            System.out.println("producto agregado: " + p1.getNombre());
        }

        if (miTienda.agregarProducto(p2)) {
            System.out.println("producto agregado: " + p2.getNombre());
        }

        if (miTienda.agregarProducto(p3)) {
            System.out.println("producto agregado: " + p3.getNombre());
        }

        if (miTienda.agregarProducto(p4)) {
            System.out.println("producto agregado: " + p4.getNombre());
        }

        if (miTienda.agregarProducto(p5)) {
            System.out.println("producto agregado: " + p5.getNombre());
        }

        miTienda.listarProductos();

        System.out.println("valor total inventario: " + miTienda.calcularValorTotal());

        if (miTienda.eliminarProducto("003")) {
            System.out.println("producto eliminado");
        }

        miTienda.listarProductos();

        System.out.println("valor total inventario: " + miTienda.calcularValorTotal());
    }
}
```

### validacion completa del ejercicio

paso 1: crea los 3 archivos en netbeans

paso 2: compila cada archivo con f9

paso 3: ejecuta testtienda con f6

paso 4: observa la consola debe mostrar:

```
producto agregado: laptop hp
producto agregado: mouse logitech
producto agregado: teclado mecanico
producto agregado: monitor samsung
producto agregado: webcam logitech
inventario de productos:
========================
codigo=001 nombre=laptop hp precio=599990.0
codigo=002 nombre=mouse logitech precio=15990.0
codigo=003 nombre=teclado mecanico precio=45990.0
codigo=004 nombre=monitor samsung precio=189990.0
codigo=005 nombre=webcam logitech precio=35990.0
total productos: 5
valor total inventario: 887950.0
producto eliminado
inventario de productos:
========================
codigo=001 nombre=laptop hp precio=599990.0
codigo=002 nombre=mouse logitech precio=15990.0
codigo=004 nombre=monitor samsung precio=189990.0
codigo=005 nombre=webcam logitech precio=35990.0
total productos: 4
valor total inventario: 841960.0
```

## resumen de lo aprendido

primero: arraylist reemplaza arreglos tradicionales con tamano dinamico

segundo: metodos principales son add remove get size contains clear

tercero: siempre usa genericos arraylist de tipo para seguridad

cuarto: siempre inicializa colecciones en el constructor

quinto: usa equals para comparar strings nunca doble igual

sexto: no modifiques una lista mientras la recorres con for each

septimo: valida indices antes de acceder con get

archivos necesarios para el proyecto completo:
producto.java
tienda.java
testtienda.java

total: 3 archivos

mantenibilidad: alta porque arraylist maneja todo automaticamente

empresas que usan colecciones: netflix spotify amazon instagram whatsapp linkedin google facebook

estadisticas: 89% de desarrolladores java usan colecciones diariamente segun jetbrains 2024

proximos pasos: practica con hashmap para pares clave valor y aprende sobre ordenamiento de colecciones
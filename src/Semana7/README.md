# semana 7: polimorfismo clases abstractas final e interfaces

tiempo estimado: 4 horas de practica

## contexto del mundo real

netflix tiene un metodo reproducir que funciona diferente para peliculas series documentales y standup. el mismo metodo reproducir se comporta de forma distinta segun el tipo de contenido. eso es polimorfismo.

spotify tiene un metodo calcular precio que funciona diferente para spotify free spotify premium y spotify family. mismo nombre diferentes implementaciones. polimorfismo en accion.

uber tiene un metodo calcular tarifa que funciona distinto para uber x uber black uber pool y uber eats. mismo metodo comportamiento diferente segun el tipo de servicio.

google maps tiene clases abstractas para rutas. no puedes crear una ruta generica debes crear ruta en auto ruta en bici ruta caminando o ruta en transporte publico. la clase ruta es abstracta.

whatsapp declara clases final para seguridad. no puedes extender la clase encriptacion porque esta marcada como final. esto previene que alguien rompa la seguridad heredando de esa clase.

youtube implementa interfaces para reproduccion. cualquier dispositivo que quiera reproducir youtube debe implementar la interfaz reproducible con los metodos play pause stop siguiente y anterior.

## polimorfismo basico

### definicion de w3schools

polimorfismo en java significa muchas formas y ocurre cuando clases relacionadas por herencia pueden ejecutar un mismo metodo de diferentes maneras. permite realizar una accion unica con distintas implementaciones, como cuando diferentes animales perro cerdo hacen sonidos diferentes aunque comparten una clase base comun.

documentacion completa: https://www.w3schools.com/java/java_polymorphism.asp

### que es polimorfismo

polimorfismo significa muchas formas. permite que objetos de diferentes clases respondan al mismo metodo de manera diferente.

un empleado puede ser tratado como persona. un perro puede ser tratado como animal. una pizza puede ser tratada como producto.

esto permite escribir codigo generico que funciona con la superclase pero ejecuta el comportamiento especifico de cada subclase.

### ejercicio 1: animales que hacen diferentes sonidos

vamos a crear un sistema de animales donde cada animal hace un sonido diferente. crearemos una clase base Animal y dos clases hijas Perro y Gato. veremos como una misma variable tipo Animal puede apuntar a diferentes tipos de animales y cada uno ejecuta su propio metodo hacerSonido. esto demuestra polimorfismo en accion.

### ejemplo completo en netbeans

paso 1: abre netbeans y haz click en file, new project.

paso 2: selecciona java application y haz click en next.

paso 3: nombra el proyecto polimorfismobasico, desmarca create main class, click finish.

paso 4: haz click derecho en source packages, new java class.

paso 5: nombra la clase Animal y escribe este codigo.

```java
public class Animal {

    protected String nombre;

    public Animal(String nombre) {
        this.nombre = nombre;
    }

    public void hacerSonido() {
        System.out.println("algun sonido");
    }
}
```

paso 6: crea otra clase llamada Perro, click derecho source packages, new java class.

paso 7: nombra la clase Perro y escribe este codigo.

```java
public class Perro extends Animal {

    public Perro(String nombre) {
        super(nombre);
    }

    @Override
    public void hacerSonido() {
        System.out.println(nombre + " dice: guau guau");
    }
}
```

paso 8: crea otra clase llamada Gato de la misma forma.

paso 9: escribe este codigo en la clase Gato.

```java
public class Gato extends Animal {

    public Gato(String nombre) {
        super(nombre);
    }

    @Override
    public void hacerSonido() {
        System.out.println(nombre + " dice: miau miau");
    }
}
```

paso 10: crea la clase TestPolimorfismo con metodo main.

paso 11: escribe este codigo en TestPolimorfismo.

```java
public class TestPolimorfismo {

    public static void main(String[] args) {

        // aqui esta el polimorfismo
        // variable tipo Animal apunta a objeto tipo Perro
        Animal animal1 = new Perro("firulais");

        // variable tipo Animal apunta a objeto tipo Gato
        Animal animal2 = new Gato("pelusa");

        // mismo metodo diferentes comportamientos
        animal1.hacerSonido();
        animal2.hacerSonido();

        // arreglo polimorfico
        Animal[] animales = new Animal[3];
        animales[0] = new Perro("rex");
        animales[1] = new Gato("michi");
        animales[2] = new Perro("toby");

        // iterar significa recorrer uno por uno
        // usamos for tipo objeto : arreglo en vez de for int i igual 0
        // porque es mas simple y no necesitamos el indice
        // Animal es la clase, a es el objeto que toma los valores en el ciclo, animales es el arreglo
        // for each Animal a en el arreglo animales ejecuta hacerSonido
        for (Animal a : animales) {
            a.hacerSonido();
        }
    }
}
```

paso 12: haz click derecho en TestPolimorfismo, run file, o presiona shift f6.

paso 13: observa la consola, debe mostrar:

```
firulais dice: guau guau
pelusa dice: miau miau
rex dice: guau guau
michi dice: miau miau
toby dice: guau guau
```

paso 14: nota como animal1 es tipo Animal pero apunta a un Perro.

```java
Animal animal1 = new Perro("firulais");
```

paso 15: cambia esta linea por esta otra.

```java
// cambia esto
Animal animal1 = new Perro("firulais");

// por esto
Animal animal1 = new Gato("garfield");
```

paso 16: ejecuta de nuevo con shift f6 y observa como ahora dice miau en vez de guau.

paso 17: esto es polimorfismo, mismo metodo, diferentes comportamientos, sin cambiar mas codigo.

### documentacion w3schools

polimorfismo en java: https://www.w3schools.com/java/java_polymorphism.asp

## clases abstractas

### definicion de w3schools

las clases abstractas en java son clases restringidas que no pueden crear objetos directamente. sirven para ocultar ciertos detalles y mostrar solo informacion esencial, definiendo metodos abstractos sin implementacion que deben ser completados por las subclases que hereden de ella.

documentacion completa: https://www.w3schools.com/java/java_abstract.asp

### que son las clases abstractas

una clase abstracta es una clase que no se puede instanciar. sirve como plantilla para otras clases.

usa clases abstractas cuando:
- quieres definir un comportamiento comun pero no tiene sentido crear objetos de esa clase
- quieres forzar a las subclases a implementar ciertos metodos
- quieres compartir codigo entre clases relacionadas

ejemplos del mundo real:
- clase figura geometrica es abstracta. no existe una figura generica solo circulos rectangulos triangulos
- clase transporte es abstracta. no existe un transporte generico solo autos motos buses
- clase cuenta bancaria puede ser abstracta. solo existen cuenta corriente cuenta vista cuenta ahorro

### ejercicio 2: figuras geometricas con calculos abstractos

vamos a crear un sistema de figuras geometricas donde cada figura calcula su area y perimetro de forma diferente. crearemos una clase abstracta Figura que define los metodos calcularArea y calcularPerimetro sin implementacion. luego crearemos Circulo y Rectangulo que heredan de Figura e implementan estos metodos con sus propias formulas matematicas. esto muestra como las clases abstractas obligan a las subclases a implementar comportamientos especificos.

### ejemplo completo en netbeans

paso 1: abre netbeans, file, new project, java application.

paso 2: nombre figurasabstractas, desmarca create main class, click finish.

paso 3: click derecho en source packages, new java class, nombre Figura.

paso 4: escribe este codigo para la clase abstracta Figura.

```java
public abstract class Figura {

    protected String color;

    public Figura(String color) {
        this.color = color;
    }

    // metodo abstracto sin implementacion
    // area es el espacio dentro de la figura
    // circulo: pi por radio al cuadrado
    // rectangulo: base por altura
    // triangulo: base por altura dividido 2
    public abstract double calcularArea();

    // metodo abstracto sin implementacion
    // perimetro es la suma de todos los lados
    // circulo: 2 por pi por radio
    // rectangulo: 2 por base mas altura
    // triangulo: lado1 mas lado2 mas lado3
    public abstract double calcularPerimetro();

    // metodo concreto con implementacion
    public void mostrarColor() {
        System.out.println("color: " + color);
    }
}
```

paso 5: crea clase Circulo, click derecho source packages, new java class.

```java
// clase Circulo hereda de Figura
// debe implementar los metodos abstractos calcularArea y calcularPerimetro
public class Circulo extends Figura {

    private double radio;

    public Circulo(String color, double radio) {
        super(color);
        this.radio = radio;
    }

    // area del circulo es pi por radio al cuadrado
    @Override
    public double calcularArea() {
        return Math.PI * radio * radio;
    }

    // perimetro del circulo es 2 por pi por radio
    @Override
    public double calcularPerimetro() {
        return 2 * Math.PI * radio;
    }
}
```

paso 6: crea clase Rectangulo de la misma forma.

```java
// clase Rectangulo hereda de Figura
// debe implementar los metodos abstractos
public class Rectangulo extends Figura {

    private double base;
    private double altura;

    public Rectangulo(String color, double base, double altura) {
        super(color);
        this.base = base;
        this.altura = altura;
    }

    // area del rectangulo es base por altura
    @Override
    public double calcularArea() {
        return base * altura;
    }

    // perimetro del rectangulo es 2 por base mas altura
    @Override
    public double calcularPerimetro() {
        return 2 * (base + altura);
    }
}
```

paso 7: crea clase TestFiguras con metodo main.

dentro del main, primero prueba crear una figura abstracta y observa el error.

```java
Figura f = new Figura("rojo");
```

veras error Figura is abstract cannot be instantiated.

borra esa linea y escribe el codigo completo del main.

```java
// clase de prueba para figuras abstractas
public class TestFiguras {

    public static void main(String[] args) {

        // esto da error de compilacion
        // Figura f = new Figura("rojo");

        // polimorfismo, Figura puede apuntar a Circulo o Rectangulo
        Figura circulo = new Circulo("azul", 5);
        Figura rectangulo = new Rectangulo("rojo", 4, 6);

        System.out.println("circulo:");
        circulo.mostrarColor();
        System.out.println("area: " + circulo.calcularArea());
        System.out.println("perimetro: " + circulo.calcularPerimetro());

        System.out.println();

        System.out.println("rectangulo:");
        rectangulo.mostrarColor();
        System.out.println("area: " + rectangulo.calcularArea());
        System.out.println("perimetro: " + rectangulo.calcularPerimetro());
    }
}
```

paso 8: click derecho TestFiguras, run file, o shift f6.

observa en consola area 78.5 para circulo y area 24.0 para rectangulo.

nota como Figura circulo igual new Circulo funciona por polimorfismo.

paso 9: experimento, agrega esta linea en el main.

```java
Figura cuadrado = new Cuadrado("verde", 10);
```

observa error cannot find symbol class Cuadrado.

esto te obliga a crear la clase Cuadrado que extienda Figura.

cuando crees Cuadrado deberas implementar calcularArea y calcularPerimetro obligatorio.

### reglas de clases abstractas

regla 1: se declaran con la palabra abstract.
- ejemplo: public abstract class Figura
- abstract va antes de class
- esto indica que es una plantilla, no una clase completa
- sirve para definir comportamiento comun a varias clases hijas

regla 2: no se pueden instanciar directamente.
- no puedes hacer: Figura f igual new Figura
- da error: Figura is abstract cannot be instantiated
- esto es porque una figura abstracta no tiene sentido por si sola
- solo tienen sentido figuras concretas como Circulo o Rectangulo

regla 3: pueden tener metodos abstractos sin implementacion.
- ejemplo: public abstract double calcularArea
- estos metodos no tienen cuerpo, solo la firma
- esto obliga a las clases hijas a implementarlos
- cada clase hija implementa el metodo a su manera

regla 4: pueden tener metodos concretos con implementacion.
- ejemplo: public void mostrarColor con su codigo completo
- estos metodos funcionan igual para todas las clases hijas
- las clases hijas heredan este comportamiento
- esto evita repetir codigo en cada clase hija

regla 5: pueden tener atributos como cualquier clase.
- ejemplo: protected String color
- pueden tener variables de instancia normales
- pueden tener constructores para inicializar estos atributos
- las clases hijas heredan estos atributos con super

regla 6: las subclases deben implementar todos los metodos abstractos o ser abstractas tambien.
- si Figura tiene calcularArea y calcularPerimetro abstractos
- Circulo debe implementar ambos metodos si o si
- si Circulo no implementa todos, debe declararse abstract
- esto garantiza que todas las clases concretas esten completas

### documentacion w3schools

clases abstractas en java: https://www.w3schools.com/java/java_abstract.asp

## clases y metodos final

### definicion de w3schools

en java la palabra clave final es un modificador que impide cambiar el valor de una variable metodo o clase. se usa principalmente para crear constantes y evitar que se modifiquen o hereden elementos del codigo como por ejemplo un valor matematico que siempre debe permanecer igual.

documentacion completa: https://www.w3schools.com/java/ref_keyword_final.asp

### que significa final

la palabra final tiene tres usos en java: variables constantes metodos que no se pueden sobrescribir y clases que no se pueden heredar.

usa metodos final cuando:
- el comportamiento no debe cambiar por seguridad
- el metodo es critico para el funcionamiento de la clase
- quieres garantizar que la implementacion no sera modificada

usa clases final cuando:
- quieres evitar que alguien extienda tu clase
- la clase maneja seguridad o configuracion critica
- quieres optimizacion de rendimiento

ejemplos reales de clases final en java:
- string es final
- integer es final
- double es final
- math es final

### ejercicio 3: calculadora con metodo final protegido

vamos a crear una calculadora donde el metodo calcularImpuesto no puede ser modificado por seguridad. crearemos una clase Calculadora con un metodo final que calcula el impuesto IVA al 19 porciento. luego intentaremos crear una CalculadoraAvanzada que intente sobrescribir este metodo y veremos el error. esto muestra como final protege metodos criticos de ser modificados.

### ejemplo metodo final

paso 1: crea proyecto metodofinal en netbeans.

paso 2: crea clase Calculadora con este codigo.

```java
public class Calculadora {

    // este metodo no se puede sobrescribir
    public final double calcularImpuesto(double monto) {
        return monto * 0.19;
    }

    public double calcularTotal(double monto) {
        return monto + calcularImpuesto(monto);
    }
}
```

paso 3: crea clase CalculadoraAvanzada con este codigo.

```java
public class CalculadoraAvanzada extends Calculadora {

    // esto da error de compilacion
    // @Override
    // public double calcularImpuesto(double monto) {
    //     return monto * 0.20;
    // }

    @Override
    public double calcularTotal(double monto) {
        return super.calcularTotal(monto) - 1000;
    }
}
```

paso 4: descomenta las lineas del metodo calcularImpuesto.

paso 5: observa el error cannot override calcularImpuesto overridden method is final.

paso 6: vuelve a comentar esas lineas para que compile.

### ejercicio 4: clase final de configuracion que no se puede heredar

vamos a crear una clase Configuracion marcada como final para evitar que sea extendida. esta clase maneja informacion critica como la version del sistema. intentaremos crear una ConfiguracionAvanzada que herede de Configuracion y veremos el error. esto muestra como final protege clases completas de ser heredadas por seguridad.

### ejemplo clase final

paso 7: crea clase Configuracion con este codigo.

```java
public final class Configuracion {

    private static final String VERSION = "1.0";

    public static String obtenerVersion() {
        return VERSION;
    }
}
```

paso 8: intenta crear clase ConfiguracionAvanzada con extends Configuracion.

paso 9: observa error cannot inherit from final Configuracion.

paso 10: borra esa clase, no se puede hacer.

### reglas de final

regla 1: final en variables las convierte en constantes.
- ejemplo: final double IVA igual 0.19
- el valor no se puede cambiar despues de asignarlo
- si intentas hacer IVA igual 0.20 da error
- por convencion las constantes se escriben en MAYUSCULAS
- esto protege valores que no deben cambiar nunca

regla 2: final en metodos impide que sean sobrescritos.
- ejemplo: public final double calcularImpuesto
- las clases hijas no pueden hacer override de este metodo
- si intentas sobrescribirlo da error: overridden method is final
- esto protege logica critica que no debe modificarse
- util para calculos de seguridad, encriptacion, validaciones

regla 3: final en clases impide que sean heredadas.
- ejemplo: public final class Configuracion
- nadie puede hacer: class MiClase extends Configuracion
- si intentas heredar da error: cannot inherit from final
- esto protege clases completas de ser extendidas
- ejemplos reales: String, Integer, Math son final

regla 4: final se usa por seguridad y optimizacion.
- seguridad: evita que codigo malicioso modifique comportamiento critico
- optimizacion: el compilador puede hacer optimizaciones
- inmutabilidad: objetos final son thread safe
- claridad: indica intencion de que algo no debe cambiar

regla 5: combinar final con otros modificadores.
- public final: accesible desde cualquier lado pero no modificable
- private final: solo accesible en la clase y no modificable
- static final: constante de clase compartida por todos
- ejemplo: public static final double PI igual 3.14159

### documentacion w3schools

final keyword en java: https://www.w3schools.com/java/ref_keyword_final.asp

## interfaces

### definicion de w3schools

en java una interfaz es una clase completamente abstracta que agrupa metodos relacionados sin cuerpo. las interfaces se implementan con la palabra clave implements y permiten definir metodos que deben ser implementados por otras clases facilitando la abstraccion y permitiendo simular la herencia multiple.

documentacion completa: https://www.w3schools.com/java/java_interface.asp

### que es una interface

una interface es un contrato que define que metodos debe implementar una clase pero no como implementarlos.

una interface define comportamientos que varias clases pueden compartir sin necesidad de herencia comun.

diferencia clave entre interface y clase abstracta:
- clase abstracta: define una relacion es un
- interface: define un comportamiento puede hacer

ejemplos:
- un auto es un vehiculo pero puede volar: no
- un auto es un vehiculo pero puede acelerar: si interfaz acelerable
- un pato es un ave pero puede nadar: si interfaz nadable

### ejercicio 5: objetos voladores con comportamiento comun

vamos a crear una interface Volable que define el contrato para cualquier objeto que pueda volar. crearemos un Avion y un Pajaro que implementan esta interface pero cada uno vuela de forma diferente. el avion vuela a 5000 metros, el pajaro a 50 metros. ambos cumplen el contrato Volable pero con implementaciones distintas. esto muestra como las interfaces definen comportamientos sin importar la jerarquia de clases.

### ejemplo completo en netbeans

paso 1: abre netbeans, file, new project, java application.

paso 2: nombre interfacesvolables, desmarca create main class, finish.

paso 3: click derecho source packages, new java interface.

paso 4: nombre Volable y escribe este codigo.

```java
public interface Volable {

    // metodos abstractos por defecto
    void despegar();
    void volar();
    void aterrizar();

    // constantes public static final por defecto
    int ALTURA_MAXIMA = 10000;
}
```

paso 5: click derecho source packages, new java class, nombre Avion.

paso 6: en la declaracion agrega implements Volable.

paso 7: escribe este codigo en Avion.

```java
public class Avion implements Volable {

    private String modelo;
    private int alturaActual;

    public Avion(String modelo) {
        this.modelo = modelo;
        this.alturaActual = 0;
    }

    @Override
    public void despegar() {
        alturaActual = 100;
        System.out.println(modelo + " despegando a " + alturaActual + " metros");
    }

    @Override
    public void volar() {
        alturaActual = 5000;
        System.out.println(modelo + " volando a " + alturaActual + " metros");
    }

    @Override
    public void aterrizar() {
        alturaActual = 0;
        System.out.println(modelo + " aterrizando");
    }
}
```

paso 8: crea clase Pajaro implements Volable.

paso 9: escribe este codigo en Pajaro.

```java
public class Pajaro implements Volable {

    private String especie;
    private int alturaActual;

    public Pajaro(String especie) {
        this.especie = especie;
        this.alturaActual = 0;
    }

    @Override
    public void despegar() {
        alturaActual = 10;
        System.out.println(especie + " despegando a " + alturaActual + " metros");
    }

    @Override
    public void volar() {
        alturaActual = 50;
        System.out.println(especie + " volando a " + alturaActual + " metros");
    }

    @Override
    public void aterrizar() {
        alturaActual = 0;
        System.out.println(especie + " aterrizando en arbol");
    }
}
```

paso 10: crea clase TestVoladores con metodo main.

paso 11: escribe este codigo en TestVoladores.

```java
public class TestVoladores {

    public static void main(String[] args) {

        // polimorfismo con interfaces
        Volable v1 = new Avion("boeing 747");
        Volable v2 = new Pajaro("aguila");

        System.out.println("avion:");
        v1.despegar();
        v1.volar();
        v1.aterrizar();

        System.out.println();

        System.out.println("pajaro:");
        v2.despegar();
        v2.volar();
        v2.aterrizar();

        System.out.println();

        // arreglo de Volable
        Volable[] voladores = {v1, v2};
        System.out.println("todos despegan:");
        for (Volable v : voladores) {
            v.despegar();
        }
    }
}
```

paso 12: click derecho TestVoladores, run file, o shift f6.

paso 13: observa en consola boeing 747 despegando a 100 metros.

paso 14: observa aguila despegando a 10 metros.

paso 15: nota como Volable v1 igual new Avion funciona por polimorfismo.

paso 16: ambos implementan Volable pero cada uno vuela diferente.

### ejercicio 6: pato con multiples comportamientos

vamos a crear un Pato que puede hacer muchas cosas: volar, nadar y caminar. crearemos tres interfaces Volable, Nadable y Caminable. el Pato implementara las tres interfaces al mismo tiempo. esto simula herencia multiple y muestra como un objeto puede tener multiples comportamientos de diferentes fuentes sin estar limitado a una sola clase padre.

### multiples interfaces

paso 17: crea interface Nadable con un metodo nadar.

```java
public interface Nadable {
    void nadar();
}
```

paso 18: crea interface Caminable con un metodo caminar.

```java
public interface Caminable {
    void caminar();
}
```

paso 19: crea clase Pato que implementa Volable, Nadable, Caminable.

paso 20: escribe este codigo en Pato.

```java
public class Pato implements Volable, Nadable, Caminable {

    private String nombre;

    public Pato(String nombre) {
        this.nombre = nombre;
    }

    @Override
    public void despegar() {
        System.out.println(nombre + " aletea y despega");
    }

    @Override
    public void volar() {
        System.out.println(nombre + " vuela bajo");
    }

    @Override
    public void aterrizar() {
        System.out.println(nombre + " aterriza en el agua");
    }

    @Override
    public void nadar() {
        System.out.println(nombre + " nada en el lago");
    }

    @Override
    public void caminar() {
        System.out.println(nombre + " camina por la orilla");
    }
}
```

paso 21: crea clase TestPato con main.

paso 22: escribe este codigo.

```java
public class TestPato {

    public static void main(String[] args) {

        Pato donald = new Pato("donald");

        donald.caminar();
        donald.despegar();
        donald.volar();
        donald.aterrizar();
        donald.nadar();
        donald.caminar();
    }
}
```

paso 23: ejecuta TestPato con shift f6.

paso 24: observa como Pato puede caminar, volar, nadar, todo junto.

paso 25: esto es herencia multiple simulada con interfaces.

### reglas de interfaces

regla 1: se declaran con la palabra interface.
- ejemplo: public interface Volable
- no se usa la palabra class, se usa interface
- esto indica que es un contrato, no una clase real

regla 2: todos los metodos son public abstract por defecto.
- no necesitas escribir public abstract, java lo asume
- esto es porque las interfaces solo definen que hacer, no como hacerlo
- quien implemente la interface decide el como

regla 3: todas las variables son public static final por defecto.
- esto significa que son constantes accesibles desde cualquier lado
- public: cualquier clase puede acceder
- static: pertenece a la interface, no a objetos
- final: no se puede cambiar el valor
- ejemplo: int ALTURA_MAXIMA igual 10000 es constante para todos

regla 4: una clase puede implementar multiples interfaces.
- ejemplo: class Pato implements Volable, Nadable, Caminable
- esto simula herencia multiple
- una clase solo puede extends una clase padre
- pero puede implements muchas interfaces

regla 5: una interface puede extender otra interface.
- ejemplo: interface VehiculoVolador extends Volable
- asi creas jerarquias de comportamientos
- una interface hija hereda los metodos de la interface padre

regla 6: las clases que implementan una interface deben implementar todos sus metodos.
- si Avion implements Volable con tres metodos
- Avion debe implementar los tres si o si
- si no implementas todos, la clase debe ser abstract
- esto garantiza que el contrato se cumple completo

### documentacion w3schools

interfaces en java: https://www.w3schools.com/java/java_interface.asp

## ejemplo integrador: sistema de pagos

### ejercicio 7: sistema de pagos completo integrando todos los conceptos

vamos a crear un sistema de pagos real que combina interface, clase abstracta y polimorfismo. crearemos una interface Pagable que define el contrato de cualquier metodo de pago. luego una clase abstracta MetodoPago que implementa parte del comportamiento comun. finalmente tres clases concretas TarjetaCredito, Transferencia y Efectivo, cada una con su propia comision. TarjetaCredito cobra 3 porciento, Transferencia cobra 1000 pesos fijos, Efectivo no cobra nada. este ejercicio integra todo lo aprendido en un caso real de negocio.

tiempo estimado: 60 minutos.

### paso a paso completo en netbeans

paso 1: abre netbeans, file, new project, java application.

paso 2: nombre sistemapagos, desmarca create main class, finish.

paso 3: click derecho source packages, new java interface, nombre Pagable.

paso 4: escribe este codigo en la interface.

```java
public interface Pagable {

    // constante de impuesto
    double IVA = 0.19;

    // metodos que todas las formas de pago deben implementar
    boolean procesarPago(double monto);
    void mostrarComprobante();
    double calcularComision();
}
```

paso 5: click derecho source packages, new java class, nombre MetodoPago.

paso 6: en la declaracion marca abstract e implements Pagable.

paso 7: escribe este codigo en MetodoPago.

```java
public abstract class MetodoPago implements Pagable {

    protected String titular;
    protected double montoTotal;

    public MetodoPago(String titular) {
        this.titular = titular;
        this.montoTotal = 0;
    }

    // metodo concreto compartido
    public void mostrarComprobante() {
        System.out.println("comprobante de pago");
        System.out.println("titular: " + titular);
        System.out.println("monto: " + montoTotal);
        System.out.println("comision: " + calcularComision());
        System.out.println("iva: " + (montoTotal * IVA));
        System.out.println("total: " + (montoTotal + calcularComision() + (montoTotal * IVA)));
    }

    // metodo abstracto que cada subclase debe implementar
    public abstract double calcularComision();
}
```

paso 8: crea clase TarjetaCredito extends MetodoPago.

paso 9: escribe este codigo en TarjetaCredito.

```java
public class TarjetaCredito extends MetodoPago {

    private String numeroTarjeta;
    private String banco;

    public TarjetaCredito(String titular, String numeroTarjeta, String banco) {
        super(titular);
        this.numeroTarjeta = numeroTarjeta;
        this.banco = banco;
    }

    @Override
    public boolean procesarPago(double monto) {
        this.montoTotal = monto;
        System.out.println("procesando pago con tarjeta " + banco);
        System.out.println("numero tarjeta: " + numeroTarjeta);
        System.out.println("monto: " + monto);
        return true;
    }

    @Override
    public double calcularComision() {
        // tarjeta de credito cobra 3 porciento de comision
        return montoTotal * 0.03;
    }
}
```

paso 10: crea clase Transferencia extends MetodoPago.

paso 11: escribe este codigo en Transferencia.

```java
public class Transferencia extends MetodoPago {

    private String cuentaOrigen;
    private String banco;

    public Transferencia(String titular, String cuentaOrigen, String banco) {
        super(titular);
        this.cuentaOrigen = cuentaOrigen;
        this.banco = banco;
    }

    @Override
    public boolean procesarPago(double monto) {
        this.montoTotal = monto;
        System.out.println("procesando transferencia desde " + banco);
        System.out.println("cuenta origen: " + cuentaOrigen);
        System.out.println("monto: " + monto);
        return true;
    }

    @Override
    public double calcularComision() {
        // transferencia tiene comision fija
        return 1000;
    }
}
```

paso 12: crea clase Efectivo extends MetodoPago.

paso 13: escribe este codigo en Efectivo.

```java
public class Efectivo extends MetodoPago {

    private String sucursal;

    public Efectivo(String titular, String sucursal) {
        super(titular);
        this.sucursal = sucursal;
    }

    @Override
    public boolean procesarPago(double monto) {
        this.montoTotal = monto;
        System.out.println("procesando pago en efectivo");
        System.out.println("sucursal: " + sucursal);
        System.out.println("monto: " + monto);
        return true;
    }

    @Override
    public double calcularComision() {
        // efectivo no tiene comision
        return 0;
    }
}
```

paso 14: crea clase TestPagos con metodo main.

paso 15: escribe este codigo en TestPagos.

```java
public class TestPagos {

    public static void main(String[] args) {

        // polimorfismo con interface Pagable
        Pagable pago1 = new TarjetaCredito("juan perez", "1234-5678-9012-3456", "banco chile");
        Pagable pago2 = new Transferencia("maria gonzalez", "987654321", "banco estado");
        Pagable pago3 = new Efectivo("pedro rodriguez", "sucursal maipu");

        double monto = 100000;

        System.out.println("pago 1 tarjeta credito:");
        pago1.procesarPago(monto);
        pago1.mostrarComprobante();

        System.out.println();

        System.out.println("pago 2 transferencia:");
        pago2.procesarPago(monto);
        pago2.mostrarComprobante();

        System.out.println();

        System.out.println("pago 3 efectivo:");
        pago3.procesarPago(monto);
        pago3.mostrarComprobante();

        System.out.println();

        // arreglo polimorfico
        Pagable[] pagos = {pago1, pago2, pago3};

        System.out.println("procesando todos los pagos:");
        for (Pagable p : pagos) {
            p.procesarPago(50000);
            System.out.println("comision: " + p.calcularComision());
            System.out.println();
        }
    }
}
```

paso 16: click derecho TestPagos, run file, o shift f6.

paso 17: en consola verifica tarjeta 100000 mas 3000 comision 3 porciento.

paso 18: verifica transferencia 100000 mas 1000 comision fija.

paso 19: verifica efectivo 100000 mas 0 comision.

paso 20: nota Pagable pago1 igual new TarjetaCredito funciona por polimorfismo.

paso 21: Pagable es la interface, MetodoPago es abstracta, TarjetaCredito es concreta.

paso 22: todos los objetos en el arreglo Pagable se tratan igual.

paso 23: cada uno ejecuta su propia version de calcularComision.

paso 24: este es el poder de combinar interface, abstracta y polimorfismo.

## comparacion tecnica

aspecto: instanciacion.
- clase abstracta: no se puede instanciar.
- interface: no se puede instanciar.
- clase final: si se puede instanciar.

aspecto: herencia.
- clase abstracta: extends una sola.
- interface: implements multiples.
- clase final: no se puede heredar.

aspecto: metodos.
- clase abstracta: abstractos y concretos.
- interface: solo abstractos.
- clase final: solo concretos.

aspecto: atributos.
- clase abstracta: cualquier tipo.
- interface: solo constantes.
- clase final: cualquier tipo.

aspecto: cuando usar.
- clase abstracta: clases relacionadas, compartir codigo.
- interface: comportamiento comun, clases no relacionadas.
- clase final: evitar herencia, seguridad.

aspecto: ejemplo real.
- clase abstracta: Vehiculo, Empleado, Figura.
- interface: Comparable, Serializable, Cloneable.
- clase final: String, Integer, Math.

## errores comunes y soluciones

### error 1: no implementar metodos abstractos

este codigo da error en netbeans.

paso 1: crea clase Circulo extends Figura sin implementar metodos.

paso 2: observa error Circulo is not abstract and does not override abstract method calcularArea.

paso 3: solucion, implementa todos los metodos abstractos con override.

paso 4: o declara Circulo como abstract si no quieres implementarlos.

### error 2: no implementar todos los metodos de interface

este codigo da error.

paso 1: crea clase Avion implements Volable.

paso 2: solo implementa despegar sin volar ni aterrizar.

paso 3: observa error Avion is not abstract and does not override abstract method volar.

paso 4: solucion, implementa los tres metodos despegar, volar, aterrizar.

### error 3: intentar heredar de clase final

este codigo da error.

paso 1: crea clase Configuracion con final.

paso 2: intenta crear clase ConfiguracionAvanzada extends Configuracion.

paso 3: observa error cannot inherit from final Configuracion.

paso 4: solucion, usa composicion en vez de herencia.

paso 5: crea atributo Configuracion config en ConfiguracionAvanzada.

### error 4: intentar sobrescribir metodo final

este codigo da error.

paso 1: crea clase Empleado con metodo final calcularImpuesto.

paso 2: crea clase Gerente extends Empleado.

paso 3: intenta override calcularImpuesto en Gerente.

paso 4: observa error overridden method is final.

paso 5: solucion, no sobrescribas metodos final o quita final de la superclase.

## ejercicio final: sistema de notificaciones

### ejercicio 8: sistema de notificaciones para practicar autonomamente

vamos a crear un sistema completo de notificaciones que envia mensajes por Email, Sms y Push. crearemos una interface Notificable con los metodos enviar, validarDestinatario y confirmarEnvio. luego una clase abstracta Notificacion que implementa confirmarEnvio pero deja abstracto calcularCosto. finalmente tres clases concretas: Email valida que tenga arroba y cuesta 0, Sms valida 9 digitos empezando con 9 y cuesta 100, Push valida token minimo 20 caracteres y cuesta 50. este es tu ejercicio final para practicar todo lo aprendido de forma autonoma.

crea un sistema completo en 90 minutos siguiendo estos pasos.

paso 1: crea proyecto sistemanotificaciones en netbeans.

paso 2: crea interface Notificable con metodos enviar, validarDestinatario, confirmarEnvio.

paso 3: crea clase abstracta Notificacion implements Notificable.

paso 4: Notificacion tiene atributos remitente, asunto, enviado.

paso 5: implementa confirmarEnvio concreto en Notificacion.

paso 6: declara metodo abstracto calcularCosto en Notificacion.

paso 7: crea clase Email extends Notificacion.

paso 8: Email valida que destinatario contenga arroba.

paso 9: Email tiene costo 0.

paso 10: crea clase Sms extends Notificacion.

paso 11: Sms valida 9 digitos empezando con 9.

paso 12: Sms tiene costo 100.

paso 13: crea clase Push extends Notificacion.

paso 14: Push valida token minimo 20 caracteres.

paso 15: Push tiene costo 50.

paso 16: crea TestNotificaciones y prueba los tres tipos.

paso 17: verifica validaciones funcionen correctamente.

paso 18: verifica calculos de costo e iva.

paso 19: usa arreglo Notificable para procesarlos todos juntos.

paso 20: observa polimorfismo en accion.

## resumen de conceptos

primero: polimorfismo permite tratar objetos de diferentes clases de manera uniforme.

segundo: clases abstractas definen plantillas con metodos abstractos y concretos.

tercero: metodos final no se pueden sobrescribir en subclases.

cuarto: clases final no se pueden heredar.

quinto: interfaces definen contratos que las clases deben cumplir.

sexto: una clase puede implementar multiples interfaces.

septimo: interface define que hacer, clase abstracta puede definir que y como.

ejemplos reales:
- polimorfismo: netflix reproduce diferente segun tipo de contenido.
- clases abstractas: android tiene Activity abstracta y muchas implementaciones.
- metodos final: String hashCode es final para garantizar consistencia.
- clases final: String, Integer, Double son final por seguridad.
- interfaces: java util List define comportamiento para ArrayList, LinkedList.

estadisticas: 80 porciento de frameworks java usan interfaces, 60 porciento usan clases abstractas, 40 porciento usan final para seguridad.

empresas: google con android, spring framework, hibernate, eclipse, todos los frameworks modernos de java.

proximos pasos: practica con colecciones ArrayList, LinkedList, HashMap que usan todos estos conceptos juntos.

## enlaces a documentacion

polimorfismo: https://www.w3schools.com/java/java_polymorphism.asp

clases abstractas: https://www.w3schools.com/java/java_abstract.asp

interfaces: https://www.w3schools.com/java/java_interface.asp

final keyword: https://www.w3schools.com/java/ref_keyword_final.asp

sobrescritura de metodos: https://www.w3schools.com/java/java_override.asp

modificadores de acceso: https://www.w3schools.com/java/java_modifiers.asp

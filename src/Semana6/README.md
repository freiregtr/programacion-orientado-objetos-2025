# semana 6: herencia en java

tiempo estimado: 4 horas de practica

## contexto del mundo real

cuando youtube creo youtube music y youtube kids no programaron todo desde cero. reutilizaron el codigo de youtube original. lo mismo pasa con instagram que creo instagram lite, o facebook que tiene facebook marketplace y facebook gaming.

spotify tiene spotify free y spotify premium. netflix tiene perfiles basicos y perfiles premium. uber tiene uber x, uber black, uber pool. todos comparten codigo base pero cada uno tiene caracteristicas especiales.

google maneja mas de 2 mil millones de lineas de codigo y sin herencia seria imposible mantenerlo. cada producto de google reutiliza codigo de otros productos. maps reutiliza el motor de busqueda, gmail reutiliza el sistema de autenticacion, youtube reutiliza la infraestructura de almacenamiento.

## el problema: duplicar codigo sin herencia

imagina que trabajas para una empresa de transporte que tiene conductores, pasajeros y administradores. todos tienen nombre, rut y edad.

### codigo que no funciona para nuestro contexto

```java
public class Conductor {

    private String nombre;
    private String rut;
    private int edad;
    private String licencia;

    public Conductor(String nombre, String rut, int edad, String licencia) {
        this.nombre = nombre;
        this.rut = rut;
        this.edad = edad;
        this.licencia = licencia;
    }

    public String getNombre() {
        return nombre;
    }

    public void setNombre(String nombre) {
        this.nombre = nombre;
    }

    public String getRut() {
        return rut;
    }

    public void setRut(String rut) {
        this.rut = rut;
    }

    public int getEdad() {
        return edad;
    }

    public void setEdad(int edad) {
        this.edad = edad;
    }

    public String getLicencia() {
        return licencia;
    }

    public void setLicencia(String licencia) {
        this.licencia = licencia;
    }
}
```

```java
public class Pasajero {

    private String nombre;
    private String rut;
    private int edad;
    private String metodoPago;

    public Pasajero(String nombre, String rut, int edad, String metodoPago) {
        this.nombre = nombre;
        this.rut = rut;
        this.edad = edad;
        this.metodoPago = metodoPago;
    }

    public String getNombre() {
        return nombre;
    }

    public void setNombre(String nombre) {
        this.nombre = nombre;
    }

    public String getRut() {
        return rut;
    }

    public void setRut(String rut) {
        this.rut = rut;
    }

    public int getEdad() {
        return edad;
    }

    public void setEdad(int edad) {
        this.edad = edad;
    }

    public String getMetodoPago() {
        return metodoPago;
    }

    public void setMetodoPago(String metodoPago) {
        this.metodoPago = metodoPago;
    }
}
```

### por que este codigo no funciona para nosotros

primero: codigo duplicado. nombre rut edad aparecen en ambas clases con los mismos getters y setters.

segundo: si necesitas cambiar como se valida el rut tienes que modificar dos archivos.

tercero: si agregas una tercera clase administrador tendrias que copiar todo otra vez.

cuarto: tienes 40 lineas de codigo duplicado entre conductor y pasajero.

quinto: mantenimiento pesadilla. un bug en la validacion de edad requiere arreglarlo en 3 lugares.

### clase de prueba para ver el problema

```java
public class TestTransporteProblema {

    public static void main(String[] args) {

        Conductor c1 = new Conductor("juan perez", "12345678-9", 35, "A3");
        System.out.println("conductor: " + c1.getNombre());
        System.out.println("rut: " + c1.getRut());
        System.out.println("edad: " + c1.getEdad());
        System.out.println("licencia: " + c1.getLicencia());

        System.out.println();

        Pasajero p1 = new Pasajero("maria gonzalez", "98765432-1", 28, "tarjeta credito");
        System.out.println("pasajero: " + p1.getNombre());
        System.out.println("rut: " + p1.getRut());
        System.out.println("edad: " + p1.getEdad());
        System.out.println("metodo pago: " + p1.getMetodoPago());
    }
}
```

salida en consola:

```
conductor: juan perez
rut: 12345678-9
edad: 35
licencia: A3

pasajero: maria gonzalez
rut: 98765432-1
edad: 28
metodo pago: tarjeta credito
```

### validacion del problema

paso 1: crea un nuevo proyecto en netbeans llamado problemaherencia

paso 2: copia la clase conductor completa

paso 3: copia la clase pasajero completa

paso 4: copia la clase testtransporteproblema con el metodo main

paso 5: ejecuta testtransporteproblema con f6 como clase principal

paso 6: cuenta cuantas lineas de codigo son identicas entre conductor y pasajero

paso 7: imagina agregar 5 clases mas: administrador supervisor operador vendedor contador

paso 8: calcula cuantas lineas duplicadas tendrias: 40 lineas por 7 clases igual 280 lineas duplicadas

paso 9: ahora imagina encontrar un bug en getrut y tener que arreglarlo en 7 lugares diferentes

## la solucion: herencia

herencia te permite crear una clase base con las caracteristicas comunes y luego crear clases especializadas que heredan esas caracteristicas.

### codigo que si funciona correctamente

clase base persona:

```java
public class Persona {

    private String nombre;
    private String rut;
    private int edad;

    public Persona() {
    }

    public Persona(String nombre, String rut, int edad) {
        this.nombre = nombre;
        this.rut = rut;
        this.edad = edad;
    }

    public String getNombre() {
        return nombre;
    }

    public void setNombre(String nombre) {
        this.nombre = nombre;
    }

    public String getRut() {
        return rut;
    }

    public void setRut(String rut) {
        this.rut = rut;
    }

    public int getEdad() {
        return edad;
    }

    public void setEdad(int edad) {
        this.edad = edad;
    }

    public void mostrarInfo() {
        System.out.println("nombre: " + nombre);
        System.out.println("rut: " + rut);
        System.out.println("edad: " + edad);
    }
}
```

clase especializada conductor:

```java
public class Conductor extends Persona {

    private String licencia;

    public Conductor() {
        super();
    }

    public Conductor(String nombre, String rut, int edad, String licencia) {
        super(nombre, rut, edad);
        this.licencia = licencia;
    }

    public String getLicencia() {
        return licencia;
    }

    public void setLicencia(String licencia) {
        this.licencia = licencia;
    }

    @Override
    public void mostrarInfo() {
        super.mostrarInfo();
        System.out.println("licencia: " + licencia);
    }
}
```

clase especializada pasajero:

```java
public class Pasajero extends Persona {

    private String metodoPago;

    public Pasajero() {
        super();
    }

    public Pasajero(String nombre, String rut, int edad, String metodoPago) {
        super(nombre, rut, edad);
        this.metodoPago = metodoPago;
    }

    public String getMetodoPago() {
        return metodoPago;
    }

    public void setMetodoPago(String metodoPago) {
        this.metodoPago = metodoPago;
    }

    @Override
    public void mostrarInfo() {
        super.mostrarInfo();
        System.out.println("metodo pago: " + metodoPago);
    }
}
```

clase de prueba:

```java
public class TestTransporte {

    public static void main(String[] args) {

        Conductor c1 = new Conductor("juan perez", "12345678-9", 35, "A3");
        System.out.println("datos del conductor:");
        c1.mostrarInfo();

        System.out.println();

        Pasajero p1 = new Pasajero("maria gonzalez", "98765432-1", 28, "tarjeta credito");
        System.out.println("datos del pasajero:");
        p1.mostrarInfo();
    }
}
```

### validacion paso a paso

paso 1: crea un nuevo proyecto en netbeans llamado sistemtransporte

paso 2: crea la clase persona con el codigo de arriba

paso 3: crea la clase conductor que extiende persona

paso 4: crea la clase pasajero que extiende persona

paso 5: crea la clase testtransporte con el metodo main

paso 6: ejecuta con f6 y observa la consola

salida esperada en consola:

```
datos del conductor:
nombre: juan perez
rut: 12345678-9
edad: 35
licencia: A3

datos del pasajero:
nombre: maria gonzalez
rut: 98765432-1
edad: 28
metodo pago: tarjeta credito
```

paso 7: nota como conductor tiene acceso a nombre rut edad sin declararlos

paso 8: nota como pasajero tambien tiene acceso a esos mismos atributos

paso 9: modifica el metodo getrut en persona y automaticamente afecta a conductor y pasajero

## comparacion tecnica entre ambos enfoques

aspecto: lineas de codigo totales
sin herencia: 120 lineas
con herencia: 80 lineas

aspecto: codigo duplicado
sin herencia: 40 lineas duplicadas
con herencia: 0 lineas duplicadas

aspecto: archivos a modificar si cambia rut
sin herencia: 2 archivos
con herencia: 1 archivo

aspecto: facilidad para agregar nueva clase
sin herencia: copiar 40 lineas otra vez
con herencia: escribir solo lo nuevo extends persona

aspecto: mantenibilidad
sin herencia: dificil bugs se replican
con herencia: facil un solo lugar para arreglar

aspecto: reutilizacion de codigo
sin herencia: 0 porciento
con herencia: 70 porciento

archivos necesarios:
sin herencia: conductor.java pasajero.java
con herencia: persona.java conductor.java pasajero.java testtransporte.java

## conceptos fundamentales de herencia

### relacion es un

la herencia establece una relacion es un entre clases.

conductor es una persona: correcto
pasajero es una persona: correcto
persona es un conductor: incorrecto

ejemplos correctos del mundo real:
iphone es un telefono
spotify premium es un servicio de musica
uber black es un servicio de transporte
macbook pro es una computadora

ejemplos incorrectos:
conductor es una licencia: incorrecto esto es composicion tiene una licencia
alumno es una universidad: incorrecto alumno estudia en universidad
persona es una direccion: incorrecto persona tiene una direccion

### relacion tiene un

cuando un objeto contiene otro como atributo eso es composicion no herencia.

empleado tiene un puesto: composicion
auto tiene un motor: composicion
alumno tiene un curso: composicion

### superclase y subclase

terminologia:
superclase: clase padre clase base
subclase: clase hija clase derivada

en nuestro ejemplo:
persona es la superclase
conductor es una subclase de persona
pasajero es una subclase de persona

jerarquia de clases:
```
object raiz de todo en java
persona extiende object implicitamente
conductor extiende persona
pasajero extiende persona
```

## la palabra clave extends

para crear herencia en java usas extends en la declaracion de la clase.

sintaxis basica:
```java
public class subclase extends superclase {
}
```

ejemplo real:
```java
public class conductor extends persona {
}
```

esto significa:
conductor hereda todos los atributos publicos y protected de persona
conductor hereda todos los metodos publicos y protected de persona
conductor puede agregar sus propios atributos y metodos
conductor puede sobrescribir metodos de persona

## constructores en herencia

los constructores no se heredan pero la subclase debe llamar al constructor de la superclase.

### el problema con constructores

```java
public class Persona {

    private String nombre;

    public Persona(String nombre) {
        this.nombre = nombre;
    }
}
```

```java
public class Conductor extends Persona {

    private String licencia;

    public Conductor(String licencia) {
        this.licencia = licencia;
    }
}
```

este codigo da error de compilacion porque conductor debe llamar al constructor de persona primero.

### la solucion con super

```java
public class Conductor extends Persona {

    private String licencia;

    public Conductor(String nombre, String licencia) {
        super(nombre);
        this.licencia = licencia;
    }
}
```

super debe ser la primera linea del constructor de la subclase.

### como funciona super en constructores

cuando creas un objeto conductor:

paso 1: se llama al constructor de conductor
paso 2: primera linea super llama al constructor de persona
paso 3: se ejecuta el constructor de persona
paso 4: se regresa al constructor de conductor
paso 5: se ejecuta el resto del constructor de conductor

ejemplo con tres niveles:

```java
public class Persona {

    public Persona() {
        System.out.println("constructor persona");
    }
}
```

```java
public class Empleado extends Persona {

    public Empleado() {
        super();
        System.out.println("constructor empleado");
    }
}
```

```java
public class Gerente extends Empleado {

    public Gerente() {
        super();
        System.out.println("constructor gerente");
    }
}
```

```java
public class TestJerarquia {

    public static void main(String[] args) {
        Gerente g = new Gerente();
    }
}
```

salida en consola:
```
constructor persona
constructor empleado
constructor gerente
```

validacion:

paso 1: copia el codigo anterior en netbeans
paso 2: ejecuta con f6
paso 3: observa el orden de ejecucion en consola
paso 4: nota como los constructores se ejecutan desde la clase mas general a la mas especifica

## modificadores de acceso en herencia

java tiene tres modificadores principales: public protected private

### public

accesible desde cualquier clase en cualquier paquete.

```java
public class Persona {

    public String nombre;

    public void saludar() {
        System.out.println("hola");
    }
}
```

cualquier clase puede acceder a nombre y saludar.

### private

accesible solo dentro de la misma clase. no se hereda.

```java
public class Persona {

    private String rut;

    private void validarRut() {
        System.out.println("validando rut");
    }
}
```

```java
public class Conductor extends Persona {

    public void mostrarRut() {
        System.out.println(rut);
    }
}
```

este codigo da error porque rut es private en persona y no es accesible desde conductor.

### protected

accesible desde la misma clase y desde subclases. este es el secreto de la herencia.

```java
public class Persona {

    protected String rut;

    protected void validarRut() {
        System.out.println("validando rut");
    }
}
```

```java
public class Conductor extends Persona {

    public void mostrarRut() {
        System.out.println(rut);
        validarRut();
    }
}
```

ahora funciona porque rut y validarrut son protected.

tabla de acceso:

modificador: private
misma clase: si
subclase: no
cualquier clase: no

modificador: protected
misma clase: si
subclase: si
cualquier clase: no

modificador: public
misma clase: si
subclase: si
cualquier clase: si

## sobrescritura de metodos override

sobrescribir significa reescribir un metodo de la superclase en la subclase con comportamiento diferente.

reglas para sobrescribir:

regla 1: mismo nombre del metodo
regla 2: mismos parametros
regla 3: mismo tipo de retorno o subtipo
regla 4: no puede ser mas restrictivo en acceso
regla 5: usar anotacion override

### ejemplo de sobrescritura

```java
public class Animal {

    public void hacerSonido() {
        System.out.println("algun sonido");
    }
}
```

```java
public class Perro extends Animal {

    @Override
    public void hacerSonido() {
        System.out.println("guau guau");
    }
}
```

```java
public class Gato extends Animal {

    @Override
    public void hacerSonido() {
        System.out.println("miau miau");
    }
}
```

```java
public class TestAnimales {

    public static void main(String[] args) {

        Animal a1 = new Animal();
        a1.hacerSonido();

        Perro p1 = new Perro();
        p1.hacerSonido();

        Gato g1 = new Gato();
        g1.hacerSonido();
    }
}
```

salida en consola:
```
algun sonido
guau guau
miau miau
```

### usando super en sobrescritura

puedes llamar al metodo de la superclase desde la subclase usando super.

```java
public class Empleado extends Persona {

    private double salario;

    @Override
    public void mostrarInfo() {
        super.mostrarInfo();
        System.out.println("salario: " + salario);
    }
}
```

esto ejecuta primero el metodo de persona y luego agrega informacion adicional.

## sobrecarga de metodos overload

sobrecarga significa tener varios metodos con el mismo nombre pero diferentes parametros.

diferencia clave:
sobrescritura: mismo metodo diferente implementacion en subclase
sobrecarga: varios metodos mismo nombre diferentes parametros misma clase o subclase

### ejemplo de sobrecarga

```java
public class Calculadora {

    public int sumar(int a, int b) {
        return a + b;
    }

    public int sumar(int a, int b, int c) {
        return a + b + c;
    }

    public double sumar(double a, double b) {
        return a + b;
    }
}
```

```java
public class TestCalculadora {

    public static void main(String[] args) {

        Calculadora calc = new Calculadora();

        System.out.println(calc.sumar(5, 3));
        System.out.println(calc.sumar(5, 3, 2));
        System.out.println(calc.sumar(5.5, 3.2));
    }
}
```

salida en consola:
```
8
10
8.7
```

java decide que metodo llamar segun los parametros que le pases.

## la palabra clave super

super tiene tres usos principales en herencia.

### uso 1: llamar al constructor de la superclase

```java
public class Conductor extends Persona {

    public Conductor(String nombre, String rut, int edad, String licencia) {
        super(nombre, rut, edad);
        this.licencia = licencia;
    }
}
```

### uso 2: llamar a un metodo de la superclase

```java
public class Conductor extends Persona {

    @Override
    public void mostrarInfo() {
        super.mostrarInfo();
        System.out.println("licencia: " + licencia);
    }
}
```

### uso 3: acceder a un atributo de la superclase

```java
public class Conductor extends Persona {

    public void mostrarNombreCompleto() {
        System.out.println("conductor: " + super.nombre);
    }
}
```

## ejemplo completo del mundo real: sistema de empleados

vamos a crear un sistema para una empresa con empleados docentes y administrativos.

tiempo estimado: 60 minutos

### paso 1: crear clase empleado

archivo empleado.java

```java
public class Empleado {

    protected String rut;
    protected String nombre;
    protected int edad;
    protected double sueldo;

    public Empleado() {
    }

    public Empleado(String rut, String nombre, int edad, double sueldo) {
        this.rut = rut;
        this.nombre = nombre;
        this.edad = edad;
        this.sueldo = sueldo;
    }

    public String getRut() {
        return rut;
    }

    public void setRut(String rut) {
        this.rut = rut;
    }

    public String getNombre() {
        return nombre;
    }

    public void setNombre(String nombre) {
        this.nombre = nombre;
    }

    public int getEdad() {
        return edad;
    }

    public void setEdad(int edad) {
        this.edad = edad;
    }

    public double getSueldo() {
        return sueldo;
    }

    public void setSueldo(double sueldo) {
        this.sueldo = sueldo;
    }

    public double calcularBonificacion() {
        return sueldo * 0.10;
    }

    public void mostrarInfo() {
        System.out.println("rut: " + rut);
        System.out.println("nombre: " + nombre);
        System.out.println("edad: " + edad);
        System.out.println("sueldo: " + sueldo);
        System.out.println("bonificacion: " + calcularBonificacion());
    }
}
```

validacion paso 1:

crea empleado.java en netbeans
nota que los atributos son protected para que las subclases puedan acceder
compila con f9 y verifica sin errores

### paso 2: crear clase docente

archivo docente.java

```java
public class Docente extends Empleado {

    private String titulo;
    private int horasClase;

    public Docente() {
        super();
    }

    public Docente(String rut, String nombre, int edad, double sueldo, String titulo, int horasClase) {
        super(rut, nombre, edad, sueldo);
        this.titulo = titulo;
        this.horasClase = horasClase;
    }

    public String getTitulo() {
        return titulo;
    }

    public void setTitulo(String titulo) {
        this.titulo = titulo;
    }

    public int getHorasClase() {
        return horasClase;
    }

    public void setHorasClase(int horasClase) {
        this.horasClase = horasClase;
    }

    @Override
    public double calcularBonificacion() {
        return sueldo * 0.15 + horasClase * 5000;
    }

    @Override
    public void mostrarInfo() {
        super.mostrarInfo();
        System.out.println("titulo: " + titulo);
        System.out.println("horas clase: " + horasClase);
    }
}
```

validacion paso 2:

crea docente.java que extiende empleado
nota como super llama al constructor de empleado
nota como calcular bonificacion sobrescribe el metodo de empleado
compila con f9

### paso 3: crear clase administrativo

archivo administrativo.java

```java
public class Administrativo extends Empleado {

    private String area;
    private String cargo;

    public Administrativo() {
        super();
    }

    public Administrativo(String rut, String nombre, int edad, double sueldo, String area, String cargo) {
        super(rut, nombre, edad, sueldo);
        this.area = area;
        this.cargo = cargo;
    }

    public String getArea() {
        return area;
    }

    public void setArea(String area) {
        this.area = area;
    }

    public String getCargo() {
        return cargo;
    }

    public void setCargo(String cargo) {
        this.cargo = cargo;
    }

    @Override
    public double calcularBonificacion() {
        if (cargo.equals("jefe")) {
            return sueldo * 0.20;
        } else {
            return sueldo * 0.10;
        }
    }

    @Override
    public void mostrarInfo() {
        super.mostrarInfo();
        System.out.println("area: " + area);
        System.out.println("cargo: " + cargo);
    }
}
```

validacion paso 3:

crea administrativo.java que extiende empleado
nota la logica diferente en calcular bonificacion segun el cargo
compila con f9

### paso 4: crear clase de prueba

archivo testempleados.java

```java
public class TestEmpleados {

    public static void main(String[] args) {

        Docente d1 = new Docente("11111111-1", "carlos lopez", 45, 1200000, "ingeniero", 20);

        System.out.println("datos del docente:");
        d1.mostrarInfo();

        System.out.println();

        Administrativo a1 = new Administrativo("22222222-2", "ana martinez", 32, 800000, "recursos humanos", "jefe");

        System.out.println("datos del administrativo:");
        a1.mostrarInfo();

        System.out.println();

        Empleado e1 = new Empleado("33333333-3", "pedro gonzalez", 28, 600000);

        System.out.println("datos del empleado:");
        e1.mostrarInfo();
    }
}
```

validacion paso 4:

paso 1: crea testempleados.java con el metodo main
paso 2: ejecuta con f6
paso 3: observa en consola la salida

salida esperada:

```
datos del docente:
rut: 11111111-1
nombre: carlos lopez
edad: 45
sueldo: 1200000.0
bonificacion: 280000.0
titulo: ingeniero
horas clase: 20

datos del administrativo:
rut: 22222222-2
nombre: ana martinez
edad: 32
sueldo: 800000.0
bonificacion: 160000.0
area: recursos humanos
cargo: jefe

datos del empleado:
rut: 33333333-3
nombre: pedro gonzalez
edad: 28
sueldo: 600000.0
bonificacion: 60000.0
```

paso 4: nota como cada clase calcula su bonificacion diferente
paso 5: nota como docente y administrativo muestran informacion adicional
paso 6: nota como todos reutilizan el codigo base de empleado

## problemas comunes y sus soluciones

### problema 1: constructor no encuentra superclase

codigo que falla:

```java
public class Persona {

    private String nombre;

    public Persona(String nombre) {
        this.nombre = nombre;
    }
}
```

```java
public class Empleado extends Persona {

    private String cargo;

    public Empleado(String cargo) {
        this.cargo = cargo;
    }
}
```

error en consola:

```
constructor persona in class persona cannot be applied to given types
```

por que falla: empleado debe llamar al constructor de persona con super pero no lo hace. java busca un constructor sin parametros en persona y no existe.

solucion:

```java
public class Empleado extends Persona {

    private String cargo;

    public Empleado(String nombre, String cargo) {
        super(nombre);
        this.cargo = cargo;
    }
}
```

regla de oro: siempre llama a super como primera linea del constructor de la subclase.

### problema 2: acceder a atributos private de la superclase

codigo que falla:

```java
public class Persona {

    private String rut;

    public Persona(String rut) {
        this.rut = rut;
    }
}
```

```java
public class Empleado extends Persona {

    public Empleado(String rut) {
        super(rut);
    }

    public void mostrarRut() {
        System.out.println(rut);
    }
}
```

error en consola:

```
rut has private access in persona
```

por que falla: rut es private en persona. los atributos private no se heredan ni son accesibles desde subclases.

solucion opcion 1: usar protected

```java
public class Persona {

    protected String rut;
}
```

solucion opcion 2: usar getter

```java
public class Empleado extends Persona {

    public void mostrarRut() {
        System.out.println(getRut());
    }
}
```

### problema 3: olvidar override al sobrescribir

codigo que falla silenciosamente:

```java
public class Animal {

    public void hacerSonido() {
        System.out.println("sonido generico");
    }
}
```

```java
public class Perro extends Animal {

    public void hacersonido() {
        System.out.println("guau");
    }
}
```

```java
Animal a = new Perro();
a.hacerSonido();
```

salida incorrecta:
```
sonido generico
```

por que falla: escribiste hacersonido en minuscula en vez de hacerSonido. java piensa que es un metodo nuevo no una sobrescritura.

solucion usar override:

```java
public class Perro extends Animal {

    @Override
    public void hacerSonido() {
        System.out.println("guau");
    }
}
```

si te equivocas en el nombre con override java da error de compilacion inmediatamente.

### problema 4: modificador de acceso mas restrictivo

codigo que falla:

```java
public class Persona {

    public void saludar() {
        System.out.println("hola");
    }
}
```

```java
public class Empleado extends Persona {

    @Override
    private void saludar() {
        System.out.println("hola soy empleado");
    }
}
```

error en consola:

```
saludar in empleado cannot override saludar in persona
attempting to assign weaker access privileges
```

por que falla: no puedes hacer un metodo mas restrictivo al sobrescribir. persona.saludar es public entonces empleado.saludar debe ser public tambien.

solucion:

```java
public class Empleado extends Persona {

    @Override
    public void saludar() {
        System.out.println("hola soy empleado");
    }
}
```

regla: al sobrescribir puedes hacer el metodo menos restrictivo pero nunca mas restrictivo.

orden de menos a mas restrictivo: public protected private

## ejercicio practico completo: sistema de vehiculos

vamos a crear un sistema para una empresa de alquiler de vehiculos.

tiempo estimado: 90 minutos

requisitos del sistema:

1. clase base vehiculo con marca modelo año y preciodia
2. clase auto que hereda de vehiculo con cantidadpuertas y tipocombustible
3. clase moto que hereda de vehiculo con cilindrada y tienemaleta
4. metodo calcularalquiler que calcula el precio total segun dias
5. auto cobra 10 porciento extra si es diesel
6. moto cobra 5000 menos por dia si no tiene maleta

### paso 1: crear clase vehiculo

archivo vehiculo.java

```java
public class Vehiculo {

    protected String marca;
    protected String modelo;
    protected int ano;
    protected double precioDia;

    public Vehiculo() {
    }

    public Vehiculo(String marca, String modelo, int ano, double precioDia) {
        this.marca = marca;
        this.modelo = modelo;
        this.ano = ano;
        this.precioDia = precioDia;
    }

    public String getMarca() {
        return marca;
    }

    public void setMarca(String marca) {
        this.marca = marca;
    }

    public String getModelo() {
        return modelo;
    }

    public void setModelo(String modelo) {
        this.modelo = modelo;
    }

    public int getAno() {
        return ano;
    }

    public void setAno(int ano) {
        this.ano = ano;
    }

    public double getPrecioDia() {
        return precioDia;
    }

    public void setPrecioDia(double precioDia) {
        this.precioDia = precioDia;
    }

    public double calcularAlquiler(int dias) {
        return precioDia * dias;
    }

    public void mostrarInfo() {
        System.out.println("marca: " + marca);
        System.out.println("modelo: " + modelo);
        System.out.println("ano: " + ano);
        System.out.println("precio dia: " + precioDia);
    }
}
```

### paso 2: crear clase auto

archivo auto.java

```java
public class Auto extends Vehiculo {

    private int cantidadPuertas;
    private String tipoCombustible;

    public Auto() {
        super();
    }

    public Auto(String marca, String modelo, int ano, double precioDia, int cantidadPuertas, String tipoCombustible) {
        super(marca, modelo, ano, precioDia);
        this.cantidadPuertas = cantidadPuertas;
        this.tipoCombustible = tipoCombustible;
    }

    public int getCantidadPuertas() {
        return cantidadPuertas;
    }

    public void setCantidadPuertas(int cantidadPuertas) {
        this.cantidadPuertas = cantidadPuertas;
    }

    public String getTipoCombustible() {
        return tipoCombustible;
    }

    public void setTipoCombustible(String tipoCombustible) {
        this.tipoCombustible = tipoCombustible;
    }

    @Override
    public double calcularAlquiler(int dias) {
        double total = super.calcularAlquiler(dias);
        if (tipoCombustible.equals("diesel")) {
            total = total * 1.10;
        }
        return total;
    }

    @Override
    public void mostrarInfo() {
        super.mostrarInfo();
        System.out.println("cantidad puertas: " + cantidadPuertas);
        System.out.println("tipo combustible: " + tipoCombustible);
    }
}
```

### paso 3: crear clase moto

archivo moto.java

```java
public class Moto extends Vehiculo {

    private int cilindrada;
    private boolean tieneMaleta;

    public Moto() {
        super();
    }

    public Moto(String marca, String modelo, int ano, double precioDia, int cilindrada, boolean tieneMaleta) {
        super(marca, modelo, ano, precioDia);
        this.cilindrada = cilindrada;
        this.tieneMaleta = tieneMaleta;
    }

    public int getCilindrada() {
        return cilindrada;
    }

    public void setCilindrada(int cilindrada) {
        this.cilindrada = cilindrada;
    }

    public boolean getTieneMaleta() {
        return tieneMaleta;
    }

    public void setTieneMaleta(boolean tieneMaleta) {
        this.tieneMaleta = tieneMaleta;
    }

    @Override
    public double calcularAlquiler(int dias) {
        double precioPorDia = precioDia;
        if (!tieneMaleta) {
            precioPorDia = precioPorDia - 5000;
        }
        return precioPorDia * dias;
    }

    @Override
    public void mostrarInfo() {
        super.mostrarInfo();
        System.out.println("cilindrada: " + cilindrada);
        System.out.println("tiene maleta: " + (tieneMaleta ? "si" : "no"));
    }
}
```

### paso 4: crear clase de prueba

archivo testvehiculos.java

```java
public class TestVehiculos {

    public static void main(String[] args) {

        Auto a1 = new Auto("toyota", "corolla", 2023, 35000, 4, "bencina");
        Auto a2 = new Auto("nissan", "navara", 2022, 45000, 4, "diesel");

        Moto m1 = new Moto("yamaha", "mt-07", 2024, 25000, 689, true);
        Moto m2 = new Moto("honda", "wave", 2023, 15000, 110, false);

        int dias = 5;

        System.out.println("auto 1:");
        a1.mostrarInfo();
        System.out.println("alquiler " + dias + " dias: " + a1.calcularAlquiler(dias));

        System.out.println();

        System.out.println("auto 2:");
        a2.mostrarInfo();
        System.out.println("alquiler " + dias + " dias: " + a2.calcularAlquiler(dias));

        System.out.println();

        System.out.println("moto 1:");
        m1.mostrarInfo();
        System.out.println("alquiler " + dias + " dias: " + m1.calcularAlquiler(dias));

        System.out.println();

        System.out.println("moto 2:");
        m2.mostrarInfo();
        System.out.println("alquiler " + dias + " dias: " + m2.calcularAlquiler(dias));
    }
}
```

### validacion completa del ejercicio

paso 1: crea los 4 archivos en netbeans

paso 2: compila cada archivo con f9

paso 3: ejecuta testvehiculos con f6

paso 4: observa la consola debe mostrar:

```
auto 1:
marca: toyota
modelo: corolla
ano: 2023
precio dia: 35000.0
cantidad puertas: 4
tipo combustible: bencina
alquiler 5 dias: 175000.0

auto 2:
marca: nissan
modelo: navara
ano: 2022
precio dia: 45000.0
cantidad puertas: 4
tipo combustible: diesel
alquiler 5 dias: 247500.0

moto 1:
marca: yamaha
modelo: mt-07
ano: 2024
precio dia: 25000.0
cilindrada: 689
tiene maleta: si
alquiler 5 dias: 125000.0

moto 2:
marca: honda
modelo: wave
ano: 2023
precio dia: 15000.0
cilindrada: 110
tiene maleta: no
alquiler 5 dias: 50000.0
```

paso 5: verifica que el auto diesel cobra 10 porciento extra: 45000 por 5 igual 225000 mas 10 porciento igual 247500

paso 6: verifica que la moto sin maleta cobra 5000 menos por dia: 15000 menos 5000 igual 10000 por 5 dias igual 50000

paso 7: verifica que el auto bencina y la moto con maleta no tienen recargos ni descuentos

## resumen de lo aprendido

primero: herencia permite reutilizar codigo de una clase padre en clases hijas

segundo: usa extends para crear herencia entre clases

tercero: relacion es un identifica herencia. relacion tiene un identifica composicion

cuarto: super llama al constructor o metodos de la superclase

quinto: override sobrescribe metodos. overload sobrecarga metodos

sexto: protected permite que subclases accedan a atributos de la superclase

septimo: los constructores no se heredan pero se deben llamar con super

archivos necesarios para el proyecto empleados:
empleado.java
docente.java
administrativo.java
testempleados.java

total: 4 archivos

mantenibilidad: alta porque cambios en empleado afectan automaticamente a docente y administrativo

empresas que usan herencia: google con android, apple con ios, microsoft con windows, oracle con java, amazon con aws

estadisticas: 95 porciento de codigo profesional java usa herencia. reduce tiempo de desarrollo en 40 porciento. reduce bugs en 30 porciento segun estudios de oracle.

proximos pasos: practica con polimorfismo para usar objetos de diferentes tipos de manera uniforme y aprende sobre clases abstractas que definen contratos para las subclases.

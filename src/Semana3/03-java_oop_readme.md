# Java Fundamentals - README 3
## Programacion Orientada a Objetos (POO)

> **Requisitos**: Java JDK 11 o superior
> 
> **IDE Esencial**: NetBeans con refactoring tools y debugging
>
> **Setup Avanzado**: Ver `netbeans_setup.md` para debugging, refactoring y UML tools
>
> **Prerrequisitos**: Haber completado README 1 (Variables) y README 2 (Funciones/Arrays)

### Objetivos de Aprendizajje
Al completar esta guia, seras capaz de:
- Entender los conceptos fundamentales de POO
- Crear clases y objetos en Java
- Aplicar encapsulacion con modificadores de acceso
- Implementar herencia entre claases
- Usar polimorfismo de manera efectiva
- Crear jerarquias de clases complejas
- Combinar todos estos conceptos en proyectos reales

---

## 1. Conceptos Basicos de POO

### 1.1 Que es la Programacion Orientada a Objetos?

La **POO** es un paradigma de programacion que organiza el codigo en **clases** y **objetos**, modelando entidades del mundo real con sus **atributos** (caracteristicas) y **metodos** (accciones).

**Conceptos fundamentales:**
- **Clase**: Es como un "molde" o "plantilla" que define las caracteristicas y comportamientos
- **Objeto**: Es una "instancia" especifica de una claase
- **Atributos**: Variables que representan las caracteristicas del objeto
- **Metodos**: Funciones que definen lo que puede hacer el objeto

### 1.2 Primera Clase - Persona

```java
// Definimos una clase llamada Persona
public class Persona {
    
    // ATRIBUTOS (características de una persona)
    private String nombre;          // El nombre de la persona
    private int edad;              // La edad de la persona
    private double altura;         // La altura en metros
    private String nacionalidad;   // País de origen
    
    // CONSTRUCTOR: método especial que se ejecuta al crear el objeto
    public Persona(String nombre, int edad, double altura, String nacionalidad) {
        this.nombre = nombre;           // 'this' se refiere al objeto actual
        this.edad = edad;              // Asignamos el parámetro al atributo
        this.altura = altura;          // del objeto
        this.nacionalidad = nacionalidad;
    }
    
    // MÉTODOS GETTER: permiten acceder a los atributos privados
    public String getNombre() {
        return this.nombre;            // Retornamos el nombre del objeto
    }
    
    public int getEdad() {
        return this.edad;              // Retornamos la edad del objeto
    }
    
    public double getAltura() {
        return this.altura;            // Retornamos la altura del objeto
    }
    
    public String getNacionalidad() {
        return this.nacionalidad;      // Retornamos la nacionalidad del objeto
    }
    
    // MÉTODOS SETTER: permiten modificar los atributos privados
    public void setNombre(String nuevoNombre) {
        this.nombre = nuevoNombre;     // Cambiamos el nombre del objeto
    }
    
    public void setEdad(int nuevaEdad) {
        if (nuevaEdad >= 0 && nuevaEdad <= 150) {  // Validación: edad debe ser realista
            this.edad = nuevaEdad;     // Solo cambiamos si la edad es válida
        } else {
            System.out.println("Edad inválida. Debe estar entre 0 y 150 años");
        }
    }
    
    public void setAltura(double nuevaAltura) {
        if (nuevaAltura > 0.3 && nuevaAltura < 3.0) {  // Validación: altura realista
            this.altura = nuevaAltura; // Solo cambiamos si la altura es válida
        } else {
            System.out.println("Altura inválida. Debe estar entre 0.3 y 3.0 metros");
        }
    }
    
    // MÉTODOS DE COMPORTAMIENTO: definen lo que puede hacer la persona
    public void saludar() {
        System.out.println("¡Hola! Mi nombre es " + this.nombre);
        System.out.println("Tengo " + this.edad + " años y soy de " + this.nacionalidad);
    }
    
    public void caminar() {
        System.out.println(this.nombre + " está caminando... ");
    }
    
    public boolean esMayorDeEdad() {
        return this.edad >= 18;        // Retorna true si es mayor de 18, false si no
    }
    
    public String obtenerCategoriaPorEdad() {
        if (this.edad < 13) {
            return "Niño/a";
        } else if (this.edad < 20) {
            return "Adolescente";
        } else if (this.edad < 60) {
            return "Adulto/a";
        } else {
            return "Adulto/a Mayor";
        }
    }
    
    // Método toString: define cómo se muestra el objeto como texto
    @Override
    public String toString() {
        return "Persona{" +
                "nombre='" + nombre + '\'' +
                ", edad=" + edad +
                ", altura=" + altura + "m" +
                ", nacionalidad='" + nacionalidad + '\'' +
                ", categoría='" + obtenerCategoriaPorEdad() + '\'' +
                '}';
    }
}

// Clase principal para probar nuestra clase Persona
public class TestPersona {
    public static void main(String[] args) {
        System.out.println("=== CREANDO OBJETOS PERSONA ===");
        
        // CREAMOS OBJETOS (instancias de la clase Persona)
        Persona persona1 = new Persona("Ana García", 25, 1.65, "Chile");
        Persona persona2 = new Persona("Juan Pérez", 17, 1.78, "Argentina");
        Persona persona3 = new Persona("María López", 45, 1.60, "México");
        
        // USAMOS LOS MÉTODOS DE LOS OBJETOS
        System.out.println("\n--- Saludos ---");
        persona1.saludar();              // Ana se presenta
        System.out.println();
        persona2.saludar();              // Juan se presenta
        
        System.out.println("\n--- Verificando mayoría de edad ---");
        System.out.println(persona1.getNombre() + " es mayor de edad: " + persona1.esMayorDeEdad());
        System.out.println(persona2.getNombre() + " es mayor de edad: " + persona2.esMayorDeEdad());
        
        System.out.println("\n--- Categorías por edad ---");
        System.out.println(persona1.getNombre() + " es: " + persona1.obtenerCategoriaPorEdad());
        System.out.println(persona2.getNombre() + " es: " + persona2.obtenerCategoriaPorEdad());
        System.out.println(persona3.getNombre() + " es: " + persona3.obtenerCategoriaPorEdad());
        
        System.out.println("\n--- Modificando atributos ---");
        persona2.setEdad(18);            // Juan cumple años
        System.out.println("Juan ahora tiene " + persona2.getEdad() + " años");
        System.out.println("¿Juan es mayor de edad ahora? " + persona2.esMayorDeEdad());
        
        System.out.println("\n--- Información completa ---");
        System.out.println(persona1);   // Automáticamente usa toString()
        System.out.println(persona2);
        System.out.println(persona3);
    }
}
```

---

## 2. Encapsulacion

### 2.1 ¿Qué es la Encapsulación?

La **encapsulación** es el principio de ocultar los detalles internos de una clase y controlar el acceso a sus atributos mediante métodos públicos (getters/setters).

**Modificadores de acceso:**
- `private`: Solo accesible desde la misma clase
- `public`: Accesible desde cualquier lugar
- `protected`: Accesible desde la misma clase, subclases y mismo paquete

### 2.2 Ejemplo Práctico - Cuenta Bancaria

```java
public class CuentaBancaria {
    
    // ATRIBUTOS PRIVADOS (encapsulados)
    private String numeroCuenta;       // Número de cuenta (no debe cambiar)
    private String titular;            // Nombre del titular
    private double saldo;             // Dinero disponible (debe protegerse)
    private String tipoCuenta;        // Tipo: "Ahorros", "Corriente", etc.
    private boolean cuentaActiva;     // Estado de la cuenta
    
    // CONSTRUCTOR
    public CuentaBancaria(String numeroCuenta, String titular, String tipoCuenta) {
        this.numeroCuenta = numeroCuenta;
        this.titular = titular;
        this.saldo = 0.0;                    // Nueva cuenta empieza con $0
        this.tipoCuenta = tipoCuenta;
        this.cuentaActiva = true;            // Cuenta activa por defecto
        
        System.out.println("Cuenta creada exitosamente para " + titular);
    }
    
    // GETTERS (solo lectura para algunos atributos críticos)
    public String getNumeroCuenta() {
        return this.numeroCuenta;            // El número no se puede cambiar
    }
    
    public String getTitular() {
        return this.titular;
    }
    
    public double getSaldo() {
        if (!this.cuentaActiva) {           // Solo mostramos saldo si cuenta está activa
            System.out.println("Cuenta inactiva. No se puede consultar saldo");
            return 0.0;
        }
        return this.saldo;
    }
    
    public String getTipoCuenta() {
        return this.tipoCuenta;
    }
    
    public boolean isCuentaActiva() {
        return this.cuentaActiva;
    }
    
    // SETTERS (con validaciones)
    public void setTitular(String nuevoTitular) {
        if (nuevoTitular != null && !nuevoTitular.trim().isEmpty()) {
            this.titular = nuevoTitular;
            System.out.println("Titular actualizado a: " + nuevoTitular);
        } else {
            System.out.println("Nombre de titular inválido");
        }
    }
    
    // MÉTODOS DE NEGOCIO (lógica específica del dominio)
    public boolean depositar(double cantidad) {
        if (!this.cuentaActiva) {           // Verificamos que la cuenta esté activa
            System.out.println("No se puede depositar en cuenta inactiva");
            return false;
        }
        
        if (cantidad <= 0) {                // Validamos que la cantidad sea positiva
            System.out.println("La cantidad debe ser mayor a $0");
            return false;
        }
        
        this.saldo += cantidad;             // Aumentamos el saldo
        System.out.println("Depósito exitoso de $" + cantidad);
        System.out.println("Nuevo saldo: $" + this.saldo);
        return true;
    }
    
    public boolean retirar(double cantidad) {
        if (!this.cuentaActiva) {           // Verificamos que la cuenta esté activa
            System.out.println("No se puede retirar de cuenta inactiva");
            return false;
        }
        
        if (cantidad <= 0) {                // Validamos cantidad positiva
            System.out.println("La cantidad debe ser mayor a $0");
            return false;
        }
        
        if (cantidad > this.saldo) {        // Verificamos fondos suficientes
            System.out.println("Fondos insuficientes. Saldo actual: $" + this.saldo);
            return false;
        }
        
        this.saldo -= cantidad;             // Reducimos el saldo
        System.out.println("Retiro exitoso de $" + cantidad);
        System.out.println("Nuevo saldo: $" + this.saldo);
        return true;
    }
    
    public boolean transferir(CuentaBancaria cuentaDestino, double cantidad) {
        if (this.retirar(cantidad)) {       // Si podemos retirar de esta cuenta
            if (cuentaDestino.depositar(cantidad)) {  // Y depositar en la otra
                System.out.println("Transferencia exitosa a " + cuentaDestino.getTitular());
                return true;
            } else {
                // Si no se pudo depositar, devolvemos el dinero
                this.depositar(cantidad);
                System.out.println("Error en transferencia. Dinero devuelto");
            }
        }
        return false;
    }
    
    public void desactivarCuenta() {
        this.cuentaActiva = false;
        System.out.println("Cuenta desactivada para " + this.titular);
    }
    
    public void activarCuenta() {
        this.cuentaActiva = true;
        System.out.println("Cuenta activada para " + this.titular);
    }
    
    public void mostrarResumen() {
        System.out.println("\n=== RESUMEN DE CUENTA ===");
        System.out.println("Número: " + this.numeroCuenta);
        System.out.println("Titular: " + this.titular);
        System.out.println("Tipo: " + this.tipoCuenta);
        System.out.println("Saldo: $" + (this.cuentaActiva ? this.saldo : "***"));
        System.out.println("Estado: " + (this.cuentaActiva ? "Activa" : "Inactiva"));
        System.out.println("========================");
    }
}

// Clase para probar la encapsulación
public class TestCuentaBancaria {
    public static void main(String[] args) {
        System.out.println("=== SISTEMA BANCARIO CON ENCAPSULACIÓN ===");
        
        // Creamos cuentas bancarias
        CuentaBancaria cuenta1 = new CuentaBancaria("001-12345", "Ana García", "Ahorros");
        CuentaBancaria cuenta2 = new CuentaBancaria("001-67890", "Juan Pérez", "Corriente");
        
        System.out.println("\n--- Operaciones Básicas ---");
        // Depositamos dinero
        cuenta1.depositar(1000.0);
        cuenta2.depositar(500.0);
        
        // Intentamos retirar
        cuenta1.retirar(300.0);          // Debe funcionar
        cuenta2.retirar(600.0);          // No debe funcionar (fondos insuficientes)
        
        // Transferencia entre cuentas
        System.out.println("\n--- Transferencia ---");
        cuenta1.transferir(cuenta2, 200.0);
        
        // Mostramos resúmenes
        System.out.println("\n--- Resúmenes Finales ---");
        cuenta1.mostrarResumen();
        cuenta2.mostrarResumen();
        
        // Probamos desactivar cuenta
        System.out.println("\n--- Desactivando Cuenta ---");
        cuenta1.desactivarCuenta();
        cuenta1.retirar(100.0);          // No debe funcionar
        cuenta1.mostrarResumen();        // Saldo oculto
        
        // Reactivamos
        cuenta1.activarCuenta();
        cuenta1.mostrarResumen();        // Saldo visible de nuevo
    }
}
```

---

## 3. Herencia

### 3.1 ¿Qué es la Herencia?

La **herencia** permite crear nuevas clases basadas en clases existentes, heredando sus atributos y métodos. La clase original se llama **clase padre (superclase)** y la nueva clase se llama **clase hija (subclase)**.

### 3.2 Jerarquía de Empleados

```java
// CLASE PADRE (Superclase)
public class Empleado {
    
    // ATRIBUTOS PROTEGIDOS (accesibles por las subclases)
    protected String nombre;           // Nombre del empleado
    protected String apellido;         // Apellido del empleado
    protected int id;                  // ID único del empleado
    protected double salarioBase;      // Salario base mensual
    protected String departamento;     // Departamento donde trabaja
    protected int añosExperiencia;     // Años de experiencia laboral
    
    // CONSTRUCTOR DE LA CLASE PADRE
    public Empleado(String nombre, String apellido, int id, double salarioBase, String departamento) {
        this.nombre = nombre;
        this.apellido = apellido;
        this.id = id;
        this.salarioBase = salarioBase;
        this.departamento = departamento;
        this.añosExperiencia = 0;          // Comienza sin experiencia
        
        System.out.println("Empleado creado: " + this.nombre + " " + this.apellido);
    }
    
    // GETTERS Y SETTERS
    public String getNombre() {
        return this.nombre;
    }
    
    public String getApellido() {
        return this.apellido;
    }
    
    public String getNombreCompleto() {
        return this.nombre + " " + this.apellido;
    }
    
    public int getId() {
        return this.id;
    }
    
    public double getSalarioBase() {
        return this.salarioBase;
    }
    
    public void setSalarioBase(double nuevoSalario) {
        if (nuevoSalario > 0) {
            this.salarioBase = nuevoSalario;
            System.out.println("Salario actualizado para " + getNombreCompleto());
        }
    }
    
    public String getDepartamento() {
        return this.departamento;
    }
    
    public int getAñosExperiencia() {
        return this.añosExperiencia;
    }
    
    public void setAñosExperiencia(int años) {
        if (años >= 0) {
            this.añosExperiencia = años;
        }
    }
    
    // MÉTODOS QUE PUEDEN SER HEREDADOS
    public void trabajar() {
        System.out.println(getNombreCompleto() + " está trabajando en " + this.departamento);
    }
    
    public void tomarDescanso() {
        System.out.println(getNombreCompleto() + " está tomando un descanso");
    }
    
    // MÉTODO QUE PUEDE SER SOBREESCRITO (OVERRIDE)
    public double calcularSalarioMensual() {
        // Salario base + bono por experiencia (2% por año)
        double bonoExperiencia = this.salarioBase * (this.añosExperiencia * 0.02);
        return this.salarioBase + bonoExperiencia;
    }
    
    // MÉTODO QUE PUEDE SER SOBREESCRITO
    public void mostrarInformacion() {
        System.out.println("\n=== INFORMACIÓN DEL EMPLEADO ===");
        System.out.println("Nombre: " + getNombreCompleto());
        System.out.println("ID: " + this.id);
        System.out.println("Departamento: " + this.departamento);
        System.out.println("Salario Base: $" + this.salarioBase);
        System.out.println("Años de Experiencia: " + this.añosExperiencia);
        System.out.println("Salario Mensual: $" + calcularSalarioMensual());
        System.out.println("===============================");
    }
}

// PRIMERA CLASE HIJA - Desarrollador
public class Desarrollador extends Empleado {  // 'extends' establece la herencia
    
    // ATRIBUTOS ESPECÍFICOS DEL DESARROLLADOR
    private String lenguajePrincipal;          // Lenguaje de programación principal
    private int proyectosCompletados;          // Número de proyectos terminados
    private String nivel;                      // Junior, Semi-Senior, Senior
    
    // CONSTRUCTOR DE LA CLASE HIJA
    public Desarrollador(String nombre, String apellido, int id, double salarioBase, 
                        String lenguajePrincipal, String nivel) {
        
        // LLAMAMOS AL CONSTRUCTOR DEL PADRE con 'super'
        super(nombre, apellido, id, salarioBase, "Desarrollo");  // Departamento fijo
        
        // Inicializamos atributos específicos de esta clase
        this.lenguajePrincipal = lenguajePrincipal;
        this.nivel = nivel;
        this.proyectosCompletados = 0;
        
        System.out.println("Desarrollador especializado en " + lenguajePrincipal + " registrado");
    }
    
    // GETTERS Y SETTERS ESPECÍFICOS
    public String getLenguajePrincipal() {
        return this.lenguajePrincipal;
    }
    
    public void setLenguajePrincipal(String nuevoLenguaje) {
        this.lenguajePrincipal = nuevoLenguaje;
        System.out.println(getNombreCompleto() + " ahora se especializa en " + nuevoLenguaje);
    }
    
    public int getProyectosCompletados() {
        return this.proyectosCompletados;
    }
    
    public String getNivel() {
        return this.nivel;
    }
    
    public void setNivel(String nuevoNivel) {
        this.nivel = nuevoNivel;
        System.out.println("" + getNombreCompleto() + " promovido a " + nuevoNivel);
    }
    
    // MÉTODOS ESPECÍFICOS DEL DESARROLLADOR
    public void programar() {
        System.out.println(getNombreCompleto() + " está programando en " + this.lenguajePrincipal + " ");
    }
    
    public void completarProyecto() {
        this.proyectosCompletados++;
        System.out.println("" + getNombreCompleto() + " completó un proyecto!");
        System.out.println("Total de proyectos completados: " + this.proyectosCompletados);
        
        // Auto-promoción basada en proyectos completados
        if (this.proyectosCompletados >= 5 && this.nivel.equals("Junior")) {
            setNivel("Semi-Senior");
        } else if (this.proyectosCompletados >= 10 && this.nivel.equals("Semi-Senior")) {
            setNivel("Senior");
        }
    }
    
    public void debuggear() {
        System.out.println(getNombreCompleto() + " está solucionando bugs ");
    }
    
    // SOBREESCRIBIMOS (OVERRIDE) el método del padre
    @Override
    public double calcularSalarioMensual() {
        // Empezamos con el cálculo del padre
        double salarioBase = super.calcularSalarioMensual();  // 'super' llama al método del padre
        
        // Agregamos bonos específicos para desarrolladores
        double bonoNivel = 0;
        switch (this.nivel) {
            case "Junior":
                bonoNivel = 0;              // Sin bono adicional
                break;
            case "Semi-Senior":
                bonoNivel = salarioBase * 0.15;  // 15% adicional
                break;
            case "Senior":
                bonoNivel = salarioBase * 0.30;  // 30% adicional
                break;
        }
        
        // Bono por proyectos completados (1% por proyecto)
        double bonoProyectos = this.salarioBase * (this.proyectosCompletados * 0.01);
        
        return salarioBase + bonoNivel + bonoProyectos;
    }
    
    // SOBREESCRIBIMOS el método de información
    @Override
    public void mostrarInformacion() {
        super.mostrarInformacion();         // Mostramos la información básica del padre
        
        // Agregamos información específica del desarrollador
        System.out.println("INFORMACIÓN ESPECÍFICA DEL DESARROLLADOR:");
        System.out.println("Lenguaje Principal: " + this.lenguajePrincipal);
        System.out.println("Nivel: " + this.nivel);
        System.out.println("Proyectos Completados: " + this.proyectosCompletados);
        System.out.println("===========================================");
    }
}

// SEGUNDA CLASE HIJA - Gerente
public class Gerente extends Empleado {
    
    // ATRIBUTOS ESPECÍFICOS DEL GERENTE
    private int equipoSize;                    // Número de personas a cargo
    private double presupuestoAnual;          // Presupuesto que maneja
    private String tipoGerencia;              // "Proyecto", "Departamento", "Regional"
    
    // CONSTRUCTOR
    public Gerente(String nombre, String apellido, int id, double salarioBase, 
                   String departamento, String tipoGerencia) {
        
        super(nombre, apellido, id, salarioBase, departamento);  // Llamamos al padre
        
        this.tipoGerencia = tipoGerencia;
        this.equipoSize = 0;                  // Comienza sin equipo
        this.presupuestoAnual = 0.0;         // Sin presupuesto inicial
        
        System.out.println("Gerente de " + tipoGerencia + " registrado");
    }
    
    // GETTERS Y SETTERS
    public int getEquipoSize() {
        return this.equipoSize;
    }
    
    public void setEquipoSize(int nuevoSize) {
        if (nuevoSize >= 0) {
            this.equipoSize = nuevoSize;
            System.out.println(getNombreCompleto() + " ahora maneja un equipo de " + nuevoSize + " personas");
        }
    }
    
    public double getPresupuestoAnual() {
        return this.presupuestoAnual;
    }
    
    public void setPresupuestoAnual(double presupuesto) {
        if (presupuesto >= 0) {
            this.presupuestoAnual = presupuesto;
            System.out.println(getNombreCompleto() + " maneja un presupuesto de $" + presupuesto);
        }
    }
    
    public String getTipoGerencia() {
        return this.tipoGerencia;
    }
    
    // MÉTODOS ESPECÍFICOS DEL GERENTE
    public void dirigirReunion() {
        System.out.println(getNombreCompleto() + " está dirigiendo una reunión con " + this.equipoSize + " personas ");
    }
    
    public void aprobarPresupuesto(double cantidad) {
        if (cantidad <= this.presupuestoAnual) {
            System.out.println("" + getNombreCompleto() + " aprobó un presupuesto de $" + cantidad);
        } else {
            System.out.println("" + getNombreCompleto() + " no puede aprobar $" + cantidad + 
                             " (excede presupuesto disponible: $" + this.presupuestoAnual + ")");
        }
    }
    
    public void evaluarEmpleado(Empleado empleado) {
        System.out.println(getNombreCompleto() + " está evaluando a " + empleado.getNombreCompleto() + " ");
    }
    
    // SOBREESCRIBIMOS el cálculo de salario
    @Override
    public double calcularSalarioMensual() {
        double salarioBase = super.calcularSalarioMensual();
        
        // Bono por tamaño del equipo (5% por cada persona a cargo)
        double bonoEquipo = this.salarioBase * (this.equipoSize * 0.05);
        
        // Bono por presupuesto manejado (0.1% del presupuesto anual / 12 meses)
        double bonoPresupuesto = (this.presupuestoAnual * 0.001) / 12;
        
        return salarioBase + bonoEquipo + bonoPresupuesto;
    }
    
    // SOBREESCRIBIMOS la información
    @Override
    public void mostrarInformacion() {
        super.mostrarInformacion();
        
        System.out.println("INFORMACIÓN ESPECÍFICA DEL GERENTE:");
        System.out.println("Tipo de Gerencia: " + this.tipoGerencia);
        System.out.println("Tamaño del Equipo: " + this.equipoSize + " personas");
        System.out.println("Presupuesto Anual: $" + this.presupuestoAnual);
        System.out.println("=======================================");
    }
}

// Clase para probar la herencia
public class TestHerencia {
    public static void main(String[] args) {
        System.out.println("=== SISTEMA DE EMPLEADOS CON HERENCIA ===");
        
        // Creamos empleados de diferentes tipos
        Empleado empleado1 = new Empleado("Carlos", "Martínez", 1001, 50000, "Recursos Humanos");
        Desarrollador dev1 = new Desarrollador("Ana", "García", 1002, 60000, "Java", "Junior");
        Gerente gerente1 = new Gerente("Luis", "Rodríguez", 1003, 80000, "Desarrollo", "Departamento");
        
        System.out.println("\n=== CONFIGURACIÓN INICIAL ===");
        
        // Configuramos el desarrollador
        dev1.setAñosExperiencia(2);
        dev1.completarProyecto();      // Completa algunos proyectos
        dev1.completarProyecto();
        dev1.completarProyecto();
        
        // Configuramos el gerente
        gerente1.setEquipoSize(8);
        gerente1.setPresupuestoAnual(500000);
        gerente1.setAñosExperiencia(7);
        
        System.out.println("\n=== ACTIVIDADES LABORALES ===");
        
        // Todos pueden trabajar (método heredado)
        empleado1.trabajar();
        dev1.trabajar();
        gerente1.trabajar();
        
        System.out.println();
        
        // Actividades específicas de cada tipo
        dev1.programar();
        dev1.debuggear();
        gerente1.dirigirReunion();
        gerente1.aprobarPresupuesto(50000);
        gerente1.evaluarEmpleado(dev1);
        
        System.out.println("\n=== INFORMACIÓN DETALLADA ===");
        
        // Mostramos información de todos (cada uno usa su versión del método)
        empleado1.mostrarInformacion();
        dev1.mostrarInformacion();
        gerente1.mostrarInformacion();
        
        System.out.println("\n=== SIMULACIÓN DE CRECIMIENTO ===");
        
        // El desarrollador completa más proyectos
        for (int i = 0; i < 7; i++) {
            dev1.completarProyecto();
        }
        
        System.out.println("\nInformación actualizada del desarrollador:");
        dev1.mostrarInformacion();
    }
}
```

---

## 4. Polimorfismo

### 4.1 ¿Qué es el Polimorfismo?

El **polimorfismo** permite que objetos de diferentes clases respondan al mismo método de manera diferente. Es la capacidad de un objeto de tomar múltiples formas.

### 4.2 Sistema de Formas Geométricas

```java
// CLASE PADRE ABSTRACTA
public abstract class Forma {
    
    // ATRIBUTOS COMUNES
    protected String color;            // Color de la forma
    protected double x, y;            // Posición en el plano
    
    // CONSTRUCTOR
    public Forma(String color, double x, double y) {
        this.color = color;
        this.x = x;
        this.y = y;
    }
    
    // GETTERS Y SETTERS
    public String getColor() {
        return this.color;
    }
    
    public void setColor(String nuevoColor) {
        this.color = nuevoColor;
        System.out.println("Color cambiado a: " + nuevoColor);
    }
    
    public double getX() {
        return this.x;
    }
    
    public double getY() {
        return this.y;
    }
    
    public void mover(double nuevaX, double nuevaY) {
        this.x = nuevaX;
        this.y = nuevaY;
        System.out.println("Forma movida a posición (" + nuevaX + ", " + nuevaY + ")");
    }
    
    // MÉTODOS CONCRETOS (implementación común)
    public void mostrarPosicion() {
        System.out.println("Posición: (" + this.x + ", " + this.y + ")");
    }
    
    // MÉTODOS ABSTRACTOS (deben ser implementados por las subclases)
    public abstract double calcularArea();      // Cada forma calcula su área diferente
    public abstract double calcularPerimetro(); // Cada forma calcula su perímetro diferente
    public abstract void dibujar();            // Cada forma se dibuja diferente
    
    // MÉTODO QUE USA POLIMORFISMO
    public void mostrarInformacionCompleta() {
        System.out.println("\n=== INFORMACIÓN DE LA FORMA ===");
        System.out.println("Tipo: " + this.getClass().getSimpleName());  // Obtiene el nombre de la clase
        System.out.println("Color: " + this.color);
        mostrarPosicion();
        System.out.println("Área: " + calcularArea());         // Llama al método específico de cada subclase
        System.out.println("Perímetro: " + calcularPerimetro()); // Polimorfismo en acción
        System.out.println("============================");
        dibujar();                                             // Cada forma se dibuja diferente
    }
}

// PRIMERA CLASE HIJA - Rectángulo
public class Rectangulo extends Forma {
    
    // ATRIBUTOS ESPECÍFICOS
    private double ancho;              // Ancho del rectángulo
    private double alto;               // Alto del rectángulo
    
    // CONSTRUCTOR
    public Rectangulo(String color, double x, double y, double ancho, double alto) {
        super(color, x, y);            // Llamamos al constructor del padre
        this.ancho = ancho;
        this.alto = alto;
    }
    
    // GETTERS Y SETTERS
    public double getAncho() {
        return this.ancho;
    }
    
    public void setAncho(double nuevoAncho) {
        if (nuevoAncho > 0) {
            this.ancho = nuevoAncho;
            System.out.println("Ancho del rectángulo actualizado: " + nuevoAncho);
        }
    }
    
    public double getAlto() {
        return this.alto;
    }
    
    public void setAlto(double nuevoAlto) {
        if (nuevoAlto > 0) {
            this.alto = nuevoAlto;
            System.out.println("Alto del rectángulo actualizado: " + nuevoAlto);
        }
    }
    
    // IMPLEMENTACIÓN DE MÉTODOS ABSTRACTOS
    @Override
    public double calcularArea() {
        return this.ancho * this.alto;  // Fórmula: ancho × alto
    }
    
    @Override
    public double calcularPerimetro() {
        return 2 * (this.ancho + this.alto);  // Fórmula: 2 × (ancho + alto)
    }
    
    @Override
    public void dibujar() {
        System.out.println("Dibujando rectángulo " + this.color + ":");
        // Dibujamos un rectángulo simple con caracteres
        for (int i = 0; i < 3; i++) {
            if (i == 0 || i == 2) {
                System.out.println("*".repeat(8));    // Bordes superior e inferior
            } else {
                System.out.println("*      *");       // Bordes laterales
            }
        }
    }
    
    // MÉTODOS ESPECÍFICOS
    public boolean esCuadrado() {
        return this.ancho == this.alto;  // Es cuadrado si ancho = alto
    }
}

// SEGUNDA CLASE HIJA - Círculo
public class Circulo extends Forma {
    
    // ATRIBUTO ESPECÍFICO
    private double radio;              // Radio del círculo
    
    // CONSTRUCTOR
    public Circulo(String color, double x, double y, double radio) {
        super(color, x, y);
        this.radio = radio;
    }
    
    // GETTERS Y SETTERS
    public double getRadio() {
        return this.radio;
    }
    
    public void setRadio(double nuevoRadio) {
        if (nuevoRadio > 0) {
            this.radio = nuevoRadio;
            System.out.println("Radio del círculo actualizado: " + nuevoRadio);
        }
    }
    
    // IMPLEMENTACIÓN DE MÉTODOS ABSTRACTOS
    @Override
    public double calcularArea() {
        return Math.PI * this.radio * this.radio;  // Fórmula: π × r²
    }
    
    @Override
    public double calcularPerimetro() {
        return 2 * Math.PI * this.radio;           // Fórmula: 2 × π × r
    }
    
    @Override
    public void dibujar() {
        System.out.println("Dibujando círculo " + this.color + ":");
        System.out.println("   ***   ");
        System.out.println(" *     * ");
        System.out.println("*       *");
        System.out.println(" *     * ");
        System.out.println("   ***   ");
    }
    
    // MÉTODOS ESPECÍFICOS
    public double calcularDiametro() {
        return this.radio * 2;
    }
}

// TERCERA CLASE HIJA - Triángulo
public class Triangulo extends Forma {
    
    // ATRIBUTOS ESPECÍFICOS
    private double base;               // Base del triángulo
    private double altura;             // Altura del triángulo
    private double lado1, lado2, lado3; // Los tres lados
    
    // CONSTRUCTOR
    public Triangulo(String color, double x, double y, double base, double altura, 
                    double lado1, double lado2, double lado3) {
        super(color, x, y);
        this.base = base;
        this.altura = altura;
        this.lado1 = lado1;
        this.lado2 = lado2;
        this.lado3 = lado3;
    }
    
    // GETTERS
    public double getBase() {
        return this.base;
    }
    
    public double getAltura() {
        return this.altura;
    }
    
    // IMPLEMENTACIÓN DE MÉTODOS ABSTRACTOS
    @Override
    public double calcularArea() {
        return (this.base * this.altura) / 2;  // Fórmula: (base × altura) / 2
    }
    
    @Override
    public double calcularPerimetro() {
        return this.lado1 + this.lado2 + this.lado3;  // Suma de los tres lados
    }
    
    @Override
    public void dibujar() {
        System.out.println("Dibujando triángulo " + this.color + ":");
        System.out.println("    *    ");
        System.out.println("   * *   ");
        System.out.println("  *   *  ");
        System.out.println(" *     * ");
        System.out.println("*********");
    }
    
    // MÉTODOS ESPECÍFICOS
    public String getTipoTriangulo() {
        if (lado1 == lado2 && lado2 == lado3) {
            return "Equilátero";
        } else if (lado1 == lado2 || lado2 == lado3 || lado1 == lado3) {
            return "Isósceles";
        } else {
            return "Escaleno";
        }
    }
}

// Clase que demuestra el polimorfismo
public class TestPolimorfismo {
    
    // MÉTODO QUE DEMUESTRA POLIMORFISMO
    // Recibe cualquier tipo de Forma, pero cada una se comporta diferente
    public static void procesarForma(Forma forma) {
        System.out.println("\n Procesando forma...");
        forma.mostrarInformacionCompleta();     // Cada forma muestra info diferente
        
        // Verificamos el tipo específico si necesitamos funcionalidad extra
        if (forma instanceof Rectangulo) {      // instanceof verifica el tipo
            Rectangulo rect = (Rectangulo) forma;  // Casting a tipo específico
            System.out.println("¿Es cuadrado? " + rect.esCuadrado());
        } else if (forma instanceof Circulo) {
            Circulo circ = (Circulo) forma;
            System.out.println("Diámetro: " + circ.calcularDiametro());
        } else if (forma instanceof Triangulo) {
            Triangulo tri = (Triangulo) forma;
            System.out.println("Tipo: " + tri.getTipoTriangulo());
        }
    }
    
    // MÉTODO QUE COMPARA ÁREAS (polimorfismo puro)
    public static void compararAreas(Forma forma1, Forma forma2) {
        System.out.println("\nCOMPARANDO ÁREAS:");
        
        double area1 = forma1.calcularArea();   // Polimorfismo: cada forma calcula diferente
        double area2 = forma2.calcularArea();
        
        System.out.println(forma1.getClass().getSimpleName() + " " + forma1.getColor() + 
                          " tiene área: " + String.format("%.2f", area1));
        System.out.println(forma2.getClass().getSimpleName() + " " + forma2.getColor() + 
                          " tiene área: " + String.format("%.2f", area2));
        
        if (area1 > area2) {
            System.out.println("La primera forma es más grande");
        } else if (area2 > area1) {
            System.out.println("La segunda forma es más grande");
        } else {
            System.out.println("Ambas formas tienen la misma área");
        }
    }
    
    // MÉTODO QUE PROCESA UN ARRAY DE FORMAS (polimorfismo con colecciones)
    public static void procesarFormas(Forma[] formas) {
        System.out.println("\n PROCESANDO MÚLTIPLES FORMAS:");
        
        double areaTotal = 0;
        double perimetroTotal = 0;
        
        for (int i = 0; i < formas.length; i++) {
            Forma forma = formas[i];
            
            System.out.println((i + 1) + ". " + forma.getClass().getSimpleName() + 
                             " " + forma.getColor());
            
            double area = forma.calcularArea();          // Polimorfismo
            double perimetro = forma.calcularPerimetro(); // Polimorfismo
            
            System.out.println("   Área: " + String.format("%.2f", area));
            System.out.println("   Perímetro: " + String.format("%.2f", perimetro));
            
            areaTotal += area;
            perimetroTotal += perimetro;
        }
        
        System.out.println("\nTOTALES:");
        System.out.println("Área total: " + String.format("%.2f", areaTotal));
        System.out.println("Perímetro total: " + String.format("%.2f", perimetroTotal));
        System.out.println("Promedio de área: " + String.format("%.2f", areaTotal / formas.length));
    }
    
    public static void main(String[] args) {
        System.out.println("=== DEMOSTRACIÓN DE POLIMORFISMO ===");
        
        // CREAMOS DIFERENTES FORMAS
        Rectangulo rect = new Rectangulo("Azul", 0, 0, 5, 3);
        Circulo circ = new Circulo("Rojo", 10, 10, 4);
        Triangulo tri = new Triangulo("Verde", 5, 5, 6, 4, 5, 5, 6);
        
        System.out.println("\n=== POLIMORFISMO CON MÉTODOS ===");
        
        // POLIMORFISMO: el mismo método funciona con diferentes tipos
        procesarForma(rect);        // Se comporta como Rectangulo
        procesarForma(circ);        // Se comporta como Círculo
        procesarForma(tri);         // Se comporta como Triángulo
        
        // COMPARAMOS ÁREAS (polimorfismo puro)
        compararAreas(rect, circ);
        compararAreas(circ, tri);
        
        System.out.println("\n=== POLIMORFISMO CON ARRAYS ===");
        
        // POLIMORFISMO CON COLECCIONES
        // Un array de Forma puede contener cualquier subclase
        Forma[] formas = {rect, circ, tri, 
                         new Rectangulo("Amarillo", 0, 0, 2, 2),
                         new Circulo("Morado", 0, 0, 3)};
        
        procesarFormas(formas);     // Procesa todas, cada una con su comportamiento
        
        System.out.println("\n=== DEMOSTRACIÓN VISUAL ===");
        
        // Todas las formas se dibujan diferente (polimorfismo visual)
        for (Forma forma : formas) {
            forma.dibujar();         // Polimorfismo: cada una se dibuja diferente
            System.out.println();
        }
        
        System.out.println("Demostración de polimorfismo completada");
    }
}
```

---

## 5. Proyecto Integrador - Sistema de Vehiculos

```java
// CLASE PADRE ABSTRACTA
public abstract class Vehiculo {
    
    // ATRIBUTOS PROTEGIDOS
    protected String marca;            // Marca del vehículo
    protected String modelo;           // Modelo específico
    protected int año;                 // Año de fabricación
    protected String color;            // Color del vehículo
    protected double precio;           // Precio de venta
    protected int kilometraje;         // Kilómetros recorridos
    protected boolean enMovimiento;    // Estado actual
    
    // CONSTRUCTOR
    public Vehiculo(String marca, String modelo, int año, String color, double precio) {
        this.marca = marca;
        this.modelo = modelo;
        this.año = año;
        this.color = color;
        this.precio = precio;
        this.kilometraje = 0;          // Nuevo vehículo sin kilometraje
        this.enMovimiento = false;     // Inicialmente detenido
        
        System.out.println("Vehículo registrado: " + marca + " " + modelo + " (" + año + ")");
    }
    
    // GETTERS Y SETTERS
    public String getMarca() {
        return this.marca;
    }
    
    public String getModelo() {
        return this.modelo;
    }
    
    public String getNombreCompleto() {
        return this.marca + " " + this.modelo + " " + this.año;
    }
    
    public int getAño() {
        return this.año;
    }
    
    public String getColor() {
        return this.color;
    }
    
    public void setColor(String nuevoColor) {
        this.color = nuevoColor;
        System.out.println("" + getNombreCompleto() + " pintado de color " + nuevoColor);
    }
    
    public double getPrecio() {
        return this.precio;
    }
    
    public void setPrecio(double nuevoPrecio) {
        if (nuevoPrecio > 0) {
            this.precio = nuevoPrecio;
            System.out.println("Precio actualizado: $" + nuevoPrecio);
        }
    }
    
    public int getKilometraje() {
        return this.kilometraje;
    }
    
    public boolean isEnMovimiento() {
        return this.enMovimiento;
    }
    
    // MÉTODOS COMUNES (concretos)
    public void encender() {
        if (!this.enMovimiento) {
            System.out.println("" + getNombreCompleto() + " encendido");
        } else {
            System.out.println("El vehículo ya está encendido");
        }
    }
    
    public void apagar() {
        if (this.enMovimiento) {
            this.enMovimiento = false;
            System.out.println("" + getNombreCompleto() + " apagado");
        } else {
            System.out.println("El vehículo ya está apagado");
        }
    }
    
    public void manejar(int kilometros) {
        if (kilometros > 0) {
            this.kilometraje += kilometros;
            System.out.println("Manejando " + kilometros + "km. Kilometraje total: " + this.kilometraje + "km");
        }
    }
    
    public double calcularDepreciacion() {
        int edad = 2024 - this.año;
        double factorDepreciacion = edad * 0.05;  // 5% por año
        return this.precio * (1 - Math.min(factorDepreciacion, 0.7));  // Máximo 70% depreciación
    }
    
    // MÉTODOS ABSTRACTOS (deben implementarse en subclases)
    public abstract void acelerar();
    public abstract void frenar();
    public abstract double calcularConsumo();
    public abstract String getTipo();
    
    // MÉTODO QUE USA POLIMORFISMO
    public void mostrarInformacionCompleta() {
        System.out.println("\n=== INFORMACIÓN DEL VEHÍCULO ===");
        System.out.println("Tipo: " + getTipo());          // Polimorfismo
        System.out.println("Marca: " + this.marca);
        System.out.println("Modelo: " + this.modelo);
        System.out.println("Año: " + this.año);
        System.out.println("Color: " + this.color);
        System.out.println("Precio original: $" + this.precio);
        System.out.println("Valor actual: $" + String.format("%.2f", calcularDepreciacion()));
        System.out.println("Kilometraje: " + this.kilometraje + "km");
        System.out.println("Consumo: " + String.format("%.2f", calcularConsumo()) + " L/100km");
        System.out.println("Estado: " + (this.enMovimiento ? "En movimiento" : "Detenido"));
        System.out.println("===============================");
    }
}

// PRIMERA SUBCLASE - Auto
public class Auto extends Vehiculo {
    
    // ATRIBUTOS ESPECÍFICOS
    private int numPuertas;            // Número de puertas
    private String tipoTransmision;    // "Manual" o "Automática"
    private boolean tieneAireAcondicionado;
    private double tamañoMotor;        // En litros
    
    // CONSTRUCTOR
    public Auto(String marca, String modelo, int año, String color, double precio,
               int numPuertas, String tipoTransmision, double tamañoMotor) {
        
        super(marca, modelo, año, color, precio);  // Llamamos al constructor padre
        
        this.numPuertas = numPuertas;
        this.tipoTransmision = tipoTransmision;
        this.tieneAireAcondicionado = true;        // Por defecto tiene A/C
        this.tamañoMotor = tamañoMotor;
        
        System.out.println("Auto de " + numPuertas + " puertas con transmisión " + tipoTransmision + " registrado");
    }
    
    // GETTERS Y SETTERS
    public int getNumPuertas() {
        return this.numPuertas;
    }
    
    public String getTipoTransmision() {
        return this.tipoTransmision;
    }
    
    public boolean isTieneAireAcondicionado() {
        return this.tieneAireAcondicionado;
    }
    
    public void setAireAcondicionado(boolean tiene) {
        this.tieneAireAcondicionado = tiene;
        System.out.println("❄️  Aire acondicionado " + (tiene ? "activado" : "desactivado"));
    }
    
    public double getTamañoMotor() {
        return this.tamañoMotor;
    }
    
    // IMPLEMENTACIÓN DE MÉTODOS ABSTRACTOS
    @Override
    public void acelerar() {
        if (!this.enMovimiento) {
            this.enMovimiento = true;
        }
        System.out.println("" + getNombreCompleto() + " acelerando suavemente por la ciudad");
    }
    
    @Override
    public void frenar() {
        if (this.enMovimiento) {
            System.out.println("" + getNombreCompleto() + " frenando con sistema ABS");
        }
    }
    
    @Override
    public double calcularConsumo() {
        // Consumo base según tamaño del motor
        double consumoBase = this.tamañoMotor * 6;  // 6L por litro de motor por 100km
        
        // Ajustes según características
        if (this.tipoTransmision.equals("Automática")) {
            consumoBase += 1.5;  // Automática consume más
        }
        if (this.tieneAireAcondicionado) {
            consumoBase += 1.0;  // A/C consume más
        }
        
        return consumoBase;
    }
    
    @Override
    public String getTipo() {
        return "Automóvil";
    }
    
    // MÉTODOS ESPECÍFICOS
    public void abrirPuertas() {
        System.out.println("Abriendo las " + this.numPuertas + " puertas del auto");
    }
    
    public void activarAlarma() {
        System.out.println("Alarma del auto activada");
    }
    
    public void cambiarMarcha(int marcha) {
        if (this.tipoTransmision.equals("Manual")) {
            System.out.println("Cambiando a marcha " + marcha);
        } else {
            System.out.println("Transmisión automática ajustando marcha automáticamente");
        }
    }
}

// SEGUNDA SUBCLASE - Motocicleta
public class Motocicleta extends Vehiculo {
    
    // ATRIBUTOS ESPECÍFICOS
    private int cilindrada;            // CC del motor
    private String tipoMoto;           // "Deportiva", "Cruiser", "Touring", etc.
    private boolean tieneMaletas;      // Si tiene compartimientos de carga
    private int numRuedas;            // Generalmente 2, pero pueden ser 3
    
    // CONSTRUCTOR
    public Motocicleta(String marca, String modelo, int año, String color, double precio,
                      int cilindrada, String tipoMoto) {
        
        super(marca, modelo, año, color, precio);
        
        this.cilindrada = cilindrada;
        this.tipoMoto = tipoMoto;
        this.tieneMaletas = false;     // Por defecto sin maletas
        this.numRuedas = 2;           // Por defecto 2 ruedas
        
        System.out.println("Motocicleta " + tipoMoto + " de " + cilindrada + "cc registrada");
    }
    
    // GETTERS Y SETTERS
    public int getCilindrada() {
        return this.cilindrada;
    }
    
    public String getTipoMoto() {
        return this.tipoMoto;
    }
    
    public boolean isTieneMaletas() {
        return this.tieneMaletas;
    }
    
    public void setMaletas(boolean tiene) {
        this.tieneMaletas = tiene;
        System.out.println("👜 Maletas " + (tiene ? "instaladas" : "removidas"));
    }
    
    public int getNumRuedas() {
        return this.numRuedas;
    }
    
    // IMPLEMENTACIÓN DE MÉTODOS ABSTRACTOS
    @Override
    public void acelerar() {
        if (!this.enMovimiento) {
            this.enMovimiento = true;
        }
        System.out.println("" + getNombreCompleto() + " acelerando con potencia y agilidad");
    }
    
    @Override
    public void frenar() {
        if (this.enMovimiento) {
            System.out.println("" + getNombreCompleto() + " frenando con sistema combinado");
        }
    }
    
    @Override
    public double calcularConsumo() {
        // Consumo base según cilindrada
        double consumoBase = this.cilindrada / 200.0;  // Fórmula simplificada
        
        // Ajustes según tipo
        switch (this.tipoMoto) {
            case "Deportiva":
                consumoBase += 2.0;  // Deportivas consumen más
                break;
            case "Cruiser":
                consumoBase += 1.0;  // Cruisers consumen moderado
                break;
            case "Scooter":
                consumoBase -= 1.0;  // Scooters son más eficientes
                break;
        }
        
        return Math.max(consumoBase, 2.0);  // Mínimo 2L/100km
    }
    
    @Override
    public String getTipo() {
        return "Motocicleta " + this.tipoMoto;
    }
    
    // MÉTODOS ESPECÍFICOS
    public void hacerWillie() {
        if (this.enMovimiento && this.cilindrada > 250) {
            System.out.println("" + getNombreCompleto() + " haciendo willie! (¡Con cuidado!)");
        } else if (this.cilindrada <= 250) {
            System.out.println("Esta moto no tiene suficiente potencia para willie");
        } else {
            System.out.println("La moto debe estar en movimiento");
        }
    }
    
    public void revisarCadena() {
        System.out.println("Revisando la cadena de transmisión de la motocicleta");
    }
    
    public void ponerseCasco() {
        System.out.println("¡Recuerda siempre usar casco al manejar motocicleta!");
    }
}

// TERCERA SUBCLASE - Camion
public class Camion extends Vehiculo {
    
    // ATRIBUTOS ESPECÍFICOS
    private double capacidadCarga;     // Toneladas que puede cargar
    private int numEjes;              // Número de ejes
    private String tipoCamion;        // "Reparto", "Carga pesada", "Volteo", etc.
    private boolean tieneRemolque;    // Si tiene remolque acoplado
    private double cargaActual;       // Carga actual en toneladas
    
    // CONSTRUCTOR
    public Camion(String marca, String modelo, int año, String color, double precio,
                 double capacidadCarga, String tipoCamion) {
        
        super(marca, modelo, año, color, precio);
        
        this.capacidadCarga = capacidadCarga;
        this.tipoCamion = tipoCamion;
        this.numEjes = capacidadCarga <= 5 ? 2 : 3;  // 2 ejes para hasta 5 ton, 3 para más
        this.tieneRemolque = false;
        this.cargaActual = 0.0;
        
        System.out.println("Camión " + tipoCamion + " con capacidad de " + capacidadCarga + " toneladas registrado");
    }
    
    // GETTERS Y SETTERS
    public double getCapacidadCarga() {
        return this.capacidadCarga;
    }
    
    public String getTipoCamion() {
        return this.tipoCamion;
    }
    
    public int getNumEjes() {
        return this.numEjes;
    }
    
    public boolean isTieneRemolque() {
        return this.tieneRemolque;
    }
    
    public void setRemolque(boolean tiene) {
        this.tieneRemolque = tiene;
        if (tiene) {
            this.capacidadCarga *= 1.5;  // Remolque aumenta capacidad 50%
        } else {
            this.capacidadCarga /= 1.5;  // Removemos el aumento
        }
        System.out.println("Remolque " + (tiene ? "acoplado" : "desacoplado") + 
                          ". Nueva capacidad: " + this.capacidadCarga + " toneladas");
    }
    
    public double getCargaActual() {
        return this.cargaActual;
    }
    
    // IMPLEMENTACIÓN DE MÉTODOS ABSTRACTOS
    @Override
    public void acelerar() {
        if (!this.enMovimiento) {
            this.enMovimiento = true;
        }
        String mensaje = "" + getNombreCompleto() + " acelerando gradualmente";
        if (this.cargaActual > 0) {
            mensaje += " (con " + this.cargaActual + " toneladas de carga)";
        }
        System.out.println(mensaje);
    }
    
    @Override
    public void frenar() {
        if (this.enMovimiento) {
            String mensaje = "" + getNombreCompleto() + " frenando con sistema neumático";
            if (this.cargaActual > this.capacidadCarga * 0.8) {
                mensaje += " (distancia de frenado extendida por carga pesada)";
            }
            System.out.println(mensaje);
        }
    }
    
    @Override
    public double calcularConsumo() {
        // Consumo base alto para camiones
        double consumoBase = 25.0;  // 25L/100km base
        
        // Aumenta con la carga
        double factorCarga = (this.cargaActual / this.capacidadCarga) * 10;  // Hasta 10L más
        
        // Tipo de camión afecta consumo
        switch (this.tipoCamion) {
            case "Reparto":
                consumoBase += 0;    // Consumo estándar
                break;
            case "Carga pesada":
                consumoBase += 8;    // Mayor consumo
                break;
            case "Volteo":
                consumoBase += 5;    // Consumo medio-alto
                break;
        }
        
        if (this.tieneRemolque) {
            consumoBase += 10;       // Remolque aumenta mucho el consumo
        }
        
        return consumoBase + factorCarga;
    }
    
    @Override
    public String getTipo() {
        return "Camión " + this.tipoCamion;
    }
    
    // MÉTODOS ESPECÍFICOS
    public boolean cargar(double toneladas) {
        if (toneladas <= 0) {
            System.out.println("La cantidad debe ser positiva");
            return false;
        }
        
        if (this.cargaActual + toneladas > this.capacidadCarga) {
            System.out.println("Excede la capacidad. Disponible: " + 
                             (this.capacidadCarga - this.cargaActual) + " toneladas");
            return false;
        }
        
        this.cargaActual += toneladas;
        System.out.println("Cargado " + toneladas + " toneladas. " + 
                          "Carga actual: " + this.cargaActual + "/" + this.capacidadCarga + " toneladas");
        return true;
    }
    
    public boolean descargar(double toneladas) {
        if (toneladas <= 0) {
            System.out.println("La cantidad debe ser positiva");
            return false;
        }
        
        if (toneladas > this.cargaActual) {
            System.out.println("No hay suficiente carga. Actual: " + this.cargaActual + " toneladas");
            return false;
        }
        
        this.cargaActual -= toneladas;
        System.out.println("Descargado " + toneladas + " toneladas. " + 
                          "Carga restante: " + this.cargaActual + " toneladas");
        return true;
    }
    
    public void descargarCompleto() {
        if (this.cargaActual > 0) {
            System.out.println("Descargando completamente: " + this.cargaActual + " toneladas");
            this.cargaActual = 0.0;
        } else {
            System.out.println("El camión ya está vacío");
        }
    }
    
    public double getPorcentajeCarga() {
        return (this.cargaActual / this.capacidadCarga) * 100;
    }
}

// CLASE DE GESTIÓN DEL PARQUE VEHICULAR
public class ParqueVehicular {
    
    private Vehiculo[] vehiculos;      // Array de vehículos
    private int contadorVehiculos;     // Contador actual
    private final int CAPACIDAD_MAXIMA = 50;  // Capacidad máxima del parque
    
    // CONSTRUCTOR
    public ParqueVehicular() {
        this.vehiculos = new Vehiculo[CAPACIDAD_MAXIMA];
        this.contadorVehiculos = 0;
        System.out.println("Parque vehicular creado con capacidad para " + CAPACIDAD_MAXIMA + " vehículos");
    }
    
    // MÉTODO PARA AGREGAR VEHÍCULO (polimorfismo)
    public boolean agregarVehiculo(Vehiculo vehiculo) {
        if (this.contadorVehiculos >= CAPACIDAD_MAXIMA) {
            System.out.println("Parque vehicular lleno");
            return false;
        }
        
        this.vehiculos[this.contadorVehiculos] = vehiculo;
        this.contadorVehiculos++;
        System.out.println("Vehículo agregado al parque. Total: " + this.contadorVehiculos);
        return true;
    }
    
    // MÉTODO QUE DEMUESTRA POLIMORFISMO
    public void mostrarTodosLosVehiculos() {
        System.out.println("\n=== INVENTARIO COMPLETO DEL PARQUE VEHICULAR ===");
        
        if (this.contadorVehiculos == 0) {
            System.out.println("No hay vehículos en el parque");
            return;
        }
        
        for (int i = 0; i < this.contadorVehiculos; i++) {
            System.out.println("\n--- Vehículo #" + (i + 1) + " ---");
            this.vehiculos[i].mostrarInformacionCompleta();  // Polimorfismo: cada uno muestra info diferente
        }
    }
    
    // SIMULACIÓN DE MANEJO (polimorfismo puro)
    public void simularManejo() {
        System.out.println("\n🚦 SIMULACIÓN DE MANEJO DE TODOS LOS VEHÍCULOS:");
        
        for (int i = 0; i < this.contadorVehiculos; i++) {
            Vehiculo v = this.vehiculos[i];
            
            System.out.println("\n--- " + v.getNombreCompleto() + " ---");
            v.encender();
            v.acelerar();            // Polimorfismo: cada vehículo acelera diferente
            v.manejar(50);           // Todos manejan 50km
            v.frenar();              // Polimorfismo: cada vehículo frena diferente
            v.apagar();
            
            // Acciones específicas según el tipo (instanceof + casting)
            if (v instanceof Auto) {
                Auto auto = (Auto) v;
                auto.abrirPuertas();
            } else if (v instanceof Motocicleta) {
                Motocicleta moto = (Motocicleta) v;
                moto.ponerseCasco();
            } else if (v instanceof Camion) {
                Camion camion = (Camion) v;
                camion.cargar(2.5);  // Cargamos algo
            }
        }
    }
    
    // ANÁLISIS ECONÓMICO (usando polimorfismo)
    public void analisisEconomico() {
        System.out.println("\nANÁLISIS ECONÓMICO DEL PARQUE VEHICULAR:");
        
        double valorTotal = 0;
        double valorDepreciado = 0;
        double consumoPromedio = 0;
        
        for (int i = 0; i < this.contadorVehiculos; i++) {
            Vehiculo v = this.vehiculos[i];
            
            valorTotal += v.getPrecio();
            valorDepreciado += v.calcularDepreciacion();    // Polimorfismo
            consumoPromedio += v.calcularConsumo();         // Polimorfismo
        }
        
        consumoPromedio /= this.contadorVehiculos;
        
        System.out.println("Valor total original: $" + String.format("%.2f", valorTotal));
        System.out.println("Valor actual depreciado: $" + String.format("%.2f", valorDepreciado));
        System.out.println("Pérdida por depreciación: $" + String.format("%.2f", valorTotal - valorDepreciado));
        System.out.println("Consumo promedio: " + String.format("%.2f", consumoPromedio) + " L/100km");
        
        // Estadísticas por tipo
        System.out.println("\nESTADÍSTICAS POR TIPO:");
        int autos = 0, motos = 0, camiones = 0;
        
        for (int i = 0; i < this.contadorVehiculos; i++) {
            if (this.vehiculos[i] instanceof Auto) autos++;
            else if (this.vehiculos[i] instanceof Motocicleta) motos++;
            else if (this.vehiculos[i] instanceof Camion) camiones++;
        }
        
        System.out.println("Autos: " + autos);
        System.out.println("Motocicletas: " + motos);
        System.out.println("Camiones: " + camiones);
    }
}

// CLASE PRINCIPAL PARA PROBAR TODO EL SISTEMA
public class TestSistemaVehiculos {
    public static void main(String[] args) {
        System.out.println("=== SISTEMA INTEGRAL DE GESTIÓN VEHICULAR ===");
        
        // CREAMOS EL PARQUE VEHICULAR
        ParqueVehicular parque = new ParqueVehicular();
        
        System.out.println("\n=== REGISTRANDO VEHÍCULOS ===");
        
        // CREAMOS DIFERENTES TIPOS DE VEHÍCULOS (polimorfismo desde la creación)
        Auto auto1 = new Auto("Toyota", "Corolla", 2022, "Blanco", 25000, 4, "Automática", 1.8);
        Auto auto2 = new Auto("Honda", "Civic", 2021, "Azul", 23000, 4, "Manual", 2.0);
        
        Motocicleta moto1 = new Motocicleta("Yamaha", "R6", 2023, "Negro", 12000, 600, "Deportiva");
        Motocicleta moto2 = new Motocicleta("Harley-Davidson", "Street 750", 2020, "Rojo", 8000, 750, "Cruiser");
        
        Camion camion1 = new Camion("Volvo", "FH16", 2019, "Verde", 80000, 25, "Carga pesada");
        Camion camion2 = new Camion("Mercedes-Benz", "Actros", 2021, "Amarillo", 75000, 15, "Reparto");
        
        // AGREGAMOS TODOS AL PARQUE (polimorfismo en acción)
        parque.agregarVehiculo(auto1);      // Auto se trata como Vehiculo
        parque.agregarVehiculo(auto2);      // Auto se trata como Vehiculo
        parque.agregarVehiculo(moto1);      // Motocicleta se trata como Vehiculo
        parque.agregarVehiculo(moto2);      // Motocicleta se trata como Vehiculo
        parque.agregarVehiculo(camion1);    // Camion se trata como Vehiculo
        parque.agregarVehiculo(camion2);    // Camion se trata como Vehiculo
        
        System.out.println("\n=== CONFIGURACIONES ESPECÍFICAS ===");
        
        // Configuraciones específicas de cada tipo
        auto1.setAireAcondicionado(true);
        auto2.cambiarMarcha(3);
        
        moto1.ponerseCasco();
        moto2.setMaletas(true);
        
        camion1.setRemolque(true);
        camion1.cargar(20.0);
        camion2.cargar(8.5);
        
        // DEMOSTRACIONES DE POLIMORFISMO
        parque.mostrarTodosLosVehiculos();   // Cada vehículo se muestra diferente
        parque.simularManejo();              // Cada vehículo maneja diferente
        parque.analisisEconomico();          // Cálculos usando polimorfismo
        
        System.out.println("\n=== PRUEBAS ESPECÍFICAS ADICIONALES ===");
        
        // Pruebas específicas que muestran el comportamiento único de cada clase
        System.out.println("\n--- Pruebas de Auto ---");
        auto1.activarAlarma();
        auto1.abrirPuertas();
        
        System.out.println("\n--- Pruebas de Motocicleta ---");
        moto1.hacerWillie();
        moto2.revisarCadena();
        
        System.out.println("\n--- Pruebas de Camión ---");
        System.out.println("Porcentaje de carga del camión 1: " + 
                          String.format("%.1f", camion1.getPorcentajeCarga()) + "%");
        camion2.descargarCompleto();
        
        System.out.println("\nDEMOSTRACIÓN COMPLETA DEL SISTEMA TERMINADA");
        System.out.println("Polimorfismo, herencia y encapsulación funcionando en conjunto!");
    }
}
```

---

## 7. Ejercicios Practicos

### Ejercicio 1: Sistema de Empleados Expandido
Expande el sistema de empleados agregando:
- Clase `Vendedor` con comisiones y metas
- Clase `Técnico` con certificaciones y herramientas
- Método polimórfico `calcularBonificacion()`

### Ejercicio 2: Biblioteca Digital
Crea un sistema con:
- Clase abstracta `Material` (libros, revistas, DVDs)
- Subclases específicas con atributos únicos
- Métodos polimórficos para calcular multas
- Sistema de préstamos con diferentes políticas

### Ejercicio 3: Tienda de Mascotas
Diseña un sistema con:
- Clase base `Mascota` 
- Subclases `Perro`, `Gato`, `Ave`
- Diferentes métodos de alimentación y cuidado
- Sistema de adopción con requisitos específicos

---

## 8. Conceptos Clave y Buenas Practicas

### 8.1 Los 4 Pilares de la POO
1. **Encapsulación** Oculta los detalles internos y controla el acceso
2. **Herencia** Reutiliza código creando jerarquías de clases
3. **Polimorfismo** Un mismo método se comporta diferente según el objeto
4. **Abstracción** Modela conceptos del mundo real simplificando la complejidad

### 8.2 Cuándo Usar Cada Concepto

**Encapsulación:**
- Siempre usa atributos `private` 
- Proporciona `getters` y `setters` con validaciones
- Protege la integridad de los datos

**Herencia:**
- Usa cuando hay una relación "es un" (Auto **es un** Vehículo)
- No abuses de la herencia (máximo 3-4 niveles)
- Prefiere composición cuando sea más apropiado

**Polimorfismo:**
- Útil para procesar colecciones de objetos diferentes
- Permite código flexible y extensible
- Usa `instanceof` y casting cuando necesites funcionalidad específica

### 8.3 Errores Comunes a Evitar
- **No validar en setters**: Siempre valida los datos de entrada
- **Herencia excesiva**: No hagas jerarquías muy profundas
- **No usar super()**: Recuerda llamar al constructor padre
- **Olvidar @Override**: Usa `@Override` para sobreescribir métodos
- **Casting sin verificar**: Usa `instanceof` antes de hacer casting

---

## Resumen y Proximos Pasos

Felicitaciones! Has dominado los conceptos fundamentales de la Programacion Orientada a Objetos en Java:

**Lo que aprendiste:**
- Crear **clases y objetos** con atributos y metodos
- Aplicar **encapsulacion** para proteger datoss
- Implementar **herencia** para reutilizar codigo
- Usar **polimorfismo** para flexibilidad
- Combinar todos estos conceptos en sistemas complejos

**Conceptos Dominados:**
- Constructores y metodos
- Modificadores de acceso (`private`, `public`, `protected`)
- Herencia con `extends` y `super()`
- Polimorfismo con metodos abstractos
- `instanceof` y casting
- Override de metodos

**Siguiente Nivel:**
Con estos fundamentos solidos, estas listo para:
- **Interfaces** y implementacion multiple
- **Clases internas** y anonimas  
- **Generics** para type safety
- **Colecciones** (ArrayList, HashMap)
- **Manejo de excepciones** avnzado
- **Patrones de diseno**

Has completado una base solida en Java! Estos conceptos son la fundacion para convertirte en un desarrollador Java competente.
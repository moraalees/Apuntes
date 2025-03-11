# Apuntes

### 🔹 **Constructores en Kotlin**

En Kotlin, una clase puede tener **un constructor primario** y **uno o más constructores secundarios**.

---

### 📌 **1. Constructor Primario**

Es el constructor principal de una clase y se define en la cabecera. Se usa para inicializar las propiedades de la clase.

**Ejemplo:**

```kotlin
class Persona(val nombre: String, val edad: Int)
```

🔹 Aquí, `nombre` y `edad` son inicializados automáticamente al crear una instancia.

**Uso:**

```kotlin
val persona = Persona("Juan", 25)
println(persona.nombre) // Juan
println(persona.edad)   // 25
```

Si necesitas ejecutar más código en la inicialización, usa `init`:

```kotlin
class Persona(val nombre: String, val edad: Int) {
    init {
        println("Persona creada: $nombre, Edad: $edad")
    }
}
```

---

### 📌 **2. Constructor Secundario**

import java.time.LocalDateTime = Fecha Actual
val fecha: LocalDateTime = LocalDateTime.now()

#### **EJEMPLO DOCUMENTACION**
```
/**
 * Clase abstracta que representa una carta genérica.
 *
 * Esta clase define las propiedades y comportamientos básicos de una carta,
 * y está diseñada para ser heredada por tipos específicos de cartas.
 *
 * @property id Identificador único de la carta.
 * @property nombre Nombre de la carta.
 * @property descripcion Descripción detallada de la carta.
 * @property especialidad Puntos de especialidad de la carta, que pueden representar
 *                        habilidades, poder, o cualquier otro atributo específico.
 *
 * @see Accionable Interface o clase que define acciones que la carta puede realizar.

PARA DESCRIBIR LA CLASE
 */

/**
     * Devuelve una representación en formato de cadena de la carta.
     *
     * Este método sobrescribe la función `toString()` de la clase `Any` para proporcionar
     * una descripción detallada de la carta.
     *
     * @return Una cadena que describe la carta, incluyendo su ID, nombre, descripción y puntos de especialidad.
     */

DESCRIBIR MÉTODO DE LA CLASE
```

Sirve para ofrecer inicializaciones alternativas y se define con `constructor`.

**Ejemplo:**

```kotlin
class Persona {
    var nombre: String
    var edad: Int

    constructor(nombre: String) {
        this.nombre = nombre
        this.edad = 18 // Valor por defecto
    }

    constructor(nombre: String, edad: Int) {
        this.nombre = nombre
        this.edad = edad
    }
}
```

**Uso:**

```kotlin
val p1 = Persona("Ana") // Edad = 18 por defecto
val p2 = Persona("Carlos", 30)
```

---

### 📌 **3. Getters y Setters**

Son funciones que permiten acceder (`get`) y modificar (`set`) propiedades de una clase.

**Por defecto, Kotlin los crea automáticamente:**

```kotlin
class Persona(var nombre: String, var edad: Int)
```

Aquí, `nombre` y `edad` ya tienen **getter y setter** sin necesidad de escribirlos.

🔹 **Getter y Setter personalizados:**

```kotlin
class Persona(var nombre: String, var edad: Int) {
    var dni: String = ""
        get() = field.uppercase() // Getter convierte el dni en mayúsculas
        set(value) {
            if (value.length == 9) field = value // Setter solo permite un DNI válido
        }
}
```

**Uso:**

```kotlin
val persona = Persona("Laura", 25)
persona.dni = "abc123456"
println(persona.dni) // ABC123456
```

---
### Apuntes sobre clases
### 1. Data class[¶](https://revilofe.github.io/section1/u05/teoria/PROG-U5.1.-clasesYobjetos/#1-data-class "Permanent link")

En Kotlin, las `data class` son clases diseñadas para almacenar datos. Se definen con la palabra clave `data` antes del nombre de la clase. Estas clases automáticamente generan métodos útiles como `toString()`, `equals()`, `hashCode()` y `copy()` basados en las propiedades definidas en el constructor primario.

Ejemplo:
```kotlin
data class Persona(val nombre: String, val edad: Int)
````

Este tipo de clase es ideal para representar modelos de datos que necesitan ser comparados o copiados fácilmente.

---

### 2. Sealed classes[¶](https://revilofe.github.io/section1/u05/teoria/PROG-U5.1.-clasesYobjetos/#2-sealed-classes "Permanent link")

Las `sealed classes` (clases selladas) son una forma de restringir la jerarquía de clases. Permiten que una clase tenga un número limitado de subclases, lo que las hace ideales para cuando necesitas representar un conjunto cerrado de tipos posibles. Se definen con la palabra clave `sealed`.

Ejemplo:

```kotlin
sealed class Resultado
data class Exito(val mensaje: String): Resultado()
data class Error(val codigo: Int): Resultado()
```

Esto garantiza que todos los tipos posibles de `Resultado` estén definidos en un solo lugar, facilitando el manejo de casos con `when`.

---

### 3. Generics[¶](https://revilofe.github.io/section1/u05/teoria/PROG-U5.1.-clasesYobjetos/#3-generics "Permanent link")

Los `generics` en Kotlin permiten definir clases, interfaces y funciones con un tipo de parámetro que se especifica en el momento de su uso. Esto permite crear estructuras de datos o funciones reutilizables y tipo-seguras sin perder flexibilidad.

Ejemplo:

```kotlin
class Caja<T>(val valor: T)
fun <T> imprimirValor(valor: T) {
    println(valor)
}
```

En este ejemplo, `T` es un parámetro de tipo genérico que puede ser reemplazado por cualquier tipo al usar la clase o función. Esto mejora la reutilización y la seguridad de tipos sin tener que duplicar código.

### 4. Clases Internamente Agrupadas[¶](https://revilofe.github.io/section1/u05/teoria/PROG-U5.1.-clasesYobjetos/#4-clases-internamente-agrupadas "Permanent link")

Las `nested classes` (clases internas agrupadas) son clases definidas dentro de otra clase. Pueden ser `static` (en Kotlin, esto significa que no mantienen una referencia a la instancia de la clase externa) o pueden ser clases normales que acceden a las propiedades y métodos de la clase externa.

Ejemplo de clase interna estática:
```kotlin
class Contenedor {
    class Caja(val contenido: String)
}
````

Ejemplo de clase interna no estática:

```kotlin
class Contenedor {
    val item = "Artículo"
    inner class Caja(val contenido: String) {
        fun mostrar() = "Item: $item, Contenido: $contenido"
    }
}
```

En este caso, la clase `Caja` tiene acceso a las propiedades de la clase `Contenedor` gracias a la palabra clave `inner`.

---

### 5. Enumeraciones[¶](https://revilofe.github.io/section1/u05/teoria/PROG-U5.1.-clasesYobjetos/#5-enumeraciones "Permanent link")

Las `enumeraciones` (o `enum classes`) son clases especiales que representan un conjunto de constantes relacionadas. Las `enum` en Kotlin permiten asociar comportamientos a los valores de la enumeración, además de ser mucho más flexibles que en otros lenguajes.

Ejemplo:

```kotlin
enum class Dia {
    Lunes, Martes, Miércoles, Jueves, Viernes, Sábado, Domingo
}
```

Puedes agregar propiedades y métodos a una enumeración:

```kotlin
enum class Dia(val esFinDeSemana: Boolean) {
    Lunes(false), Martes(false), Miércoles(false), Jueves(false), Viernes(false), Sábado(true), Domingo(true);

    fun mensaje() = if (esFinDeSemana) "¡Es fin de semana!" else "Es un día laborable"
}
```

---

### 6. Objects[¶](https://revilofe.github.io/section1/u05/teoria/PROG-U5.1.-clasesYobjetos/#6-objects "Permanent link")

El `object` en Kotlin se usa para definir una clase singleton, es decir, una clase que tiene una sola instancia en todo el programa. Además, los `objects` pueden contener propiedades, funciones y constructores.

Ejemplo:

```kotlin
object Configuracion {
    val version = "1.0"
    fun mostrarVersion() {
        println("Versión $version")
    }
}
```

En este caso, `Configuracion` es un singleton, y puedes acceder a sus miembros sin crear una instancia.

---

### 7. Companion objects[¶](https://revilofe.github.io/section1/u05/teoria/PROG-U5.1.-clasesYobjetos/#7-companion-objects "Permanent link")

Los `companion objects` son objetos que están definidos dentro de una clase y actúan como un miembro estático de esa clase, similar a los métodos estáticos en otros lenguajes como Java. La diferencia es que en Kotlin no existen miembros estáticos, pero los `companion objects` cumplen una función similar.

Ejemplo:

```kotlin
class Persona(val nombre: String) {
    companion object {
        const val tipo = "Humano"
        fun crear(nombre: String): Persona = Persona(nombre)
    }
}
```

En este caso, el `companion object` permite acceder a `tipo` y a la función `crear()` sin necesidad de instanciar la clase `Persona`. Se accede usando el nombre de la clase, como `Persona.tipo`.

---

### 1. Visibilidad[¶](https://revilofe.github.io/section1/u05/teoria/PROG-U5.2.-VisibilidadEnClases/#1-visibilidad "Permanent link")
En Kotlin, la visibilidad de clases, funciones y propiedades está definida por modificadores de visibilidad. Los modificadores más comunes son:
- `public`: Visible desde cualquier lugar (por defecto).
- `internal`: Visible solo dentro del módulo (proyecto).
- `protected`: Visible solo dentro de la clase y sus subclases.
- `private`: Visible solo dentro de la clase o archivo donde se define.

Ejemplo:
```kotlin
class Persona {
    public var nombre: String = "Juan"
    private var edad: Int = 30
}

````

---
### 1. Concepto de Herencia[¶](https://revilofe.github.io/section1/u05/teoria/PROG-U5.3.-Herencia/#1-concepto-de-herencia "Permanent link")

La **herencia** es un principio fundamental de la programación orientada a objetos que permite que una clase (subclase) herede propiedades y comportamientos (métodos) de otra clase (superclase). Esto promueve la reutilización del código y la extensión de funcionalidades.

Ejemplo:

```kotlin
open class Animal {
    fun respirar() {
        println("El animal está respirando")
    }
}

class Perro : Animal() {
    fun ladrar() {
        println("El perro está ladrando")
    }
}
```

Aquí, `Perro` hereda el método `respirar()` de `Animal`.

---

### 2. Herencia en Kotlin[¶](https://revilofe.github.io/section1/u05/teoria/PROG-U5.3.-Herencia/#2-herencia-en-kotlin "Permanent link")

En Kotlin, para que una clase pueda ser heredada, debe ser declarada como `open`. Las clases, funciones y propiedades son `final` por defecto, lo que significa que no pueden ser heredadas o sobrescritas, a menos que se marque explícitamente con `open`.

Ejemplo:

```kotlin
open class Vehiculo(val marca: String) {
    open fun conducir() {
        println("Conduciendo el vehículo")
    }
}

class Coche(marca: String, val modelo: String) : Vehiculo(marca) {
    override fun conducir() {
        println("Conduciendo el coche $marca $modelo")
    }
}
```

En este caso, la clase `Vehiculo` se declara como `open`, permitiendo que `Coche` herede de ella y sobrescriba la función `conducir()`.

---

### 3. Sobreescritura[¶](https://revilofe.github.io/section1/u05/teoria/PROG-U5.3.-Herencia/#3-sobreescritura "Permanent link")

La **sobreescritura** es el proceso mediante el cual una subclase proporciona una implementación específica de un método que ya está definido en su superclase. En Kotlin, para sobreescribir un método, la función en la superclase debe ser `open` y la subclase debe usar la palabra clave `override`.

Ejemplo:

```kotlin
open class Animal {
    open fun hacerSonido() {
        println("El animal hace un sonido")
    }
}

class Gato : Animal() {
    override fun hacerSonido() {
        println("El gato maúlla")
    }
}
```

Aquí, `hacerSonido` es sobreescrita en la clase `Gato`, cambiando su comportamiento.

---

### 4. Interfaces[¶](https://revilofe.github.io/section1/u05/teoria/PROG-U5.3.-Herencia/#4-interfaces "Permanent link")

Las **interfaces** en Kotlin son similares a las interfaces en otros lenguajes orientados a objetos. Una interfaz puede contener métodos abstractos y métodos con implementación. Las clases pueden implementar una o varias interfaces.

Ejemplo:

```kotlin
interface Volador {
    fun volar()
}

class Pajaro : Volador {
    override fun volar() {
        println("El pájaro está volando")
    }
}
```

En este caso, la clase `Pajaro` implementa la interfaz `Volador` y proporciona su propia implementación del método `volar()`.

---

### 5. Clases abstractas[¶](https://revilofe.github.io/section1/u05/teoria/PROG-U5.3.-Herencia/#5-clases-abstractas "Permanent link")

Una **clase abstracta** en Kotlin es una clase que no se puede instanciar directamente y que puede contener métodos abstractos (sin implementación) o métodos con implementación. Las clases abstractas se utilizan para proporcionar una base común para las subclases.

Ejemplo:

```kotlin
abstract class Animal {
    abstract fun hacerSonido()

    fun dormir() {
        println("El animal está durmiendo")
    }
}

class Perro : Animal() {
    override fun hacerSonido() {
        println("El perro ladra")
    }
}
```

En este caso, `Animal` es una clase abstracta con el método abstracto `hacerSonido()`, que debe ser implementado en la clase `Perro`.

---
### 1. Conceptos de Herencia, Superclase y Subclase[¶](https://revilofe.github.io/section1/u06/teoria/PROG-U6.1.-jerarquiaDeClases/#1-conceptos-de-herencia-superclase-y-subclase "Permanent link")
La **herencia** es un concepto clave en la programación orientada a objetos, que permite que una clase (subclase) herede propiedades y comportamientos (métodos) de otra clase (superclase). La **superclase** es la clase base que contiene los atributos y métodos que son comunes a todas las clases derivadas. La **subclase** es la clase que hereda las características de la superclase y puede agregar o modificar su propio comportamiento.

Ejemplo:
```kotlin
open class Animal {
    fun respirar() {
        println("El animal está respirando")
    }
}

class Perro : Animal() {
    fun ladrar() {
        println("El perro está ladrando")
    }
}
````

En este ejemplo, `Animal` es la superclase y `Perro` es la subclase que hereda el método `respirar()` de `Animal`.

---

### 2. Clases Abstractas e Interfaces: Forzando la Herencia y Especificación[¶](https://revilofe.github.io/section1/u06/teoria/PROG-U6.1.-jerarquiaDeClases/#2-clases-abstractas-e-interfaces-forzando-la-herencia-y-especificacion "Permanent link")

- **Clases abstractas**: Son clases que no pueden ser instanciadas directamente y pueden contener métodos abstractos (sin implementación) y métodos con implementación. Las subclases están obligadas a implementar los métodos abstractos.

Ejemplo:

```kotlin
abstract class Animal {
    abstract fun hacerSonido()
    fun dormir() {
        println("El animal está durmiendo")
    }
}

class Perro : Animal() {
    override fun hacerSonido() {
        println("El perro ladra")
    }
}
```

- **Interfaces**: Son similares a las clases abstractas, pero una clase puede implementar varias interfaces. Las interfaces pueden contener métodos con o sin implementación.

Ejemplo:

```kotlin
interface Volador {
    fun volar()
}

class Pajaro : Volador {
    override fun volar() {
        println("El pájaro está volando")
    }
}
```

---

### 3. Modificadores `open`, `final`, y `abstract`: Controlando la Herencia y la Sobrescritura[¶](https://revilofe.github.io/section1/u06/teoria/PROG-U6.1.-jerarquiaDeClases/#3-modificadores-open-final-y-abstract-controlando-la-herencia-y-la-sobrescritura "Permanent link")

Kotlin utiliza modificadores para controlar la herencia y la sobrescritura de métodos:

- `open`: Permite que una clase o función sea heredada o sobreescrita. Las clases y métodos son `final` por defecto, lo que significa que no pueden ser heredados o sobrescritos a menos que se marque como `open`.
    
    Ejemplo:
    
    ```kotlin
    open class Animal {
        open fun hacerSonido() {
            println("El animal hace un sonido")
        }
    }
    ```
    
- `final`: Impide que una clase o función sea heredada o sobrescrita.
    
    Ejemplo:
    
    ```kotlin
    final class Perro : Animal() {
        override fun hacerSonido() {
            println("El perro ladra")
        }
    }
    ```
    
- `abstract`: Marca una clase o función como abstracta, lo que significa que no se puede instanciar directamente y debe ser implementada por las subclases.
    
    Ejemplo:
    
    ```kotlin
    abstract class Animal {
        abstract fun hacerSonido()
    }
    ```
    

---

### 4. Incidencia de los constructores en la herencia[¶](https://revilofe.github.io/section1/u06/teoria/PROG-U6.1.-jerarquiaDeClases/#4-incidencia-de-los-constructores-en-la-herencia "Permanent link")

En Kotlin, los **constructores primarios** de las clases también se heredan y deben ser invocados desde las subclases. Si una clase tiene un constructor primario, la subclase debe invocar este constructor a través de la palabra clave `super`.

Ejemplo:

```kotlin
open class Animal(val nombre: String) {
    fun respirar() {
        println("$nombre está respirando")
    }
}

class Perro(nombre: String, val raza: String) : Animal(nombre) {
    fun ladrar() {
        println("$nombre está ladrando")
    }
}
```

En este ejemplo, el constructor primario de `Animal` es heredado por `Perro`, y se pasa al constructor de `Animal` usando `super(nombre)`.

---

### 5. Sobrescritura de Métodos en Clases Heredadas[¶](https://revilofe.github.io/section1/u06/teoria/PROG-U6.1.-jerarquiaDeClases/#5-sobrescritura-de-metodos-en-clases-heredadas "Permanent link")

Cuando una subclase hereda un método de la superclase, puede sobrescribir ese método para proporcionar una implementación específica. Esto se hace usando la palabra clave `override`.

Ejemplo:

```kotlin
open class Animal {
    open fun hacerSonido() {
        println("El animal hace un sonido")
    }
}

class Perro : Animal() {
    override fun hacerSonido() {
        println("El perro ladra")
    }
}
```

Aquí, `Perro` sobrescribe el método `hacerSonido()` de la clase `Animal` para dar su propia implementación.

---

### 6. Diseño y Aplicación de Jerarquías de Clases[¶](https://revilofe.github.io/section1/u06/teoria/PROG-U6.1.-jerarquiaDeClases/#6-diseno-y-aplicacion-de-jerarquias-de-clases "Permanent link")

El diseño de jerarquías de clases implica crear un sistema de clases interrelacionadas mediante herencia. Este enfoque permite la reutilización del código, promoviendo la extensión y modificación de comportamientos sin tener que duplicar el código.

Un ejemplo de jerarquía de clases:

```kotlin
open class Vehiculo(val marca: String) {
    open fun conducir() {
        println("Conduciendo el vehículo")
    }
}

class Coche(marca: String, val modelo: String) : Vehiculo(marca) {
    override fun conducir() {
        println("Conduciendo el coche $marca $modelo")
    }
}

class Moto(marca: String, val tipo: String) : Vehiculo(marca) {
    override fun conducir() {
        println("Conduciendo la moto $marca $tipo")
    }
}
```

En este ejemplo, `Vehiculo` es la superclase común a `Coche` y `Moto`. Ambas subclases sobrescriben el método `conducir()` para adaptarlo a su tipo de vehículo.

---
## 1. SOLID.[¶](https://revilofe.github.io/section1/u06/teoria/PROG-U6.3.-principiosSOLID/#1-solid "Permanent link")

**SOLID** es un conjunto de cinco principios fundamentales de diseño de software que buscan mejorar la mantenibilidad, escalabilidad y comprensión del código. Fue introducido por Robert C. Martin (también conocido como Uncle Bob). Estos principios se enfocan en la creación de código más limpio, modular y fácil de modificar.

Las siglas **SOLID** corresponden a los siguientes principios:

- **S**: Single Responsibility Principle (SRP) - Principio de Responsabilidad Única.
- **O**: Open/Closed Principle (OCP) - Principio de Abierto/Cerrado.
- **L**: Liskov Substitution Principle (LSP) - Principio de Sustitución de Liskov.
- **I**: Interface Segregation Principle (ISP) - Principio de Segregación de Interfaces.
- **D**: Dependency Inversion Principle (DIP) - Principio de Inversión de Dependencias.

Cada uno de estos principios tiene como objetivo mejorar la estructura del código y facilitar su evolución a lo largo del tiempo.

---

## 2. Principios de SOLID.[¶](https://revilofe.github.io/section1/u06/teoria/PROG-U6.3.-principiosSOLID/#2-principios-de-solid "Permanent link")

### 1. **Single Responsibility Principle (SRP) - Principio de Responsabilidad Única**
Este principio establece que una clase debe tener una única razón para cambiar, es decir, debe tener una sola responsabilidad. Si una clase tiene más de una responsabilidad, es probable que el código sea más difícil de mantener y modificar.

Ejemplo:
```kotlin
// No sigue SRP
class Reporte {
    fun generarReporte() {
        // lógica para generar reporte
    }

    fun enviarReporte() {
        // lógica para enviar reporte
    }
}

// Sigue SRP
class Reporte {
    fun generarReporte() {
        // lógica para generar reporte
    }
}

class EnvioReporte {
    fun enviarReporte() {
        // lógica para enviar reporte
    }
}
```


### 2. **Open/Closed Principle (OCP) - Principio de Abierto/Cerrado**

Una clase debe estar abierta para su extensión, pero cerrada para su modificación. Esto significa que deberías ser capaz de extender el comportamiento de una clase sin modificar su código base. Para ello, es útil el uso de la herencia o interfaces.

Ejemplo:

```kotlin
// No sigue OCP
class Calculadora {
    fun calcularArea(figura: String): Double {
        return when (figura) {
            "Círculo" -> Math.PI * 5 * 5
            "Cuadrado" -> 5 * 5
            else -> 0.0
        }
    }
}

// Sigue OCP
interface Figura {
    fun calcularArea(): Double
}

class Circulo(val radio: Double) : Figura {
    override fun calcularArea(): Double = Math.PI * radio * radio
}

class Cuadrado(val lado: Double) : Figura {
    override fun calcularArea(): Double = lado * lado
}

class Calculadora {
    fun calcularArea(figura: Figura): Double {
        return figura.calcularArea()
    }
}
```

### 3. **Liskov Substitution Principle (LSP) - Principio de Sustitución de Liskov**

Este principio dice que los objetos de una clase derivada deben ser sustituibles por objetos de la clase base sin alterar la funcionalidad del programa. En otras palabras, las subclases deben ser completamente intercambiables con sus clases base.

Ejemplo:

```kotlin
// No sigue LSP
open class Vehiculo {
    open fun arrancar() = println("Vehículo arrancando")
}

class Bicicleta : Vehiculo() {
    override fun arrancar() {
        throw Exception("Las bicicletas no arrancan")
    }
}

// Sigue LSP
open class Vehiculo {
    open fun arrancar() = println("Vehículo arrancando")
}

class Coche : Vehiculo() {
    override fun arrancar() = println("Coche arrancando")
}
```

### 4. **Interface Segregation Principle (ISP) - Principio de Segregación de Interfaces**

Este principio sugiere que una clase no debe ser forzada a implementar interfaces que no necesita. Es mejor tener interfaces específicas para cada tipo de comportamiento que una única interfaz general.

Ejemplo:

```kotlin
// No sigue ISP
interface Maquina {
    fun imprimir()
    fun escanear()
    fun faxear()
}

class Impresora : Maquina {
    override fun imprimir() {
        println("Imprimiendo")
    }

    override fun escanear() {
        throw Exception("No escanea")
    }

    override fun faxear() {
        throw Exception("No faxea")
    }
}

// Sigue ISP
interface Impresora {
    fun imprimir()
}

interface Escaner {
    fun escanear()
}

class ImpresoraConEscaner : Impresora, Escaner {
    override fun imprimir() {
        println("Imprimiendo")
    }

    override fun escanear() {
        println("Escaneando")
    }
}
```

### 5. **Dependency Inversion Principle (DIP) - Principio de Inversión de Dependencias**

Las clases de alto nivel no deben depender de clases de bajo nivel. Ambas deben depender de abstracciones (interfaces o clases abstractas). Además, las abstracciones no deben depender de los detalles, los detalles deben depender de las abstracciones.

Ejemplo:

```kotlin
// No sigue DIP
class Motor {
    fun arrancar() {
        println("Motor arrancando")
    }
}

class Coche {
    private val motor = Motor()
    
    fun arrancar() {
        motor.arrancar()
    }
}

// Sigue DIP
interface Arrancable {
    fun arrancar()
}

class Motor : Arrancable {
    override fun arrancar() {
        println("Motor arrancando")
    }
}

class Coche(private val motor: Arrancable) {
    fun arrancar() {
        motor.arrancar()
    }
}
```

Estos principios SOLID ayudan a crear sistemas de software más modulares, fáciles de extender y mantener, promoviendo un diseño robusto y flexible.
### Imports frecuentes en Kotlin:

```kotlin
import kotlin.math.* // Para funciones matemáticas estándar como sqrt, pow, etc.
import java.util.*  // Para trabajar con colecciones como ArrayList, HashMap, etc.
import java.io.*    // Para trabajar con entradas y salidas, como File, BufferedReader, etc.
import kotlin.collections.* // Para operaciones extendidas sobre colecciones como map, filter, etc.
import kotlin.random.Random // Para generar números aleatorios
import kotlin.concurrent.thread // Para crear hilos de ejecución en paralelo
import java.time.LocalDate // Para trabajar con fechas y tiempos
import java.util.UUID //Te da un id aleatorio para ejercicios en los que necesitas generar un id.
```

### Funciones por defecto para **Listas**, **Arrays**, y **Tuplas**:

#### **Listas:**

```kotlin
// Crear una lista inmutable
val lista = listOf(1, 2, 3, 4, 5)

// Crear una lista mutable
val listaMutable = mutableListOf(1, 2, 3, 4)

// Agregar un elemento a una lista mutable
listaMutable.add(6)

// Filtrar elementos en una lista
val filtrada = lista.filter { it > 2 }  // [3, 4, 5]

// Transformar los elementos de una lista
val transformada = lista.map { it * 2 }  // [2, 4, 6, 8, 10]

// Obtener el primer elemento
val primero = lista.first()  // 1

// Obtener el último elemento
val ultimo = lista.last()  // 5

// Verificar si la lista contiene un elemento
val contiene = lista.contains(3)  // true

// Ordenar una lista
val ordenada = lista.sorted()  // [1, 2, 3, 4, 5]

// Agrupar elementos de una lista
val grupos = lista.groupBy { it % 2 }  // {0=[2, 4], 1=[1, 3, 5]}
```

#### **Arrays:**

```kotlin
// Crear un array
val array = arrayOf(1, 2, 3, 4, 5)

// Crear un array con valores predeterminados
val arrayDeCeros = Array(5) { 0 }  // [0, 0, 0, 0, 0]

// Acceder a un elemento de un array
val valor = array[0]  // 1

// Modificar un elemento del array
array[0] = 10  // [10, 2, 3, 4, 5]

// Convertir un array a lista
val listaDesdeArray = array.toList()  // [10, 2, 3, 4, 5]

// Convertir una lista a array
val arrayDesdeLista = lista.toTypedArray()  // [10, 2, 3, 4, 5]

// Filtrar elementos en un array
val filtradoArray = array.filter { it > 2 }  // [10, 3, 4, 5]
```

#### **Tuplas (Pair y Triple):**

```kotlin
// Crear un par (tupla de 2 elementos)
val par = Pair("Hola", 5)

// Acceder a los elementos del par
val (texto, numero) = par  // texto = "Hola", numero = 5

// Crear un triple (tupla de 3 elementos)
val triple = Triple("Kotlin", 1, 3.14)

// Acceder a los elementos del triple
val (lenguaje, version, pi) = triple  // lenguaje = "Kotlin", version = 1, pi = 3.14
```

### Imports frecuentes relacionados con **Listas**, **Arrays**, **Tuplas**, y similares:

```kotlin
import kotlin.collections.* // Para trabajar con listas, conjuntos, mapas, etc.
import kotlin.array.*         // Para trabajar con arrays
import kotlin.Pair           // Para usar Pair de manera explícita
import kotlin.Triple          // Para usar Triple de manera explícita
import java.util.*           // Para trabajar con colecciones como ArrayList, HashMap, etc.
import kotlin.math.*          // Funciones matemáticas que puedes usar en arrays o listas, como sum, average, etc.
```

### Funciones de conversión en Kotlin:

#### **Conversión entre colecciones:**

```kotlin
// Convertir una lista a un conjunto (Set)
val lista = listOf(1, 2, 2, 3, 4)
val conjunto = lista.toSet()  // {1, 2, 3, 4}

// Convertir un conjunto (Set) a una lista
val listaDesdeSet = conjunto.toList()  // [1, 2, 3, 4]

// Convertir una lista a un array
val arrayDesdeLista = lista.toTypedArray()  // [1, 2, 2, 3, 4]

// Convertir un array a una lista
val listaDesdeArray = arrayOf(1, 2, 3, 4).toList()  // [1, 2, 3, 4]

// Convertir un mapa a una lista de pares clave-valor
val mapa = mapOf(1 to "a", 2 to "b")
val listaDePares = mapa.toList()  // [(1, "a"), (2, "b")]
```

#### **Conversión entre tipos de datos:**

```kotlin
// Convertir un String a un número entero
val numero = "123".toInt()  // 123

// Convertir un String a un número decimal
val decimal = "3.14".toDouble()  // 3.14

// Convertir un entero a un String
val numeroString = 123.toString()  // "123"

// Convertir un número decimal a un String
val decimalString = 3.14.toString()  // "3.14"

// Convertir un String a un Booleano
val esTrue = "true".toBoolean()  // true

// Convertir un Booleano a un String
val booleanString = true.toString()  // "true"
```

#### **Conversión de tipos numéricos:**

```kotlin
// Convertir entre tipos numéricos
val entero: Int = 10
val largo: Long = entero.toLong()  // 10L
val flotante: Float = entero.toFloat()  // 10.0f
val doble: Double = entero.toDouble()  // 10.0

// Convertir de un tipo mayor a uno menor (con posibilidad de pérdida de datos)
val largoGrande: Long = 1000L
val enteroConvertido: Int = largoGrande.toInt()  // 1000 (si el valor es demasiado grande puede perder precisión)
```

#### **Conversión de tipos en colecciones (Mapeado y Transformación):**

```kotlin
// Convertir una lista de enteros a una lista de cadenas
val listaNumeros = listOf(1, 2, 3)
val listaStrings = listaNumeros.map { it.toString() }  // ["1", "2", "3"]

// Convertir una lista de cadenas a una lista de enteros
val listaDeCadenas = listOf("1", "2", "3")
val listaEnteros = listaDeCadenas.map { it.toInt() }  // [1, 2, 3]

// Convertir una lista de números a una lista de dobles
val listaNumeros2 = listOf(1, 2, 3)
val listaDobles = listaNumeros2.map { it.toDouble() }  // [1.0, 2.0, 3.0]
```

#### **Conversión de objetos:**

```kotlin
// Convertir un objeto a su representación en cadena
val persona = Persona("John", 25)
val personaString = persona.toString()  // Si tienes sobrescrita la función toString en la clase Persona

// Convertir una fecha a un formato String
val fecha = LocalDate.now()
val fechaString = fecha.toString()  // "2025-03-08" (por ejemplo)
```

### Imports frecuentes para conversiones:

```kotlin
import kotlin.collections.*   // Para trabajar con colecciones como List, Set, Map, etc.
import kotlin.math.*           // Para realizar conversiones matemáticas como redondear, obtener potencias, etc.
import java.time.*             // Para trabajar con fechas y conversiones de tipo LocalDate, LocalDateTime, etc.
import java.util.*             // Para trabajar con colecciones de Java como ArrayList, HashMap, etc.
```


---

### 📌 **Funciones de manipulación de texto**

#### 🔹 Convertir texto a mayúsculas y minúsculas

```kotlin
val texto = "Hola Mundo"
println(texto.uppercase()) // "HOLA MUNDO"
println(texto.lowercase()) // "hola mundo"
```

#### 🔹 Reemplazar texto

```kotlin
val mensaje = "Hola Kotlin"
val nuevoMensaje = mensaje.replace("Hola", "Adiós")
println(nuevoMensaje) // "Adiós Kotlin"
```

#### 🔹 Dividir una cadena

```kotlin
val nombres = "Ana, Juan, Pedro"
val lista = nombres.split(", ")
println(lista) // [Ana, Juan, Pedro]
```

---

### 📌 **Funciones matemáticas**

#### 🔹 Números aleatorios

```kotlin
import kotlin.random.Random

val numero = Random.nextInt(1, 10) // Número entre 1 y 9
println(numero)
```

#### 🔹 Redondear un número

```kotlin
val num = 3.14159
println("%.2f".format(num)) // "3.14"
```

#### 🔹 Calcular potencia y raíz

```kotlin
import kotlin.math.*

println(sqrt(25.0)) // 5.0
println(pow(2.0, 3.0)) // 8.0
```

---

### 📌 **Funciones de listas y arrays**

#### 🔹 Ordenar una lista

```kotlin
val numeros = listOf(5, 2, 8, 1)
println(numeros.sorted()) // [1, 2, 5, 8]
```

#### 🔹 Buscar un elemento en una lista

```kotlin
val lista = listOf("manzana", "pera", "uva")
println(lista.contains("pera")) // true
```

#### 🔹 Recorrer una lista con un `forEach`

```kotlin
val colores = listOf("Rojo", "Azul", "Verde")
colores.forEach { println(it) } //Esto es lo mismo que usar un for
```

---

### 📌 **Funciones de control de flujo**

#### 🔹 Comprobar si un número es par o impar

```kotlin
fun esPar(numero: Int): Boolean {
    return numero % 2 == 0
}

println(esPar(4)) // true
println(esPar(7)) // false
```

#### 🔹 Usar `when` como switch

```kotlin
val dia = 3
val nombreDia = when(dia) {
    1 -> "Lunes"
    2 -> "Martes"
    3 -> "Miércoles"
    else -> "Día no válido"
}
println(nombreDia) // "Miércoles"
```

---

### 📌 **Funciones de fechas y tiempo**

#### 🔹 Obtener la fecha y hora actual

```kotlin
import java.time.LocalDateTime

val fechaHora = LocalDateTime.now()
println(fechaHora)
```

#### 🔹 Dar formato a una fecha

```kotlin
import java.time.LocalDate
import java.time.format.DateTimeFormatter

val fecha = LocalDate.now()
val formato = DateTimeFormatter.ofPattern("dd/MM/yyyy")
println(fecha.format(formato)) // Ejemplo: "08/03/2025"
```

---
### 🔹 **Tipos de Herencia en POO**

1️⃣ **Especificación** → La clase hija es una versión más concreta de la clase padre.

- Ejemplo: `Vehiculo → Coche` (Coche hereda de Vehiculo y añade más detalles).

2️⃣ **Especialización** → Se modifica o mejora un comportamiento de la clase padre.

- Ejemplo: `Empleado → Gerente` (Gerente redefine cómo se calcula el bono).

3️⃣ **Extensión** → Se agregan nuevas funcionalidades sin cambiar la base.

- Ejemplo: `Animal → Perro` (Perro hereda respirar() pero añade ladrar()).

4️⃣ **Construcción** → Se define una estructura base que las clases hijas deben seguir.

- Ejemplo: `Figura → Círculo/Rectángulo` (todas deben implementar calcularArea()).

🔹 **Resumen:**

- **Especificación** → Hacer más concreta la clase.
- **Especialización** → Modificar el comportamiento.
- **Extensión** → Agregar funcionalidades.
- **Construcción** → Establecer una estructura obligatoria.

### 🔹 **Expresiones Regulares en Kotlin (Regex) – Explicación Completa**

📌 **Ejemplo: Validar un correo electrónico**

```kotlin
val emailRegex = "^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\\.[a-zA-Z]{2,}$".toRegex()
val email = "ejemplo@email.com"
println(email.matches(emailRegex)) // true
```

---

### **Explicación detallada de los símbolos usados**

| Símbolo             | Significado                                                                                                                                                                                                                                                      |
| ------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `^`                 | **Inicio de la cadena**. La coincidencia debe comenzar desde el primer carácter.                                                                                                                                                                                 |
| `[a-zA-Z0-9._%+-]+` | **Grupo de caracteres permitidos antes de `@`**:<br>🔹 `[a-zA-Z0-9]` → Letras (mayúsculas y minúsculas) y números.<br>🔹 `._%+-` → Se permiten los caracteres `. _ % + -`.<br>🔹 `+` → Indica **uno o más** caracteres de este grupo (al menos uno obligatorio). |
| `@`                 | **Debe haber una `@` en la dirección**. Es un carácter obligatorio.                                                                                                                                                                                              |
| `[a-zA-Z0-9.-]+`    | **Dominio permitido después de `@`**:<br>🔹 `[a-zA-Z0-9]` → Letras y números.<br>🔹 `.-` → Se permiten `.` y `-` en el dominio.<br>🔹 `+` → Debe haber al menos un carácter en el dominio.                                                                       |
| `\\.`               | **Punto literal antes de la extensión**.<br>🔹 Se usa `\\.` porque `.` por sí solo en regex significa "cualquier carácter", así que lo escapamos con `\\` para que sea un punto literal.                                                                         |
| `[a-zA-Z]{2,}$`     | **Extensión del dominio**:<br>🔹 `[a-zA-Z]` → Solo letras (mayúsculas y minúsculas).<br>🔹 `{2,}` → **Mínimo 2 caracteres**, sin máximo (permite `.com`, `.es`, `.online`, etc.).<br>🔹 `$` → **Fin de la cadena**. No debe haber caracteres adicionales.        |

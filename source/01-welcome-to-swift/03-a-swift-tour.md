# Un Recorrido Por Swift

Es costumbre que el primer programa que se crea al aprender un nuevo lenguaje de programación es aquel que imprime la frase _«¡Hola, mundo!»_ en la pantalla. En Swift, esto se puede conseguir con una sola línea de código:

```swift
print("¡Hola, mundo!")
// Imprime "¡Hola, mundo!"
```

Si has desarollado anteriormente en C u Objective-C, esta sintaxis te resultará familiar; en Swift, esta línea de código representa un programa como tal. No hace falta importar una biblioteca aparte para contar con funciones como entrada/salida o manejo de cadenas de texto. Todo código escrito en el ámbito \(del inglés _scope_\) global se utiliza como punto de entrada para el programa, por lo que no necesitamos una función `main()`. Tampoco hace falta escribir punto y coma al final de cada declaración.

Esta guía te proporciona suficiente información para comenzar a desarrollar código en Swift al enseñarte cómo realizar una variedad de tareas de programación. No te preocupes si hay algo que no entiendes: todo lo presentado en esta guía se explica en detalle en el resto de este libro.

{% hint style="info" %}
Nota.

Para una mejor experiencia, abre este capítulo como un playground en Xcode. Los playgrounds te permiten editar bloques de código y ver el resultado inmediatamente.

[https://example.com](https://example.com)
{% endhint %}

### 

### Valores Sencillos

Usa `let` para crear una constante y `var` para crear una variable. No es necesario que conozcamos el valor de una constante durante la compilación, pero tal valor debe asignarse exactamente una única vez. Esto significa que puedes usar constantes para nombrar un valor que solo se define una vez, pero que se usa muchas veces.

```swift
var miVariable = 42
miVariable = 50
let miConstante = 42
```

Una constante o variable debe ser del mismo tipo que el valor que se le quiera asignar. Sin embargo, no hace falta ser explícitos al respecto. El proporcionar un valor a una variable o constante durante su creación, le permite al compilador inferir el tipo de dicha variable o constante. En el anterior ejemplo, el compilador infiere que `miVariable` es un entero porque su valor inicial es un entero.

Si el valor inicial no proporcionara suficiente información \(o si no hubiera un valor inicial\), especificamos el tipo al escribirlo después de la variable, seguido por dos puntos.

```swift
let enteroImplicito = 70
let doubleImplicito = 70.0
let doubleExplicito: Double = 70
```

> EXPERIMENTA
>
> Crea una constante con un tipo específico `Float` y un valor de `4`.



Los valores nunca son convertidos a un tipo diferente de manera implícita. Si necesitas convertir un valor a un tipo diferente, debes crear –explícitamente–, una instancia del tipo deseado.

```swift
let etiqueta = "El ancho es "
let ancho = 94
let etiquetaAncho = etiqueta + String(ancho)
```

> EXPERIMENTA
>
> Remueve la conversión a `String` en la última línea. ¿Cuál es el error que aparece?



Hay una manera incluso más sencilla de insertar valores en una cadena de texto: Escribe el valor en paréntesis, precedido por un backslash \(`\`\). Por ejemplo:

```swift
let manzanas = 3
let naranjas = 5
let resumenManzanas = "Tengo \(manzanas) manzanas."
let resumenFrutas = "Tengo \(manzanas + naranjas) frutas."
```

> EXPERIMENTA
>
> Usa `\()` para insertar una operación con números de coma flotante en una cadena de texto y para incluir el nombre de una persona en un saludo.



Usa tres comillas dobles para cadenas de texto que ocupan más de una línea. La sangría \(del inglés _indentation_\) al inicio de cada línea de la cadena de texto es removida siempre y cuando concuerde con la sangría de las comillas de cierre. Por ejemplo:

```swift
let cita = """
He dicho "Tengo \(manzanas) manzanas."
Y luego he dicho "Tengo \(manzanas + naranjas) frutas."
"""
```



Crea arrays y diccionarios usando corchetes \(`[]`\) y accede a sus elementos referenciándolos por su índice o su clave en corchetes. Está permitido el uso de coma después del último elemento.

```swift
var listaDeCompras = ["cereal", "frutas", "helado"]
listaDeCompras[1] = "botella de agua"

var ocupaciones = [
    "Malcolm": "Capitán",
    "Kaylee": "Mecánico",
]
ocupaciones["Jayne"] = "Relaciones Públicas"
```



Los arrays crecen automáticamente a medida que agregas elementos.

```swift
listaDeCompras.append("pintura azul")
print(listaDeCompras)
```



Para crear un array o un diccionario vacíos, usa la sintaxis de inicialización.

```swift
let arrayVacio: [String] = []
let diccionarioVacio: [String: Float] = [:]
```



Si es posible inferir información sobre el tipo de datos, podrás declarar un array vacío así `[]` y un diccionario vacío así `[:]`. Por ejemplo, al especificar un nuevo valor para una variable o al pasar un argumento a una función.

```swift
listaDeCompras = []
ocupaciones = [:]
```



### Control de Flujo

Usa `if` y `switch` para crear condicionales, y usa `for-in`, `while`, y `repeat-while` para crear bucles. Los paréntesis alrededor de la condición o de la variable del bucle son opcionales. Las llaves alrededor del cuerpo son obligatorias.

```swift
let puntajesIndividuales = [75, 43, 103, 87, 12]
var puntajeDelEquipo = 0
for puntaje in puntajesIndividuales {
    if puntaje > 50 {
        puntajeDelEquipo += 3
    } else {
        puntajeDelEquipo += 1
    }
}
print(puntajeDelEquipo)
// Imprime "11"
```



En una declaración `if`, el condicional debe ser una expresión de tipo Boolean; esto significa, que una declaración de la forma `if puntaje { ... }` es un error, ya que no se compara implícitamente con cero.

Puedes usar `if` y `let` en conjunto para lidiar con valores que podrían no existir. Estos valores son representados como opcionales. Un valor opcional puede contener un valor o `nil` –para indicar la ausencia de un valor–. Agrega un signo de interrogación \(`?`\) después del tipo de un valor para señalar dicho valor como opcional.

```swift
var stringOpcional: String? = "Hola"
print(stringOpcional == nil)
// Imprime "false"

var nombreOpcional: String? = "John Appleseed"
var saludo = "¡Hola!"
if let nombre = nombreOpcional {
    saludo = "Hola, \(nombre)."
}
```

> EXPERIMENTA
>
> Cambia `nombreOpcional` a `nil`. ¿Cuál saludo obtienes? Agrega una cláusula `else` que defina un saludo diferente si `nombreOpcional` es `nil`.



Si el valor opcional es `nil`, el condicional evalúa a `false` y el código en las llaves es ignorado. En caso contrario, se obtiene el valor opcional y se le asigna a la constante después de `let`, lo cual hace que el valor obtenido esté disponible dentro del bloque de código.

Otra forma de lidiar con valores opcionales es proporcionar un valor por defecto a través del operador `??`. Si el valor opcional no existe, se usa el valor por defecto en su lugar.

```swift
let nickname: String? = nil
let nombreCompleto: String = "John Appleseed"
let saludoInformal = "Hi \(nickname ?? nombreCompleto)"
```



Los bucles tipo switch sportan cualquier tipo de datos así como una gran variedad de operaciones comparativas, por lo que no se limitan a enteros y pruebas de calidad.

```swift
let vegetal = "pimiento rojo"
switch vegetal {
case "apio":
    print("Add some raisins and make ants on a log.")
case "pepino", "berro":
    print("That would make a good tea sandwich.")
case let x where x.hasSuffix("pimiento"):
    print("¿Es un \(x) picante?")
default:
    print("Todo sabe bien en una sopa.")
}
// Imprime "¿Es un pimiento rojo picante?"
```

> EXPERIMENTA
>
> Remueve el caso default. ¿Cuál es el error que aparece?



Observa cómo es posible usar `let` con un patrón para asignar el valor que concuerde con dicho patrón a una constante.

Una vez ejecutado el código dentro del caso que concuerda, el programa abandona el bucle switch. La ejecución no continúa al siguiente caso, por lo que no es necesario indicar la salida del bucle explícitamente al final del código de cada caso.

Puedes usar `for-in` para iterar sobre los elementos de un diccionario al proporcionar un par de nombres que serán usados para cada par llave-valor. Los diccionarios son colecciones sin un orden particular, por lo que se itera sobre sus llaves y valores de manera arbitraria.

```swift
let numerosInteresantes = [
    "Primos": [2, 3, 5, 7, 11, 13],
    "Fibonacci": [1, 1, 2, 3, 5, 8],
    "Cuadrados": [1, 4, 9, 16, 25],
]
var mayor = 0
for (_, numeros) in numerosInteresantes {
    for numero in numeros {
        if numero > mayor {
            mayor = numero
        }
    }
}
print(mayor)
// Imprime "25"
```

> EXPERIMENTA
>
> Reemplaza `_` por una variable con nombre y haz seguimiento del tipo de número que resultó ser el mayor.



Usa `while` para repetir un bloque de código hasta que se satisfaga una condición. La condición del bucle puede ir al final, para asegurar que este se ejecute al menos una vez.

```swift
var n = 2
while n < 100 {
    n *= 2
}
print(n)
// Imprime "128"

var m = 2
repeat {
    m *= 2
} while m < 100
print(m)
// Imprime "128"
```



Es posible tener índices en un bucle al usar `..<` para crear un rango de índices.

```swift
var total = 0
for i in 0..<4 {
    total += i
}
print(total)
// Imprime "6"
```



Usa `..<` para crear un rango que omita el valor superior, y usa `...` para crear uno que incluya ambos valores.



### Funciones y Clausuras

Usa `func` para declarar una función. Para llamar una función, escribe una lista de argumentos en paréntesis después de su nombre. Usa `->` para separar el nombre de los parámetros y su tipo del tipo que devuelve la función.

```swift
func saludar(persona: String, dia: String) -> String {
    return "Hola, \(persona), hoy es \(dia)."
}
saludar(persona: "Bob", dia: "Martes")
```

> EXPERIMENTA
>
> Remueve el parámetro `dia`. Agrega un parámetro que incluya el almuerzo especial de hoy en el saludo.



Por defecto, las funciones usan los nombres de sus parámetros como etiquetas para sus argumentos. Crea tu propia etiqueta para un argumento anteponiéndola al nombre del parámetro, o agrega `_` para no usar una etiqueta para un argumento.

```swift
func saludar(_ persona: String, en dia: String) -> String {
    return "Hola, \(persona), hoy es \(day)."
}
saludar("Juan", en: "Miercoles")
```



Usa una tupla \(del inglés _tuple_\) para crear un valor compuesto; por ejemplo, para devolver múltiples valores desde una función. Los elementos de una tupla se pueden referenciar bien sea por nombre o por número.

```swift
func calcularEstadisticas(puntajes: [Int]) -> (min: Int, max: Int, suma: Int) {
    var min = puntajes[0]
    var max = puntajes[0]
    var suma = 0

    for puntaje in puntajes {
        if puntaje > max {
            max = puntaje
        } else if puntaje < min {
            min = puntaje
        }
        suma += puntaje
    }

    return (min, max, suma)
}
let estadisticas = calcularEstadisticas(puntajes: [5, 3, 100, 3, 9])
print(estadisticas.suma)
// Imprime "120"
print(estadisticas.2)
// Imprime "120"
```



Las funciones pueden anidarse. Las funciones anidadas tienen acceso a variables que hayan sido declaradas en la función externa. Puedes usar funciones anidadas para organizar código que resulta extenso o complejo.

```swift
func devolverQuince() -> Int {
    var y = 10
    func agregar() {
        y += 5
    }
    agregar()
    return y
}
devolverQuince()
```



Las funciones son un tipo de primera clase. Esto, quiere decir, que una función puede devolver otra función como su valor.

```swift
func crearIncrementador() -> ((Int) -> Int) {
    func agregarUno(numero: Int) -> Int {
        return 1 + numero
    }
    return agregarUno
}
var incrementar = crearIncrementador()
incrementar(7)
```



Una función puede tomar a otra función como uno de sus argumentos.

```swift
func coincideAlguno(lista: [Int], condicion: (Int) -> Bool) -> Bool {
    for elemento in lista {
        if condicion(elemento) {
            return true
        }
    }
    return false
}
func menorQueDiez(numero: Int) -> Bool {
    return numero < 10
}
var numeros = [20, 19, 7, 12]
coincideAlguno(lista: numeros, condicion: menorQueDiez)
```



Las funciones son, en realidad, un caso especial de clausura \(del inglés _closure_\): bloques de código que pueden ser llamados más tarde. El código en una clausura tiene acceso a elementos como variables y funciones que están disponibles en el ámbito en el cual se creó la clausura, incluso cuando la clausura se encuentra en un ámbito diferente al momento de ejecutarse; ya has visto un ejemplo de esto con las funciones anidadas. Puedes crear una clausura anónima al encerrar el código en llaves \(`{}`\). Usa `in` para separar los argumentos y el tipo devuelto por la función del cuerpo de la función. 

```swift
numeros.map({ (numero: Int) -> Int in
    let resultado = 3 * numero
    return resultado
})
```

> EXPERIMENTA
>
> Reescribe la clausura de manera que devuelva cero para todos los números impares.



Existen muchas maneras de crear una clausura de forma más concisa. Cuando se conoce el tipo de una clausura, como es el caso de un _callback_ para un delegado, puedes omitir el tipo de sus parámetros, el tipo devuelto, o de ambos. Las clausuras de una sola sentencia devuelven el valor de su única sentencia de manera implícita.

```swift
let mappedNumbers = numeros.map({ numero in 3 * numero })
print(mappedNumbers)
// Imprime "[60, 57, 21, 36]"
```



Puedes referenciar parámetros por número en vez de nombre; este enfoque es, especialmente, útil para clausuras muy concisas. Una clausura que se pasa como el último argumento de una función puede aparecer inmediatamente después de los paréntesis. Cuando una clausura es el único argumento de una función, puedes omitir los paréntesis por completo.

```swift
let numerosOrdenados = numeros.sorted { $0 > $1 }
print(numerosOrdenados)
// Imprime "[20, 19, 12, 7]"
```



### Objetos y Clases

Usa `class` seguido del nombre de la clase para crear una clase. Para declarar una propiedad de una clase, se escribe igual que al declarar una constante o variable, excepto que esta existiría en el contexto de una clase. Similarmente, la declaración de métodos y funciones se hace de la misma forma.

```swift
class Figura {
    var numeroDeLados = 0
    func descripcionBasica() -> String {
        return "Una figura con \(numeroDeLados) lados."
    }
}
```

> EXPERIMENTA
>
> Agrega una constante con `let` y otro método que tome un argumento.



Crea una instancia de una clase al poner paréntesis después del nombre de la clase. Usa sintaxis de punto para acceder a las propiedades y métodos de la instancia.

```swift
var figura = Figura()
figura.numeroDeLados = 7
var descripcionFigura = descripcionBasica()
```



A esta versión de la clase `Figura` le hace falta algo importante: un inicializador que establezca la clase al crear una instancia. Usa `init` para crear uno.

```swift
class FiguraConNombre {
    var numeroDeLados: Int = 0
    var nombre: String

    init(nombre: String) {
        self.nombre = nombre
    }

    func descripcionBasica() -> String {
        return "Una figura con \(numeroDeLados) lados."
    }
}
```



Observa cómo se usa `self` para diferenciar la propiedad `nombre` del argumento \(del inicializador\) `nombre`. Al crear una instancia de una clase, los argumentos del inicializador se pasan como cuando se llama una función. Cada propiedad requiere que se le asigne un valor, bien sea al declararla \(como con `numeroDeLados`\) o en el inicializador \(como con `nombre`\).

Usa `deinit` para crear un «desinicializador» \(del inglés _deinitializer_\) si necesitas llevar a cabo alguna limpieza antes de que el objeto sea «desasignado» \(del inglés _deallocated_\).

Las subclases incluyen el nombre de su súperclase después de su propio nombre, separados por una coma. No es requerimiento de las clases pasar ninguna clase base estándar a las subclases, por lo que puedes incluir u omitir una súperclase si así lo requieres.

Aquellos métodos de una subclase que sobreescriben la implementación de una súperclase, se marcan con `override`; sobreescribir un método por accidente, sin usar `override`, es detectado por el compilador como un error. El compilador también detecta métodos con `override` que no sobreescriben ningún método de la súperclase.

```swift
class Cuadrado: FiguraConNombre {
    var longitudLado: Double

    init(longitudLado: Double, nombre: String) {
        self.longitudLado = longitudLado
        super.init(nombre: nombre)
        numeroDeLados = 4
    }

    func area() -> Double {
        return longitudLado * longitudLado
    }

    override func descripcionBasica() -> String {
        return "Un cuadrado con lados de longitud \(longitudLado)."
    }
}
let prueba = Cuadrado(longitudLado: 5.2, nombre: "cuadrado de prueba")
prueba.area()
prueba.descripcionBasica()
```

> EXPERIMENTA
>
> Crea otra subclase de `FiguraConNombre` llamada `Circulo`, que tome un radio y un nombre como argumentos de su inicializador. Implementa los métodos `area()` y `descripcionBasica()` en la clase `Circulo`.



Aparte de simples propiedades que se almacenan, las propiedades pueden tener un _getter_ y un _setter_.

```swift
class TrianguloEquilatero: FiguraConNombre {
    var longitudLado: Double = 0.0

    init(longitudLado: Double, nombre: String) {
        self.longitudLado = longitudLado
        super.init(nombre: nombre)
        numeroDeLados = 3
    }

    var perimetro: Double {
        get {
            return 3.0 * longitudLado
        }
        set {
            longitudLado = newValue / 3.0
        }
    }

    override func descripcionBasica() -> String {
        return "Un triángulo equilátero con lados de longitud \(longitudLado)."
    }
}
var triangulo = TrianguloEquilatero(longitudLado: 3.1, nombre: "un triángulo")
print(triangulo.perimetro)
// Imprime "9.3"
triangulo.perimetro = 9.9
print(triangulo.longitudLado)
// Imprime "3.3000000000000003"
```



En el setter de `perimetro`, el nuevo valor tiene el nombre implícito de `newValue`. Puedes proporcionar un nombre explícito en paréntesis después de `set`.

Observa cómo el inicializador de la clase `TrianguloEquilatero` tiene tres pasos diferentes:

1. Establecer el valor de las propiedades declaradas por la subclase.
2. Llamar al inicializador de la súperclase.
3. Cambiar el valor de las propiedades definidas por la súperclase. Cualquier otra configuración adicional que use métodos, getters, o setters también puede llevarse a cabo en este punto.

Si no necesitas calcular la propiedad, pero igual necesitas proporcionar código que se ejecuta antes y después de establecer un nuevo valor, usa `willSet` and `didSet`. El código que proporciones se ejecutará cada vez que el valor cambie fuera del inicializador. Por ejemplo, la clase a continuación se asegura de que la longitud de los lados de su triángulo siempre sea la misma que la longitud de los lados de su cuadrado.

```swift
class TrianguloYCuadrado {
    var triangulo: TrianguloEquilatero {
        willSet {
            cuadrado.longitudLado = newValue.longitudLado
        }
    }
    var cuadrado: Cuadrado {
        willSet {
            triangulo.longitudLado = newValue.longitudLado
        }
    }
    init(tamano: Double, nombre: String) {
        cuadrado = Cuadrado(longitudLado: tamano, nombre: nombre)
        triangulo = TrianguloEquilatero(longitudLado: tamano, nombre: nombre)
    }
}
var trianguloYCuadrado = TrianguloYCuadrado(size: 10, nombre: "otra figura de prueba")
print(trianguloYCuadrado.cuadrado.longitudLado)
// Imprime "10.0"
print(trianguloYCuadrado.triangulo.longitudLado)
// Imprime "10.0"
trianguloYCuadrado.cuadrado = Cuadrado(longitudLado: 50, nombre: "cuadrado más grande")
print(trianguloYCuadrado.triangulo.longitudLado)
// Imprime "50.0"
```



Al trabajar con valores opcionales, puedes escribir `?` antes de operaciones como métodos, propiedades, y _subscripting_. Si el valor antes de `?` es `nil`, todo lo que sigue a `?` es ignorado y el valor de toda la expresión es `nil`. En caso contrario, se obtiene el valor opcional y todo lo que sigue a `?` opera sobre el valor obtenido. En ambos casos, el valor de toda la expresión es un valor opcional.

```swift
let cuadradoOpcional: Cuadrado? = Cuadrado(longitudLado: 2.5, nombre: "cuadrado opcional")
let longitudLado = cuadradoOpcional?.longitudLado
```



### Enumeraciones y Estructuras

Utiliza `enum` para crear una enumeración. Al igual que las clases y todos los demás tipos con nombre, las enumeraciones pueden tener métodos asociados con ellas.

```swift
enum Escala: Int {
    case ace = 1
    case dos, tres, cuatro, cinco, seis, siete, ocho, nueve, diez
    case jack, reina, rey
    
    func descripcionBasica() -> String {
        switch self {
        case .ace:
            return "ace"
        case .jack:
            return "jack"
        case .reina:
            return "reina"
        case .rey:
            return "rey    "
        default:
            return String(self.rawValue)
        }
    }
}

let ace = Escala.ace
let valorBrutoAce = ace.rawValue
```

> EXPERIMENTA
>
> Crea una función que compare dos valores `Escala` comparando sus valores brutos.



De manera predeterminada, Swift asigna los valores brutos comenzando por cero y aumentando en uno cada vez, pero es posible cambiar dicho comportamiento al especificar valores explícitamente. En el ejemplo anterior, a `Ace` se le asigna explícitamente un valor bruto de `1` y el resto de los valores brutos se asignan en orden. También es posible utilizar cadenas de texto o números de coma flotante como el tipo bruto de una enumeración. Usa la propiedad `rawValue` para acceder al valor bruto del caso de una enumeración.

Utiliza el inicializador `init?(RawValue:)` para crear una instancia de una enumeración a partir de un valor bruto. Este inicializador devuelve el caso \(de la enumeración\) que coincida con el valor bruto o `nil` si no existe tal enumeración `Escala`.

```swift
if let escalaTransformada = Escala(rawValue: 3) {
    let descripcionTres = escalaTransformada.descripcionSimple()
}
```



Los valores de los casos de una enumeración son valores reales, no solo otra forma de escribir sus valores brutos. De hecho, en los casos en los que no existe un valor bruto significativo, no es necesario que proporciones uno.

```swift
enum Palo {
    case corazones, diamantes, picas, treboles

    func descripcionBasica() -> String {
        switch self {
            case .corazones:
                return "corazones"
            case .diamantes:
                return "diamantes"
            case .picas:
                return "picas"
            case .treboles:
                return "treboles"
        }
    }
}

let corazones = Palo.corazones
let descripcionCorazones = corazones.descripcionBasica()
```

> EXPERIMENTA
>
> Crea un método `color()` para la enumeración `Palo` que devuelva «negro» para picas y tréboles, y «rojo» para corazones y diamantes.



Fíjate en las dos formas en que se referenció el caso `corazones` de la enumeración: al asignar un valor a la constante `corazones`, el caso `Palo.corazones` se referencia por su nombre completo porque la constante no tiene un tipo especificado explícitamente. Dentro del bucle switch, el caso se referencia mediante la forma abreviada `.corazones` porque ya sabemos que el valor de `self` es un tipo de palo. Puedes utilizar la forma abreviada siempre que el tipo del valor ya sea conocido.

Si una enumeración tiene valores brutos, se establece que dicho valores forman parte de la declaración, lo que significa que cada instancia de un caso de enumeración en particular siempre tendrá el mismo valor bruto. Otra opción para los casos de enumeración es tener valores asociados con el caso; estos valores se determinan al crear la instancia y pueden ser diferentes para cada instancia de un caso de enumeración. Puedes ver los valores asociados como si actuaran como propiedades almacenadas de la instancia del caso de enumeración. Por ejemplo, considera el caso en el que se le pide a un servidor las horas de salida y puesta del sol. El servidor responderá con la información solicitada o responderá con una descripción de lo que haya salido mal.

```swift
enum RespuestaServidor {
    case resultado(String, String)
    case falla(String)
}

let success = RespuestaServidor.resultado("6:00 am", "6:00 pm")
let falla = RespuestaServidor.falla("Sin respuesta.")

switch success {
    case let .resultado(amanecer, atardecer):
        print("El amanecer se da a las \(amanecer) y el atardecer se da a las \(atardecer).")
    case let .falla(mensaje):
        print("Error...  \(mensaje)")
}
```

> EXPERIMENTA
>
> Agrega un tercer caso a `RespuestaServidor` y al bucle switch.



Observa cómo las horas de amanecer y atardecer se extraen del valor `RespuestaServidor` como parte de la comparación del valor con los casos del bucle switch.

Usa `struct` para crear una estructura. Las estructuras soportan muchos de los mismos comportamientos que las clases, incluyendo métodos e inicializadores. Una de las diferencias más importantes entre estructuras y clases es que las estructuras siempre son copiadas al pasarlas en tu  código, pero las clases se pasan por referencia.

```swift
struct Carta {
    var escala: Escala
    var palo: Palo
    func descripcionSimple() -> String {
        return "El \(escala.descripcionBasica()) de \(palo.descripcionBasica())."
    }
}
let tresDePicas = Carta(escala: .tres, palo: .picas)
let descripcionTresDePicas = tresDePicas.descripcionBasica()
```

> EXPERIMENTA
>
> Crea una función que devuelva un array que contenga una baraja completa de cartas, con una carta de cada combinación de escala y palo.



### Protocolos y Extensiones

Usa `protocol` para declarar un protocolo.

```swift
protocol ProtocoloEjemplo {
    var descripcionBasica: String { get }
    mutating func ajustar()
}
```



Las classes, enumeraciones, y estructuras pueden adoptar protocolos.

```swift
class ClaseBasica: ProtocoloEjemplo {
     var descripcionBasica: String = "Una clase muy básica."
     var otraPropiedad: Int = 69105
     func ajustar() {
          descripcionBasica += " Ahora 100% ajustada."
     }
}
var a = ClaseBasica()
a.ajustar()
let descripcionA = a.descripcionBasica

struct EstructuraBasica: ProtocoloEjemplo {
     var descripcionBasica: String = "Una estructura básica"
     mutating func ajustar() {
          descripcionBasica += " (ajustada)"
     }
}
var b = EstructuraBasica()
b.ajustar()
let descripcionB = b.descripcionBasica
```

> EXPERIMENTA
>
> Agrega otro requisito a `ProtocoloEjemplo`. ¿Qué cambios debes hacer en `ClaseBasica` y `EstructuraBasica` para que estas cumplan con el protocolo?



Nota el uso de la palabra clave `mutating` en la declaración de `EstructuraBasica` para marcar un método que modifica la estructura. En la declaración de `ClaseBasica` no se necesita que ninguno de sus métodos esté marcado como modificador ya que los métodos de una clase siempre pueden modificar la clase misma.

Utiliza `extension` para agregar funcionalidad a un tipo existente, como nuevos métodos y propiedades calculadas. Puedes usar una extensión para hacer que un tipo se ajuste a un protocolo, bien sea un tipo que se declara en otro lugar,  o incluso un tipo que se importa de una biblioteca o framework.

```swift
extension Int: ProtocoloEjemplo {
    var descripcionBasica: String {
        return "El número \(self)"
    }
    mutating func ajustar() {
        self += 42
    }
 }
print(7.descripcionBasica)
// Imprime "El número 7"
```

> EXPERIMENTA
>
> Crea una extensión para el tipo `Double` que agregue la propiedad `valorAbsoluto`.



Puedes usar el nombre de un protocolo como cualquier otro tipo con nombre; por ejemplo, para crear una colección de objetos que tiene tipos diferentes, pero que todos se ajusten a un solo protocolo. Al trabajar con valores cuyo tipo es un tipo de protocolo, los métodos externos a la definición del protocolo no estarán disponibles.

```swift
let valorProtocolo: ProtocoloEjemplo = a
print(valorProtocolo.descripcionBasica)
// Imprime "Una clase muy básica. Ahora 100% ajustada."
// print(valorProtocolo.otraPropiedad)  // Remueve este comentario para ver el error
```



Aun cuando el tipo de _runtime_ de la variable `valorProtocolo` es del tipo `ClaseBasica`, el compilador lo trata como el tipo dado de `ProtocoloEjemplo`. Esto significa que no puedes acceder, de manera accidental, a métodos o propiedades que la clase implementa además de su conformidad con el protocolo.



### Manejo de Errores

Puedes representar errores mediante cualquier tipo que adopte el protocolo `Error`.

```swift
enum ErrorImpresora: Error {
    case noHayPapel
    case noHayToner
    case enLlamas
}
```



Usa `throw` para arrojar un error y `throws` para marcar una función que puede arrojar un error. Si arrojas un error en una función, la función se interrumpe inmediatamente y el código que llamó a la función se encargará de manejar el error.

```swift
func enviar(tarea: Int, impresoraDestino nombreImpresora: String) throws -> String {
    if nombreImpresora == "Nunca Tiene Toner" {
        throw ErrorImpresora.noHayToner
    }
    return "Tarea enviada"
}
```



Hay muchas maneras de manejar los errores. Una forma es usando `do-catch`. Dentro del bloque `do`, marcas el código que puede arrojar un error escribiendo `try` delante de él. Dentro del bloque `catch`, al error se le asigna automáticamente el nombre `error`, a menos que le asignes un nombre diferente.

```swift
do {
    let respuestaImpresora = try enviar(tarea: 1040, impresoraDestino: "Bi Sheng")
    print(respuestaImpresora)
} catch {
    print(error)
}
// Imprime "Tarea enviada"
```

> EXPERIMENTA
>
> Cambia el nombre de la impresora a `"Nunca Tiene Toner"`, de manera que la función `enviar(tarea:impresoraDestino:)` arroje un error.



Puedes usar múltiples bloques `catch` que manejen errores específicos. Para esto, define un patrón después de `catch` al igual que lo haces después de `case` en un bucle switch.

```swift
do {
    let respuestaImpresora = try enviar(tarea: 1440, impresoraDestino: "Gutenberg")
    print(respuestaImpresora)
} catch ErrorImpresora.enLlamas {
    print("Dejaré esto por aquí, con el resto del fuego.")
} catch let errorImpresora as ErrorImpresora {
    print("Error impresora: \(errorImpresora).")
} catch {
    print(error)
}
// Imprime "Tarea enviada"
```

> EXPERIMENTA
>
> Agrega código de manera que se arroje un error dentro del bloque `do`. ¿Qué tipo de error es necesario arrojar para que este sea manejado por el primer bloque `catch`? ¿Qué tal con los bloques segundo y tercero?



Otra forma de manejar los errores es usando `try?` para convertir el resultado en un opcional. Si la función arroja un error, el error específico se descarta y el resultado es `nil`. De lo contrario, el resultado es un opcional que contiene el valor que devolvió la función.

```swift
let exitoImpresora = try? enviar(tarea: 1884, impresoraDestino: "Mergenthaler")
let fallaImpresora = try? enviar(tarea: 1885, impresoraDestino: "Nunca Tiene Toner")
```



Usa `defer` para crear un bloque de código que se ejecute después de todo el código de una función, justo antes de que la función devuelva su valor. El código se ejecuta sin importar que la función arroje un error. Puedes utilizar `defer` para escribir códigos de configuración y limpieza, uno al lado del otro, aun cuando estos deban ejecutarse en momentos diferentes.

```swift
var refrigeradorEstaAbierto = false
let contenidoRefrigerador = ["leche", "huevos", "sobras"]

func conocerContenidoRefrigerador(_ alimento: String) -> Bool {
    refrigeradorEstaAbierto = true
    defer {
        refrigeradorEstaAbierto = false
    }

    let resultado = contenidoRefrigerador.contains(alimento)
    return resultado
}
conocerContenidoRefrigerador("banana")
print(refrigeradorEstaAbierto)
// Imprime "false"
```



### Genéricos

Escribe un nombre entre paréntesis angulares \(`<>`\) para crear una función o tipo genérico.

```swift
func crearArray<Item>(repitiendo item: Item, numeroDeVeces: Int) -> [Item] {
    var resultado: [Item] = []
    for _ in 0..<numeroDeVeces {
        resultado.append(item)
    }
    return resultado
}
crearArray(repitiendo: "toc", numeroDeVeces: 4)
```



También puedes crear formas genéricas de funciones y métodos, al igual que, de clases, enumeraciones, y estructuras.

```swift
// Reimplementamos el tipo opcional de la librería estándar de Swift
enum OptionalValue<Wrapped> {
    case none
    case some(Wrapped)
}
var posibleEntero: OptionalValue<Int> = .none
posibleEntero = .some(100)
```



Utiliza `where` justo antes del cuerpo de la función para especificar una lista de requerimientos; por ejemplo, para requerir el tipo para implementar un protocolo, para requerir que dos tipos sean el mismo, o para requerir que una clase tenga una súperclase en particular.

```swift
func anyCommonElements<T: Sequence, U: Sequence>(_ lhs: T, _ rhs: U) -> Bool
    where T.Element: Equatable, T.Element == U.Element
{
    for lhsItem in lhs {
        for rhsItem in rhs {
            if lhsItem == rhsItem {
                return true
            }
        }
    }
    return false
}
anyCommonElements([1, 2, 3], [3])
```

> EXPERIMENTA
>
> Modifica la función `anyCommonElements(_:_:)` para crear una función que devuelva un array de los elementos que dos secuencias cualesquiera tienen en común.



Escribir `<T: Equatable>` es igual a escribir `<T> ... where T: Equatable`.



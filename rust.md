<center><h1><b>RUST LANG NOTES</b></h1></center>

## Prettiers y Linterns

-   Prettier: **`Rustfmt`**

-   Lintern: **`Clippy`**

<br />

# Variables

-   Variables no mutables

```rs
let nonumber = 10;
println!("The number is {}.", nonumber);
nonumber = 15
println!("The number is {}.", nonumber);
[SALIDA] = ErrorMessage
```

-   Variables mutables

```rs
let mut nonumber = 10;
println!("The number is {}.", nonumber);
nonumber = 15
println!("The number is {}.", nonumber);
[SALIDA] = {
  The number is 10.
  Now the number is 15.
}
```

-   Propiedad reemplazada de variables

```rs
// Declaramos la variable con un nombre "novalue"
let novalue = 5;

// Declaramos una segunda variable llamandola como al primera "novalue"
let novalue = novalue + 5;

// Declaramos la tercera variables, ocultando el valor de la primera y de la segunda "novalue"
let novalue = novalue * 2;

println!("The number is {}.", novalue);
[SALIDA] = The number is 20.
```

<br />

# Tipos de datos, números, texto y boleanos

```rs
let int_number: u32 = 14;
let float_number: f32 = 14.1;

let is_bigger = 1 > 4;
println!("Is 1 > 4? {}", is_bigger);

// IMPORTANTE
// Los tipo char, se marcan con una comilla simple '
let uppercase_s = 'S';
let lowercase_f = 'f';
let smiley_face = '😃';
// String siempre con comillas dobles
let string: &str = "Hola, como estan";
```

-   Firmado = Números Enteros
-   Sin signo = Naturales

![tabla](https://imgur.com/g9k2QqI.png)

## Tuplas

```rs
// Longitud de la tupla = 3
let tuple_e = ('E', 5i32, true);
// Se obtienen como
tuple_e.0 tuple_e.1 tuple_e.2
```

## Estructuras

```rs
// Estructura con campos de valor
struct Student { name: String, level: u8, remote: bool }
// Estructura solo con tipos
struct Grades(char, char, char, char, f32);
// Estructura de unidad
struct Unit;
```

-   Creación de un instancia de una estructura

```rs
// Instanciar estructura clasica, especifica campos de forma random, o en orden específico
let user_1 = Student { name: String::from("Constance Sharma"), remote: true, level: 2 };
let user_2 = Student { name: String::from("Dyson Tan"), level: 5, remote: false };

// Instanciar tuplas, pasamos el valor en el mismo orden que el tipo definido
let mark_1 = Grades('A', 'A', 'B', 'A', 3.75);
let mark_2 = Grades('B', 'A', 'A', 'C', 3.25);

println!("{}, level {}. Remote: {}. Grades: {}, {}, {}, {}. Average: {}",
         user_1.name, user_1.level, user_1.remote, mark_1.0, mark_1.1, mark_1.2, mark_1.3, mark_1.4);
println!("{}, level {}. Remote: {}. Grades: {}, {}, {}, {}. Average: {}",
         user_2.name, user_2.level, user_2.remote, mark_2.0, mark_2.1, mark_2.2, mark_2.3, mark_2.4);
```

## Conversión de un literal de cadena en un tipo String

```rs
// Estructura clasica
struct Student { name: String, level: u8, remote: bool }
...
let user_2 = Student { name: String::from("Dyson Tan"), level: 5, remote: false };
```

## Definición de una enumeración

```rs
enum WebEvent {
    // Una variante de enum puede ser como una estructura unitaria sin campos ni tipos de datos
    WELoad,
    // Una variante de enum puede ser como una estructura de tupla con tipos de datos pero sin campos con nombre
    WEKeys(String, char),
    // Una variante de enum puede ser como un struct clásico con campos con nombre y sus tipos de datos
    WEClick { x: i64, y: i64 }
}
```

## Definición de una enumeración con estructuras

```rs
// Definir una estructura de tupla
struct KeyPress(String, char);

// Definir una estructura clasica
struct MouseClick { x: i64, y: i64 }

// Redefine las variantes del enum para utilizar los datos de los nuevos structs
// Actualizar la página Variante de carga para que tenga el tipo booleano
enum WebEvent { WELoad(bool), WEClick(MouseClick), WEKeys(KeyPress) }
```

## Creación de una instancia de una enumeración

-   Variante de estructura: WEClick(MouseClick)

```rs
let we_load = WebEvent::WELoad(true);
// Instanciar una estructura MouseClick y vincular los valores de las coordenadas
let click = MouseClick { x: 100, y: 250 };

// Configurar la variante WEClick para utilizar los datos de la estructura de clics
let we_click = WebEvent::WEClick(click);
```

-   Variante de tupla: WEKeys(KeyPress)

```rs
// Instanciar una tupla KeyPress y vincular los valores de las teclas
let keys = KeyPress(String::from("Ctrl+"), 'N');

// Establezca la variante WEKeys para utilizar los datos de la tupla keys
let we_key = WebEvent::WEKeys(keys);
```

## Ejemplo de enumeraciones

```rs
// Definir una estructura de tupla
#[derive(Debug)]
struct KeyPress(String, char);

// Definir una estructura clásica
#[derive(Debug)]
struct MouseClick { x: i64, y: i64 }

// Definir las variantes del enum WebEvent para utilizar los datos de los structs
// y un tipo booleano para la página Variante de carga
#[derive(Debug)]
enum WebEvent { WELoad(bool), WEClick(MouseClick), WEKeys(KeyPress) }

// Instanciar una estructura MouseClick y vincular los valores de las coordenadas
let click = MouseClick { x: 100, y: 250 };
println!("Mouse click location: {}, {}", click.x, click.y);

// Instanciar una tupla KeyPress y vincular los valores de las teclas
let keys = KeyPress(String::from("Ctrl+"), 'N');
println!("\nKeys pressed: {}{}", keys.0, keys.1);

// Instanciar las variantes del enum WebEvent
// Establecer el valor booleano de carga de la página a true
let we_load = WebEvent::WELoad(true);
// Configurar la variante WEClick para utilizar los datos de la estructura de clics
let we_click = WebEvent::WEClick(click);
// Establezca la variante WEKeys para utilizar los datos de la tupla keys
let we_key = WebEvent::WEKeys(keys);

// Imprime los valores de las variantes del enum WebEvent
// Utilice la sintaxis {:#?} para mostrar la estructura y los datos del enum de forma legible
println!("\nWebEvent enum structure: \n\n {:#?} \n\n {:#?} \n\n {:#?}", we_load, we_click, we_key);
```

<br />

# Funciones

```rs
fn goodbye(message: &str) {
  println!("\n{}", message);
}

fn main() {
  let formal = "Formal: Good bye.";
  let casual = "Casual: See you later!";
  goodbye(formal);
  goodbye(casual);
}

[SALIDA] => {
  Formal: Good bye.
  Casual: See you later!
}
```

-   Devolución de un valor

```rs
fn divide_by_5(num: u32) -> u32 {
    num / 5
}

fn main() {
    let num = 25;
    println!("{} divided by 5 = {}", num, divide_by_5(num));
}

[SALIDA] => {
    25 divided by 5 = 5
}
```

### Se puede usar la palabra clave `return` en cualquier punto de la función para detener la ejecución y devolver un valor al autor de la llamada. Normalmente, la palabra clave `return` se usa junto con una prueba condicional.

<br />

# Creación y uso de matrices

```rs
// Crear una matriz de enteros de 3x3
let days = ["Lunes", "Martes", "Miercoles", "Jueves", "Viernes", "Sabado", "Domingo"];
// Declaramos un array, inicializado con todos los valores de 0 a 4
let bytes = [0; 5];
```

```
En tiempo de compilación, la firma de una matriz se define como [T; size]:

T es el tipo de datos de todos los elementos de la matriz.
size es un entero no negativo que representa la longitud de la matriz.
La firma revela dos características importantes sobre las matrices:

Todos los elementos de una matriz tienen el mismo tipo de datos. El tipo de datos nunca cambia.
El tamaño de una matriz es fijo. La longitud nunca cambia.
```

## Indexación de matrices

```rs
let days = ["Lunes", "Martes", "Miercoles", "Jueves", "Viernes", "Sabado", "Domingo"];

let first = days[0];
let second = days[1];
```

<br />

# Definición de vectores

```rs
// Crear un vector de enteros de 3 elementos
let three_nums = vec![15, 3, 46];
println!("Vector inicial: {:?}", three_nums);

// Creamos un vecto de 0 que se rellena con los valores de 0 a 4
let zeroes = vec![0; 5];
println!("Vector de ceros: {:?}", zeroes);

[SALIDA] => {
    Vector inicial: [15, 3, 46]
    Vector de ceros: [0, 0, 0, 0, 0]
}

// | ---------VECTORES MUTABLES--------- |

// Creamos un vector vacio, que se declara como mutable para que podamos agregar elementos
let mut fruits = Vec::new();
```

<br />

# Definición de condicionales

```rs
if 1 == 2 {
    println!("1 is not equal to 2");
} else {
    println!("1 is equal to 2");
};

let saludo = if 1 == 2 {
    "Buenos dias"
} else {
    "Buenas noches"
};
```

<br />

# Definición de un mapa hash

```rs
// El comandos `use` permite importar una librería en el código
use std::collections::HashMap;
// Creamos HashMap vacio
let mut reviews: HashMap<String, String> = HashMap::new();

// Agregamos un par clave-valor al mapa
reviews.insert(String::from("Blue"), String::from("Great movie!"));
reviews.insert(String::from("Yellow"), String::from("Good movie!"));
reviews.insert(String::from("Red"), String::from("Bad movie!"));

```

## Obtención de un valor de clave

```rs
let color: &str = "Blue";
println!("Valor de {} es {}", color, reviews.get(color));
```

## Eliminación de un par clave-valor

```rs
let color: &str = "Blue";
reviews.remove(color);

println!("Valor de {} es {}", color, reviews.get(color));

[SALIDA] => Valor de Blue es None
```

<br />

# Bucles

## Loop

```rs
loop {
    println!("Loop Infinito");
}

loop {
  println!("Loop");
  break; // Se detiene el bucle
}

let mut counter: u32 = 0;

loop {
  println!("{}", counter);
  counter += 1;
  if counter == 10 {
    break counter;
  }
}
```

## While

```rs
while counter < 10 {
  println!("{}", counter);
  counter += 1;
}
```

## For

```rs
for counter in 0..10 {
  println!("{}", counter);
}

let books = ["The Road to Rust", "The Rust Programming Language", "The Rust Book"];
for book in books.iter() {
  println!("{}", book);
}
```

# Trata de Errores

-   `panic!` es como un throw en Java, pero en Rust.
-   `panic!` se usa para lanzar una excepción.

```rs
fn main() {
    panic!("An error has occurred.");
}

let vect = vec![1, 2, 3];
println!("{:?}", vect[6]); // Causara un `panic!`
```

```rs
enum Option<T> {
  None, // No hay valor
  Some(T), // Hay un valor
}

let frutas = vec!["Manzana", "Pera", "Naranja"];

let primera = frutas.get(0);
println!("{:?}", primera);
let segunda = frutas.get(1);
println!("{:?}", segunda);
let no_existente = frutas.get(99);
println!("{:?}", no_existente);

[SALIDA] => {
  Some("Manzana")
  Some("Pera")
  None
}
```

## Detección de patrones

```rs
let frutas = vec!["Manzana", "Pera", "Naranja"];
for &index in [0, 2, 99].iter() { // &index es una referencia a un índice
  match frutas.get(index) { // match es una expresión de patrón
    Some(fruta) => println!("{}", fruta), // Si el índice existe, imprime el valor
    None => println!("No existe la fruta en el índice {}", index), // Si el índice no existe, imprime un mensaje
  }
}

[SALIDA] => {
  Manzana
  Naranja
  No existe la fruta en el índice 99
}
```

## Uso de `unwrap` y `expect`

```rs
let gift = Some("Golosina");
assert_eq!(gift.unwrap(), "Golosina");

let empty: Option<&str> = None;
assert_eq!(empty.unwrap(), "Golosina"); // Se lanza un `panic!`
```

```rs
let a = Some("value");
assert_eq!(a.expect("No hay valor"), "value");

let b = None;
assert_eq!(b.expect("No hay valor"), "No hay valor"); // Se lanza un `panic!`
```

## Uso del tipo Result para controlar errores

```rs
enum Result<T, E> {
  Ok(T),
  Err(E),
}

#[derive(Debug)]
struct DivisionByZeroError;

fn safe_division(dividend: f64, divisor: f64) -> Result<f64, DivisionByZeroError> {
    if divisor == 0.0 {
        Err(DivisionByZeroError)
    } else {
        Ok(dividend / divisor)
    }
}

fn main() {
    println!("{:?}", safe_division(9.0, 3.0));
    println!("{:?}", safe_division(4.0, 0.0));
    println!("{:?}", safe_division(0.0, 2.0));
}

[SALIDA] => {
  Ok(3.0)
  Err(DivisionByZeroError)
  Ok(0.0)
}
```

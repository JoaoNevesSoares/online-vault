# [[Rust Learning Center]]

> [!tip]- Compiler Explorer
> [CompilerExplorer](https://rust.godbolt.org)

>[!tip]- check Rust Version
>`$ rustc --version`

>[!tip]- IDE support
>The Rust team has been focusing on enabling great IDE support via `rust-analyzer`. See [Appendix D](https://doc.rust-lang.org/book/appendix-04-useful-development-tools.html) for more details.

>[!tip]- Formatar código
>Ferramenta _rustfmt_. 
>(vem incluído com a instalação do rust no MacOS/Linux)

> [!tip]- Cargo book - Buscar como passar argumentos durante cargo run/build e transformar em constantes ou macro
> [cargo book](https://doc.rust-lang.org/cargo/)
# Anatomia do programa _Hello World_ em Rust
```rust
//filename: main.rs
fn main() {
    println!("Hello, world");
}
```
1. Para compilar um programa em Rust
	- `$ rustc main.rs`
2. `println!("Hello, world");` **NÃO** é uma função, é uma **MACRO** (tem um "_!_" após o _println_).

# [[Cargo]]
>[!quote] If you start using Cargo, adding deppendencies will be much easier to do!

>Let’s recap what we’ve learned so far about Cargo:
>_All commands bellow must be executed inside acargo project dir!_
> -   We can create a project using `cargo new`.
> -   We can build a project using `cargo build`.
> -   We can build and run a project in one step using `cargo run`.
> -   We can build a project without producing a binary to check for errors using `cargo check`.
> -   Instead of saving the result of the build in the same directory as our code, Cargo stores it in the _target/debug_ directory.

# Variáveis e imutabilidade
Por padrão, no Rust, as variáveis são _imutáveis_. Um dos motivos de utilizar essa abordagem é segurança e facilidade para programação concorrente. 
> Uma _variável imutável_, não pode ter seu conteúdo (valor) modificado uma vez que declarada no programa.
```rust
// declaring variables in Rust
let x =5;
let y = &x;
```

>[!nfo] Uma variável não pode ter um valor atribuído que seje diferente do seu tipo especificado.
>```rust 
>// This example does not compile!!!
>fn main() {
>    let mut x:u32 = 1;
>    x = "Hello world";
>    println!("{x}");
>}
>```
## Constantes em Rust
Constantes se diferenciam de variáveis por serem _sempre_ imutáveis e precisam ter seu tipo _anotado_. Além disso, constantes possuem escopo global, sendo possível declara-las externamente às funções, o que não é permitido com as variáveis declaradas utilizando _let_.
```rust
// declaring constants
const THREE_HOURS_IN_SECONDS: u32 = 60*60*3
```
>[!tip] A convenção para nomes de constantes em Rust é utilizar todas as letras em _UpperCase_ 
>

# Tipo de dados
>[!info] Rust é uma linguagem de programação _statically typed_
>Isso quer dizer que, os tipos das variáveis/constantes devem ser conhecidos em tempo de compilação. Em alguns casos, o compilador consegue inferir qual o tipo que está sendo utilizado com base no _p-value_ (lado direto da atribuição).
## Tipos primitivos / Escalares
Estão presentes em Rust:
- integers
- floating point
- boolean
- character
### Tipo: Integer
u[8/16/32/64/128] para valores _Unsigned_
i[8/16/32/64/128] para valores _Signed_
- _isze_ / _usize_ para definir o tipo do inteiro de acordo com a arquitetura utilizada.
>[!info] Handling Overflow
> - Wrap in all modes with the `wrapping_*` methods, such as `wrapping_add`.
> - Return _None_ value if there is overflow with the `checked_*` methods.
> - Return the value and a boolean indicating whether there was overflow with the `overflow_*` methods
> - Saturate at the value's minimum or maximum values with the `saturating_*` methods

### Tipo: Floating Point
-default: f64
- f32
- All floating point are signed
Exemplo:
```rust
let x = 2.0; //default is f64
let y: f32 = 1.99; // setting the type f32
```

# Tipos Compostos primitivos
Tipos compostos podem agrupar múltiplos valores em um tipo. Rust possui 2 tipos compostos primitivos: tuplas e arrays.
## Tuplas
- Possuem tamanho fixo, após serem declaradas, não é possível aumentar ou diminuir o número de elementos.
- Os valores presentes em uma tupla _NÃO_ precisam ser do mesmo tipo
```rust
//testando uso composto de dados
fn main(){
let tup = (500, 6.4, 1);
let tup_x: (i32,f64,u8) = (10,22.3,1); // É opcional declarar o tipo dos valores que a tupla irá receber.
let (x, y, z) = tup; // tupla pode ser "destruída" em diferentes variáveis.
let third = tup_x.2; // referenciando um valor da tupla por um índice (indices vão de 0 n-1)
// Indice não pode ser uma variável nem uma constante nomeada
println!("The value of y is {y} in tup");
println!("The third value of tup_x is {third}");
println!("The first value of tup_x is {}",tup_x.0);
}
```
## Arrays
- Possuem número fixo de elementos
- Todos os elementos presentes em um array devem ser do mesmo tipo
- Arrays são úteis quando precisa-se que os dados estejam alocados na _stack_ ao invés da _heap_.
```rust
// Declaração típica de um array em Rust
let a: [i32; 4] = [1,3,5,7];
let b = [1,2,3,4,5];
let c = [0.0;10]; // [x; y] -> inicializa um array com y copias do valor x
```
`i32` indica o tipo dos elementos, e `4` indica o número de elementos

### Exemplo completo:
```rust
fn main(){

 let t = ([1;2], [3;4]);
 let (a, _) = t;
 println!("{}",a[0] + t.1[0]); // qual o resultado ?
}
```
> A sintaxe [x; y] declara um array com _y_ cópias do valor _x_, já sintaxe (a, \_) desconstrói a tupla _t_ e vincula _a_ para [1;2] 
> 
# Funções
- São declaradas com a `keyword` `fn`
- Utiliza a convenção de nomes _Snake_case_ para funções e variáveis.
- Rust não se importa onde é definida as funções, a única coisa que importa é que deve estar no escopo que o caller possa enxergar.
## Parametros
> Na assinatura de funções, é **obrigatório** declarar o tipo de cada parametro. Essa é uma decisão deliberada do Design do Rust. A necessidade de tipos na assinatura de funções garante que o compilador quase nunca precise procurar em um outro lugar do código para descobrir qual é o tipo do parametro.

```rust
fn main() {
	let x:i32 = 10;
	let y:i32 = 12;
	soma_dois(x,y);
}
fn soma_dois(x:i32, y:i32){

	println!("{}",x+y);
}
```

## Retorno de funções
- Indicamos que uma função retorna um valor através da `->` seguido pelo tipo do retorno
- As funções assinaladas com retorno,retornam valor inplicitamente ao final do seu escopo
- É possível retornar antes utilizando o keyword `return`

# Statements and Expressions (Declarações e expressões)
> [!info] O que é um statement (declaração)?
> Declarações são instruções que performam alguma ação e _não retornam_ um valor.
> Criar uma variável e instânciar um valor para ela é o que chamamos de _statement_.
> - Exemplo: `let x = 6;` em **Rust**
> Dessa forma em rust não é permitido construções do tipo: 
> 	- `x = y = 10;`, 
> 	- `let x = (let y = 6);`
> 

> [!info] O que são Expressions? 
> Expressões são instruções que avaliam para um valor resultado.
> Ex: `5 + 6` avalia para 11;
> Exemplo de expressões:
> - Uma chamada de função é uma expressão
> - uma chamada de uma macro é uma expressão
> - Um novo bloco de escopo criado com _{ }_ é uma expressão
> Exemplo:
> ```rust
> fn main() {
> 	let y = { 
> 		let x = 3;
> 		x +3};
> 	println!("O valor de y = {y}");
> }
> ```
> Neste exemplo específico, nota-se que em Rust Expressões não incluem terminar com dois pontos "_;_"

### Atribuições multiplas aninhadas em Rust
> Atribuições do tipo x = y = z não são permitidas com o uso de _let_, uma das formas é criar um escopo único para atribuição e retorna-lo ao final.
```rust
// implementação de int x = y = z = 10;
let x:i32 = {let y:i32 = {let z:i32 = 10; z}; y};
```

# Structs
> Os valores dos campos da struct pode serem de diferentes tipos, e diferente das tuplas, que os valores devem ser acessados em ordem, a struct possui nome para os campos tornando-os mais flexiveis para acesso dos dados.
- _Field data can be of different types_
## Tuple Structs
>Tuple structs are useful when you want to give the whole tuple a name and make the tuple a different type from other tuples.
```rust
struct Color(i32, i32, i32); 
struct Point(i32, i32, i32); 
fn main() { 
	let black = Color(0, 0, 0); let origin = Point(0, 0, 0); 
}
```
>`black` and `origin` values are different types because they’re instances of different tuple structs. Each struct you define is its own type, even though the fields within the struct might have the same types.
## Unit-Like Structs without Any Fields
- São structs que não possuem _nenhum campo_.
>Can be useful when you need to implement a trait on some type but don’t have any data to store in the type itself.
```Rust
struct AlwaysEqual;
fn main() {
    let subject = AlwaysEqual;
}
```


# Fluxo de Controle
## Condicionais IF-ELSE
`if _expression_ { _execute this block_}`
- A expressão de um condicional **deve** avaliar para um **tipo booleano**.
> [!bug] O trecho abaixo resulta em erro!
> ```rust
> fn main() { 
> 	let number = 3;
> 	if number { // number não é um booleano
> 		println!("Número é três!");
> 	}
> }
> ```

- Using if in a _let_ statement
1. Opção
	```rust
	fn main() {
	let condition = true;
	let x = if condition { 0 } else { 1 };
	}
	```
2. Opção
```rust
fn main() {
	let x;
	if cond {
		x =1;
	}
	else{
		x =2;
	}

}
```
A segunda opção funciona mesmo que x não seja declarado como `mut` pois _x_ será atribuído apenas uma única vez.

## Laços usando `loop`
- Loops criados com a palavra reservada `loop` executam indefinidamente até uma condição explícita de parada com a palavra reservada `break`!
> [!quote] One of the uses of a `loop` is to retry an operation you know might fail, such as checking whether a thread has completed its job.
### retornando valores de `loop`
- É possível que um bloco `loop` retorne um valor, este deve ser indicado após a palavra reservada `break`.
```rust
// Retorno de um loop como assignment de uma variável com let.
fn main() {
let mut x = 0;
let y = loop {
	
	
	if x <10{
	
	x+=1;
	
	}
	
	else {
	
	break x*100;
	
	}
};
println!("loop x = {x}, y = {y}");
}
```


### Rótulos em loops
- É possível rotular loops em rust para termina-los dentro de um loop mais interno.
- Sintaxe: `'rotulo: loop {}` – `break 'rotulo;`

## Laços usando `while`
- Semelhante a outras linguagens de programação
```rust
fn main() {
	let mut number = 3;
	while number !=0{
		println!("{number}!");
		number -= 1;
	}
	println!("LIFTOFF!!");
}
```

## Laços usando `for`
>[!info] While vs For
>Usar `while` para iterar sobre uma coleção de dados é mais lento que utilizar a instrução `for`, pois o compilador adiciona código em tempo de execução toda vez que performarmos um verifição de condição para saber se o índice está no intervalo do array a cada iteração do laço.
### Iterando sobre um conjunto de dados
```rust
fn main() {
	let a = [10,20,30,40];

	for element in a {
	
	println!("O valor do elemento é {element}");
	
	}
}
```

### Iterando sobre um intervalo de dados
```rust
fn main() {
	let mut a: [usize; 10] = [0,0,0,0,0,0,0,0,0,0];

	for index in 0..10 {

		a[index] = index;

	println!("valor de a[{}] = {}",index,a[index]);
	}
}
```

# Ownership

> _Memory is managed through a system of ownership with a set of rules that the compiler checks. 
> If any of the rules are violated, the program won’t compile. None of the features of ownership will slow down your program while it’s running._
> 

## Regras de Ownership
- Em Rust, cada valor possui um _owner_.
- Só é possível ter um único _owner_ por vez.
- Quando o _owner_ saí de escopo, o valor será dropped.

## Como o Rust sabe _limpar_ os dados que estão na HEAP ?

> Em rust a memória é retornada automaticamente assim que a variável que a possui sai do escopo.

- tipo `String`
	Esse tipo manipula dados alocados na heap e com isso é possível armazenar quantidade de texto que é desconhecida para nós em tempo de compilação.
	- Criando uma String
		`let s = String::from("hello");`

## Movendo dados e interagindo

- Segue o exemplo com valor _inteiro_
```rust
fn main() {

let x = 5;
let y = x;

}
```
Podemos ler o código acima do modo: "_Víncule o valor 5 em x e faça uma cópia do valor em x para y_". Isso ocorre dessa forma pois x e y estão na _stack_.

- Segue o exemplo com tipo _String_.
```rust
fn main(){

	let s1 = String::from("Sou uma string na Heap");
	let s2 = s1;
}
```
Quando vínculamos uma variável com um tipo de dado que está armazenado na _heap_, como fizemos em _s1_, cria-se um envólucro contendo 3 entradas na _stack_: 
1. Um ponteiro para area de memória onde está armazenado o valor na _heap_.
2. O tamanho atual que o valor ocupa na memória.
3. A capacidade total que foi destinada para o valor na _heap_.
e o valor propiamente dito está armazenado na _heap_.
Quando fazemos a operação `s2 = s1` estamos copiando o conteúdo de _s1_ presente na _stack_ e vínculando a _s2_. **Em nenhum momento estamos copiando o valor da string armazenada na heap!!**
>[!bug] Agora s1 e s2 estão referenciando a mesma posição na Heap
>Este é um erro que o Rust resolve fazendo que _s1_ saia de escopo depois da atribuição `let s2= s1;` e tornando _s2_ a única referência válida para aquele bloco de memória. Portanto ao fazer referência à _s1_ após esta linha, causará erro de compilação.
### Cópia do conteúdo armazenado na HEAP
Chamamos esta operação de copiar o conteúdo da heap de _cópia profunda_. Em rust o método `.clone` é responsável por realizar este processo.
```rust
fn main() {
    let s = String::from("sou uma string");
    let s1 = s.clone();
    println!("s1 é um clone e possui conteúdo == {s1}");
    println!("s é o original e possui conteúdo == {s}");
}
```


## Ownership e funções
Passar uma variável para uma função irá _mover_ ou _copiar_.
- Quando a variável for de um tipo em que o valor é armazenado na _heap_. Ao passar para uma função fará com que a variável perca seu escopo e mova o conteúdo.
```rust
fn main() {
    let s = String::from("hello");  // s comes into scope

    takes_ownership(s);             // s's value moves into the function...
                                    // ... and so is no longer valid here
} // Here Nothing special happens because s has already lost his scope after //takes_ownership funcion

fn takes_ownership(some_string: String) { // some_string comes into scope
    println!("{}", some_string);
} // Here, some_string goes out of scope and `drop` is called. The backing
  // memory is freed.
```
- Agora, se for o caso de um tipo escalar em que o valor é armazenado na _stack_, irá copiar o conteúdo para outra variável na heap e manter o escopo da variável passada para função.
```rust
fn main() {
    let x = 5;                      // x comes into scope
    makes_copy(x);                  // x would move into the function,
                                    // but i32 is Copy, so it's okay to still
                                    // use x afterward
} // Here, x goes out of scope

fn makes_copy(some_integer: i32) { // some_integer comes into scope
    println!("{}", some_integer);
} // Here, some_integer goes out of scope. Nothing special happens.

```

## References and borrowing
>[!info] Resumo
> Refêrencias previnem que uma variável passe sua _ownership_ e termine seu escopo.

>Referências permite fazer uma referência a um valor de uma variável sem obter a ownership dela.

>[!tip] Dereferencing
>O oposto da refêrencia que é obtido ao usar o operador `*`, será visto com mais detalhes no capitulo 8 e discutido os detalhes no capitulo 10.
- Exemplo: Passar a refêrencia uma variável para outra
	```rust
	fn main(){
		let s = String::from("eu sou uma string");
		let ref_to_s = &s;
		println!("Imprimindo o valor da referência {ref_to_s}");
		println!("S ainda existe = {s}");
	}
	```
Utiliza-se o símbolo _&_ para passar uma refêrencia para outra variável. Neste caso a variável s não perde o ownership e só será desalocada quando o escopo da função _main_ terminar.
- Exemplo: Passar valores da _HEAP_ como argumento para funções sem perder referência
	```rust
	fn main(){
	let s = String::from("eu sou uma string");
	reference_passing(&s);
	println!("S ainda existe = {s}");
	}
	
	fn reference_passing(sx: &String){
	println!("imprimindo s dentro de uma função: {sx}");
	}
	```

### Mutable References
Para passar uma referência mutável para uma função é necessário a seguinte sintaxe:
- Como argumento `foo(mut &varname);`
- Como parametro `fn foo(varname: &mut type){}`

>[!bug] Restrição
>Só é possível existir uma única referência mutável para um valor específico.
>Essa restrição previne que multiplas referências para mesma area de memória em um determinado escopo de código. Essa restrição permite que o Rust previna condições de _data races_ em tempo de compilação. 
>	_data race_ é:
>- A condição em que dois ou mais ponteiros tentem acessar a mesma posição de memória ao mesmo tempo para ler ou escrever.
>- Onde não existe um mecanismo para sincronizar o acesso ao dado.
>- >** _Rust prevents this problem by refusing to compile code with data races!_**
>

### Regras de Referências
- A qualquer momento, você só pode ter ou uma referencia mutável ou várias referências imutáveis para a mesma variável.

# Managing Rust projects

- Crate:
	It is the smallest amount of code that the Rust compiler considers at a time. Crates can contain modules, and modules may be defined in other files that get compiled with the crate. Crate can come in one of two forms: 
	- _binary crate_: programs that compile and execute. each must have a `fn main()` funcion.
	- _Library crate_: don't have `main` function, and they don't compile to an executable. They define functionality intended to be shared with multiple projects.
- Crate _root_:
	Is a source file that the Rust compiler starts from and makes up the root module of your crate.
- Package:
	A _package_ is a bundle of one or more crates that provides a set of functionality. A package contains a _Cargo.toml_ file that describes how to build those crates. A package can contain as many binary crates as you like, but at most only one library crate. A package must contain at least one crate, whether that’s a library or binary crate.

Para criar um package:
`$ cargo new my-project`
 - Cargo follows a convention that _src/main.rs_ is the crate root of a binary crate with the same name as the package.
 - Cargo knows that if the package directory contains _src/lib.rs_, the package contains a library crate with the same name as the package, and _src/lib.rs_ is its crate root.
> How modules Work
> - **Start from the crate root**: When compiling a crate, the compiler first looks in the crate root file (usually _src/lib.rs_ for a library crate or_src/main.rs_ for a binary crate) for code to compile.
> -   **Declaring modules**: In the crate root file, you can declare new modules; say, you declare a “garden” module with `mod garden;`. The compiler will look for the module’s code in these places:
> 	- Inline, within curly brackets that replace the semicolon following `mod garden`
> 	- In the file _src/garden.rs_
> 	- In the file _/src/garden/mod.rs_
> 

>[!tip] Best practices for packages with a binary and a Library
>	The module tree should be defined in _src/lib.rs_. Then, any public items can be used in the binary crate by starting paths with the name of the package. The binary crate becomes a user of the library crate just like a completely external crate would use the library crate: it can only use the public API. This helps you design a good API; not only are you the author, you’re also a client!

Re-exporting Names with pub use

# Using External Packages
<div class="rich-link-card-container"><a class="rich-link-card" href="https://dev.to/yjdoc2/make-a-combined-library-and-binary-project-in-rust-d4f" target="_blank">
	<div class="rich-link-image-container">
		<div class="rich-link-image" style="background-image: url('https://dev.to/social_previews/article/597565.png')">
	</div>
	</div>
	<div class="rich-link-card-text">
		<h1 class="rich-link-card-title">Make a Combined Library and Binary Project in Rust</h1>
		<p class="rich-link-card-description">
		In this article, we will take a look at how to create a combined library-binary project in Rust.  In...
		</p>
		<p class="rich-link-href">
		https://dev.to/yjdoc2/make-a-combined-library-and-binary-project-in-rust-d4f
		</p>
	</div>
</a></div>
<div class="rich-link-card-container"><a class="rich-link-card" href="https://web.mit.edu/rust-lang_v1.25/arch/amd64_ubuntu1404/share/doc/rust/html/book/first-edition/crates-and-modules.html#importing-external-crates" target="_blank">
	<div class="rich-link-image-container">
		<div class="rich-link-image" style="background-image: url('https://web.mit.edu/rust-lang_v1.25/arch/amd64_ubuntu1404/share/doc/rust/html/book/first-edition/favicon.png')">
	</div>
	</div>
	<div class="rich-link-card-text">
		<h1 class="rich-link-card-title">Crates and Modules - The Rust Programming Language</h1>
		<p class="rich-link-card-description">
		
		</p>
		<p class="rich-link-href">
		https://web.mit.edu/rust-lang_v1.25/arch/amd64_ubuntu1404/share/doc/rust/html/book/first-edition/crates-and-modules.html#importing-external-crates
		</p>
	</div>
</a></div>

<div class="rich-link-card-container"><a class="rich-link-card" href="https://www.reddit.com/r/rust/comments/jx6rwm/multiple_library_files_modules_with_multiple/" target="_blank">
	<div class="rich-link-image-container">
		<div class="rich-link-image" style="background-image: url('')">
	</div>
	</div>
	<div class="rich-link-card-text">
		<h1 class="rich-link-card-title">r/rust - Multiple library files (modules?) with multiple binaries in Cargo Project</h1>
		<p class="rich-link-card-description">
		5 votes and 4 comments so far on Reddit
		</p>
		<p class="rich-link-href">
		https://www.reddit.com/r/rust/comments/jx6rwm/multiple_library_files_modules_with_multiple/
		</p>
	</div>
</a></div>

```rust
fn example(width: usize, height: usize) {
    // Base 1d array
    let mut grid_raw = vec![0; width * height];

    // Vector of 'width' elements slices
    let mut grid_base: Vec<_> = grid_raw.as_mut_slice().chunks_mut(width).collect();

    // Final 2d array `&mut [&mut [_]]`
    let grid = grid_base.as_mut_slice();

    // Accessing data
    grid[0][0] = 4;
}
```

# Enums
> Enums representa diferentes tipos que um valor pode assumir.


## Option Enum
> Em Rust, um tipo pode ser "`Algum`" ou `"Nenhum"`. 

> [!info] É uma Enum presente na _Standard Library_ do Rust
> Seu uso é comum para lidar com casos onde um valor pode representar alguma coisa, mas também pode representar **nada**.
> Em termos do _type system_, significa que o compilador pode verificar se o programador tratou todos os casos que deveria, _essa funcionalidade pode previnir bugs que são extremamente comum em outras linguagens de programação._
> 
- Não existe o valor `NULL` em Rust. 
- Solução: `enum Option<T>`
```rust
enum Option<T> {
    None,
    Some(T),
}
```
- `<T>` significa que a variante `Some` do ennum `Option` pode guardar um certo dado de qualquer tipo.

> [!bug] Um dos erros mais comuns das linguagens de programação que utilizam de `NULL`
> É assumir que um valor não é `NULL`, quando na verdade é!
> Rust elimina o risco de assumir incorretamente que um valor é não-nulo limitando o programador a fazer o _handling_ do tipo `Option<T>` nos casos que um valor pode vir a ser `NULL`.
> Exemplo:
let x: i8 = 5; 
let y: Option<i8> = Some(5);
> let sum = x + y;
> // Esse código Não compila!
> ```
> > error[E0277]: cannot add `Option<i8>` to `i8`
> 
> Como resolver:
> ```rust
> fn main() {
>let x: i8 = 5;
>let y: Option<i8> = Some(5);
>let sum: i8;
>match y {
>Some(T) => {sum = x + y.unwrap();},
>None => { println!("Value is NULL"); return;} ,
>}
>println!("x + y = {}",sum);
>}
>```
> - Uma solução mais idiomática
>
>
>```rust
fn main() {
let x: i8 = 5;
let y: Option<i8> = Some(5);
let sum: i8;
if y.is_some() {
sum = x + y.unwrap();
}
else{
return;
}
println!("x + y = {}",sum);
}


# Generic Types, Traits, and Lifetimes

## Generics

## Traits
> [!info] Traits are similar to a feature often called _interfaces_ in other languages, although with some differences.

- Cada tipo implementando uma trait deve providenciar seu próprio "conteúdo" para o corpo das assinaturas dos métodos declarados na Trait.

> [!tip] `impl Trait` e Closures & Iterators
> The ability to specify a return type only by the trait it implements is especially useful in the context of closures and iterators, which we cover in Chapter 13. Closures and iterators create types that only the compiler knows or types that are very long to specify. The `impl Trait` syntax lets you concisely specify that a function returns some type that implements the `Iterator` trait without needing to write out a very long type. 

Trait e _Trait bounds_ nos deixam escrever código que usa parametros do tipo genérico para reduzir código duplicado além de especificar para o compilador que queremos que o tipo genérico tenha um comportamento específico.

## Lifetimes

Lifetimes garantem que referencias serão válidas o tempo necessário que precisar.

[[Rust Concurrency]]

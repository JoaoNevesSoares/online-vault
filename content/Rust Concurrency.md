- Criar threads para rodar multiplos pedações de código ao mesmo tempo.
- _Message-passing_ Concurrency, onde _channels_ enviam mensagens entre threads
- _Shared-state_ Concurrency, onde várias threads possuem acesso a algum dado.
- Os Traits **Sync** e **Send** que extendem a garantia da concorrencia em tipos definidos pelo usuário e tipos providos pelo standard library

# Usando Threads in Rust

>The Rust standard library uses a _1:1_ model of thread implementation

## Criando Threads com método _spawn()_
```rust
use std::thread;

fn main() {
	
	thread::spawn(
		|| {
			//thread code
		});
}
```
Neste Exemplo criamos uma thread com método spawn() da library _std::thread_ passamos como argumento uma closure que executa algum código em concorrente.

## A keyword _move_ 
- Faz com que a closure pegue o _ownership_ dos valores do ambiente. É usualmente utilizada com threads, para passar os ownership dos dados para a thread. Uma das razões de utilizar _move_ é que os dados do ambiente da thread pai, pode acabar antes da thread filha terminar, e consequentemente "dropando" os valores que pode resultar em _dangling references_.
```rust
use std::thread;
fn main() {
	let list = vec![1, 2, 3];
	println!("Before defining closure: {:?}", list);
	thread::spawn( move || println!("From thread: {:?}", list)) .join().unwrap();
}
```
- No Exemplo acima, se não utilizar _move_ pode ocorrer um erro de `borrow outlive` que não deixa compilar.

## Channels: Multiple senders, unique receiver


## Mutexes

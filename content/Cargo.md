>Cargo is Rust’s build system and package manager

- Rust community crate registry
<div class="rich-link-card-container"><a class="rich-link-card" href="https://crates.io" target="_blank">
	<div class="rich-link-image-container">
		<div class="rich-link-image" style="background-image: url('https://crates.io/assets/og-image.png')">
	</div>
	</div>
	<div class="rich-link-card-text">
		<h1 class="rich-link-card-title">crates.io: Rust Package Registry</h1>
		<p class="rich-link-card-description">
		
		</p>
		<p class="rich-link-href">
		https://crates.io
		</p>
	</div>
</a></div>

- Clap: Command Line Argument Parser for Rust
<div class="rich-link-card-container"><a class="rich-link-card" href="https://docs.rs/clap/4.1.6/clap/" target="_blank">
	<div class="rich-link-image-container">
		<div class="rich-link-image" style="background-image: url('https://docs.rs/-/rustdoc.static/favicon-16x16-8b506e7a72182f1c.png')">
	</div>
	</div>
	<div class="rich-link-card-text">
		<h1 class="rich-link-card-title">clap - Rust</h1>
		<p class="rich-link-card-description">
		Command Line Argument Parser for Rust
		</p>
		<p class="rich-link-href">
		https://docs.rs/clap/4.1.6/clap/
		</p>
	</div>
</a></div>

# Glossário
>[!info] Dependencias
>We call the libraries that your code needs dependencies.

>[!info] Crates
>Packages of code are referred to as _crates_. That is: A collection of Rust Source code files.

> [!info] Library Crate
> Contains code that is intended to be used in other programs and can't be executed on its own.


# Cargo.toml Structure

- _[dependencies]_
Under this section you tell Cargo which external crates your project depends on and which versions of those crates you require.

# Dependencies Documentation
- `cargo doc --open` 
the command above will build documentation provided by all your dependencies locally and open it in your browser.

# Encapsulation
```text
We’ll also discuss encapsulating implementation details, which lets you reuse code at a higher level: once you’ve implemented an operation, other code can call your code via its public interface without having to know how the implementation works. The way you write code defines which parts are public for other code to use and which parts are private implementation details that you reserve the right to change. This is another way to limit the amount of detail you have to keep in your head.
```
## Namespacing
```
You can create scopes and change which names are in or out of scope. You can’t have two items with the same name in the same scope; tools are available to resolve name conflicts.
```

# Crates
Crates can contain modules, and the modules may be defined in other files that get compiled with the crate.

## Library Crates
They don’t have a `main` function, and they don’t compile to an executable. Instead, they define functionality intended to be shared with multiple projects. For example, the `rand` crate we used in [Chapter 2](https://doc.rust-lang.org/book/ch02-00-guessing-game-tutorial.html#generating-a-random-number) provides functionality that generates random numbers.

## Crate root
Is a source file that the Rust compiler starts from and makes up the root module of your crate.

# Module system

- **Start from the crate root**:
when compiling a crate, the compiler first looks in the crate root file (_/src/main.rs_ and _/src/lib.rs_) for code to compile.
- **Declaring modules**: In the crate root file, you can declare new modules; Example: `mod garden` the compiler will look for the module's code in these places:
	- /src/garden.rs
	- /src/garden/mod.rs
- **Path to code in Modules**:
Once a module is part of your crate, you can refer to code in that module from anywhere else in that same crate, as long as the privacy rules allow, using the path to the code. For example, an `Asparagus` type in the garden vegetables module would be found at`crate::garden::vegetables::Asparagus`.
- **The `use` Keyword**:

## Path to referring to an Item in the Module
_Our preference in general is to specify absolute paths because it’s more likely we’ll want to move code definitions and item calls independently of each other._

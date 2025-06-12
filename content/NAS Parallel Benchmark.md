
>[!info] O que é NAS
> NAS significa: _Numerical Aerodynamic Simulation_, é um programa que reúne esforços em larga escala para avançar o estado da arte da aerodinâmica computacional.

# Considerações a respeito do desenvolvimento de benchmarks significativos para supercomputadores HPC
- Benchmarks devem ser "genéricos" e não devem favorecer nenhuma arquitetura paralela em particular. Esse requisito impede o uso de quaulquer código especifico de alguma arquitetura, como exemplo: _message passing code_.
- Os requerimentos de tamanho da memória e tempo de execução devem ser facilmente ajustáveis para acomodar novos sistemas com o aumento de poder.

> É esperado das pessoas que vão implementar os benchmarks em um dado sistema que sejam livres (dentro dos limites das especificações) a resolver os problemas da forma mais apropiada para o sistema. Isso incluí a forma que irão escolher os algoritmos e estruturas de dados, a gerência/alocação de CPU e memória. – _Programmers are free to utilize language constructs that give the best performance possible on the particular system being studied._

# Algumas definições do sistema
- Processor
> É definido como a unidade de hardware capaz executar tanto instruções _floating point addition_ quanto instruções _floating point multiplication_.
- Local Memory
> Refere-se a memória com acesso randomico que pode ser acessada pelo processador em menos de 1 microsegundo.
- Main Memory
> A memória local combinada de todos os processors.
- Mass Storage
>Memória não-volátil com acesso randomico e tempo inferior a 40ms.
- Nós computacionais
> Refere-se aos nós de processamento primariamente designados para computação de alta velocidade de instruções _floating point_.
- Nós de serviço
> Refere-se aos nós de processamento primariamente designados aos serviços do sistema incluindo: Compilação, ligação,e comunicação externa com os computadores na rede.

# Important Benchmark Rules
- Todas as operações em ponto flutuante devem ser perfomadas usando 64-bit _floating point arithmetic_.
- Qualquer extensão ou biblioteca de rotinas que é empregado na implementação dos Benchmarks devem estar disponível para todos os usuários.
- Todas as regras aplicam-se igualmente para todas as chamadas de subrotinas, extensões das linguagens e diretivas de compilação.

[[EP]]

# Makefile

1. O primeiro Makefile irá entrara na pasta do benchmark especificado e setar a variável do shell CLASS para a classe passada por linha de comando

# Rust directory structure / Build and Make file


<div class="rich-link-card-container"><a class="rich-link-card" href="https://doc.rust-lang.org/cargo/reference/build-scripts.html" target="_blank">
	<div class="rich-link-image-container">
		<div class="rich-link-image" style="background-image: url('https://doc.rust-lang.org/cargo/favicon.png')">
	</div>
	</div>
	<div class="rich-link-card-text">
		<h1 class="rich-link-card-title">Build Scripts - The Cargo Book</h1>
		<p class="rich-link-card-description">
		
		</p>
		<p class="rich-link-href">
		https://doc.rust-lang.org/cargo/reference/build-scripts.html
		</p>
	</div>
</a></div>
<div class="rich-link-card-container"><a class="rich-link-card" href="https://doc.rust-lang.org/cargo/reference/environment-variables.html" target="_blank">
	<div class="rich-link-image-container">
		<div class="rich-link-image" style="background-image: url('https://doc.rust-lang.org/cargo/favicon.png')">
	</div>
	</div>
	<div class="rich-link-card-text">
		<h1 class="rich-link-card-title">Environment Variables - The Cargo Book</h1>
		<p class="rich-link-card-description">
		
		</p>
		<p class="rich-link-href">
		https://doc.rust-lang.org/cargo/reference/environment-variables.html
		</p>
	</div>
</a></div>

<div class="rich-link-card-container"><a class="rich-link-card" href="https://docs.rs/clap/latest/clap/#" target="_blank">
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
		https://docs.rs/clap/latest/clap/#
		</p>
	</div>
</a></div>

https://metajack.im/2013/12/12/building-rust-code-using-make/

<div class="rich-link-card-container"><a class="rich-link-card" href="https://github.com/sagiegurari/cargo-make" target="_blank">
	<div class="rich-link-image-container">
		<div class="rich-link-image" style="background-image: url('https://opengraph.githubassets.com/6154bbaf0f2466150ccf35f4748913b751d110f1b6f314074a7110614a9063cc/sagiegurari/cargo-make')">
	</div>
	</div>
	<div class="rich-link-card-text">
		<h1 class="rich-link-card-title">GitHub - sagiegurari/cargo-make: Rust task runner and build tool.</h1>
		<p class="rich-link-card-description">
		Rust task runner and build tool. Contribute to sagiegurari/cargo-make development by creating an account on GitHub.
		</p>
		<p class="rich-link-href">
		https://github.com/sagiegurari/cargo-make
		</p>
	</div>
</a></div>
<div class="rich-link-card-container"><a class="rich-link-card" href="https://www.reddit.com/r/rust/comments/fzj945/introducing_dors_makefiles_for_cargo_that_treat/" target="_blank">
	<div class="rich-link-image-container">
		<div class="rich-link-image" style="background-image: url('')">
	</div>
	</div>
	<div class="rich-link-card-text">
		<h1 class="rich-link-card-title">r/rust - Introducing Dors -- makefiles for cargo that treat workspaces as first-class citizens</h1>
		<p class="rich-link-card-description">
		25 votes and 4 comments so far on Reddit
		</p>
		<p class="rich-link-href">
		https://www.reddit.com/r/rust/comments/fzj945/introducing_dors_makefiles_for_cargo_that_treat/
		</p>
	</div>
</a></div>


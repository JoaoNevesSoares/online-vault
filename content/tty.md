#draft 
tty refere-se a palavra _teletype_, um dispositivo físico utilizado para receber e enviar mensagens a distância no século passado.
Nos computadores atuais tty's são dispositivos de entrada/saída do sistema sistema operacional que permite receber entrada/saída de texto. 
## Comando $ _tty_ 
Retorna o nome do dispositivo de terminal atual na entrada padrão.

## man ttyname
Algumas funcionalidades do tty utilizando linguagem C. Essas funcionalidades operam sobre o [[File descriptor]] para o tipo do dispositivo de terminal.
```c
#include <stdio.h>
#include <unistd.h>
int main(){
	// isatty() essa function determina se file descriptor 'fd' refere-se a um terminal válido. 
	int fd = 0;
	if(isatty(fd)){
		printf("is a valid terminal\n");
		//ttyname() essa funcao retorna o nome do dispositivo de terminal
		printf("%s\n",ttyname(fd));
	}
	else{
		printf("not a valid terminal\n");
	}
	return 0;
}
```

## Utilidades
Se algum momento a interface gráfica do sistema crashar, é possivel alterar para um tty em modo texto para resolver consertar o problema ou continuar trabalhando. Alguns usuários preferem atualizar o sistema através de um tty modo texto, ao contrário do graphical environment. matar um programa que está causando erro na interface gráfica através tty de texto.

## Referências
<div class="rich-link-card-container"><a class="rich-link-card" href="https://youtu.be/N1bz1DTD8Io" target="_blank">
	<div class="rich-link-image-container">
		<div class="rich-link-image" style="background-image: url('https://www.youtube.com/embed/N1bz1DTD8Io?feature=oembed')">
	</div>
	</div>
	<div class="rich-link-card-text">
		<h1 class="rich-link-card-title">What Is A TTY And How To Use It</h1>
		<p class="rich-link-card-description">
		What is a tty and how do I use it?  I've been asked this question a few times in recent weeks, so I thought I would make a brief video discussing this.REFERE...
		</p>
		<p class="rich-link-href">
		https://youtu.be/N1bz1DTD8Io
		</p>
	</div>
</a></div>




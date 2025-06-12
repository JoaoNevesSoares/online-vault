<div class="rich-link-card-container"><a class="rich-link-card" href="https://forums.freebsd.org/threads/very-unhappy-with-freebsd-13-motd.81620/" target="_blank">
	<div class="rich-link-image-container">
		<div class="rich-link-image" style="background-image: url('https://forums.freebsd.org/styles/freebsd/xenforo/logo.og.png')">
	</div>
	</div>
	<div class="rich-link-card-text">
		<h1 class="rich-link-card-title">Very unhappy with FreeBSD 13 MOTD</h1>
		<p class="rich-link-card-description">
		This may not be the right audience, but I'm very displeased with FreeBSD 13 changing the traditional /etc/motd logic and turning it into what I see as over-engineered triviality which contradicts...
		</p>
		<p class="rich-link-href">
		https://forums.freebsd.org/threads/very-unhappy-with-freebsd-13-motd.81620/
		</p>
	</div>
</a></div>

# Description:
Arquivo que contém a mensagem que é exibida quando o usuário loga no sistema.

# Arquivos
- `var/run/motd`
> Arquivo que é exibido pelo login(1)
- `/etc/motd.template`
> Durante o startup, uma linha contendo a string com versão do kernel é anexada neste arquivo e o conteúdo deste é escrito em `/var/run/motd`
- `.hushlogin` 
> Arquivo utilizado para suspender a mensagem de login

# Suspender a mensagem de login
Usuário pode suspender a mensagem do dia criando o arquivo `.hushlogin` no seu home directory ou através do login.conf(5)

# MORE INFORMATION:
man motd
man [[login.conf]]


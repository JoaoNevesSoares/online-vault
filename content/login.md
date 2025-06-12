# Descrição
Authentication of users is configurable via [[PAM]]. Password authentication is the default.

# Comando
	$ login
> Executa o login no sistema operacional
```
$ login -p
```
> By default login discards any previous environment. the -p option disables this behavior

# Login Class
In –> [[login.conf]]
Provides:
- "allow/deny" records based on time
- tty and remote host name.

# Arquivos
- `/etc/ftab`
>login changes the protection and ownership of certain devices specified in this file.
- `/etc/login.conf`
> login class capabilities database
- `.hushlogin`
> Desativa a mensagem de login do sistema que está em `/etc/run/motd`
- /var/mail/user
> system mailboxes
- /etc/pam.d/login
> [[pam]] configuration file
- 
# login adds information to user environment:
- user's home directory (HOME)
- command interpret (SHELL)
- search path (PATH)
- terminal type (TERM)
- user name (LOGNAME AND USER
Other environment variables may be set due to entries in "login class" in user's system passwd record. The login class also controls the maximum and current process resources limits granted to a login, process priorities and others aspects.

# LINKS -> INFO
[[login.conf]]
[[UUCP]]
[[MOTD]]
[[PAM]]

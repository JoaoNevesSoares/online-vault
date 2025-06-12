# Características Gerais
- Tradeoff entre simular realismo vs  simplicidade
- Nachos surgiu em 1992 para ser usado como projeto na cadeira de sistemas operacionais na universidade de UC Berkley
- Tanto o hardware virtual quanto o kernel do sistema operacional rodam como procesos normais do UNIX.
-  Permite rodar programas do usuário escritos em C e compilados para MIPS R2/3000 (arquitetura RISC). 
- Simula precisamente o comportamento de sistemas em rede. Cada "máquina" com nachos roda como se fosse um processo separado localmente que comunica-se por sockets UNIX, simulando uma rede local. Dessa forma uma thread em um processo nachos pode enviar pacote de dados para outra thread em outro processo nachos. Tudo simulado no mesmo hardware real.
- Simulação deterministica, com níveis de não determinismo, baseado em aleatoriedade gerada por "seed", (ou seja, permite comportamento repetitivo.)
- Usa Sinais (_Signals_) UNIX para simular dispositivos I/O assíncrono como Disco.
- Simula um temporizador(_Timer_) que é incrementado sempre que um programa executa uma instrução ou sempre quando houver uma chamada para rotinas de baixo nível do sistema operacional.
- Simula interrupção de sistemas, que são invocadas quando o _Timer_ chega em um determinado ponto.

# Gerenciamento de Threads

- Baseado no _FastThreads_ 
- Por **Default** o escalonamento das threads é _não preemptivo_, isso significa que uma vez que a thread começa a executar, ou ela continua até terminar, ou ela se bloqueia voluntariamente para algum evento de I/O. 
- Permite alterar a política de escalonamento para _preemptivo_ por fatia de tempo (_Time-Sliced_). Envolve dividir o tempo disponível na CPU em intervalos iguais de tempo. A troca de contexto (_preempção_ das threads) ocorre em pontos aleatórios mas recorrentes (repetitive).
- "_Concorrent programs are correct only if they work when "**a context switch can happen at any time**"_ "

# Sistema de Arquivos
- Simplificado
- Não possuí sincronização de acesso. Apenas uma única thread pode acessar o sistema de arquivos por vez. 
- Arquivos possuem um tamanho máximo bem pequeno.
- Não possível hierarquia de diretórios
Ao nível de hardware, a simulação de disco é baseada em requisições de "read sector" and "write sector" e signals para completar uma operação por meio de uma interrupção. 
- O conteúdo do disco é armazenado em arquivo Unix. As operações de leitura e escrita em setores do disco é performada por rotinas normais como read/write do Unix.
- Uma vez conteúdo do disco é atualizado, calcula-se quanto tempo a "simulação" de acesso ao disco durou, baseado no trilha e setor requisitado. 
- Nachos não endereça a possibilidade de recuperação de crash de disco, com (write-ahead logging), ou estrutura de log


[[Nachos 5.0j]]
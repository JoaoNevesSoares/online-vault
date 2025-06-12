# Sistema de Submissão  e Avaliação de Propostas de TCC
> [!tip] Diagrama de Casos de Uso
> Fazer o diagrama de casos de uso simples e depois avaliar o uso de relacionamentos.

>[!tip] Diagrama de classes:
>Cuidado especial na definição do nome da classe e de seus atributos e tipos. Métodos não serão cobrados aqui nesta etapa.

# Diagrama: Casos de Uso

## Atores
- Professor Coordenador/Organizador
- Aluno
- Administrador
- Professores Revisores

## Casos de Uso de acordo com Atores
### Aluno
- Submeter proposta (enviar arquivo da proposta e cadastrar título, adicionar palavra chaves, especificar orientador)
- Visualizar Submissão (visualizar status submissão corrente, visualizar revisões concluídas).
- Alterar Arquivo submetido
### Professor Revisor
- Informar Tópico de Interesse
- Visualizar propostas Submetidas
- Selecionar Proposta (Descarregar Arquivo da proposta, preencher formulário de revisão).
### Professor Coordenador/Organizador
- Cadastrar turma do semestre atual.
- Configurar informações da Turma (Adicionar prazos)
- Vincular alunos
- Alocar revisores (Distribuir Propostas: Escolher revisor)
- Visualizar lista de submissões
- Visualizar revisões (Observar status, Visualizar formulários preenchidos)

### Administrador
- Gerenciar Cadastros professores (adicionar, editar informações (alterar disponibilidadae professor), excluir professor)
- Atribuir professor como Organizador.
- Gerenciar Cadastros de Alunos (adicionar,editar,remover, alunos)


# Diagrama de Classes

## Classes óbvias
- Usuário (produz e consome informações do software)
- Turma (unidade organizacional relavante para aplicação)
- Administrador (papel desempenhado pelo usuário que interage com o sistema)
- Professor Coordenador (papel desempenhado pelo usuário que interage com o sistema)
- Professor Revisor (papel desempenhado pelo usuário que interage com o sistema)
- Aluno (papel desempenhado pelo usuário que interegage com o sistema)
- Proposta (faz parte do domínio de informação do problema)
- formulário (faz parte do domínio de informação do problema)
## Classes menos óbvias
- Login
- cadastro
- palavra-chave
- Arquivo-Csv


# Dúvidas
É melhor criar uma classe Login com atributos como usuário e senha, e vincular a classe Usuário através de uma associação ou definir os atributos usuário e senha na classe usuário diretamente ?

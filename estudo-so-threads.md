## [Estudo] Sistemas Operacionais

## THREADS

São “processos leves”, Melhoram a eficiência de aplicações concorrentes.
A comunicação entre as threads de um processo é mais simples e rápida que a comunicação entre processos.
Cada thread possui seu próprio contexto de hardware.

### Ambiente Monothread:
Ambiente onde um processo suporta apenas um fluxo de execução em seu espaço de endereçamento, ou seja, um programa.
Para ter concorrência é preciso o uso de mais de um processo em conjunto para realizar uma tarefa. Aplicações concorrentes aumentam a demanda do sistema, A comunicação entre processo é feita por Pipes / Sinais.
### Ambiente Multithread:
Ambiente onde um processo suporta mais de um fluxo de execução em seu espaço de endereçamento.  O fluxo de execução está associado a uma função e às funções por ela chamadas,  Ao designar que a criação de um novo fluxo de execução a uma função, o programador cria uma nova thread.
A criação, a eliminação e a troca de contexto são mais simples e rápidas do que se fossem processos Threads compartilham o processador da mesma forma que os processos. As  Threads passam pelos mesmos estados que os processos.

```markdown

IMAGEM DAS THREADS 

```

Assim como processos possuem PCBs, threads possuem TCBs. No TCB são armazenados:
```markdown
Prioridade,  Estado e Contexto de Hardware.   
```
Por compartilharem o espaço de endereçamento, **threads de um mesmo processo se comunicam através de posições de memória**.

### Implementação:  
A biblioteca de funções que implementam o ambiente Multithread pode ser de 3 modos:  

**Modo usuário:**  Com rotinas implementadas fora do kernel do SO. 
**Modo kernel:**  Com rotinas implementadas pelo kernel do SO 
**Modo híbrido:**  Com rotinas implementadas por uma combinação do dois anteriores / Scheduler Activations:  Modo híbrido com melhoria na comunicação


### Modo Usuário:
São conhecidas como TMU (Threads em Modo Usuário); 
São implementadas pela aplicação:  A biblioteca de threads deve prover funções para que a aplicação possa manipular as threads.  O SO não sabe que a aplicação é Multithread ; A troca de contexto é mais rápida;  Problemas com tratamento de sinais e com E/S;
### Modo Kernel:
São conhecidas como TMK (Threads em Modo Kernel);
São implementadas pelo Kernel através de System Calls; A troca de contexto é mais lenta que o TMU.
### Modo Híbrido:
Combina as vantagens do **TMU e do TMK**;  Um processo pode ter várias TMKs que podem ter várias TMUs cada uma.
O escalonamento feito pelo kernel trata das TMKs  O escalonamento feito pela biblioteca trata das TMUs. Cabe ao programador definir a configuração da sua aplicação.
Problemas:  Só existe paralelismo entre TMKs  Se uma TMU de uma TMK realiza uma operação de E/S, todas as TMUs dessa TMK ficam bloqueadas.
Os problemas do modo híbrido são causados porque o kernel não sabe da existência das TMUs. Neste modo, a biblioteca e o kernel se comunicam para que, caso haja um bloqueio, uma outra thread seja escalonada. Cada camada, kernel e biblioteca, implementam seu escalonamento.

## SINCRONIZAÇÃO
	### 1. Conceito:
	Aplicações concorrentes são aquelas em que multiplos processos ou threads executam cooperativamente em busca de um resultado comum. Essas aplicações compartilham recursos do S.O.
Para que haja o compartilhamento de recursos, os processos de uma aplicação concorrente tem que estar sincronizados através de MECANISMOS DE SINCRONIZAÇÃO oferecidos pelo S.O.
```markdown
IMAGEM DE PROCESSOS E THREADS 
```

Cabe ao programador dizer ao S.O. onde começará a concorrência dos processos e onde haverá sincronização. Uma das notações utilizadas é através de comandos FORK e JOIN, usado por sistemas UNIX para criar subprocessos.

### 2. Compartilhamento de Recursos

O grande problema de compartilhar recursos é causar problemas de consistência. Isto é, dois recursos acessarem a região crítica ao mesmo tempo, gerando um resultado errado.
	Ex: Uma Conta possui 10 reais. Realiza-se duas operações simultâneas, Subtraindo 8 de sua conta e adicionando 2. Como foram feitas ao mesmo tempo, ambos iram considerar o valor inicial 10 e um resultado irá sobreescrever o outro. Sendo assim, se a conta de subtração foi feita por ultimo, o resultado será 2. Caso tenha sido a conta de adição, será 12.
 Devem existir mecanismos para controlar esse compartilhamento.
Esses problemas são conhecidos como **RACE CONDITIONS**.

### 3. EXCLUSÃO MÚTUA
	É a forma mais simples de impedir que dois processos acessem o mesmo recurso simultaneamente.
	Se um processo acessa um recurso e outro também quer fazê-lo, este deve aguardar pelo término da utilização. Chamamos isso de **EXCLUSÃO MÚTUA**.
	A parte do código onde é feito o acesso ao recurso compartilhado é chamado de **REGIÃO CRÍTICA**.
	Seguindo os protocolos de exclusão mútua, somente um processo poderá estar na região crítica.  Após um processo deixar a região crítica, outro processo é escolhido para entrar nela.  
O processo de escolha de processos para acessar a região crítica pode fazer com que um processo nunca seja escolhido, causando **STARVATION**.


### 4. Exclusão Mútua por Software

 ```markdown
IMAGEM DE EXCLUSAO MUTUA POR SOFTWARE 
```
Este algoritmo apresenta a deficiência de permanecer em **BUSY WAIT** (espera ocupada). Ou seja, fica em constante estado de checagem da entrada do processo na região crítica (em loop), consumindo tempo do processador desnecessariamente. Esse problema é resolvido com o uso de **SEMÁFOROS ou MONITORES**.

### 5. Sincronização Condicional 

Ocorre quando o acesso ao recurso compartilhado requer sincronização associada a uma condição.
O processo que deseja acessar o recurso ainda não disponível deve permanecer em espera ocupada até que o mesmo esteja disponível.

### 6. SEMÁFOROS
Implementa a exclusão mútua e a sincronização condicional entre processos.
São varáiveis inteiras e não negativas que podem ser manipuladas por instruções especiais:
```markdown
	DOWN (P) // UP (V).
 ```
**UP:** incrementa o valor de um semáforo  
**DOWN:** decrementa o valor de um semáforo. Se o semáforo já for zero, o processo entra em Wait.

Os semáforos podem ser:  Binários (valores 0 ou 1), chamados de mutex (mutual exclusion semaphores) ou Contadores, que podem assumir qualquer valor inteiro maior ou igual a 0.

A exclusão mútua pode ser implementada através de um mutex associado ao recurso compartilhado  Não ocorre busy wait  DOWN e UP funcionam como protocolos de entrada e saída da Região Crítica.
Cada semáforo está associado a um recurso 
```markdown
	0: o recurso está em uso        &    1: o recurso está disponível
```

### 7.Sincronização – Troca de Mensagens
Os mecanismos de sincronização vistos até agora assumem o acesso, por parte dos processos, à variáveis comuns. Nestes casos, utiliza-se memória compartilhada  Quando não há a possibilidade da utilização de memória compartilhada, faz-se necessário um outro mecanismo, denominado troca de mensagens.

Troca de mensagens é um mecanismo de comunicação e sincronização entre processos através de um canal de comunicação. A comunicação entre os processos se dá através do envio (SEND) e da recepção (RECEIVE) de mensagens.  Essas rotinas são também responsáveis por sincronizar o trânsito das mensagens.


### 8.DEADLOCK
É a situação onde um processo aguarda pela liberação de um recurso ou por um evento que nunca ocorrerá;  Também conhecido como bloqueio perpétuo. Ocorre, na maioria das vezes por situações onde a exclusão mútua é necessária, mas não é utilizada, ou ainda, é mal utilizada.
Condições necessárias: 
Exclusão mútua: Um recurso só pode estar alocado a um processo em um determinado instante.  
Espera por recurso: Um processo pode esperar por recursos além daqueles já alocados.
Não-preempção: Um recurso não pode ser liberado de um processo apenas porque outros processos o desejam.
Espera circular: um processo aguarda por um recurso alocado a outro processo, e vice-versa.

#### Prevenção:
Para prevenir deadlocks, basta garantir que uma das condições necessárias não ocorra.  

```markdown
**Exclusão mútua:**  Não se pode deixar de utilizar.  
**Espera por recurso:**  Todos os recursos deveriam ser alocados ao processo antes do início da execução  ; Grande desperdício  ; Grande dificuldade em determinar todos os recursos;  Starvation.  
**Não-preempção:**  Somente se for possível retirar um recurso já alocado a um processo ; Pode causar erro de execução; Starvation . 
**Espera circular:** Limitar a um recurso por processo ; Limitaria muito o grau de concorrência.
```

**Detecção:**
Mecanismo que determina a existência de deadlock, identificando os recursos e processos envolvidos.  O SO deve possuir estruturas de dados e algoritmos de Deadlock específicos para cada recurso.  Ao solicitar a alocação de um recurso, o SO verifica a existência de espera circular.

**Correção:**
Após a detecção do deadlock, o sistema deve resolver o problema. A solução mais simples é a eliminação de um ou mais processos e a liberação dos recursos alocados por eles, quebrando a espera circular. Outra solução é o rollback:  O sistema suspende um processo, libera seus recursos, e após o término do deadlock, restaura os recursos ao processo original para ele possa ser executado.  Muito difícil de ser implementado.


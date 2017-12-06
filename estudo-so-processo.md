## [SISTEMAS DE INFORMAÇÃO](https://boechat.github.io/estudo-si)
## [SISTEMAS OPERACIONAIS](https://boechat.github.io/estudo-si/estudo-so)


# PROCESSOS

### 1. Processos e Threads 

. Threads  
. Sincronização e Comunicação entre processos

### 2. O que é Processo?
Processo é um programa em execução
Para que os processos possam existir em sistemas multiprogramáveis, é necessário armazenar informações que permitam a manipulação dos processos.
Então, Processo é o conjunto de informações para que o SO implemente a concorrência entre programas e suas corretas execuções

### 3. O que é Contexto?
A troca do processo que está sendo executado no processador por outro é denominada troca de contexto.

O contexto de um processo abrange:  
```markdown

Contexto de hardware  
Contexto de software  
Espaço de endereçamento

```

### 4.Contexto de hardware
Contém os valores dos registradores:  
```markdown
Registradores gerais  
PC  
SP 
PSW  
```
Quando o processo está em execução, esses valores estão no **hardware**;  Quando o processo é substituído, os valores são copiados para uma **estrutura interna do SO.**

![Contexto Hardware](https://boechat.github.io/estudo-si/so001.png)

### 5. Contexto de Software
É composto pelos limites e características dos recursos que podem ser alocados pelo processo
```markdown
Pode ser dividido em:  
Identificação 
Quotas  
Privilégios
```

#### Identificação :
```markdown
PID = Número inteiro que representa uma identificação única do processo no sistema  
UID  = Número inteiro que representa a identificação do usuário “dono” do processo  Utilizado para implementar segurança
```
#### Quotas: 
Limites de cada recurso que o processo pode alocar
Ex. de **Quotas**:   Número máximo de arquivos abertos simultaneamente,  Tamanho máximo de memória , Tamanho máximo do buffer de E/S  & Número máximo de processos filhos.

#### Privilégios:
Definem que ações são permitidas ou não 
Exemplos: Criação de processos privilegiados,  Alteração de parâmetros do sistema ,Alteração da configuração dos dispositivos de hardware  & Acesso a arquivos.

#### Espaço de Endereçamento :
É a área de memória pertencente ao processo onde instruções e dados do programa são armazenados para a execução . 
Cada processo possui seu espaço de endereçamento . Deve ser protegido dos outros processos.

### 6. PCB (Controle de Bloco de Processo)
**DEFINIÇÃO:** A estrutura de dados interna ao SO que implementa um processo é o bloco de controle do processo (process control block – PCB).
**PARA QUE SERVE?**  É nele que estão armazenadas as informações do contexto de hardware, do contexto de software e do espaço de endereçamento

![PCB](https://boechat.github.io/estudo-si/so002.png)

### 7.ESTADOS DO PROCESSO
Em sistemas multiprogramáveis os processos não têm exclusividade na utilização da CPU.  Os processos alternam de estado, dependo de eventos gerados pelo SO ou pelo próprio processo .
Esses estados são:  
```markdown
Execução  Pronto  Espera 
Running   Ready   Wait
```

#### .Execução (running)
```markdown
Quando o processo está sendo executado pela CPU  
```
Em sistemas com uma única CPU, somente um processo pode estar nesse estado
Em sistemas multiprocessados:  Mais de um processo pode estar nesse estado  e Um processo pode estar em execução em mais de uma CPU

#### .Pronto (ready)
```markdown
Quando um processo está aguardando para ser executado
```
Cabe ao SO selecionar o processo a ser executado (estado running)  
Este mecanismo de escolha é chamado escalonamento  Os processos prontos aguardam em uma lista de prioridades

#### .Espera (wait)
```markdown
Também chamado de bloqueado (blocked); 
```
![Lista de Processos](https://boechat.github.io/estudo-si/so003.png)

### MUDANÇAS DE ESTADOS DO PROCESSO
#### .Ready ⇒ Running (a)  
Após a sua criação, o processo fica aguardando na lista de prontos (ready)
De acordo com a política de escalonamento do SO, em um determinado momento, um processo em estado ready é escolhido para ser executado (running)  
#### .Running ⇒ Wait (b) 
 Ocorre a pedido do processo (e.g. operação de E/S) 
O processo fica esperando pela ocorrência de um evento  
#### .Wait ⇒ Ready (c)  
Quando o evento que o processo estava aguardando acontece (e.g. término da operação de E/S solicitada)  Não existe a transição Wait ⇒ Running
Running ⇒ Ready (d)  Quando o processo é interrompido pelo SO (e.g. término do timeslice)

### 8. Criação e Eliminação de Processos
Um processo é criado no momento em que o SO cria o seu PCB e o insere nas estruturas internas do SO  A partir de então, o processo pode ser gerenciado.  
Analogamente, um processo é eliminado quando seus recursos são liberados e seu PCB é eliminado.  

Para esses momentos especiais, são criados 2 estados: Criação(new)/Término (exit)

```markdown
Criação (new)  Quando o SO já criou o PCB, mas não o colocou na lista de processos prontos (ready) 
Terminado (exit)  Quando o processo não tem mais um programa executando, mas o seu PCB ainda não foi eliminado
Um processo vai para o estado exit quando o programa terminou naturalmente , outro processo o eliminou ou ocorre ausência de recursos necessários.
```

![Estados e Relacionamentos](https://boechat.github.io/estudo-si/so004.png)

### 9. CPU BOUND/ I/O BOUND

Pode-se classificar os processos em:  

CPU-bound  Processo que passa a maior parte do tempo entre os estados running e ready.
Realiza poucas operações de E/S. Exemplo: Aplicações científicas 
I/O-bound  Processo que passa a maior parte do tempo no estados wait  Grande número de operações de E/S.  Exemplos: aplicações comerciais e processos interativos.

### 10. Foreground e Background  
Todos processo possui pelo menos dois canais para a realização de operações de E/S  : Canal de entrada (input) e Canal de saída (output) 

Um processo foreground é aquele que, durante seu processamento, permite a interação direta com o usuário através dos canais de E/S.  
Um processo background é aquele em que não há a interação com o usuário através dos canais de E/S.

### 11. Processos – Independentes, Subprocessos e Threads
Quando uma aplicação necessita implementar concorrência, utiliza uma das técnicas: 
```markdown
Processos Independentes / Subprocessos  Ou Threads
```

#### INDEPENDENTES:
É a maneira mais simples de implementar concorrência
Não existe vínculo entre o processo criado e seu criador  
Exige a alocação de um novo PCB

#### SUBPROCESSOS:
São processos criados dentro de uma estrutura hierárquica;  Processo criador é o processo-pai , Processo criado é o processo-filho ou subprocesso .

A criação pode ser recursiva. Se o processo pai morre, os filhos morrem também. Cada processo novo tem o seu PCB. 
Podem compartilhar quotas.

#### THREADS:
 “Processos leves”. 

Reduzem o tempo e a quantidade de recursos envolvidos na criação e eliminação de processos. Cada thread tem seu contexto de hardware, mas compartilha o contexto de software e o espaço de endereçamento.  A comunicação entre as threads de um processo é mais simples e rápida que a comunicação entre processos.



### 12. SINAIS
Mecanismo que permite notificar processos de eventos gerados pelo SO ou por outros processos. Podem ser gerados por uma sequência de teclas (e.g. Ctrl-C ou Ctrl-Alt-Del), Eventos temporizados, Ocorrência de Exceções ou Interrupções e  Operações de sincronismo.
Os sinais a serem tratados por um processo ficam armazenados em seu PCB.  Os sinais ficam pendentes até que o processo seja escalonado. O tratamento de sinais é semelhante ao de interrupções, mas o desvio se dá para um handler que pode ser o próprio processo.
O sinal está para o processo assim como as interrupções e exceções estão para o SO.

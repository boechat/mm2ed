           ## [SISTEMAS DE INFORMAÇÃO](https://boechat.github.io/estudo-si)
            ## [SISTEMAS OPERACIONAIS](https://boechat.github.io/estudo-si/estudo-so)
  

## ESCALONAMENTO

### Políticas de Escalonamento 
São os critérios adotados para a seleção de qual processo no estado **pronto(ready)** será escolhido para utilizar o processador **(running)**.  
A parte do SO responsável pela implementação das políticas de escalonamento é o **escalonador (scheduler)**.

Após a ação do escalonador, ocorre a troca de contexto entre o processo corrente e o selecionado.
A troca de contexto é realizada por uma parte do SO chamada **dispatcher**.

Critérios de Escalonamento :
```markdown
> Utilização do Processador: O processador deve permanecer a maior parte do tempo ocupado.
> Throughput:  Número de processos executados em um intervalo de tempo  É desejável que seja o maior possível
> Tempo de CPU:  Tempo que um processo leva no estado de running durante seu processamento
> Tempo de Espera:  Tempo total que o processo passa no estado de ready durante seu processamento  É desejável que seja o menor possível  
> Tempo de Turnaround: Tempo total que o processo leva desde sua criação até o seu término . É desejável que seja o menor possível . 
> Tempo de Resposta:  Tempo decorrido entre uma requisição ao sistema ou aplicação e a exibição da resposta  É desejável que seja o menor possível.
```
### Escalonamento Preemptivo e não-preemptivo

**Preempção** é a interrupção da execução de um processo para sua substituição por outro processo.  
Escalonamento não-preemptivo  Foi o primeiro tipo de escalonamento implementado em sistemas multiprogramados;  O processo só sai do estado running se terminar ou realizar alguma operação de E/S;
Escalonamento preemptivo  O SO pode interromper a execução de um processo e colocá-lo no estado ready e selecionar um novo processo para utilizar o processador. 
É possível priorizar a execução de alguns processos. O compartilhamento do processador é mais uniforme. Atualmente a maioria dos SOs utiliza escalonamento preemptivo.

### Escalonamento FIFO
Também conhecido como FCFS (First Come First Served).
**O primeiro processo a entrar no estado ready é o primeiro a ser escalonado.**
A medida que os processos entram no estado ready, são colocados em uma fila.
Quando o processo em execução termina, o primeiro processo da fila é escolhido.

```markdown
Exemplos:  
Três processos (A, B, C) com tempos de CPU 10, 4, 3, respectivamente.  
Ordem de chegada na fila:   A, B, C  
                            B, C, A
```
Qual o tempo de espera médio nos dois casos?  Qual o tempo de turnaround médio nos dois casos?


O algoritmo não se preocupa em diminuir os tempos de espera e de turnaround.

**Processos CPU-Bound levam vantagem sobre processos I/O-Bound.**  Originalmente é não-preemptivo.

### Escalonamento SJF

Shortest Job First  
Seleciona o processo com menor tempo ainda por executar.  
Quais os tempos médios de espera e turnaround para o exemplo anterior?  
Problema: Como estimar o tempo restante?  
Originalmente não-preemptivo.
**Pode causar starvation em processos CPU-Bound.**

### Escalonamento Cooperativo 

Busca aumentar o grau de multiprogramação em políticas que não tenham preempção  O processo libera o processador voluntariamente.  
Problema:  A decisão cabe ao processo e não ao SO  
Os Windows 3.11 e 95 utilizavam variações desse escalonamento

### Escalonamento Circular 

Também conhecido como round robin, **É o FIFO preemptivo com o uso de timeslice.** Indicado para sistemas de tempo compartilhado.

Exemplos:
```markdown
Três processos (A, B, C) com tempos de CPU 10, 4, 3, respectivamente 
Ordem de chegada na fila: A, B, C  
Qual o tempo de espera médio?  Qual o tempo de turnaround médio?  
```

Processos CPU-Bound são privilegiados.  
Um refinamento do escalonamento circular é o **escalonamento circular virtual.**
No E.C.V existem duas filas:

```markdown	
Uma, fila principal, para os processos em estado de pronto. 
Outra, fila auxiliar, para os processos que acabaram de sair do estado de espera.
```
A fila auxiliar é utilizada primeiro. 
A fila principal só é utilizada se a fila auxiliar estiver vazia.

### Escalonamento Por Prioridades

Escalonamento preemptivo baseado na prioridade de execução do processo.  
O processo no estado de pronto com maior prioridade é escalonado.
Caso haja empate, é utilizado escalonamento FIFO.
**Não há preempção por tempo .**
Só há preempção se houver um processo pronto com prioridade maior que aquele em execução;  A prioridade de execução pode ser estática ou dinâmica.
A prioridade de execução pode ser estática ou dinâmica.
**Processos com prioridade baixa podem sofrer starvation .**
Se for utilizada prioridade dinâmica, é possível utilizar a técnica de aging nos processos em espera.
Aging incrementa a prioridade dos processos com o passar do tempo.
Utilizado em sistemas de tempo real.

### Escalonamento Circular com Prioridade

O processo permanece em execução até que:  
```markdown	
Termine seu processamento  
Vá para o estado de espera  
Sofra preempção por tempo  
Sofra peempção por prioridade 
```
É amplamente utilizado .
Pode utilizar prioridades estáticas ou dinâmicas.

### Escalonamento por Múltiplas Filas

São utilizadas diversas filas de processos em espera.  
Cada fila possui sua prioridade.  
Os processos das filas com maior prioridade são escolhidos primeiro.
A escolha do processo em cada fila pode seguir qualquer política.  
Os processos são associados às filas no momento da criação dos mesmos.


### Escalonamento por Múltiplas Filas com Realimentação

É semelhante ao escalonamento por múltiplas filas, mas os processos podem mudar de fila durante seu processamento;
A mudança é feita pelo SO seguindo um mecanismo adaptativo. Um escalonamento circular é utilizado em cada fila  A fatia de tempo varia de forma inversamente proporcional a prioridade da fila;
Processos I/O-Bound devem estar em filas de mais alta prioridade.

## [Estudo] Sistemas Operacionais

## PROCESSOS


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


```markdown
IMAGEM PROCESSO CONTEXTO DE HARDWARE!!!
```
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

```markdown
IMAGEM DO PCB!
```

### 7.ESTADOS DO PROCESSO
Em sistemas multiprogramáveis os processos não têm exclusividade na utilização da CPU.  Os processos alternam de estado, dependo de eventos gerados pelo SO ou pelo próprio processo .
Esses estados são:  
```markdown
Execução  Pronto  Espera 
Running   Ready   Wait
```

.Execução (running)
 Quando o processo está sendo executado pela CPU  
Em sistemas com uma única CPU, somente um processo pode estar nesse estado
 Em sistemas multiprocessados:  Mais de um processo pode estar nesse estado  e Um processo pode estar em execução em mais de uma CPU
.Pronto (ready)
 Quando um processo está aguardando para ser executado
 Cabe ao SO selecionar o processo a ser executado (estado running)  
Este mecanismo de escolha é chamado escalonamento  Os processos prontos aguardam em uma lista de prioridades
.Espera (wait)
Também chamado de bloqueado (blocked); Quando um processo aguarda por algum evento ou recurso 
 Ex.: Um processo que aguarde uma leitura do disco  Ficam organizados em listas  Uma lista para cada tipo de evento


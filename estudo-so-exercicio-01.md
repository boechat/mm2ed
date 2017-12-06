## EXERCICIOS PROCESSOS & THREADS

### 1.	Em sistemas operacionais que rodam em dispositivos controladores utilizados na IoT, o trecho de código ao lado é muitas vezes utilizado. Sabendo que dado_disponível é uma função que testa se a posição de memória passada como parâmetro foi alterada, o trecho de codigo é CPU-BOUND ou I/O-Bound? Por que?
```markdown
for (;;)
{
	if (dado_disponivel (0xFF87))
		break;
}
```

### 2. Navegadores web muitas vezes fazem uso de threads quando o usuário solicita a abertura de uma nova aba de navegação. Conhecendo a natureza do acesso a páginas web, qual o tipo de implementação de threads deve ser utilizado para que esses navegadores funcionem adequadamente? Por que?

### 3.	Para cada um dos itens abaixo, indique a que parte do contexto do processo o item pertence e, sendo o sistema multithread TMK, se o item pertence ao PCB ou ao TCB:
```markdown
a) O ponteiro da Pilha 
b) O número máximo de subprocessos que podem ser criados
c) A JVM ao executar um programa JAVA
d) O campo utilizado para dar prioridade no escalonamento 
e) Uma variável global
```

### 4. Observe a saída de um comando que existe os processos e seus estados:
```markdown
UID	    PID	ESTADO	CMD
aluno1  1329	P		  edit cola.txt
prof    1330	E		  print prova.pdf
aluno2  1332	W 		chrome search=”o que sao threads?”
```
Para cada uma das afirmações abaixo, explique o motivo de ser falsa:	

#### A)	Ao receber um sinal, o processo cujo PID é 1329 passa imediatamente para o estado de espera (wait) para aguardar pelo processo que enviou o sinal.
#### B)	O processo do aluno2 passa para execução (running) assim que receber todo o conteúdo da busca efetuada.

### 5. Para o programa abaixo, executado de forma concorrente, reescreva as funçãoes proca, procb e procc, acrescentando as primitivas de sincronização para que a frase “Vou passar em SO e POO” seja escrita sem erros. Não é permitido alterar as chamadas das funções puts, nem alterar a ordem em que se encontram dentro de cada função. Não se esqueça de declarar e inicializar eventuais variáveis necessárias.
void proca ()	void procb ()	void procc ()		void main(void)
```markdown

{		              {		             {			            { COBEGIN()
puts (“vou”);	    puts (“vou”);	   puts (“vou”);		  proca (); procb(); procc();
puts(“e”);	      puts(“e”);	     puts(“e”);		      COEND();
}		              }		             }			            }
```

### 6. Diferencie Cache de Memória Secundária, evidenciando vantagens e desvantagens de serem aplicadas.

### 7. O que é uma system call e qual sua importância para a segurança do sistema? Como as system calls são utilizadas por um programa?

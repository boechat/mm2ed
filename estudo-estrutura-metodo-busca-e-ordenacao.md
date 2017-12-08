## [SISTEMAS DE INFORMAÇÃO](https://boechat.github.io/estudo-si)
## [ESTRUTURA DE DADOS](https://boechat.github.io/estudo-si/estudo-estrutura)

# Métodos de Busca & Ordenação

### ALOCAÇÃO ESTÁTICA vs ALOCAÇÃO DINÂMICA

Antes de retomar o estudo com os métodos de ordenação, cabe fazer um pequena revisão num dos conceitos básicos de alocação de dados em C.
Vamos então diferenciar **Alocação ESTÁTICA de DINÂMICA.**

**ALOCAÇÃO ESTÁTICA:** Falaremos que uma alocação é estática quando seu tamanho é declarado previamente e não se altera. 
Por exemplo: Ao definirmos que  **int vet [ 3]** sabemos que o vetor em questão tem 3 elementos, acessado pelos indices 0, 1 e 2.

**ALOCAÇÃO DINÂMICA:** Ela é utilizada durante o programa para reservar memória conforme o processo/usuário necessitar. Dessa forma, caso seja necessário utilizar um vetor que não se sabe o tamanho, teremos que utilizar uma função chamada “malloc”.
**Malloc** é definida como:
```c
    (tipo) = malloc (quantidade X tamanho em bytes);
                     OU
    vet = (int*) malloc n (sizeof(int));
```

# MÉTODO DE ORDENAÇÃO
## BUBBLE SORT (bolha)

Definição: O método de busca **Bubble Sort** (Bolha) corresponde a analisar sequencialmente cada um dos elementos de um vetor, comparando os elementos vizinhos entre si. Caso eles estejam fora de ordem, os elementos trocam.

```markdown
5 3 **6** **1** 8 7 2 4
```
No exemplo acima, o vetor V = [5,3,6,1,8,7,2,4] está passando para uma reorganização de forma crescente. primeiro será feito a verificação entre 5 e 3.
Deve-se usar uma variavel de controle. 

- 5 é menor que 3? Não, logo troca.    [ 3 5 6 1 8 7 2 4 ]
- Pula para o proximo termo. 5 é menor que 6? Sim. Mantém. [ 3 5 6 1 8 7 2 4 ]
- Proximo termo. 6 é menor que 1? Não, logo troca [ 3 5 1 6 8 7 2 4].
- Pula para o próximo sucessivamente, até o vetor estar ordenado.

# MÉTODO DE ORDENAÇÃO
## INSERTION SORT (inserção)

Definição: O Insertion Sort começa a trabalhar com o segundo valor do vetor e vai jogando ele para a esquerda (início do vetor). Ele percorre todo o vetor uma única vez, porém para fazer o movimento descrito (jogar para o início) ele utiliza-se de outro laço interno.

![Insertion Sort-001](https://boechat.github.io/estudo-si/estrutura001.png)

Exemplos:
```c
void insertionSort(int vetorDesordenado[], int n )
{
   int i, j, auxiliar;
   for( j=1; j < n; j++ ) 
   {
     auxiliar = vetorDesordenado[j];
       i = j-1;
            while(i >= 0 && vetorDesordenado[i] > auxiliar)
             {				
                vetorDesordenado[i+1] = vetorDesordenado[i]; 
                  i--;
             }
             vetorDesordenado[i+1] = auxiliar; 
   }
 }
```


# MÉTODO DE BUSCA
## SELECTION SORT (seleção)

Definição: Baseado em se passar sempre o menor valor do vetor para a primeira posição (ou o maior dependendo da ordem requerida), depois o de segundo menor valor para a segunda posição, e assim é feito sucessivamente com os n-1 elementos restantes, até os últimos dois elementos.

Exemplo:
```c
void selection_sort(int num[], int tam) 			
{   int i, j, min, aux;					
  for (i = 0; i < (tam-1); i++) 				
     min = i;					
	     for (j = (i+1); j < tam; j++)	
 {       if(num[j] < num[min]) 		
         min = j;    }
     if (i != min) {				
       aux = num[i];				
       num[i] = num[min];			
       num[min] = aux;     } 
      }
 }			
```

# MATRIZ DINÂMICA

Definição: C não permite alocação dinâmica de conjuntos bidimensionais. Logo, é necessário que você transforme a matriz em um conjunto unidimensional (Vetor) para poder alocar dados dinamicamente.
Como a matriz é comumente representada por matriz = [i][j] , ao transformar em vetor teremos a fórmula :

```c
M = i * n + j

onde “i” é o indice de linha, “n” é a posição e “j” a coluna 
```
![Matriz Dinamica](https://boechat.github.io/estudo-si/estrutura002.png)

### Declarando uma Matriz dinâmica:###

```c
Tendo como exemplo: 
		 mat[ i ][ j ] 
         mapeado em v[ i * n + j ] 
...

float *mat;				 /* matriz m x n representada por um vetor */
...

mat = (float*) malloc(m*n*sizeof(float));       /* onde m = qtd.linha e n= qtd.coluna */

```
## Exemplo

Em matemática, matriz transposta é a matriz que se obtém da troca de linhas por colunas de uma dada matriz. Sabendo disso, desenvolva uma função que pegue uma matriz e retorna a sua transposta.
```c
/* Solução 1: matriz alocada como vetor simples */


float* transposta (int m, int n, float* mat)		/função recebe tam.linha e de coluna e o vetor/
{	 int i, j;
  	float* trp;				/declara um vetor (ponteiro)/
trp = (float*) malloc(n*m*sizeof(float));       /* aloca matriz transposta com n linhas e m colunas */
for (i=0; i<m; i++)			 /* preenche matriz */
for (j=0; j<n; j++)
trp[ j*m+i ] = mat[ i*n+j ];   
return trp;
}
```
```c
/* Solução 2: matriz alocada como vetor de ponteiros */


float** transposta (int m, int n, float** mat)
{
int i, j;
float** trp;
trp = (float**) malloc(n*sizeof(float*));	/* aloca matriz transposta com n linhas e m colunas */
for (i=0; i<n; i++)
trp[i] = (float*) malloc(m*sizeof(float));

for (i=0; i<m; i++)					/*após alocar, preenche matriz */
for (j=0; j<n; j++)
trp[ j ] [ i ] = mat[ i ][ j ];
return trp;
}

```

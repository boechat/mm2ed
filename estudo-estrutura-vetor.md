## [SISTEMAS DE INFORMAÇÃO](https://boechat.github.io/estudo-si)
## [ESTRUTURA DE DADOS](https://boechat.github.io/estudo-si/estudo-estrutura)
  
# VETORES : Uma breve revisão

Definição: Vetor é uma estrutura de dados definidos num conjunto enumerado.

Vetores|
-----------------|
int v[10];
int v[2] = [0,1]
int v[] = [0,1]

O acesso é feito com um indice **(i)**, iniciando por 0.

O vetor é alocado em posições contíguas na memória (sequenciais).
Sendo assim, num vetor de 10 inteiros você está reservando 10 vezes valores inteiros (de 4 bytes), ou seja, 40 bytes.

Como o vetor nada mais é do que um **PONTEIRO**, caso você peça para o programa imprimir o “v” (de int v [ 10] ), ele imprimirá apenas o endereço de memória de v.

Podemos escrever então:
```markdown
*(v + i)  ou v [ i ]
--------------------      
&v [ i ] ou  (v + i)
```
### Passagem de Vetor para Função:

Se v é um ponteiro, logo v [ ] pode ser escrito como *v
```markdown
int função (int *v, int n)
```
Para alocar um Vetor de inteiros como 10 elementos, fazemos:
```markdown
int*v ;
v = (int *) malloc (10* sizeof (int));
```
O malloc aloca um espaço na memoria dinamica e guarda em v. Caso não tenha mais espaço, retorna valor **NULL**.
```markdown
v = (int *)malloc(10*sizeof(int))
```

## QUESTÕES
1. Faça um programa que permita ao usuário entrar com n (int) e a seguir n (valores reis) que serão armazenados em um vetor. A seguir, o programa deverá permitir que o usuário entre com um valor real; se este valor estiver contido no vetor, o programar deverá imprimir a posição, do contrário, imprimirá um aviso.
Observações:
- Crie uma função para fazer a busca no vetor.
- Não é necessário verificar se o usuário entrou corretamente com o valor de n.



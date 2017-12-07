## [SISTEMAS DE INFORMAÇÃO](https://boechat.github.io/estudo-si)
## [ESTRUTURA DE DADOS](https://boechat.github.io/estudo-si/estudo-estrutura)

# Funções Recursivas

**Definição:**  Muitos problemas têm a seguinte propriedade: cada instância do problema contém uma instância menor do mesmo problema. Dizemos que esses problemas têm **estrutura recursiva.**  
Para resolver um tal problema, podemos aplicar o seguinte método:

- Se a instância em questão for pequena, 
  - Resolva-a diretamente (use força bruta se necessário);
- Senão,
  - reduza-a a uma instância menor do mesmo problema,
  - aplique o método à instância menor,
  - volte à instância original.

A aplicação desse método produz um algoritmo recursivo. Para mostrar como isso funciona, examinaremos um exemplo concreto.

### Exemplo:
> Determine o valor de um elemento máximo de um vetor  **v[0..n-1]** . 
*É claro que o problema só faz sentido se o vetor não é vazio, ou seja, se n ≥ 1.*

*O problema poderia ser resolvido percorrendo o vetor de forma Iterativa (Como aprendemos em Prog.I e Prog.II).*

```c
int maximo (int n, int v[]) { 				
   int j, x;
   x = v[0];
   for (j = 1; j < n; j += 1)
      if (x < v[j]) x = v[j];
   return x;
}
```
Agora, a solução para o mesmo problema de **forma recursiva** seria:

```c
int maximoRec (int n, int v[ ] )
{  
   int x;
   if (n == 1)			    
      return v[0];
   else {				      
      	x = maximoRec (n-1, v);                  

      if (x > v[n-1])                                     
         	return x;			     
      else                                              
         	return v[n-1];                           
   }				
}  
```
Passo a passo:
```
caso n seja igual a 1, retorna o elemento do primeiro indice (v[0] ) 

Do contrario, chama a função maximoRec novamente, utilizando a variavel ‘x’ 
x é o máximo de v[0..n-2]         (N = numero de elementos)
Digamos que o tamanho do vetor seja 5. (N=5). Logo, x vai inicialmente
chamar a função maximoRec (4,v). Como a função foi chamada novamente,
ela vai continuar se chamando ((3,v), (2,V)) até n ser igual a 1 ( 1,V)
Após isso, ela irá executar: n ==1, então retorna elemento v[0] para o termo
seguinte. (v[0]) x> v[1] ? se sim, retorna v[0] pro proximo nível. do contrário,
será retornado v[1]. Isso se segue até achar o maior elemento do vetor.
```

## QUESTÕES:
### FR1) Crie uma função recursiva que receba como parâmetro um vetor INT V e o número N de elementos desse vetor. A função deve retornar o produto de todos os elementos do vetor.

Resolução:
```c
Int PROD (int v[ ], int n);
{
if (n<1)
	return 1;
else
return v [ n-1] * prod (v, n-1);
}
```

### FR2) Crie uma função recursiva que receba como parâmetro INT N , sendo um número maior/igual 1 e retorne o número correspondente à fibonacci.

```markdown
Se considerarmos Fibonacci como uma sequência de números demonstrada por
	             1,1,2,3,5,8,13,... Elementos
        ordem  1,2,3,4,5,6,7,.....Elementos

Podemos inferir que Fib (N) = 1, quando N é de ordem menor/igual a 2.
Escrevendo assim a equação de Fibonacci como:
Fib (Elementos) = Fib ( Elementos- 1) + Fib (Elementos - 2)
```

Resolução:
```c
int fib( int N)
	{ 
if (n <= 2 )
		return 1; 
else
return fib (n-1) + Fib (n-2)
}
```
### FR3) A função Fatorial é determinada comumente como F(n!). Faça uma função em C que calcule o fatorial de um número inteiro. 

```markdown 
n! = n*(n-1)!
```` 

Resolução:
```c
int fat ( int n)
{
if (n == 0) 
		return 1;
else
		return fat ( n-1 ) * n
}
```

## LINKS Úteis

[Lista de Exercicios de Recursividade 1 - USP](http://www.ime.usp.br/~pf/algoritmos/aulas/recu.html)

[Lista de Exercicios de Recursividade 2 - USP](http://wiki.icmc.usp.br/images/d/d0/Icc2_lista2.pdf)
### VIDEO
[Vídeo do canal Me Salva! Sobre Recursividade](https://www.youtube.com/watch?v=kS_VJYWeqIQ)

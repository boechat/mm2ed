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
// caso n seja igual a 1, retorna o elemento do primeiro indice (v[0] ) 

//Do contrario, chama a função maximoRec novamente, utilizando a variavel ‘x’ 
  // x é o máximo de v[0..n-2]         (N = numero de elementos)
  // Digamos que o tamanho do vetor seja 5. (N=5). Logo, x vai inicialmente
  // chamar a função maximoRec (4,v). Como a função foi chamada novamente,
  //  ela vai continuar se chamando ((3,v), (2,V)) até n ser igual a 1 ( 1,V)
  // Após isso, ela irá executar: n ==1, então retorna elemento v[0] para o termo
  //seguinte. (v[0]) x> v[1] ? se sim, retorna v[0] pro proximo nível. do contrário,
  //será retornado v[1]. Isso se segue até achar o maior elemento do vetor.
```

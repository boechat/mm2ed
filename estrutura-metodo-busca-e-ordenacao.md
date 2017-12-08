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

[[IMAGE - estrutura001]]





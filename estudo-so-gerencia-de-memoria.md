## GERÊNCIA DE MEMÓRIA

**Definição:** É a parte do SO responsável por manipular funções relativas à memória.
**Função:**  Maximizar o número de processos, e seus dados, em memória para minimizar o número de operações de E/S ; Implementar Memória Virtual &  Garantir a segurança dos espaços de endereçamento.

### Alocação Contígua Simples 
Implementada nos primeiros SOs:
A memória é dividida entre duas áreas: **Programa do usuário & Sistema operacional**

```markdown
IMAGEM MP/SO 
```

O usuário tem acesso à toda a memória principal. **Inclusive à área do S.O.!** 
Para proteger a área do SO, alguns sistemas implementam um mecanismo de proteção básico composto por um registrador.
A cada acesso à memória, se o mesmo for realizado fora da área permitida, o processo é cancelado.
**Esta alocação só permite um programa em execução e pode gerar desperdício de memória.**

#### OVERLAY

Na **alocação contínua simples**, os programas são limitados ao tamanho da memória principal.

Uma técnica utilizada é a divisão do programa em módulos.
Alguns módulos devem ser independentes. Somente um dos módulos independentes está em memória em um determinado momento. No momento da utilização do módulo, se este não estiver em memória, ele é trazido da memória secundária.Está técnica é conhecida como **Overlay**. 

A área de memória principal para onde os módulos são trazidos é conhecida como área de overlay, Cabe ao programador definir quais serão os módulos que poderão sofrer overlay e qual a área de overlay. 
O tamanho da área de overlay é o tamanho do maior módulo. 
**Pode degradar o desempenho devido às transferências de áreas de memória.**

```markdown
IMAGEM OVERLAY
```

### Alocação Particionada - Estática

Nos primeiros sistemas multiprogramáveis, a memória era dividida em pedaços de tamanho fixo chamados partições. O tamanho das partições eram definidos na inicialização do sistema.
Nas primeiras versões, cada programa só poderia ser carregado e executado em uma partição específica devido ao código absoluto
Um programa com código absoluto só pode ser carregado e executado a partir de um endereço de memória pré-determinado a tempo de compilação. Com isso, dois processos com código absoluto iniciando na mesma posição de memória não podem ser executados ao mesmo tempo. A essa gerência de memória deu-se o nome de alocação particionada estática absoluta.

O processo de geração de código evolui para o código realocável. Nele os endereços são relativos ao início do código. Com isso, o programa pode ser carregado em qualquer partição que ele caiba.
A essa gerência de memória deu-se o nome de alocação particionada estática relocável.

```markdown
IMAGEM ALOC PART ESTATICA
```

Neste tipo de gerência de memória, a proteção é implementada por dois registradores que armazenam o endereço início e o endereço fim da partição em que está o processo em execução. 
Caso seja feito um acesso fora desses limites, o programa é interrompido.
Também nessa  gerência, os programas não ocupam completamente as partições, gerando a **fragmentação interna.**

```markdown
IMAGEM ALOC PART ESTATICA-2
```
### Alocação Particionada - Dinâmica

Na alocação particionada dinâmica, as partições não tem tamanho fixo: O tamanho da partição é determinado pelo tamanho do programa,Assim, não existe fragmentação interna Porém, a medida que os processos terminam, pode ocorrer fragmentação externa.
Existem duas soluções para o problema da fragmentação externa:
 ```markdown
> A medida que os processos terminem, áreas livres adjacentes são concatenadas.
> As áreas são todas agrupadas  -Necessita que seja possível fazer a realocação dinâmica dos programas.
 ```

```markdown
IMAGEM ALOC PART DINAMICA
```
ESTRATÉGIAS DE ALOCAÇÂO

Como determinar qual área de memória utilizar para alocar a um processo? Existem 3 estratégias: 
```markdown
Best-fit ; Worst-fit  & First-fit;
```
**Best-fit** : A melhor partição (tamanho mais próximo do processo) é escolhido.
	             Pode aumentar Fragmentação externa.

**Worst-fit**: Pior partição escolhida (a com o tamanho mais distante).
	             Pode diminuir fragmentação externa.

**First-fit**: Primeira partição com o tamanho maior que o processo é escolhida.
	            Mais rápida das estratégias

### SWAPPING

É uma técnica utilizada para aumentar ainda mais a utilização da memória Quando um processo não pode ser colocado em execução por falta de memória, o SO escolhe um processo em memória e o transfere para a memória secundária (swap out) ;Posteriormente o processo é trazido de volta à memória principal (swap in) para voltar a ser executado.

A escolha de qual processo deve sofrer swap out deve ser feita de forma a escolher o processo com a menor chance de voltar a executar. Se há muitas operações de swap, dize-se que o sistema está em thrashing .
**Processos em estado de espera são escolhidos antes que processos no estado de pronto; **

É necessário a realocação dinâmica ; Para tal é necessário um registrador de relocação.
O registrador de relocação recebe o valor da posição inicial do processo, A cada acesso à memória o endereço é somado ao registrador de relocação.

```markdown
IMAGEM REGISTRADOR ALOC + INSTR
```

### MEMÓRIA VIRTUAL

É uma técnica de gerência de memória que combina a memória principal e a memória secundária para dar ao usuário a ilusão de existir uma memória muito maior que a memória principal. É necessário suporte do hardware, pois parte das funções da memória virtual são implementadas diretamente na arquitetura.

#### Espaço de Endereçamento Virtual
Um processo no ambiente de memória virtual não faz acesso a endereços reais, mas a endereços virtuais. O endereço virtual é traduzido para o endereço real pelo hardware no momento do acesso à memória; A tradução de endereço virtual para endereço físico é denominada **mapeamento**.

O espaço de endereçamento dos processos passa a ser virtual. Os endereços da memória principal fazem parte do espaço de endereçamento real 
O espaço de endereçamento virtual pode conter endereços cujos conteúdos não estejam na memória principal, e sim na memória secundária

### MAPEAMENTO

Realiza a tradução do endereço virtual para endereço físico. É realizado por um hardware chamado MMU (Memory Management Unit) que é configurado pelo SO. Cada processo possui uma configuração própria para a MMU chamada tabela de mapeamento .A escolha de qual tabela de mapeamento utilizar é feita através de um registrador da MMU.
Se as tabelas mapeassem cada célula de memória, o seusamanho seria tão grande quanto a própria memória .Assim, o mapeamento é feito por blocos de memória. Quanto maior o bloco, menor a tabela
```markdown
IMAGEM TABELA
```

### PAGINAÇÃO

É a técnica de memória virtual onde os blocos de memória tem tamanho fixo e são chamados de **páginas.**
O mapeamento é feito através de tabelas de páginas. Cada página virtual possui uma entrada na tabela de páginas (ETP).
```markdown
IMAGEM TABELA DE PAGINAS
``` 
Quando um programa é executado, as páginas são trazidas da memória secundária para as páginas da memória física, conhecidas como frames.
A cada acesso à memória, a ETP correspondente é acessada para indicar o frame.
Nessa técnica, o endereço virtual é formado pelo número da página virtual (NPV) e pelo deslocamento dentro da página.
O NPV funciona como o índica da tabela de páginas. O endereço físico é composto pelo endereço do frame mais o deslocamento.

Além das informações de mapeamento, cada ETP possui, entre outras informações, um bit de validade.
Esse bit indica se a página está, ou não, na memória.
Se ao acessar um endereço de memória, **o bit de validade não estiver ligado** , ocorre um page fault.
Ao ocorrer um **page fault** , o SO recebe uma interrupção para trazer a página da memória secundária para a memória principal.
O processo que ocasionou o page fault **passa do estado de execução para o estado de espera** até o término da transferência da página para a memória principal Ao término da transferência, o processo volta para a lista de prontos.




# Programas de computador

Um programa é uma descrição, mais ou menos detalhada de eventos (como no programa de um espetáculo) ou de uma sequencia detalhada de ações que permitem relizar determinada tarefa (p.e. a receita para fazer um bolo).

No caso dos computadores os programas são definidos numa linguagem precisa e própria para ser executada pelo computador. Na realidade, para facilitar o trabalho dos programadores, existem muitas linguagens de programação, com diferentes fins, que recorrem a programas interpretadores para traduzir dessa linguagem para as instruções que o computador é realmente capaz de executar.

Aqui vamos introduzir a atividade de programar usando a linguagem Python.

# Programando em Python

Ao definir um programa estamos a construir uma descrição de várias operações com as respetivas sequências de instruções, para cada uma desempenhar sua tarefa. As instruções de que partimos serão as já oferecidas na linguagem. Com estas podemos definir novas operações que funcionam como novas instruções a utilizar na definição de outras operações e assim sucessivamente. Muitas vezes podemos tirar partido de bibliotecas de operações já desenvolvidos por outros programadores, para criar as nossas operações e programas. 

> Instalar python ou usar um interpretador online...

As linguagens são muitas vezes representadas por texto de acordo com um vocabulário limitado e regras muito precisas. Descrevemos o nosso programa, escrevendo um texto de acordo com essas regras que depois damos ao interpretador da linguagem para fazer a execução no computador.


## Valores, operadores e variáveis 

Todas as linguagens baseiam-se em alguns conceitos fundamentais comuns, muitas vezes inspirados na matemática e baseados no funcionamento do próprio computador. Um computador tem memória para guardar dados e um processador para executar instruções, incluindo cálculos. Assim, as linguagens podem usar valores, possuem variáveis para representar "memórias" onde guardamos valores e têm operadores aritméticos para fazermos cálculos com os valores e as variáveis.

Os valores numéricos são representados de forma semelhante ao que estamos habituados. Por exemplo.

    23
    -98.5

> note que se usa a notação inglesa de ponto em vez de vírgula para as décimas

Usando operadores aritméticos, podemos construir expressões e estas serão avaliadas pelo computador. Por exemplo:

    23 + -98.5
    2*3 - 5/2

> o produto é representado por * e a divisão por /

Valores intermédios podem ser guardados em memórias, as variáveis da linguagem, e estas podem ser usadas nas expressões em lugar de valores:

    x = 10
    y = 3*x
    total = x + y

Note que cada linha anterior representa uma instrução de atribuição de um valor a uma variável. O sinal `=` não significa "igual" mas sim, atribuir à variável indicada o valor da expressão. A execução decorre por ordem, de cima para baixo, sendo usados nas expressões os valores que as variáveis guardam nesse instante. As variáveis são criadas à medida que lhes atribuímos valores e podem ter quase qualquer nome. 

## Funções

Uma construção muito comum na matemática que permite representar por um nome cálculos bastante complicados são as funções. Esta é a base para a criação de novas operações nas linguagens de programação. Podemos definir em python a função que calcula o quadrado de um valor com o seguinte código:

```python
def quadrado( x ):
    y = x * x
    return y
```

Seguindo esta definição em detalhe: a palavra `def` introduz a definição de uma função; `quadrado` será o seu nome e terá um parâmetro, o `x`. 
Depois, indentadas por espaços à esquerda, as instruções que definem o comportamento da função: o parâmetro é usado para calcular o valor que se guarda temporariamente em `y`; a instrução `return` termina a avaliação da função e indica que o resultado da função é o valor guardado em `y` (também se costuma dizer que a função retorna o valor em `y`).

Note que vimos a definição duma função, mas ainda não usámos esta definição para nada, logo, ainda não executámos as suas instruções. Mas uma vez definida, podemos usar e executar esta função sempre que necessário, como nos seguintes exemplos:

```python
z = quadrado( 5 )
zz = quadrado ( z )
resultado = quadrado( 3 ) + quadrado( 4 )
```

# Exercícios

...



# Programando em Python - parte II

Programas mais complexos têm necessidades um pouco mais complexas do que avaliar simples expressões. São assim oferecidas instruções para controlar melhor as operações que definimos. Em particular, vamos agora falar de tomar decisões e calcular coisas diferentes dependendo de determinadas condições.

## Valores lógicos

Para além de valores numéricos, as linguagens de programação suportam valores lógicos. Tal significa que existe a noção de Verdade e Falso, que pode traduzir, por exemplo, o resultado de comparar um valor com outro. Exemplo:  5 > 3 é Verdade; x < y pode avaliar no valor Verdade ou Falso, dependendo dos valores que estão nas variáveis x e y nesse momento.

Em python os valores lógicos são representados por `True` e `False`. As variáveis podem guardar também este tipo de valores:

```python
x = 10
y = 10
xgrande = x > y
```

Neste exemplo a variável `xgrande` vai conter `False`, pois x não é maior que y (10 não é maior que 10, é igual!).

> Nas comparações são válidos os habituais operadores <, >, >= e <=. Para verificar a igualdade usa-se o operador `==` (note a diferença para a atribuição de variáveis que vimos antes).

## Execução condicional (Se... senão...)

Uma das utilizações das condições vistas antes é na tomada de decisão sobre que instruções executar. Por exemplo, como obter a diferença absoluta entre os valores em x e y? Para tal podemos especificar o nosso programa de acordo com o seguinte esboço:

    se x >= y:  diferença = x-y
    senão: diferença = y-x

É exatamente este tipo de especificação que podemos fazer em python recorrendo às palavras inglesas `if` e `else` de acordo com a seguinte regra (atenção aos `:` e aos espaços à esquerda das instruções):

```python
if x >= y:
    diferenca = x-y
else:
    diferenca = y-x
```
A parte `else` pode ser dispensada se não for necessária, por exemplo para obter sempre um valor obsoluto em `x`:

```python
if x<0:
    x = -x
```

# Exercícios

...

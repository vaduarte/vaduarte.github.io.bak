
# Desenvolver um jogo em Python com Panda3D

O Panda3D é um pacote de código desenvolvido por um conjunto de programadores, que ajuda os outros programadores na linguagem python a desenvolverem jogos mais rapidamente. 

Neste turorial vamos desenvolver um jogo a duas dimenções (2D) mesmo que o Panda tenha a capacidade de trabalhar com objetos tridimensionais (3D). Vamos recriar o jogo "Asteroids", onde uma nave no espaço procura destruir todos os asteroids que vagueiam em seu redor.



## Jogos - programas interativos

Os jogos são exemplos de programas interativos, ou seja, que estão constantemente a interagir com o utilizador e a mudar o que aparece no ecrã em consequência desta interação. Assim, podemos dizer que um jogo segue, normalmente, uma sequência repetitiva de instruções, como no seguinte esboço de programa:

    lê recursos (imagens, soms, modelos de objetos, etc.)
    equanto vidas > 0 e jogo não acabou
        lê nível
        enquanto vidas > 0 e nível não acabou 
            lê evento (rato, teclado, ...)
            processa evento (move jogador, dispara, ...)
            atualiza atores e cenário do jogo
            mostra nova imagem

    termina jogo

Os atores serão as imagens animadas do nosso jogo e os eventos os acontecimentos que mudam o nosso jogo, como as ações do jogador no teclaro para jogar. Torna-se claro do esboço acima que estes programa executam repetidamente o que se costuma chamar o ciclo de jogo (game loop). Neste ciclo o jogo reage às ações do jogador, atualiza todos os atores e redesenha a imagem no ecrã. Este ciclo repete-se muitas vezes por segundo e, para ter uma boa animação, tal como nos filmes, deseja-se que seja capaz de redesenhar o ecrã 30 ou mais vezes por segundo (a que se chama a taxa de refrescamento ou _frame-rate_).

## Usando Python e o Panda3D

Para programar o nosso jogo temos de possuir o interpretador da linguagem Python e o pacote com o código do Panda (conjunto de código que já inclui muita da programação típica nos jogos). Para escrever o programa necessitamos de usar um editor de texto para escrever todas as nossas instruções. Veja o tutorial de introdução à linguagem Python.

Com é habitual nos programas de computador vamos construir uma série de definições e ações que depois usamos para executar o nosso jogo. Começamos por, usando o que já é fornecido, definir que o nosso jogo será um caso particular de uma jogo 2D (Game2D) já implementado. Em python tal é indicado definindo num ficheiro (p.e. `asteroidsgame.py`) uma classe que se baseia na classe Game2D já existente.

```python
from game2d import Game2D

class AsteroidsGame(Game2D):

    def __init__(self):
        Game2D.__init__(self)

    def gameLoop(self, task, dt):
        return Game2D.cont
```

Com esta definição, estamos a dizer que, quando um jogo AsteroidsGame for criado, iniciamos todo o código já fornecido pelo Game2D (`Game2D.__init__()`) e definimos a função `gameLoop` que será chamada a cada ciclo de jogo para fazermos todas as alterações nos atores ou outras ações necessárias. Neste momento não faz nada a não ser indicar que o jogo deve continuar (não terminou).

Podemos incluir também neste ficheiro a criação e início da execução do nosso jogo. Em python tal será conseguido criando um objecto, instância do AsteroidsGame e mandando executar o seu método run (que foi obtido do Game2D). O ficheiro fica agora assim:

```python
from game2d import Game2D

class AsteroidsGame(Game2D):

    def __init__(self):
        Game2D.__init__(self)

    def gameLoop(self, task, dt):
        return Game2D.cont

mygame = AsteroidsGame()
mygame.run()
```

Se mandar executar este programa no interpretador python, não deve acontecer muito pois ainda falta programar toda a mecanica do nosso jogo, seus atores e respetivo comportamento.

    python asteroidsgame.py

Deve aparecer uma nova janela vazia e nada parece acontecer. Na realidade o método run foi chamado mas nunca termina e o método gameLoop está constantemente a ser chamado, mas nada faz.


## Desenhando no ecrã

os jogos têm tipicamente de afixar várias imagens no ecrã, umas podem fazer parte do cenário outras correspondem aos atores animados do jogo. O Panda3D já define a classe `GameActor` para representar qualquer ator e este inclui nas caracteristicas do seu aspeto uma imagem que será afixada no ecrã.

No nosso jogo vamos criar variáveis deste tipo para guardar todos objetos a mostrar no ecrã. Na criação de cada um devemos indicar a posição no ecrã, dimensão e a respetiva imagem. Para representar posições e dimensões recorremos às classes `LPoint2` e `LVector2` do Panda3D. 

### O cenário

O cenário de fundo no nosso jogo será um campo de estrelas sobre o qual a nave e os asteroides se movem. Para tal, quando iniciamos o nosso jogo, vamos acrescentar como que um ator fitício que apenas fica parado no fundo com a imagem do cenário pretendido (`starts.jpg`). Acrescente ao método `__init__` as seguintes linhas de código:

```python
        bg = GameActor("stars.jpg", 
                    LPoint2(self.width/2,self.height/2), 
                    LVector2(self.width,self.height),
                    False)
        bg.setBin("background", 0)
```
Para definir este "ator" indicamos o seu aspecto (a imagem) e um ponto no meio da janela, assim como um vetor que define as dimensões da janela. Como estamos a usar algumas classes do Panda3D (que não fazem parte da linguagem original python), temos de informar de onde estas são obtidas, colocando no inicio do ficheiro:

```python
from gameactor import GameActor
from panda3d.core import LPoint2, LVector2
```

Experimente executar agora o seu programa e veja se já tem a imagem de fundo.


## Atores do jogo Asteroids

Cada ator do jogo corresponde a um personagem com determinado comportamento que é representado por uma imagem animada no ecrã. No nosso jogo, temos à partida, a nave controlada pelo jogador e os asteroides que vagueiam no espaço.

### Nave

Esta vai ser representada por uma imagem como a seguinte:

O seu comportamento é definido pelas ações do jogador no teclado. Assim temos de programar as alterações à nave para cada acção do jogador. Vamos definir que se a tecla -> for premida a nave deve rodar no sentido dos ponteiros no relógio e ao contrário se a tecla <- for premida. 

Depois vamos também querer que a nave se possa mover pelo ecrã e disparar tiros contra os asteroides.

### Asteroides

Cada asteroide terá uma de várias imagens possíveis:

O seu comportamento corresponde a vaguear pelo espaço de jogo e, assim, o seu comportamento tem de ser programado no próprio jogo para efetuar essa animação.

### Outros atores

Veremos mais tarde que outros atores serão necessários. Quando quizermos que o jogador dispare tiros da sua nave para destruir os asteroides, cada tiro será representado com mais um ator, com uma imagem próprio e com o comportamento de se mover pelo ecrã em linha reta para tentar atingir um asteroide.





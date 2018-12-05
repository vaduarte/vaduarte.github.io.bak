

# Aplicações na Web - Parte II

(Actividade da ExpoFCT 2018)
[https://cienciavivadifct.bitbucket.io/](https://cienciavivadifct.bitbucket.io/)

Esta atividade é um exemplo da utilização das tecnologias base de implementação
de páginas web (HTML, CSS, e TypeScript) para implementar um "jogo" muito simples,
que consiste na simulação de um conjunto de bolas a serem largadas numa caixa.

Nesta página encontras as instruções de construção deste jogo num conjunto de passos
que te levarão à implementação final.

## Tutorial

Bem-vindo ao tutorial de Aplicações Web da ExpoFCT 2018. Neste tutorial vamos olhar
para uma linguagem de programação chamada JavaScript e como usá-la para implementar
um simples demo de bolas saltitantes. Para implementar este "jogo" segue as instruções abaixo:

### Passo 1: Preparação

Abre o ficheiro [`index.html`](index.html) no browser e, de seguida, abre a consola de programador (`Ctrl+Shift+J`).
É nesta consola que vamos criar o nosso jogo!

Vês a caixa vazia na página web? Estes é o elemento básico do nosso jogo, o canvas.
É neste canvas que serão desenhados os objetos do jogo.

### Passo 2: Desenhar uma bola

Vamos começar por desenhar uma bola no meio do canvas. Para desenhar a bola precisamos de indicar qual a sua cor (`rgb(0, 153, 51)`), raio (`10`), e posição no canvas (`(x=500, y=300)`). Para tal copia o código abaixo:

```js

var canvas = document.getElementById("pool")
var ctx = canvas.getContext('2d');

var x = 10;
var y = 300;
var color = "rgb(0,153,51)";
var radius = 10;

function draw(x, y, color, radius) {
    ctx.save();
    ctx.beginPath();
    ctx.fillStyle = color;
    ctx.arc(x, y, radius, 0, 2 * Math.PI);
    ctx.fill();
    ctx.restore();
}
```
Para desenhar a bola basta escreveres na consola do browser `draw(x, y, color, radius)`.

Podes experimentar desenhar bolas noutros locais do canvas, alterando o valor de `x` ou `y`; dar outra cor à bola, alterando a variável `color` (podes escolher a tua cor preferida [aqui](https://www.w3schools.com/colors/colors_picker.asp)); mudar o tamanho da bola alterando o valor de `radius`.

### Passo 3: Física!

Um jogo com uma bola sem fazer nada é um pouco aborrecido! Neste passo vamos acrescentar movimento à bola atraves de deslocamento horizontal (`dx`) e vertical (`dy`). Definir o movimento da bola é, no fundo, atualizar a sua posição (`x`, `y`) de frame em frame. Para tal, precisamos de criar uma função (`update`) que define este comportamento, ou seja, que atualiza as coordenadas da bola dado um deslocamento em x (`dx`) e em y (`dy`).

Por último, para completar a animação precisamos de, em cada frame, limpar o canvas, atualizar a posição da bola (chamando a função `update`), e voltar a desenhá-la no ecrã. Para isto vamos usar a função `gameLoop`.

```js
var dx=1;
var dy=0;
```

```js
function update () {
    x += dx;
    y += dy;
}
```

```js
function gameLoop() {
    ctx.fillStyle = "rgb(255,255,255)";
    ctx.fillRect(0,0,canvas.width,canvas.height);
    update(dx, dy);
    draw(x,y,color,radius);
    requestAnimationFrame(gameLoop);
}
```

Para ativar a parte de física temos de chamar a função que atualiza o ecrã a cada animação: `gameLoop()`.

### Passo 4: Saltar nas paredes do canvas

No último passo o nosso pequeno jogo ficou mais interessante ao adicionar movimento
à bola. No entanto, seria bom que a bola ao bater numa extremidade do canvas
saltasse na direção oposta. Para isso, temos de alterar a nossa definição da função `update`.
O código em baixo faz exatamente isso: verifica qual a
extremidade em que a bola bateu e inverte o valor do deslocamento para que a
bola se desloque no sentido oposto. Copia o código abaixo.

```js
function update () {
    x += dx;
    y += dy;

    if ((x + radius) >= canvas.width) {
        dx = -(dx);
        x = canvas.width - radius;
    }

    if ((x - radius) <= 0) {
        dx = -(dx);
        x = radius;
    }

    if ((y + radius) >= canvas.height) {
        dy = -(dy);
        y = canvas.height - radius;
    }

    if ((y - radius) <= 0) {
        dy = -(dy);
        y = radius;
    }
}
```

### Passo 5: Adicionar gravidade

Vamos tornar o nosso jogo ainda mais interessante e realista ao adicionar gravidade.
No nosso jogo a gravidade é simulada como um deslocamento vertical constante (`gravity`), que é adicionado ao deslocamento vertical da bola (`dy`) a cada frame. O seguinte código adiciona gravidade ao jogo:

```js
var gravity = 1.5;
dy += gravity;
```

Acrescenta-o à definição da função `update` ficando assim:

```js
function update () {
    x += dx;
    y += dy;
    if ((x + radius) >= canvas.width) {
        dx = -(dx);
        x = canvas.width - radius;
    }

    if ((x - radius) <= 0) {
        dx = -(dx);
        x = radius;
    }

    if ((y + radius) >= canvas.height) {
        dy = -(dy);
        y = canvas.height - radius;
    }

    if ((y - radius) <= 0) {
        dy = -(dy);
        y = radius;
    }
    var gravity = 1.5;
    dy += gravity;
}
```

### Passo 6: Agitar

Ok, a gravidade é engraçada, mas ao fim de um tempo a bola fica parada no chão
tornando o nosso jogo um pouco aborrecido. Vamos adicionar a opção de agitar a
bola para que esta fique outra vez a saltar. Repara que esta funcionalidade
está ligada a um botão da interface, permitindo assim uma maior interação entre
o utilizador e o canvas.

Copia o seguinte código para adicionar a funcionalidade de agitar a bola:

```js
function random(min, max) {
    var num = Math.floor(Math.random() * (max - min + 1)) + min;
    return num;
}

function shake() {
    dx = random(-20, 20);
    dy = random(-25, 0);
}
```

### Passo 7: Acrescentar botões à pagina

Vamos adicionar algumas funcionalidades à interface do nosso jogo! Vamos acrescentar botões para:

* agitar as bolas
* ligar ou desligar a gravidade
* colocar o jogo em pausa

Para isso é necessário alterar o código HTML, isto no entanto não é possível fazer
através da consola de programador, é preciso editar directamente o ficheiro.

Faz download do [zip com os ficheiros do projeto](jumpingballs.zip). Depois de extraído o zip,
abre o ficheiro `index.html` com um editor de texto e acrescenta os seguintes elementos à div `buttons`.

```html
<button id="freezeButton">Freeze</button>
<button id="shakeButton">Shake</button>
<button id="gravityButton">Gravity <span id="gravity">ON</span></button>
<div class="controlbox">
    <label for="number">#balls</label>
    <input id="number" type="text" size="3"/>
</div>
<button id="setBallsButton">Set</button>
```

Abre o ficheiro `index.html` no browser e agora na interface devem ser
visíveis botões para controlar as diferente funcionalidades do jogo. Nota que
os botões ainda não fazem nada, no próximo passo vamos ligar os botões ao código
do jogo.

Ainda dentro da pasta do projeto existe um ficheiro com o nome `pool.js`. Este
ficheiro tem o código JavaScript com toda a lógica do nosso jogo das bolas saltitonas.

A diferença do nosso código anterior para este novo código é a definição
de uma classe para as bolas. Uma classe vai permitir a criação de vários objetos
com comportamento semelhante, neste caso bolas. A classe inclui os valores iniciais
da posição, deslocamento e ainda a cor da bola. Esta classe permite ainda
definir o comportamento das bolas, por exemplo o que acontece quando uma bola bate
na extremidade do canvas.

### Passo 8: Ligar os botões ao código do jogo

Vamos tornar o nosso jogo um pouco mais interativo, permitindo que o utilizador
controle certos aspetos da física que o nosso jogo implementa. O código abaixo
liga os botões `freeze` e `shake` da interface da página web.

Abre o ficheiro `pool.js` existente na pasta do projeto e adiciona o seguinte
código:

```js
var freezing = false;
var freezeButton = document.getElementById('freezeButton');
freezeButton.onclick = function() { freezing = !freezing; };

var shakeButton = document.getElementById('shakeButton');
shakeButton.onclick = function() { shake() };

var gravity = false;
var gravityButton = document.getElementById('gravityButton');
gravityButton.onclick = function() { gravity = !gravity; };
```

É necessário também actualizar o código da função `update` e `gameLoop`. Agora com os
botões da interface ligados passa a ser preciso verificar se a gravidade está ligada ou
se o jogo está em pausa antes de executar as operações.

O novo código da gravidade a alterar no final da função `update`:

```js
if( gravity )
    this.dy += GRAVITY;
```

Substitui também o código da função `gameLoop` pelo seguinte código:

```js
function gameloop() {
    context.fillRect(0, 0, canvas.width, canvas.height);

    if( !freezing )
        balls[0].update();

    balls[0].draw(context);
    loopRef = requestAnimationFrame(gameloop);
}
```

### Passo 9: Mais bolas!

Vamos agora adicionar mais bolas ao nosso jogo. O ficheiro de JavaScript `pool.js`
já está preparado para a adição de mais bolas, existe uma classe `Ball`
que vai premitir a criação e desenho de várias bolas no canvas do jogo.

A única coisa a fazer é desenhar realmente as várias bolas no canvas, para tal
é preciso alterar a função `gameLoop`, cujo novo código se encontra abaixo.

Substitui então o código da função `gameLoop` pelo seguinte código:

```js
function gameloop() {
    context.fillRect(0, 0, canvas.width, canvas.height);

    for(var i = 0; i < balls.length; i++){
        if( !freezing )
            balls[i].update();

        balls[i].draw(context);
    }

    loopRef = requestAnimationFrame(gameloop);
}
```

### Passo 10: Colisões

De forma a tornar o nosso jogo mais dinâmico vamos adicionar código que permite
detetar colisões entre bolas. Para cada bola que existe no canvas é preciso
verificar se alguma das restantes bolas colidiu com esta. Uma colisão acontece
quando a área de desenho de duas se sobrepõe, o código abaixo verifica esta situação
e quando isso acontece a velocidade das bolas é alterada para que se desloquem
em sentidos opostos.

Vamos começar por adicionar um botão para ligar/desligar as colisões das bolas,
adiciona o seguinte código ao ficheiro `index.html`:

```html
<button id="collisionButton">Collisions <span id="gravity">ON</span></button>
```

Copia o código abaixo para o ficheiro `pool.js` para tratar das colisões entre bolas:

```js
var colliding = false;
var collisionButton = document.getElementById('collisionButton');
collisionButton.onclick = function () { colliding = !colliding; };

function testCollision(b0, b1) {
    if (Math.sqrt((b0.x + b0.dx - b1.x - b1.dx) * (b0.x + b0.dx - b1.x - b1.dx) +
        (b0.y + b0.dy - b1.y - b1.dy) * (b0.y + b0.dy - b1.y - b1.dy)) < RADIUS * 2) {
        collideX(b0, b1);
        collideY(b0, b1);
    }
}
function collideX(ball0, ball1) {
    var dxAvg = (Math.abs(ball0.dx) + Math.abs(ball1.dx)) / 2;
    if (Math.sign(ball0.dx) == Math.sign(ball1.dx)) { //both in the same direction, one continues the other bounces back
        if (Math.abs(ball0.dx) > Math.abs(ball1.dx)) {
            ball0.dx = -Math.sign(ball0.dx) * dxAvg;
            ball1.dx = Math.sign(ball1.dx) * dxAvg;
        }
        else {
            ball0.dx = Math.sign(ball0.dx) * dxAvg;
            ball1.dx = -Math.sign(ball1.dx) * dxAvg;
        }
    }
    else { //frontal collision, both bounce back
        var dxAvg = (Math.abs(ball0.dx) + Math.abs(ball1.dx)) / 2;
        if (Math.sign(ball0.dx) == 0) {
            ball0.dx = Math.sign(ball1.dx) * dxAvg;
            ball1.dx = -Math.sign(ball1.dx) * dxAvg;
        }
        else if (Math.sign(ball1.dx) == 0) {
            ball1.dx = Math.sign(ball0.dx) * dxAvg;
            ball0.dx = -Math.sign(ball0.dx) * dxAvg;
        }
        else {
            ball0.dx = -Math.sign(ball0.dx) * dxAvg;
            ball1.dx = -Math.sign(ball1.dx) * dxAvg;
        }
    }
    var middleX = (ball0.x + ball1.x) / 2;
    if (ball0.x < middleX) {
        ball0.x = middleX - RADIUS - 1;
        ball1.x = middleX + RADIUS + 1;
    }
    else {
        ball0.x = middleX + RADIUS + 1;
        ball1.x = middleX - RADIUS - 1;
    }
}
function collideY(ball0, ball1) {
    var dyAvg = (Math.abs(ball0.dy) + Math.abs(ball1.dy)) / 2;
    if (Math.sign(ball0.dy) == Math.sign(ball1.dy)) {
        if (Math.abs(ball0.dy) > Math.abs(ball1.dy)) {
            ball0.dy = -Math.sign(ball0.dy) * dyAvg;
            ball1.dy = Math.sign(ball1.dy) * dyAvg;
        }
        else {
            ball0.dy = Math.sign(ball0.dy) * dyAvg;
            ball1.dy = -Math.sign(ball1.dy) * dyAvg;
        }
    }
    else {
        if (Math.sign(ball0.dy) == 0) {
            ball0.dy = Math.sign(ball1.dy) * dyAvg;
            ball1.dy = -Math.sign(ball1.dy) * dyAvg;
        }
        else if (Math.sign(ball1.dy) == 0) {
            ball1.dy = Math.sign(ball0.dy) * dyAvg;
            ball0.dy = -Math.sign(ball0.dy) * dyAvg;
        }
        else {
            ball0.dy = -Math.sign(ball0.dy) * dyAvg;
            ball1.dy = -Math.sign(ball1.dy) * dyAvg;
        }
    }
}
```

É preciso ainda actualizar a função `gameLoop`:

```js
function gameloop() {
    context.fillRect(0, 0, canvas.width, canvas.height);
    for (var i = 0; i < balls.length; i++) {
        if (!freezing) {
            balls[i].update();
            if (colliding)
                for (var j = i + 1; j < balls.length; j++)
                    testCollision(balls[i], balls[j]);
        }
        balls[i].draw(context);
    }
    loopRef = requestAnimationFrame(gameloop);
}
```

## Recursos extra

* Um [tutorial](http://www.typescriptgames.com/HTML5CanvasBasics.html) sobre como instalar e correr um projeto TypeScript.

* Um [tutorial da mozilla](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/Object_building_practice) sobre como utilizar o canvas criando um demo de bolas saltitonas parecido ao nosso.

* Um exemplo de uma animação mais complexa que simula o movimento de um cardume
de peixes - [Fishes flocking fun with JavaScript](http://paal.org/blog/2014/11/06/fishes-flocking-fun-with-javascript/).


# Aplicações na Web - Parte I

(Actividade da ExpoFCT 2018)
[https://cienciavivadifct.bitbucket.io/](https://cienciavivadifct.bitbucket.io/)

Esta actividade destina-se a demonstrar como é possível fazer uma pequena aplicação Web, ilustrando a criação de uma página web que nos deixa consultar os dados disponíveis na Internet e organizá-los da forma mais conveniente. A informação que vamos disponibilizar na nossa página é aquela proveniente do site [Open Movie Database](http://www.omdbapi.com/)

## Passo 1: Criar uma página web vazia

Em primeiro lugar vamos criar uma página web muito simples, apenas contendo a estrutura que pretendemos. Para isso, vamos editar um ficheiro no nosso computador, utilizando um editor de texto simples.

Podemos utilizar um ficheiro de texto contendo código escrito numa linguagem chamada HTML. Podemos utilizar para isso qualquer editor de texto disponível no computador. Grave o seu ficheiro no ambiente de trabalho com o nome `naWeb.html`. Nesse ficheiro pode colocar o seguinte código:

```html
<DOCTYPE html>
<html>
	<head>
  <meta charset="UTF-8">
		<title>Aplicações na Web - ExpoFCT 2018</title>
	</head>
	<body>

	</body>
</html>
```

Esta página está vazia mas já contém a estrutura básica que precisaremos para a página. O código HTML é composto por etiquetas que definem uma estrutura hierárquica para os vários elementos da página. As etiquetas têm um nome (ex: `html`), um elemento HTML a abrir (ex: `<head>`), e outro a fechar (ex: `</head>`). No exemplo acima, temos um elemento da página `<head>`, que define um conjunto de informações importantes da página tal como o seu título, o aspecto geral da página e o seu comportamento. Temos também o elemento `<body>` da página onde se definem os elementos visíveis da página.

## Passo 2: Criar a estrutura interna da página web

As páginas web que conhecemos dividem-se em divisórias, que em HTML são representadas pela etiqueta `<div>`, e que podem conter outras divisórias ou elementos HTML, como imagens ou elementos de `input` (caixas de texto ou botões). Para além disso, cada elemento HTML pode ainda ser enriquecido de outra forma através de atributos que de forma convencionada alteram o seu aspecto ou comportamento. Copie o código abaixo para dentro da etiqueta `<body>` da sua página:

```html
<div class="container">
  <div>
	  <div>
	    <img src="http://ctp.di.fct.unl.pt/~jcs/expofct15/naWeb/images/logo_fctunl.png">
	  </div>

	  <div class="nav">
	    <input id="search" type=text size=40>
	    <input type="submit" id="searchButton" class="btn-primary" value="Search">
	  </div>
	  <h1>Search the web for movie posters</h1>
  </div>
  (mais à frente vamos colocar mais código aqui)
</div>
```

Se abrir a sua página num browser, deve obter um resultado semelhante a:

![Primeira fase](http://ctp.di.fct.unl.pt/~jcs/expofct15/naWeb/images/first.png){height=4cm}\ 

Podem observar-se várias zonas e elementos nesta página, identifique quer na página, quer no código, a imagem, a caixa de texto para introduzir o texto de pesquisa, o botão que despoleta a pesquisa e o título. Repare que alguns elementos têm os atributos `class`, `src`, `id`, `type`, ou `value` com valores específicos. É da articulação de uma série de elementos, atributos, e código noutras linguagens que é feita uma página Web.

## Passo 3: Criar uma montra para os posters de filmes

Para colocar os nossos posters na página precisamos de criar mais divisórias. Copie para o código da sua página, no local onde se lê `(resto do código aqui)`, o seguinte código:

```html
  <div id="myCarousel" class="carousel slide" data-ride="carousel">
    <div id="posters" class="carousel-inner" role="listbox">
      <div class="item active">
        <img src="http://ctp.di.fct.unl.pt/~jcs/expofct15/naWeb/images/1.jpg">
      </div>
      <div class="item">
      	<img src="http://ctp.di.fct.unl.pt/~jcs/expofct15/naWeb/images/2.jpg">
      </div>
    </div>

    <a class="left carousel-control" href="#myCarousel" role="button" data-slide="prev">
      <span class="glyphicon glyphicon-chevron-left" aria-hidden="true"></span>
      <span class="sr-only">Previous</span>
    </a>
    <a class="right carousel-control" href="#myCarousel" role="button" data-slide="next">
      <span class="glyphicon glyphicon-chevron-right" aria-hidden="true"></span>
      <span class="sr-only">Next</span>
    </a>
  </div>
```

## Passo 4: Mudar o aspecto dos elementos existentes

O aspecto dos elementos HTML de uma página é regido por um conjunto de regras de estilo, que vamos passar a escrever. Para obtermos resultados mais rapidamente, podemos fazer uso de uma biblioteca de regras de estilos que nos ajudará. Insira na zona de cabeçalho da pagina `<head>` as seguintes linhas de código:

```html
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<link rel="stylesheet" href="http://maxcdn.bootstrapcdn.com/bootstrap/3.2.0/css/bootstrap.min.css">
<script src="https://ajax.googleapis.com/ajax/libs/jquery/1.11.1/jquery.min.js"></script>
<script src="http://maxcdn.bootstrapcdn.com/bootstrap/3.2.0/js/bootstrap.min.js"></script>
```

Através dos nomes dos elementos e dos seus atributos é possível especificar que regras se aplicam a que elementos e como é que se estes se formatam. Para perceber um pouco melhor copie estas regras para a sua página, para o fim da secção `<head>`.

```html
<style>
.container {
  background: url(http://ctp.di.fct.unl.pt/~jcs/expofct15/naWeb/images/logo-expofct2012.png)
  background: right -60px no-repeat;
}
#myCarousel {
  background-color: darkgrey;
}
.item {
  text-align: center;
  height: 500px;
}
.item > img {
  margin: auto;
  min-height: 100%;
}
.nav {
  float: right;
  margin: 20 0 10 0;
}
</style>
```

O aspecto da página deve ter mudado drasticamente depois destas duas modificações, certo? Deve ter algo como:

![Segunda fase](http://ctp.di.fct.unl.pt/~jcs/expofct15/naWeb/images/second.png){height=6cm}\ 

Com estas últimas regras foi possível modificar o aspecto de vários elementos, em tamanho, côr, posição no ecrã, e até adicionar novos elementos, como o logo da ExpoFCT.

Experimente agora usar as duas setas que aparecem no ecrã. Já têm algum comportamento (mágico) associado. Esse comportamento está pré-programado no código que incorporámos na página por via do elemento `<script>` acima. Já se carregar no botão `Search`, não terá qualquer resposta, pois não? Pois, é que não há magia, temos que agora resolver essa parte do puzzle.

## Passo 4: Adicionar comportamento à página.

Para que a nossa página possa agora ter um comportamento mais rico, vamos adicionar uma ligação ao serviço [OMDb](http://www.omdbapi.com/) que é disponibilizado na Internet. Para tal podemos adicionar o seguinte código no cabeçalho da página (fim da secção `<head>`).

```html
<script>

function search(){
  $.ajax({
      dataType: "json",
      async: true,
      cache: false,
      crossDomain: true,
      jsonp: true,
      url: "http://www.omdbapi.com/?apikey=YOUR-API-KEY-HERE"+"&t="+$("#search").val(),
      success: function(data) {
        if(data != null && data.Poster != undefined) {
          $(".item.active").removeClass("active");
          $("#posters").append($("<div>",{class:"item active"}).append($("<img>",{src:data.Poster})));
          alert($("#search").val() + " adicionado!");
        } else {
          alert("Não conheço nenhum filme chamado " + $("#search").val() + "!");
        }
      },
    });
  }

</script>
```

Este código define a maneira de consultar o serviço remoto (`function search()`) fazendo uso dos elementos do ecrã `$(".item.active")` e `$("#posters")` e alterando a sua estrutura (função `append`). Também define que o botão com o identificador `#searchButton` vai usar a função search em caso de ser activado através da linha de código, adiciona-o depois da definição da função `search`:

```js
$(function() { $("#searchButton").click(search); });
```
Usamos o comando `if` para, caso não tenhamos recebido uma resposta (`data != null`) e o poster não exista (`data.Poster != undefined`), adicionar o poster ao carrousel e abrir uma janela de alerta atraves do:
```js
alert($("#search").val() + " adicionado!");
```

Caso não exista um poster com esse titulo, é executado tudo o que está dentro do `else`, ou seja a mensagem de erro:
```js
alert("Não conheço nenhum filme chamado " + $("#search").val() + "!");
```

Para se poder utilizar o serviço [OMDb](http://www.omdbapi.com/) é necessário uma chave que identifique a origem dos pedidos feitos ao serviço. O pedido da chave pode ser feito [aqui](http://www.omdbapi.com/apikey.aspx), bastanto para isso selecionar o tipo de conta **FREE**, inserir o seu email, primeiro e último nome e finalmente uma breve descrição sobre a aplicação web que vai utilizar o serviço [OMDb](http://www.omdbapi.com/).

Uma vez obtida a chave, deve substituir no código a parte que diz `YOUR-API-KEY-HERE` pela chave que recebeu (pode usar a chave d348ff6a).

Agora sim, deve conseguir experimentar a página web para pesquisar filmes na internet e coleccionar alguns posters. É claro que esta construção é só a ponta de um iceberg gigantesco, mas é certamente um dos blocos que ajuda a construir a Internet tal como a conhecemos.


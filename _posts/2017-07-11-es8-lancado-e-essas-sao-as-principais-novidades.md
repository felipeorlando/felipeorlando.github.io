---
title: EcmaScript 8 é lançado e essas são as principais novidades!
og-image: es8.jpg
cover-image: es8.jpg
description: Depois do update pequeno que tivemos em 2016 com o EcmaScript 7, finalmente temos oficializadas grandes novidades que ouviamos por aí!
---

Depois do update pequeno que tivemos em 2016 com o EcmaScript 7, finalmente temos oficializadas **grandes** novidades que ouviamos por aí! 🎉

<!--more-->

![ES8]({{ site.url }}/img/es8.jpg)

Anunciada no final de julho de 2017 pela TC39, a nova atualização conta com novidades significativas na linguagem, sendo uma delas as Async Functions.

Com o anúncio oficial, é esperado que as empresas/comunidades por trás dos navegadores comecem a implementar aos poucos as novas funcionalidades através de atualizações.

Pra não se contenta com o básico, é possível ler a <a href="http://www.ecma-international.org/memento/presentation.htm" target="_blank">especificação do ECMAScript 2017</a> no site oficial da Ecma International.

⚠️  Lembrando que, se tratando de suporte aos atuais navegadores, precisamos ficar de olho com relação a compatibilidade. Para isso, indico o <a href="https://developer.mozilla.org/en-US/Add-ons/WebExtensions/Browser_support_for_JavaScript_APIs" target="_blank">MDN</a>.

### Sumário
1. [String padding](#string-padding)
1. [Object.values](#objectvalues)
1. [Object.entries](#objectentries)
1. [Object.getOwnPropertyDescriptors](#objectgetownpropertydescriptors)
1. [Vírgulas restantes ignoradas em funções](#vírgulas-restantes-ignoradas-em-funções)
1. [Async functions](#async-functions)

___

### String Padding
Há dois novos métodos que manipulam string: `padStart()` e `padEnd()`. Os métodos recebem um número inteiro como argumento e verificam se a string tem aquele tamanho.

Veja como são declarados os métodos com seus parâmetros:

{% highlight javascript %}
str.padStart(tamanhoMinimo [, stringSubstituta]);

str.padEnd(tamanhoMinimo [, stringSubstituta]);
{% endhighlight %}

Se o tamanho da string for maior que o número passado como parâmetro, nada é feito. Se for menor, é adicionado um espaço no início ou no fim (por isso duas funções diferentes):

{% highlight javascript %}
'test'.padStart(1);   // 'test'
'test'.padStart(6);   // '  test'

'test'.padEnd(4); // 'test'
'test'.padEnd(7); // 'test   '
{% endhighlight %}

Como segundo parâmetro podemos passar a string que substituirá o tamanho excedido, em vez de deixar o espaço por padrão:

{% highlight javascript %}
'test'.padStart(6, 'F');      // 'FFtest'
'test'.padStart(6, 'FELIPE'); // 'FEtest'

'test'.padEnd(7, 'F');        // 'testFFF'
'test'.padEnd(7, 'FELIPE');   // 'testFEL'
'test'.padEnd(13, 'FELIPE');  // 'testFELIPEFEL'
{% endhighlight %}

### Object.values
O método `Object.values()` tem como principal objetivo retornar apenas os valores de um objeto dentro de um Array, na exata ordem que eles foram declarados:

{% highlight javascript %}
const objeto = { x: 'men', y: 1 };
Object.values(objeto); // ['men', 1]

const  objeto = ['batman', 'coringa']; // o mesmo que { 0: 'batman', 1: 'coringa' }
Object.values(objeto); // ['batman', 'coringa']
{% endhighlight %}

Quando os chaves do objeto são números inteiros, a ordem é de acordo com os números, de módo crescente:

{% highlight javascript %}
	const objeto = { 100: 'ultimo', 1: 'primeiro', 50: 'meio' };
	Object.values(objeto); // ['primeiro', 'meio', 'ultimo']
{% endhighlight %}

### Object.entries
Se temos como necessidade transformar um objeto em array, levando em consideração que queremos agurpar as chaves com seus respectivos valores, o `Object.entries` pode nos ajudar, sem segredos:

{% highlight javascript %}
const obj = { x: 'xxx', y: 1 };
Object.entries(obj); // [['x', 'xxx'], ['y', 1]]

const obj = ['e', 's', '8'];
Object.entries(obj); // [['0', 'e'], ['1', 's'], ['2', '8']]

const obj = { 10: 'xxx', 1: 'yyy', 3: 'zzz' };
Object.entries(obj); // [['1', 'yyy'], ['3', 'zzz'], ['10': 'xxx']]
Object.entries('es8'); // [['0', 'e'], ['1', 's'], ['2', '8']]
{% endhighlight %}

### Object.getOwnPropertyDescriptors
Com o método `getOwnPropertyDescriptors`, é possível obter informações de propriedades de objetos.

{% highlight javascript %}
Object.getOwnPropertyDescriptors(objeto)
{% endhighlight %}

O `objeto` é passado como parâmetro para a função, retornando até 5 informações: `configurable`, `enumerable`, `writable`, `get`, `set` e `value`.

{% highlight javascript %}
const objeto = {
  get es7() { return 777; },
  get es8() { return 888; }
};

Object.getOwnPropertyDescriptors(obj);

// {
//   es7: {
//     configurable: true,
//     enumerable: true,
//     get: function es7(){}, //the getter function
//     set: undefined
//   },
//   es8: {
//     configurable: true,
//     enumerable: true,
//     get: function es8(){}, //the getter function
//     set: undefined
//   }
// }
{% endhighlight %}

### Vírgulas restantes ignoradas em funções
Esta nem é uma novidade tão mirabolante, mas é útil. Agora não teremos `SyntaxError` quando adicionarmos vírgulas excedentes na separação de argumentos em funções.

{% highlight javascript %}
function orlando(arg1, arg2, arg3,) {
  // ...
}

orlando('a', 'b', 'c',);
{% endhighlight %}

Talvez a maior utilidade quando usamos spread operator como último argumento e vamos passar vários argumentos quando formos invocar a função, utilizando múltiplas linhas.

### Async functions
Com certeza a funcionalidade mais usada do ES8 desde já, utilizando transpiladores. Talvez seja por ser a maneira mais fácil de se trabalhar com a assincronia do Javascript.

Para quem ainda não sabe como funciona, essa funcionalidade nos dá duas palavras chaves para se utilizar nas funções: `async` e `await`.

Adicionado o modificador `async` antes de declarar uma função, a transforma em uma função assíncrona, fazendo com que qualquer processo interno dessa função seja assíncrono.

Já o modificador `await` é utilizado em funções que ficam dentro do escopo de funções assíncronas (somente), fazendo que o fluxo  da função assíncrona seja interrompido, esperando pela promisse da função interna. Sacou? 🤔

Temos a seguinte função:

{% highlight javascript %}
async function falar(tempo, numero) {
  function timeout(ms) {
    return new Promise(resolve => setTimeout(resolve, ms));
  }
  await timeout(tempo);
  // 👆 o fluxo seguinte aguarda o retorno do timeout(),
  // só depois é executado o código abaixo:
  console.log(numero);
}
{% endhighlight %}

Utilizando a função acima, podemos criar outra e executá-la:

{% highlight javascript %}
async function contador() {
  await falar(3000, 1);
  await falar(2000, 2);
  await falar(1000, 3);
}

contador() // imprime na sequência: 1 2 3
{% endhighlight %}

Se a função acima fosse assíncrona e não utilizasse o `await`, teríamos como retorno `3 2 1`.

Para entender melhor, leia <a href="https://braziljs.org/blog/async-await-js-assincronamente-sincrono/" target="_blank">esse artigo</a> no blog da BrazilJS. 💛

___

Fonte: <a href="https://hackernoon.com/es8-was-released-and-here-are-its-main-new-features-ee9c394adf66" target="_blank">Dor Moshe - Hackernoon</a> ❤️

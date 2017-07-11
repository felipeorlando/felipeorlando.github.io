---
title: ES2017 é lançado e essas são as principais novidades!
layout: post
excerpt_separator: "<!--more-->"
---

Depois do update pequeno que tivemos em 2016 com o EcmaScript 7, finalmente temos oficializadas **grandes** novidades que ouviamos por aí! 🎉

<!--more-->

<div align="center">
	<blockquote class="twitter-tweet" data-lang="pt"><p lang="en" dir="ltr">ES2017 (the 8th edition of the JavaScript Spec) was officially released and published yesterday! <a href="https://t.co/1ITn5bzaqj">https://t.co/1ITn5bzaqj</a> 👏</p>&mdash; Kent C. Dodds (@kentcdodds) <a href="https://twitter.com/kentcdodds/status/880121426824630273">28 de junho de 2017</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>
</div>

Anunciada no final de julho de 2017 pela TC39, a nova atualização conta com novidades significativas na linguagem, sendo uma delas as Async Functions.

Com o anúncio oficial, é esperado que as empresas/comunidades por trás dos navegadores comecem a implementar aos poucos as novas funcionalidades através de atualizações.

Pra não se contenta com o básico, é possível ler a <a href="http://www.ecma-international.org/memento/presentation.htm" target="_blank">especificação do ECMAScript 2017</a> no site oficial da Ecma International.

⚠️  Lembrando que, se tratando de suporte aos atuais navegadores, precisamos ficar de olho com relação a compatibilidade. Para isso, indico o <a href="https://developer.mozilla.org/en-US/Add-ons/WebExtensions/Browser_support_for_JavaScript_APIs" target="_blank">MDN</a>.

### Sumário
1. [String padding](#)
1. [Object.values](#)
1. [Object.entries](#) 
1. [Object.getOwnPropertyDescriptors](#)
1. [Vírgulas restantes em funções ignoradas](#)
1. [Async functions](#)
1. [Shared memory and atomics](#)

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
Lorem ipsum dolor sit amet.

### Vírgulas restantes em funções ignoradas
Lorem ipsum dolor sit amet.

### Async functions
Lorem ipsum dolor sit amet.

### Memória compartilhada e Atomic
Lorem ipsum dolor sit amet.

___

Fonte: <a href="https://hackernoon.com/es8-was-released-and-here-are-its-main-new-features-ee9c394adf66" target="_blank">Dor Moshe - Hackernoon</a>
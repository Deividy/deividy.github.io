---

layout: post
title: JavaScript Scope Chain
comments: true
header-img: "img/coding.jpg"
author: Deividy Metheler Zachetti

---

O unico jeito de criar escopo em JavaScript é definindo uma função, sempre que uma função é 
definida ela cria um escopo, esse escopo tem uma ligação com o escopo de onde a função foi definida,
e isso é o que conhecemos como Scope Chain, ou cadeia de escopo.

Por definição **toda função em JavaScript é um closure**, pois são objetos, e tem uma
cadeia de escopo associada a elas.

Ou seja:

    var scope = 'global';

    function fnOuter() {
        console.log(scope);         // => undefined
        var scope = 'outer';

        return (function() {
            console.log(scope);     // => 'outer'
            scope = 'inner';
            return scope;
        }());
    }

    console.log(scope)  // => 'global'
    fnOuter();          // => 'inner'



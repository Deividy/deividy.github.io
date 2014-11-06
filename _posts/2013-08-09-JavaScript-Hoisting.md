---

layout: post
title: JavaScript Hoisting
comments: true
header-img: "img/coding.jpg"
author: Deividy Metheler Zachetti

---

Definições de variáveis e funções, são 'hoisted', ao topo da função onde foram definidos.

Considere o seguinte código JavaScript:

    fnExpression();          // => throw TypError!
    var fnExpression = function() {
        return "I'm a expression assigned to a variable";
    }
    fnExpression();         // => "I'm a expression assigned to a variable"

    fnStatement();          // => "I'm a statement with name"
    fuction fnStatement() {
        return "I'm a statement with name";
    }
    fnStatement();          // => "I'm a statement with name"

    var scope = 'global';
    function fn() {
        return scope;          
        var scope = 'local';
    }
    fn();                   // => undefined


O interpretador JavaScript transforma nisso:
    
    var fnExpression, scope;
    function fnStatement() {
        return "I'm a statement with name";
    }
    function fn() {
        var scope;
        return scope;
        scope = 'local';
    }

    fnExpression();
    fnExpression = function() {
        return "I'm a expression assigned to a variable";
    }
    fnExpression();

    fnStatement();
    fnStatement();

    scope = 'global';
    fn();

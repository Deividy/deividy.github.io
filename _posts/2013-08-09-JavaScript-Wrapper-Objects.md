---

layout: post
title: JavaScript Wrapper Objects
comments: true
header-img: "img/coding.jpg"
author: Deividy Metheler Zachetti

---

Tudo em JavaScript, com exceção de **null** e **undefined**, é um objeto, até mesmo os valores primitivos 
(String, Number or Boolean) herdam de **Object.prototype**. 
A diferença é que os valores primitivos são objetos **imutáveis**. Isso quer dizer que mesmo sendo objetos não podemos setar propriedades neles, podemos apenas ‘pegar’ suas propriedades/métodos (Isso não quer dizer que não podemos modificar os seus prototypes).

Quando tentamos setar alguma propriedade em algum valor primitivo, ao invés do interpretador retornar um erro, ele cria um objeto temporário para isso, conhecido como Wrapper Object, e em seguida exclui esse objeto.

> **Wrapper objects** são os objetos criados temporariamente quando setamos alguma propriedade em um valor primitivo.

    var s = 'Deividy';    // => undefined
    s.test = 123;         // => 123
    s.test;               // => undefined;

    var b = true;         // => undefined
    b.test = 123;         // => 123
    b.test;               // => undefined;

    Boolean.prototype.testMethod = function() { 
        return "test”; 
    };

    true.testMethod()     // => test

    var S = new String(‘Deividy’);       // => undefined
    S;                                   // => String { 0:’D', 1:’e', 2:’i', 3:’v', 4:’i', 5:’d', 6:’y’ };
    S.toString();                        // => Deividy
    S.test = 123;                        // => null
    S.test;                              // => 123

**Remember:** Valores primitivos são imutáveis, objetos são mutáveis.

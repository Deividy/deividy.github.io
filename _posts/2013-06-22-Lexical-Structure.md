---

layout: default
title: Lexical Structure Notes

---

# JS Lexical Structure Notes

**Unicode** character set, **case-sensitive**, whitespace and line breaks are ignored. The JS Interpreter
assumes that the source code it is interpreting has already been normalized and makes no attempt to normalize identifiers,
strings or regular expressions itself.

**undefined** is not a reserved word, is a special type of var.

Semicolons (**;**) are optionals in some cases, JS treats a line break as semicoln if the next nonspace character cannot be interpreted as a continuation of the current statement.

In JS strings are compost by **16bits** each letter.

Words from: [JS Definitive Guide 6th Edition](http://shop.oreilly.com/product/9780596805531.do)

> Roughly, an **expression** is something that computes a value but doesn’t do anything: it doesn’t alter the program state in any way. 
> **Statements**, on the other hand, don’t have a value (or don’t have a value that we care about), but they do alter the state.

> The other broad category of statement is control structures, such as conditionals and loops.

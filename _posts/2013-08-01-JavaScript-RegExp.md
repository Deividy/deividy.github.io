---

layout: default
title: Study book of Statements
comments: true

---

# Regular Expression

This is my study book of [JavaScript Definitive Guide 6th Edition](http://shop.oreilly.com/product/9780596805531.do).

Literals of primitive type, like strings and numbers, evalute (obviously) to the same value each time they are encountered in a program.
Object literals (or initializers) such as { } and [ ] create a new object each time they are encountered. If you write var a = [] in the body
of a loop, for example, each iteration of the loop will create a new empty array.

Regular expression literals are a special case. The ECMAScript 3 specification says that a RegExp literal is converted to a RegExp object when
the code is parsed, and each evaluation of the code returns the same object. The ECMAScript 5 specification reverses this and requires that each evaluation of a RegExp
return a new object. IE has always implemented the ECMAScript 5 behavior and most current browsers have now switched to it, even before they fully implemented the standard.

### Pontuation characters with special meaning
^ $ . * + ? = ! : | \ / ( ) [ ] { }

<!--break-->

## Nongreedy and greedy repetition

Greedy repetition is things like `{2}, ?, +, *`, nongreedy repetition is when we use 'combos', like (`??, +?, *? {1, 5}?`)


We can group with (), also specify the match position with ^ $ \b \B

(?=p) (?!p) is positive and negative lookahead assertion but they do not include those characters in the match


In JS we have only 3 flags

- i case-insesitiive
- g global
- m multiline


### String methods for pattern matching

- .search()
- .replace()
- .match()
- .join()

### The RegExp object

Have four properties:

- .source read-only the regular expression
- .global read-only bool (g flag)
- .ignoreCase read-only bool (i flag)
- .multiline read-only bool (m flag)

Have 2 methods:

- .exec() (Similar to match, but a little different, it return null if find nothing and return always the same kind of array)
- .test() It takes a string and returns true if the string contains a match for the regex, calling test() is equivalent to calling exec() and returning true if the return value of exec() is not null.



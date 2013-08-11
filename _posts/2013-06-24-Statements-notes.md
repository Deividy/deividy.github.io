---

layout: default
title: Study book of Statements
comments: true

---

# JS Statements

This is my study book of [JavaScript Definitive Guide 6th Edition](http://shop.oreilly.com/product/9780596805531.do).

 A JS program is simply a sequence of statements, separated from one another with semicolons.

    { 
        var x = 10, y = 12;
        function fn (v) {
            --y;
            return ++v;
        }
        
        fn(x);
        console.log(x, y);
        fn(y);
        console.log(x, y);
        console.log(fn(x), fn(y));
    
        console.log(x, y);
    }
    console.log(x, y);
    The curly braces are optional and does only one thing, let your code more readable.

JavaScript does not have block scope and variables declared within a statement block are not private to the block 

A compound statement allows you to use multiple statements where JavaScript syntax expects a single statement. The empty statement is the opposite: it allows you to include no statements where one is expected. like: 


<!--break-->

    ;

    var f = function (x) { return x+1; }        // Expression assigned to a variable
    function f(x) { return x+1; }               // Statement includes variable name

    function funcName(args...) {
        // statements
    }

The difference between a function declared with function and with var is that the function declared with function is hoisted, and with var it is hoisted only the var name, the definition stays on the same place

    var x = 1;
    if (x == 1) ;

    var f = function (x) { return x+1; }
    function fn(x) { return x+1; }
    
    // will be
    var x, f;
    function fn(x) { return x+1; }

    x = 1;
    if (x == 1) ;

    f = function(x) { return x+1; }

    // that means:
    console.log(fn(123));           // => 123
    function fn(v) { return v; }

    console.log(f(123));            // => throws a TypeError
    var f = function (v) { return v; }


Function declaration statements differ from function definition expressions in that they include a function name. Both forms create a new function object, but the function declaration statement also declares the function name as a variable and assigns the function object to it. Like variables declared with var, functions defined with function definition statements are implicitly “hoisted” to the top of the containing script or function, so that they are visible throughout the script or function. With var, only the variable declaration is hoisted—the variable initialization code remains where you placed it. With function declaration statements, however, both the function name and the function body are hoisted: all functions in a script or all nested functions in a func- tion are declared before any other code is run. This means that you can invoke a Java- Script function before you declare it.

if (!var) check if is null, undefined, false, 0, "" or NaN

The matching case of a switch is determined using the === not the ==

### Enumeration order becomes implementation dependent (and non-interoperable) if:
 - The object inherits enumerable properties OR
 - The object has properties that are interger array indexes OR
 - You have used delete to delete existing properties of the object OR
 - You have used Object.defineProperty() or similar methods to alter property attributes of the object.

Typically (but not in all implementations), inherited properties are enumerated after all the noninherited "own" properties of an object, but are also enumerated in the order in which they were defined. If an object inherits properties from more than one "prototype" - i.e., if it has more than one object in its "prototype chain" - then the properties of each prototype object in the chain are enumerated in creation order before enumerating the properties of the next object. Some (but not all) implementations enumerate array properties in numeric order rather than creation order, but they revert to creation order if the array is given other non-numeric properties as well or if the array is sparse (i.e., if some array indexes are missing).

#### Labeled statements

"By labeling a statement, you give it a name that you can use to refer to it elsewhere in your program. You can label any statement, although it is only useful to label statements that have bodies, such as loops and conditionals. By giving a loop a name, you can use break and continue statements inside the body of the loop to exit the loop or to jump directly to the top of the loop to begin the next iteration. break and continue are the only JavaScript statements that use statement labels"

    mainLoop: while (token != null) {
        continue mainloop;
    }

    var matrix      = getData(),
        sum         = 0, 
        success     = false;

    computeSum: if (matrix) {
        for (var x = 0; x < matrix.length; x++) {
            var row = matrix[x];
            if (!row) break computeSum;

            for (var y = 0; y < row.length; y++) {
                var cell = row[y];
                if (isNaN(cell)) break computeSum;
                sum += cell;
            }
        }
        success = true;
    }
    // The break statements jump here.

##### Continue;
 - In a while loop, the specified expression at the beginning of the loop is tested again, and if its true, the loop body is executed starting from the top.
 - In a do/while loop, execution skips to the bottom of the loop, where the loop condition is tested again before restarting the loop at the top.
 - In a for loop, the increment expression is evaluted, and the test expression is tested again to determine if another iteration should be done.
 - In a for/in loop, the loop starts over with the next property name being assigned to the specified variable.

The identifier associated with a catch clause has block scope - it is only defined within the catch block.

    // Simulate a for loop with while
    initialize ;
    while ( test ) {
        try { body; }
        finally { increment; }
    }

"Note, however, that a body that contains a break statement behaves slightly differently (causing an extra increment before exiting) in the while loop than it does in the for loop, so even with the finally clause, it is not possible to completely simulate the for loop with while."

#### with;
 The with statement is used to temporarily extend the scope chain.
    
    with (object)
        statement

 This statement adds object to the front of the scope chain, executes statement, and then restores the scope chain to its original state.
 The with statement is forbidden in strict mode and should be considered deprecated in non-strict mode.

    with (document.forms[0] {
        name.value = '';
        address.value = '';
        email.value = '';
    }

    var f = dcocument.forms[0];
    f.name.value = '';
    f.address.value = '';
    f.email.value = '';

 Keep in mind that the scope chain is used only when looking up identifiers, not when creating new ones.

#### debugger = breakpoint

#### "use strict"
 'use strict' is a directive introduce in ECMAScript 5.

 The strict mode of ECMAScript 5 is a restricted subset of the language that fixes a few important language deficiencies and provides stronger error checking and increased security.
 The differences between strict mode and non-strict mode are the following (the first three are particularly important):
 - The with statement is not allowed in strict mode.
 
 - In strict mode, all variables must be declared: a ReferenceError is thrown if you assign a value to an identifier that is not a declared variable, function, function parameter, catch clause parameter, or property of the global object. (In non-strict mode, this implicitly declares a global variable by adding a new property to the global object.)
 
 - In strict mode, functions invoked as functions (rather than as methods) have a this value of undefined. (In non-strict mode, functions invoked as functions are always passed the global object as their this value.) This difference can be used to determine whether an implementation supports strict mode:
 
    var hasStrictMode = (function() { "use strict"; return this===undefined}());

 Also, in strict mode, when a function is invoked with call() or apply(), the this value is exactly the value passed as the first argument to call() or apply(). (In nonstrict mode, null and undefined values are replaced with the global object and non-object values are converted to objects.)
 
 - In strict mode, assignments to nonwritable properties and attempts to create new properties on nonextensible objects throw a TypeError. (In non-strict mode, these attempts fail silently.)
 
 - In strict mode, code passed to eval() cannot declare variables or define functions in the caller’s scope as it can in non-strict mode. Instead, variable and function definitions live in a new scope created for the eval(). This scope is discarded when the eval() returns.
 
 - In strict mode, the arguments object (§8.3.2) in a function holds a static copy of the values passed to the function. In non-strict mode, the arguments object has “magical” behavior in which elements of the array and named function parameters both refer to the same value.
 
 - In strict mode, a SyntaxError is thrown if the delete operator is followed by an unqualified identifier such as a variable, function, or function parameter. (In non- strict mode, such a delete expression does nothing and evaluates to false.)
 
 - In strict mode, an attempt to delete a nonconfigurable property throws a TypeError. (In non-strict mode, the attempt fails and the delete expression eval- uates to false.)
 
 - In strict mode, it is a syntax error for an object literal to define two or more prop- erties by the same name. (In non-strict mode, no error occurs.)
 
 - In strict mode, it is a syntax error for a function declaration to have two or more parameters with the same name. (In non-strict mode, no error occurs.)
 
 - In strict mode, octal integer literals (beginning with a 0 that is not followed by an x) are not allowed. (In non-strict mode, some implementations allow octal literals.)
 
 - In strict mode, the identifiers eval and arguments are treated like keywords, and you are not allowed to change their value. You cannot assign a value to these iden- tifiers, declare them as variables, use them as function names, use them as function parameter names, or use them as the identifier of a catch block.
 
 - In strict mode, the ability to examine the call stack is restricted. argu ments.caller and arguments.callee both throw a TypeError within a strict mode function. Strict mode functions also have caller and arguments properties that throw TypeError when read. (Some implementations define these nonstandard properties on non-strict functions.)




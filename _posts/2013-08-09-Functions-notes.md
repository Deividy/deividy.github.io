---

layout: default
title: Function notes

---

# JS Function
 
My notes  about the reading of [JavaScript Defiitive Guide 6th Edition](http://shop.oreilly.com/product/9780596805531.do)

 JS functions definitions can be nested within other functions, and they have access to any variable that are in scope where they are defined. This means that JS functions are closures. (I got the power!)

 - Functions can be defined:
    
    var fn = function (args) { };
    var fn = function fun(args) { };
    var fn = (function() { }());
    function fn () {  }

Any legal JavaScript identifier can be a function name. Try to choose function names that are descriptive but concise. Striking the right balance is an art that comes with experience. Well-chosen function names can make a big difference in the readability (and thus maintainability) of your code.

 - Function declaration statements are hoisted.
 - Function defined with expression are not hoisted, in fact variable declarations are hoisted, but assignments to those variables are not hoisted

Expression are evaluated to produce a value, but statements are executed to make omething happen

 - Functions with no return value are sometimes called procedures
 - If a function hit a return statement it stops the execution of the function and return the value of its expression (if any) to the caller.
 - If a function does not contain a return statement, it simply executes each statement in the function body and returns the undefined value to the caller.

<!--break-->
### Invoking functions

#### as functions
  In ECMAScript 3 and nonstrict ECMAScript 5, the invocation context (the this value) is the global object. In strict mode, however, the invocation context is undefined.

#### as methods
 In a method invocation expression the object (where the method is invoked) becomes the invocation context.

    var o = {
           m: function () {
               var self = this;
               console.log(this === o);            // => true
               f();

               function f() {
                   console.log(this === o);        // => false: this is global or undefined
                   console.log(self === o);        // => true
               }
           }
    };

##### Method chaining
 To do a method chaining we need to return the context (this) of the function is executed to the caller, then we can do things like:

        me.method1().method2().method3().run();

#### as constructors
 If a function or method invocation is preceded by the keyword new, then it is a constructor invocation.
Constructor functions do not normally use the return keyword. They typically initialize the new object and then return implicitly when they reach the end of their body. In this case, the new object is the value of the constructor invocation expression. If, however, a constructor explicitly used the return statement to return an object, then that object becomes the value of the invocation expression. If the constructor uses return with no value, or if it returns a primitive value, that return value is ignored and the new object is used as the value of the invocation.

#### indirectly through their call() and apply() methods
 call() and apply() let us pass the context to invoke any function.

### Arguments
 - if we dont specify a parameter in a function invocation it will be undefined
 - inside any function we have the Arguments object, it is an array-like object that have all arguments used to invoke the function
 - Functions that can accept any number of arguments are called variadic functions, variable arity functions, or varargs functions

The Arguments object has one very unusual feature. In non-strict mode, when a function has named parameters, the array elements of the Arguments object are aliases for the parameters that hold the function arguments. The numbered elements of the Arguments object and the parameter names are like two different names for the same variable. Changing the value of an argument with an argument name changes the value that is retrieved through the arguments[] array. Conversely, changing the value of an argument through the arguments[] array changes the value that is retrieved by the argument name. 
This special behavior of the Arguments object has been removed in the strict mode of ECMAScript 5. There are other strict-mode differences as well. In non-strict functions, arguments is just an identifier. In strict mode, it is effectively a reserved word. Strict mode functions cannot use arguments as a parameter name or as a local variable name, and they cannot assign values to arguments.

    function f(x) {
           console.log(x);
           arguments[0] = null;
           console.log(x);         // => null
    }

 - arguments.callee refers to the currently running function
 - arguments.caller refers to the function that called this one

    var factorial = function (x) {
           if (x <= 1) return 1;
           return x * arguments.callee(x - 1);
    };

 - JS method parameters have no declared types, and no type checking is performed on the values you pass to a function.
 - JS performs liberal type conversion as needed.

### Function as values
 - Functions can be defined and invoked.
 - JS functions are not only syntax but also values, they can be assigned to variables, stored in the properties of objects or elements of array, passed as arguments to functions, ...

 - Functions are not primitive values in JS, but a specialized kind of object, which means that functions can have properties.

        uniqueInterger.counter = 0;
 
        function uniqueInterger() {
            return uniqueInterger.counter++;
        }

        function factorial(n) {
            if (isFinite(n) && n > 0 && n == Math.round(n)) {
                if (!(n in factorial)) {
                    factorial[n] = n * factorial(n - 1);
                }
                return factorial[n];
            } else {
                return NaN;
            }
        }

        factorial[1] = 1;

### Namespaces   
 JS has function scope: variables declared within a function are visible throughout the function (including nested functions) but do not exist outside of the function.
 Variables declared outside of a function are global variables and are visible throughout your JS program. JS does not define any way to declare variables that are hidden within a single block of code, and for this reason, it is sometimes useful to define a function simply to act as a temporary namespace in which you can define variables without polluting the global namespace.

        // anonymous
        (function() {
            // do something
        }());

        var extend = (function () {
           // Check the presence of an IE bug: in many versions of IE, the for/in loop
           // won't enumerate an enumerable property of o if the prototype of o has a non enumerable property by the same name.
           // This means that properties like toString are not handled correctly unless we explicitly check for them.
           for (var p in { toString: null }) {
               return function extend(o) {
                   for (var i = 1; i < arguments.length; i ++) {
                       var source = arguments[i];
                       for (var prop in source) {
                           o[prop] = source[prop];
                       }
                   }
                   return o;
               };
           }

           // If we get here, it means that the for/in loop did not enumerate the toString property
           // of the test object. So return a version of extend() function that explicitly tests for the
           // nonenumerable properties of Object.prototype
           return function patched_extend(o) {
               for (var i = 1; i < arguments.length; i++) {
                   var source = arguments[i];
                   for (var prop in source) {
                       o[prop] = source[prop];
                   }

                   for (var j = 0; j < protoprops.length; j++) {
                       prop = protoprops[j];
                       if (source.hasOwnProperty(prop)) {
                           o[prop] = source[prop];
                       }
                   }
               }
               return o;
           };

           var protoprops = [ "toString", "valueOf", "constructor", "hasOwnProperty", "isPrototypeOf", "propertyIsEnumerable", "toLocaleString" ];
        
        }());

The open parenthesis before function is required because without it, the JS interpreter tries to parse the function keyword as a function declaration statement. With the parenthesis, the interpreter correctly recognizes this as a function definition expression. It is idiomatic to use the parentheses, even when they are not required, around a function that is to be invoked immediately after being defined.

## Closures
 - Functions are executed using the variable scope that was in effect when they were defined, not the variable scope that is in effect when they are invoked.
 - In order to implement lexical scoping, the internal state of a JS function object must include not only the code of the function but also a reference to the current scope chain.
 - The combination of a function object and a scope in which the function's variables are resolved is called a closure in computer science literature.
  "This is an old term that refers to the fact that the function’s variables have bindings in the scope chain and that therefore the function is “closed over” its variables."
 In fact, all JS functions are closures, they are objects and they have a scope chain associated with them.
 
        var scope = "global scope"
        function checkScope() {
            var scope = "local scope";
            function f () {
                return scope;
            }
            return f;
        }
        checkScope()()                  // => local scope

### Functions are executed using the scope chain that was in effect when they were defined.

The scope chain is some like a list of objects. 
 - Each time a JS function is invoked, a new object is created to hold the local variables for that invocation, and that object is added to the scope chain.
 - When the function returns, that variable binding object is removed from the scope chain.
  > If there were no nested functions, there are no more references to the binding object and it gets garbage collected.
  > If there were nested functions defined, then each of those functions has a reference to the scope chain, and that scope chain refers to the variable binding object.
   - If those nested functions objects remained within their outer function, however, then they themselves will be garbage collected, along with the variable binding object they referred to.
   - If the function defines a nested function and returns it or stores it into a property somewhere, then there will be an external reference to the nested function. It won't be garbage collected, and the variable binding object it referes to won't be garbage collected

---

    var uniqueInterger = (function() {
        var counter = 0;
        return function () {
            return counter++;
        }
    }());
    function counter (n) {
        return {
            get count() { 
                return n++; 
            },
            set count(newValue) {
                if (newValue >= n) {
                    n = newValue;
                } else {
                    throw Error("count can only be st to a larger value");
                }
            }
        }
    }

    var c = counter(5);
    console.log(c.count);           // => 5
    console.log(c.count);           // => 6
    c.count = 2000;
    console.log(c.count);           // => 2000
    c.count = 2000;                 // => Error!

    function addPrivateProperty(o, name, predicate) {
        var value;

        o["get" + name] = function () { 
            return value; 
        };

        o["set" + name] = function (v) {
            if (predicate && !predicate(v)) {
                throw Error("set" + name + ": invalid value " + v);
            }
            value = v;
        };
    }

    var o = { };
    addPrivateProperty(o, 'Name', function (v) {
        return typeof v == "string"; 
    });

    addPrivateProperty(o, 'LastName', function (v) {
        return typeof v == "string"; 
    });


    o.setName('Deividy');
    o.setLastName('Metheler');
    console.log(o.getName() + " " + o.getLastName());       // => Deividy Metheler
    o.setName(o);                                           // => throw error

Nested functions do not make private copies of the scope or make static snapshots of the variable binds, the scope chain associated with a closure is "live".
Every function invocation has a this value, and a closure cannot access the this value of its outer function unless the outer function has saved that value into a variable.

### Functions Properties, Methods and Constructor
 - arguments.length returns the number of arguments passed
 - arguments.callee.length returns the number of arguments expected
 - prototype every function has a different prototype object. When a function is used as a constructor, the newly created object inherits properties from the prototype object
 - call and apply allow you to indirectly invoke a function if it were a method of some other object
  In ECMAScript 5 strict mode the first argument to call() or apply() becomes the value of this, even if it is a primitive value or null or undefined. In ECMAScript 3 and non-strict mode, a value of null or undefined is replaced with the global object and a primitive value is replaced with the corresponding wrapper object.
        
        function fn (x, y) {
            return x + y;
        }

        fn.call(o, 1, 2)
        fn.apply(o, [1, 2])
        
 - bind() was added in ECMAScript 5, when you invoke the bind() method on a function and pass an object, the method returns a new function. Invoking the new function (as a function) invokes the original function as a method of the object. Any arguments you pass to the new function are passed to the original function.

        function fn(y) {
            return this.x + y;
        }
        var o = { x: 1 };
        var g = f.bind(o);
        g(2);               // => 3
 
 The ECMAScript 5 bind() method does more than just bind a function. It also performs partial applicaton: any arguments you pass to bind() after the first bound along with the this value.
        
        var sum = function(x, y) { return x + y; }
        var succ = sum.bind(null, 1);
        succ(2)                                 // => 3

        function fn(y, z) {
            return this.x + y + z;
        }
        var g = fn.bind({ x: 1 }, 2);
        g(3);                                   // => 6

        
        // The original ECMAScript 5 bind() does have some features that cannot be simulated with this ECMAScript 3 code.
        // 1) The origina returns a function object with its length property properly set to the 
        // arity of the ound function minus the number of bound arguments (but not less than zero).
        // 2) The bind can be used for partial application of constructor functions. If the function returned by
        // bind() is used as a contructor, the this passed to bind() is ignored, and the original function is invoked as
        // a constructor, with some arguments already bound. 
        // Functions returned by the bind() method od not have a prototype property (the prototype property of regular
        // functions cannot be deleted) and objects created when these bound functions are used as constructors inherit 
        // from the prototype of the original, unbound constructor. Also, a bound constructor works just like the unbound
        // constructor for the purpose of the instaceof operator

        Function.prototype.bind = function(o /*, args */) {
            var self = this, boundArgs = arguments;
            return function () {
                var args = [ ], i;
                
                for (i = 1; i < boundArgs.length; i++) {
                    args.push(boundArgs[i]);
                }
                for (i = 0; i < arguments.length; i++) {
                    args.push(arguments[i]);
                }

                return self.apply(o, args);
            }
        }

- partial application is sometimes called currying.

- The Function() constructor

        var f = new Function("x", "y", "return x * y;");
    
 - The Function() constructor allows JS functions to be dynamically created and compiled at runtime.
 - The Function() constructor parses the function body and creates a new function object each time it is called. If the call to the constructor appears within a loop or within a frequently called function, this process can be inefficient. By contrast, nested functions and function definition expressions that appear within loops are not recompiled each time they are encountered.
 - The functions it creates do not use lexical scoping; instead, they are always compiled as if they were top-level functions.

        var scope = "global";
        function constructFunction() {
            var scope = "local";
            return new Function("return scope");
        }

        constructFunction()();          // => "global"

#### Memoization

        function memoize(f) {
            var cache = { };
            return function() {
                var key = arguments.length + Array.prototype.join.call(arguments, ",")
                if (key in cache) {
                    return cache[key];
                }
                return cache[key] = f.apply(this, arguments);
            }
        }



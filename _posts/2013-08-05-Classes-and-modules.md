---

layout: default
title: JS Classes and Modules notes

---

# JS Classes and Modules

This is my study book of [JavaScript Defiitive Guide 6th Edition](http://shop.oreilly.com/product/9780596805531.do)

 In JS, classes are based on JS's prototype-based inheritance mechanism. If two objects inherit properties from the same prototype object, then we say that they are instances of the same class.
 One of the most important features of JS classes is that the are dynamically extendable.

### Classes and Prototypes
 A class in JS is a set of objects that inherit properties from the same prototype object.

 We can create classes without a constructor
 
 The prototype property of the constructor is used as the prototype of the new object. This means that all objects created with the same constructor inherit from the same object and are therefore members of the same class.

    function Person(name) { 
        this.name = name;    
    }
    Person.prototype = {
        isMe: function () {
            return this.name == 'Deividy';
        }
    }
    Person.prototype.toString = function() {
        return "Noo!";
    }

    p = new Person('John');
    console.log(p instanceof Person);                                // => true
    console.log(p.constructor === Person);                           // => false
    console.log(p.constructor.prototype === Person.prototype)        // => false
    console.log(p.prototype === Person)                              // => false
    console.log(p.prototype === Person.prototype)                    // => false
    console.log(p.__proto__ === Person)                              // => ralse


    var F = function() {};
    F.prototype.constructor === F;                                  // => true


    Person.prototype > Constructor = Person()


**Constructor Object**
  As we've noted, the constructor function (an object) defines a name for a JS class. Properties you add to this constructor object serve as class fields and class methods.

**Prototype Object**
  The properties of this object are inherited by all instances of the class, and properties whose values are functions behave like instance methods of the class.

**Instance Object**
  Each instance of a class is an object in its own right, and properties defined directly on an instance are not shared by any other instances. Nonfunction properties defined on instances behave as the instance fields of the class.


First, write a constructor function that sets instance properties on new objects. Second, define instance methods on the prototype object of the constructor. Third, define class fields and class properties on the constructor itself. 

<!--break-->
    // Constructor
    function Complex() { }
    
    // Public instance method
    Complex.prototype.toString = function () {};

    // Static
    Complex.parse = function (s) { return s; };
    
    // Underscore to indicate private
    Complex._format = /^\{([^,]+),([^}]+)\}$/;

 - JS prototype-based inheritance mechanism is dynamic: an object inherits properties from its prototype, EVEN if the protype changes after the object is created.
 - It is possible to add methods to Object.prototype, making them available on all objects. (Not reocommended)

 - duck typing is a programming philosopy that focuses on what an object can do (what methods it has) rather than what its class is.

 - Two arrays created in two different frames inherit from two identical but distinct prototype objects, and an array created in one frame is not instanceof the Array() constructor of another frame.

 - "What is the class of this object?" duyck: "What can this object do?"

 When I see a bird that walks like a duck and swims like a duck and quacks like a duck, I call that bird a duck. - James Whitcomb Riley

 - "If an object can walk and swim and quack like a Duck, then we can treat it as a Duck, even if it does not inherit from the prototype object of the Duck class."

 - One approach to duck-typing is laissez-faire: we simply assume that our input objects implement the necessary methods and perform no checking at all.

---

    functions quacks (o /*, ... */) {
        for (var i = 1; i < arguments.length; i++) {
            var arg = arguments[i];
            
            switch(typeof arg) {
                case 'string':
                    if (typeof o[arg] !== "function") {
                        return false;
                    }
                    continue;
                
                case 'function':
                    arg = arg.prototype;
                
                case 'object':
                    for(var m in arg) {
                        if (typeof arg[m] !== "function") {
                            continue;
                        }
                        if (typeof o[m] !== "function") {
                            return false;
                        }
                    }
            }
        }
        return true;
    }

    
 - A set is a data structure that represents an unordered collection of values, with no duplicates.

 - An enumerated type is a type with a finite set of values that are listed (or "enumerated")
 when the type is defined. In C and languages derived from it, enumerated types are declared with 
 the enum keyword.

    function enumeration(namesToValues) {
        var enumeration = function() { throw "Can't Instantiate Enumerations" };
        
        var proto = enumeration.prototype = {
            constructor: enumeration,
            toString: function() { 
                return this.name; 
            },
            valueOf: function() { 
                return this.value; 
            },
            toJSON: function() { 
                return this.name; 
            }
        };

        enumeration.values = [ ];

        for(name in namesToValues) {
            var e = Object.create(proto);
            
            e.name = name;
            e.value = namesToValues[name];
            
            enumeration[name] = e;
            enumeration.values.push(e);
        }

        enumeration.foreach = function(f, c) {
            for(var i = 0; i < this.values.length; i++) {
                f.call(c, this.values[i]);
            }
        };

        return enumeration;
    }


### Standard Conversion Methods
 - toString()
 - toLocaleString()
 - valueOf()
 - toJSON()

### JS equality operators compare objects by reference, not by value.
- That is, given two object references, they look to see if both references are to the same object.
- It is sometimes useful to compare objects according to some ordering.
- One reason to define a compareTo() method for a class is so that arrays of instances of that class can be sorted.

### Subclasses
- The key is proper initialization of the prototype object.

### Composition
- Separate interface from implementation.

## Classes in ECMAScript 5
 - Properties Nonenumerable
 - Immutable Classes
 - Encapsulation Object State
 - Prevent Class Extensions
 - Property Descriptors

    function StringSet() {
        this.set = Object.create(null);
        this.n = 0;
        this.add.apply(this, arguments);
    }

    StringSet.prototype = Object.create(AbstractWritableSet.prototype, {
        constructor: { value: StringSet },
        contains: { value: function(x) { return x in this.set; } }    
    });

## Modules

    var Cool = (function() {
        function Cool() { }
        function private() {
            return "I'm private";
        }
        Cool.prototype.privateReturn = private();
        return Cool;
    }());

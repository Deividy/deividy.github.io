---

layout: default
title: Object notes
comments: true

---

# JS Object

This is my study book of [JavaScript Definitive Guide 6th Edition](http://shop.oreilly.com/product/9780596805531.do).

 An Object is an unordered collection of properties, each of which has a name and a value. Property names are strings, so we can say that object map strings to values. This string-to-value mapping goes by various names: "hash", "hashtable", "dictionary" or "associative array". An Object is more than a simple string-to-value map, however.
 A JS Object also inherits the properties of another object, know as its "prototype".
 Any value in JS that is not a string, a number, true, false, null or undefined is an object. And even though strings, numbers, and booleans are not objects, they behave like immutable objets.
 If the variable x refers to an object, and the code var y = x; is executed, the variable y holds a referece to the same object, not a copy of that object.

 A property has a name and a value. A property name may be any string, including the empty string, but no object may have two properties with the same name. The value may be any JS value, or (in ECMAScript 5) it may be a getter or a setter function (or both).
 In addition to its name and value, each property has associated values that we'll call property attributes:
 - The writable attribute specifies whether the value of the property can be set.
 - The enumerable attribute specifies whether the property name is returned by for/in loop.
 - The configurable attribute specifies whether the property can be deleted and wheter its attributes can be altered.

 Prior to ECMAScript 5 (BTW, node uses ECMAScript 5 :)), all properties in objects created by your code are writable, enumerable, and configurable. In ECMAScript 5, you can configure the attributes of your properties.

In addition to its properties, every object has three associated object attributes:
 - An object's prototype is a reference to anther object from which properties are inherited.
 - An object's class is a string that categorizes the type of an object.
 - An object's extensible flag specifies (in ECMAScript 5) wheter new properties may be added to the object.

<!--break-->
Some terms we'll use to distinguish among three broad categories of JS objects and two types of properties:
 - A native object is an object or class of objects defined by the ECMAScript specification.
 - A host object is an object defined by the host environment (such as a web browser) within which the JS interpreter is embedded.
 - A user-defined object is any object created by the execution of JS code.
 - An own property is a property defined directly on an object.
 - An inherited property is a poperty defined by an object's prototype object.


### Object creation 
 We can create objects with object literals, with the new keyword or in ECMAScript 5 with Object.create();
          
#### Object literals
 An object literal is a comma-separeted list of colon-separeted name: value pairs, enclosed with curly braces.

    var empty = { };
    var complex = {
        x: 0,
        y: 0,
        book: {
           title:  "JS Book",
           version: 1.2,
           "for": "reserved keywords in generally must be quoted",
           "another-stuff": "For special we need to use quotes"
        },
        z: otherObject.propertyZ + otherObject.propertyY
    }

 IE, and some implementations of ECMAScript 3, consider a trailing comma following the last property in an object literal an error, other implementations ignore it.
 An object literal is an expression that creates and initializes a new and distinct object each time it is evaluted. The value of each property is evaluated each time the literal is evaluted. This means that a single object literal can create many new objects if it appears within the body of a loop in a function that is called repeatedly, and that the property values of these objects may differ from each other.

#### Creating objects with new

    var o = new Object();       // the same as { }
    var a = new Array();        // the same as [ ]
    var d = new Date();         // create a new Date object representing the current local time
    var r = new RegExp('js');   // Create a RegExp object for pattern matching

#### Prototypes (basic)
 All objects crated by object literals have the same prototype object, and we can refer to this prototype object in JS code as Object.prototype. Objects created using the new keyword and a constructor invocations use the value of the prototype property of the constructor function as their prototype.

#### Object.create()
 It creates a new object, using its first argument as the prototype of that object. Also takes an optional second argument that describes the properties of the new object.
 Object.create() is a static function.

    var o1 = Object.create({ x: 1, y: 2 });         // o1 inherits properties x and y.
    var o2 = Object.create(null);                   // o1 inherits no properties or methods.
    var o3 = Object.create(Object.prototype);       // the same of { } or new Object()

 If you pass null to create a new object, this new object will have no prototype, will not inherit anything, not even basic methods like toString().
    
    // "cross ECMAScripts inherit"

    function inherit(p) {
        if (p == null) throw TypeError();
        if (Object.create) {
            return Object.create(p); // ECMAScript 5
        }
        var t = typeof p;
        if (t !== "object" && t !== "function") throw TypeError();
        function f() { };
        f.prototype = p;
        return new f();
    }


    var a = new Object().toString();                        // => '[object Object];
    var b = Object.create(a).toString();                    // => '[object Object]'
    var c = Object.create(null).toString();                 // => throw a TypeError
    var d = Object.create(Object.prototype).toString();     // => '[object Object]'


##### Inheritance

##### Getting

    var o = { }
    o.x = 1;
    var p = inherit(o);
    p.y = 2;
    var q = inherit(p);
    q.z = 3;
    var s = q.toString();
    q.x + q.y                   // => 3: x and y are inherited from o and p

Suppose you query the property x in the object o. If o does not have an own property with that name, the prototype object o is queried for the property x. If the prototype object does not have an own property by that name, but has a prototype itself, the query is perfomed on the prototype of the prototype. This continues until the property x is found or until an object with a null prototype is searched.
The prototype attribute of an object creates a chain or linked list from which properties are inherited.

##### Setting properties

    var u = { r: 1 },
        c = inherit(u);

    c.x = 1;
    c.y = 1;
    c.r = 2
    u.r;                // => 1: the prototype object is not affected
    
Property assignment examines the prototype chain to determine whether the assignment is allowed. If o inherits a read-only property named x, for example, then the assignment is not allowed. If the assignment is allowed, however, it always creates or sets a property in the original object and never modifies the prototype chain. The fact that inheritance occurs when querying properties but not when setting them is a key feature of JavaScript because it allows us to selectively override inherited properties.

There is one exception to the rule that a property assignment either fails or creates or sets a property in the original object. If o inherits the property x, and that property is an accessor property with a setter method, then that setter method is called rather than creating a new property x in o. Note, however, that the setter method is called on the object o, not on the prototype object that defines the property, so if the setter method defines any properties, it will do so on o, and it will again leave the prototype chain unmodified.

##### Property access errors

    var book = { sub: "test" };
    book.subtitle;                      // => undefined

    var len = book.subtitle.length;     // throw a TypeError exception, undefined doesn't have a length property
    
    // guard
    var len = undefined;
    if (book) {
        if (book.subtitle) len = book.subtitle.length;
    }

    // A concise and idiomatic alternative to get subtitle length or undefined    
    var len = book && book.subtitle && book.subtitle.length;

    // The prototype properties of built-in constructors are read-only.
    Object.prototype = 0;           // Assignement fails silently; Object.prototype unchanged

In strict mode, any failed attempt to set a property throws a TypeError exception.
An attempt to set a property p of an object o fails in these circumstances:
 - o has an own property p that is read-only: it is not possible to set read-only properties.
 - o has an inherited property p that is read-only: it is not possible to hide an inherited read-only property with an own property of the same name.
 - o does not have an own property p; o does not inherit a property p with a setter method, and o’s extensible attribute is false. If p does not already exist on o, and if there is no setter method to call, then p must be added to o. But if o is not extensible, then no new properties can be defined on it.

##### Deleting Properties

- The delete operator does not operate on the value of the property but on the property itself.
- The delete operator only deletes own properties, not inherited ones.

        var o = { x: 1 };
        delete o.x;                 // => true
        delete o.x;                 // => true
        delete o.toString;          // => true
        delete 1;                   // => true
        o.x;                        // => undefined
        o.toString();               // => '[object Object]'

#### Testing Properties

- in operator
- .hasOwnProperty()
- .propertyIsEnumerable()
- query property (a.x)

        var a = { x: 1 };
        var b = Object.create(a);
        b.y = "1";

        "x" in b                        // => true
        b.hasOwnProperty('x');          // => false
        b.hasOwnProperty('y');          // => true
        b.propertyIsEnumerable('x');    // => false
        b.propertyIsEnumerable('y');    // => true

### Property attributes
 - value
 - writable
 - enumerable
 - configurable

 - Object.getOwnPropertyDescriptor(object, property);
    
    Object.getOwnPropertyDescriptor({ x: 1 }, "x" });               // => { value: 1, writable, true, enumerable: true, configurable: true }
    Object.getOwnPropertyDescriptor(Object.prototype, 'toString');  // => { value: Function: toString], writable: true, enumerable: false, configurable: true }
    Object.getOwnPropertyDescriptor({ }, 'toString');               // => undefined

 To set read-only and set-only properties we can use only a get or only a set.
 We also have:
  - Object.definePropety(object, property, definitions);
  - Object.defineProperties(object, objectPropertyDefinitionsMap);
 
     var o = { };
     Object.defineProperty(o, "x", { 
        value: 1,
        writable: true,
        enumerable: false,
        configurable: true
     });

The property descriptor you pass to Object.defineProperty() does not have to include all four attributes. If you’re creating a new property, then omitted attributes are taken to be false or undefined. If you’re modifying an existing property, then the attributes you omit are simply left unchanged. Note that this method alters an existing own property or creates a new own property, but it will not alter an inherited property.

     var o = Object.defineProperties({ }, {
        x: { 
            value: 1,
            writable: true,
            enumerable: true,
            configurable: true
        },
        y: {
            value: 2,
            writable: false,
            enumerable: false,
            configurable: false
        },
        r: {
            get: function () {
                return Math.sqrt(this.x * this.x + this.y * this.y);
            },
            enumerable: false,
            configurable: true
        }
    });

 The second object of Object.create is the object mapper properties.
 - Object.create(objectPrototype, objectPropertyDefinitionsMap);

 Calls to Object.defineProperty() or .defineProperties() that attempt to violate them throw TypError:
 - If an object is not extensible, you can edit its existing own properties, but you cannot add new properties to it.
 - If a property is not configurable, you cannot change its configurable or enumerable attributes.
 - If an accessor property is not configurable, you cannot change its getter or setter methods, and you cannot change it to a data property.
 - if a data property is not configurable, you cannot change it to an accessor property.
 - If a data property is not configurable, you  cannot change its writable attribute from false to true, but you can change it from true to false.
 - If a data property is not configurable and not writable, you cannot change its value. You can change the value of a property that is configurable but nonwritable, howerver (because that would be the same as making it writable, then changing the value, then converting it back to nonwritable);

 Legacy API for Getters and Setters
 - __lookupGetter__()
 - __loopupSetter__()
 - __defineGetter__()
 - __defineSetter__()

#### Object Attributes
 - prototype
 - class
 - extensible attributes

##### The prototype attribute
 ECMAScript 5 allows access to a prototype of an object with Object.getPrototypeOf();

    var p = { x: 1 };
    var o = Object.create(p);
    p.isPrototypeOf(o);         // => true
    Object.isPrototypeOf(o);    // => true

#### The class attribute
 An object’s class attribute is a string that provides information about the type of the object. Neither ECMAScript 3 nor ECMAScript 5 provide any way to set this attribute, and there is only an indirect technique for querying it, the .toString();

    "[object class]"

    function classOf(object) {
        if (object === null) {
            return "Null"   
        }
        if (object === undefined) {
            return "Undefined";
        }
        return Object.prototype.toString.call(object).slice(8, 1);
    }

    classOf(null);      // => 'Null'
    classOf(1):         // => 'Number'
    classOf([]);        // => 'Array'
    function f() { };
    classOf(new f());   // => 'Object'

#### The extensible attribute
The extensible attribute of an object specifies whether new properties can be added to the object or not. In ECMAScript 3, all built-in and user-defined objects are implicitly extensible, and the extensibility of host objects is implementation defined. In ECMA- Script 5, all built-in and user-defined objects are extensible unless they have been converted to be nonextensible, and the extensibility of host objects is again implemen- tation defined.
 ECMAScript 5
 - Object.preventExtension(): makes an object no extensible, there is no way to make that object extensible again
 - Object.isExtensible()
 - Object.seal(): works like Object.preventExtension(), but it also makes all of the own properties of that object nonconfig- urable. This means that new properties cannot be added to the object, and existing properties cannot be deleted or configured. Existing properties that are writable can still be set, however. There is no way to unseal a sealed object.
 - Object.isSealed();
 - Object.freeze(): works like Object.seal(), but it also makes all of the object’s own data properties read-only. (If the object has accessor properties with setter methods, these are not affected and can still be invoked by assignment to the property.) 
 - Object.isFrozen();

Object.preventExtensions(), Object.seal(), and Object.freeze() all return the object that they are passed, which means that you can use them in nested function invocations

     var o = Object.seal(Object.create(Object.freeze({ 
        x: 1 
     }), { 
        y: { 
            value: 2, 
            writable: true 
        } 
    }));

### Object creation
 - literal ({ }): use Object.prototype as their prototype  
 - new (new Object): use the value pf the prototype property of their constructor function as their prototype
 - Object.create(): use the first argument to that function, may be null, as their prototype



---

layout: default
title: Study book of Expressions and Operators
comments: true

---

# JS Expressions and Operators

This is my study book of [JavaScript Definitive Guide 6th Edition](http://shop.oreilly.com/product/9780596805531.do).

 An expression is a phrase of JS that a JS interpreter can evaluate to produce a value

 Simplest expressions are known as primary expressions, are those that stand alone

 When an object creation expression is evaluted, JS first creates a new emmpty object, next, it invokes the specified function with the specified arguments, passing the new object as the value of the this keywords.
 
 Functions written for use as constructors do not return a value, and the value of object creation expressions is the newly created and initialized object. If a constructor does return an object value, that value becomes the value of the object creation expression and the newly object is discarded.

 Nice table of operators is in Pag. 80

 Unary + and - tries to convert his value into Number and positive or negative

<!--break-->

 Lvalue is a historical term that means "an expressions that can legally appear on the left side of an assignment expression"

 Some operators has side efects, its the case of delete, ++ and --

 Pos/Pre-Increment/Decrement (++ / --)

    var x = 1;
    var y = x++; // y = 1, x = 2;

    var x = 1;
    var y = ++x: // y = 2, x = 2;

**The + operator**
If either of its operand values is an object, it converts it to a primitive using the object-to-primitive algorithm. Date objects are converted by their .toString(), and all other objects are converted via .valueOf(), if that method returns a primitive value. Most objects do not have a useful .valueOf(), however, so they are converted via .toString() as well.

After object-to-primitve conversion, if either operand is a string, the other is converted to a string and concatenation is performed.

Othewrise, both operands are converted to numbers (or to NaN) and addition is performed.

    var x = 1 + 2; // => 3
    var x = 1 + "2"; // => '12'
    var x = 1 + 2 + "5"; // => '35'
    var x = 1 + (2 + "5"); // => '125'
    var x = "1" + 5 + 2; // => "152"


    == Equality (truthy)
    === Strict equality

#### The strict equality operator === evaluates its operands, and then compares the two values as follows, performing no type conversion:
- If the two values have different types, they are not equal.
- If both values are null or both values are undefined, they are equal.
- If both values are the boolean value true or both are the boolean value false, they are equal.
- If one or both values is NaN, they are not equal. The NaN value is never equal to any other value, including itself! To check whether a value x is NaN, use x !== x. NaN is the only value of x for which this expression will be true.
- If both values are numbers and have the same value, they are equal. If one value is 0 and the other is -0, they are also equal.
- If both values are strings and contain exactly the same 16-bit values (see the sidebar in §3.2) in the same positions, they are equal. If the strings differ in length or content, they are not equal. Two strings may have the same meaning and the same visual appearance, but still be encoded using different sequences of 16-bit values. JavaScript performs no Unicode normalization, and a pair of strings like this are not considered equal to the === or to the == operators. See String.localeCompare() in Part III for another way to compare strings.
- If both values refer to the same object, array, or function, they are equal. If they refer to different objects they are not equal, even if both objects have identical properties.


#### The equality operator == is like the strict equality operator, but it is less strict. If the values of the two operands are not the same type, it attempts some type conversions
and tries the comparison again:
- If the two values have the same type, test them for strict equality as described above. If they are strictly equal, they are equal. If they are not strictly equal, they are not equal.
- If the two values do not have the same type, the == operator may still consider them equal. Use the following rules and type conversions to check for equality:
  - If one value is null and the other is undefined, they are equal.
  - If one value is a number and the other is a string, convert the string to a number
and try the comparison again, using the converted value.
  - If either value is true, convert it to 1 and try the comparison again. If either value
is false, convert it to 0 and try the comparison again.
  -  If one value is an object and the other is a number or string, convert the object to a primitive using the algorithm described in §3.8.3 and try the comparison again. An object is converted to a primitive value by either its toString() method or its valueOf() method. The built-in classes of core JavaScript attempt valueOf() conversion before toString() conversion, except for the Date class, which performs toString() conversion. Objects that are not part of core Java- Script may convert themselves to primitive values in an implementation-defined way.
  -  Any other combinations of values are not equal.

As an example of testing for equality, consider the comparison:
    
    "1" == true
This expression evaluates to true, indicating that these very different-looking values are in fact equal. The boolean value true is first converted to the number 1, and the comparison is done again. Next, the string "1" is converted to the number 1. Since both values are now the same, the comparison returns true.

### Remember that JavaScript strings are sequences of 16-bit integer values, and that string comparison is just a numerical comparison of the values in the two strings. 

#### eval()

    var geval = eval;
    var x = "global", y = "global";
    function f() {
        var x = "local";
        eval("x += 'changed'");
        return x;
    }

    function g() {
        var y = 'local';
        geval("y += 'changed'");
        return y;
    }

    console.log(f(), x); // => "localchanged global"
    console.log(g(), y); // => "local globalchanged"

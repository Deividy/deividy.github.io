---

layout: default
title: Array Notes

---

# JS Array

This is my study book of [JavaScript Definitive Guide 6th Edition](http://shop.oreilly.com/product/9780596805531.do).

JS arrays are a specialized form of JS Object, and array indexes are really little more than property names that happen to be integers. 

Inherit properties from **Array.prototype**

**zero-base 32-bit indexes**

Max index **2(32) - 2 (4294967294)**

    var a = [1, 2, 3, , ];
    a.length;               // => 4

    var a = new Array(5);
    a;                     // => [ , , , , ]
    a[0];                  // => undefined

    var a = new Array(5, 4, 3, 2, 1);
    a;                    // => [5, 4, 3, 2, 1]

**Sparse array**
A sparse array is one in which the elements do not have contiguous indexes starting at 0.

**Array that are dense, not sparse.**

When an array is sparse, the length property is greater than the number of elements, and all we can say about it is that length is guaranteed to be larger than the index of every element in the array.
A array will never have an element whose index is greather or equal to its length.

    var a = [1, 2, 3];
    delete a[1];
    1 in a;             // => false
    a.length;           // => 3

Deleting an array element is similar to (but subtly different than) assigning undefined to that element. Note that using delete on an array element does not alter the length property and does not shift elements with higher indexes down to fill in the gap that is left by the deleted property. If you delete an element from an array, the array becomes sparse.

<!--break-->

    var keys = Object.keys(a);
    var values = [ ];
    for (var i = 0, len = keys.length; i < len; i++) {
        if (!a[i]) {
            continue;
        }

        if (a[i] === undefined) {
            continue;
        }

        if (!(i in a)) {
            continue;
        }

        var key = keys[i];
        values[i] = a[key];
    }


**Multidimensional Arrays**
JS does not support true multidimensional arrays, but you can approximate them with arrays of arrays.

    var table = new Array(10);
    for (var i = 0; i < table.length; i++) {
        table[i] = new Array(10);
    }

    for (var row = 0; row < table.length; row++) {
        for (var col = 0; col < table[row].length; col++) {
            table[row][col] = row*col;
        }
    }

    var product = table[5][7];          // => 35


### Array methods

#### ECMAScript 3
 - [ ].join()                   return
 - [ ].reverse()                modify
 - [ ].sort()                   modify
 - [ ].concat()                 return
 - [ ].slice()                  return
 - [ ].splice()                 modify and return deleted
 - [ ].push()                   modify and return inserted index
 - [ ].pop()                    modify and return deleted
 - [ ].unshift()                modify and return last index
 - [ ].shift()                  modify and return deleted
 - Array.toString()             return
 - Array.toLocaleStrig()        return

#### ECMAScript 5
Most of the methods accept a function as their first argument and invoke that function for each element (or some elements).
If the array is sparse, the function you pass is not invoked for nonexistent elements.
In most cases, the function you supply is invoked with three arguments: the value of the array element, the index of the array element, and the array itself.
Most of the ECMAScript 5 array methods that accept a function as their first argument accept an optional second argument. If specified, the function is invoked as if it is a method of this second argument. That is, the second argument you pass be- comes the value of the this keyword inside of the function you pass. The return value of the function you pass is important, but different methods handle the return value in different ways. 
None of the ECMAScript 5 array methods modify the array on which they are invoked. If you pass a function to these methods, that function may modify the array, of course.

 - [ ].forEach(function (value, index, array) { });
 - [ ].map(function (value, index, array) { return value; });
 - [ ].filter(function (value, index, array) { return (true or false); });
 - [ ].every(function (value, index, array) { return (true or false); });
 - [ ].some(function (value, index, array) { return (true or false); });
 - [ ].reduce(function (aculumator, value, index, array) { return value; });
 - [ ].reduceRight(function (acumulator, value, index, array) { return value; });
 - [ ].indexOf(value);
 - [ ].lastIndexOf(value);

- Array.isArray([ ]);        // ECMAScript 5
- [ ] instance of Array;     // is not the best way, it can be fuzzy

    var isArray = Function.isArray || function (object) {
        return typeof object === "object" && Object.prototype.toString.call(object) === "[object Array]";
    }

- Array-like objects

Array special features:
 - The length property is automatically update as new elements are added to the list
 - Setting length to a smaller value truncates the array.
 - Arrays inherit useful methods from Array.prototype
 - Arrays have a class attribute of "Array"

    var o = { };
    while (i < 10) {
        a[i] = i * i;
        i++;
    }
    a.length = i;

    var total = 0;
    for (var j = 0; j < a.length; j++) {
        total += a[j];
    }

    function isArrayLike(o) {
        if (o && typeof o === "object" && isFinite(o.length) && o.length >= 0 && o.length === Math.floor(o.length) && o.length < 4294967296) {
            return true;
        }
        return false;
    }
    
- Strings as Arrays
  In ECMAScript 5, strings behave like read-only arays. Instead of accessing individual characters with the charAt() method, you can use square brackets.

    var s = "JavaScript";
    Array.prototype.join.call(s, " ");                      // => "J a v a S c r i p t"
    Array.prototype.filter.call(s, function (value) {
        return value.match(/[^aeiou]/);
    }).join("");                                            // => "JvScrpt"

Keep in mind that strings are immutable values, so when they are treated as arrays, they are read-only arrays. Array methods like push(), sort(), reverse(), and splice() mod- ify an array in place and do not work on strings. Attempting to modify a string using an array method does not, however, cause an error: it simply fails silently.




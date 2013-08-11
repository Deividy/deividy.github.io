---

layout: default
title: CoffeeScript Accelerated JavaScript Development

---

# CoffeeScript Notes

This is my study book of [CoffeeScript Accelerated JavaScript Development](http://pragprog.com/book/tbcoffee/coffeescript).

### Embedding JS in CS
 - Just put your JS code surrounding it with backticks
    
        console.log `impatient ? useBackticks() : learnCoffeeScript()`

 - CS wraps code for namespacing, but you can remove it with -b ('bare') flag
 - we can execute a function using do

        do fn
        fn()

 - A function will be always defined with var, in CS we have no way to define functions with function keyword, the one exception is when we use the class keyword
 - Strict equality or Nothing, CS dont provide anyway to use the equality comparator of JS (==), is and == will always do strict equality
 
 Again;
  - Every function creates a scope, and the only way to create a scope is to define a function
  - A variable lives in the outermost scope in which an assignment has been made to that variable
  - Outside of its scope, a variable is invisible

 Variable's scope is defined explicitly in JS using the var keyword while CS infers scope from assignments.

<!--break-->
 
 - Shadowing variable name is a bad thing, dont do this

        x = 5
        triple = (x) -> x *= 3
        triple x                // => 15
        x                       // => 5

        hey = (x = x) -> console.log x
        hey()                   // => undefined
        x                       // => 5

 - context = this
 - scope = where the variable's are resolved
 - The context is determined purely by how a function is called; unlike scope, it has nothing to do with where the function is defined.
 
 - When the new keyword is put in front of a function call, its context is the new object.
 - When a function is called with call or apply, the context is the first argument given.
 - Otherwise, if a function is called as an object property (obj.func) or ob["func"], it runs in that object's context.

 - How => works

        callback = (message) => @voicemail.push message

        var callback;
        callback = (function(__this) {
            var __func = function (message) {
                return this.voicemail.push(message);
            };
            return function () {
                return __func.apply(__this, arguments);
            };
        })(this);

 - You can use arbitrary expressions as default arguments, the expression will be execute from whatever context the function is being called in.

---

    spoiler = (filter..., theEnding) -> console.log theEnding
    spoiler 'Darth Vader is Luke\'s father!'              // => 'Darth Vader is Luke's father!'

    birds = [ 'duck', 'duck', 'duck', 'coffee!' ]
    [ ducks..., coffee ] = birds
    ducks                                                 // => 'duck, duck, duck'
    coffee                                                // => 'coffee'


### Collections and Iteration
 - In JS every object is a hash, and almost everything is an Object. Except primitive values (booleans, numbers and strings) and special constants like undefined and NaN
 - When the CS compiler sees :, it know that you're building an object.

        drawSprite x, y, invert:true

        drawSprite(x, y, {
            invert: true
        });

 - Same-Name Key-Value Pairs { me }, works only with explicit curly braces
 - Soaks 'a?.b' 

        cats?['Garfield']?.eat() if lasagna?

        abc = [ 'a', 'b', 'c', 'd' ]
        abc[0..-1]                      # => [ 'a', 'b', 'c' ]
        abc[2..0]                       # => [ ]: always will be empty if the first number is greater than secound

 .. defines an inclusive range
 ... defines a exclusive range

        [1..5]                          # => [1, 2, 3, 4, 5]
        [1...5]                         # => [1, 2, 3, 4]



 - we can use splice with ranges to

        arr = ['a', 'c']
        ar[1...2] = [ 'b' ]             # => ['a', 'b']

 - Curiously, JS provides strings with a slice method, even though its behavior is identical to substring. This is handy, because it means you can use CoffeeScript’s slicing syntax to get substrings.

        'The year is 2013'[-4..]        # => 2013

 - hasOwnProperty, for own

        for own sword of Kahless


        for sword of Kahless
            continue unless Kahless.hasOwnProperty(sword)

 - with for.. of we can use when
 - with for.. in and array like we can use by

 - When you write for x of obj or for x in arr, you’re making assignments to a variable named x in the current scope. You can take advantage of this by using those variables after the loop. 
 - We can use do to capture the loop variable on each iteration
        
        for name, occupation of murderMysteryCharacters
            break if occupation is 'butler'

        console.log "#{name} did it!"

        for x in arr
            do (x) ->
                setTimeout (-> console.log x), 0

 
 - while, until and loop
 - loop is forever until break
 
#### Pattern Matching (or, Destructuring Assignment)
  - It's NOT an array or an object, its a Pattern


        [firstName, middleInitial, lastName] = ['Joe', 'T', 'Plumber']
        # firstName = 'Joe'; middleInitial = 'T'; lastName = 'Plumber'

        myRect =
            x: 100
            y: 200
        {x: myX, y: myY} = myRect

        {languages: [favoriteLanguage, otherLanguages...]} = resume
        # Take resume.languages, assign its first entry to a vari- able called favoriteLanguage, then assign the remaining entries to a new array called otherLanguages.


 - Better to use many small files, each with a WELL-DEFINED PURPOSE! than a few large files that make readers feel like rats in a maze.

 - always use the root object to set a global property

        class Tribble
            constructor: () ->
                @isAlive = true
                Tribble.count++
            
            breed: () ->
                return new Tribble if (@isAlive)
            
            die: () ->
                Tribble.count-- if (@isAlive)
                @isAlive = false

            @count: 0
            @makeTrouble: () ->
                console.log ('Trouble!' for i in [1..@count]).join(' ')


 - the object itself
 - the prototype object
 - and the instance

 - ' strict string
 - You can use """ to write multilines strings in a human-readable format.


### Docco
### Eco
### Zappa
### Zombie.js

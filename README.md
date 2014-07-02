JS-Unplugged
============
DOM-less, Library-less JavaScript

## Variables, Primitives, Loops, Conditionals & Comparisons

### block statements {} vs. expression statements ; ###
An expression statement is any valid unit of code that resolves to a value. It can be used anywhere a value is expected.

#### expression statements ####
```javascript
var name = 'Dustin';

fn();

1 < 2;

fn(1 < 2); // expressions can be function parameters
```

A block statement is used to group statements and to associate a block of statements with a control flow statement or a function statement. The block is delimited by a pair of curly brackets.

#### block statements ####
```javascript
{
    // list of zero or more statements
}

while (false) { // associate block with while loop
    // list of zero or more statements
}

function fn() { // associate block with function statement
    // list of zero or more statements
}
```

### "semicolons"; ###
Any expression statement, or any statement that resolves to a value, should end with a semicolon. This includes variable assignments and function calls. Block statements do not require semicolon termination.

```javascript
var name = "Dustin";

if (true) {
} // no semicolon

```

### {curly brackets} ###
With the exception of function statements, expression statements can appear anywhere a block statement is expected. If a block statement containing a single expression is to be associated with a control flow statement, the curly brackets are optional. To make your code more maintainable and more readable, it is suggested to use them anyway.
```javascript
// anti-pattern
if (true) return;

// suggested pattern
if (true) {
    return;
}
```

### variables ###
There are three different types of variable statements. Variable declaration, variable assignment, and variable reassignment. Any variable declared with the `var` keyword can be reassigned. Any variable that is declared without assignment is initialized to the global value `undefined`.

```javascript
// declaration
var name;

// assignment
var name = 'Justin';

// reassignment
name = 'Dustin';
```

Variables are used to hold references to values. To declare two or more variables in a single statement, we seperate the declarations with a comma:
```javascript
var name = 'Dustin',
    age = 24;
```

### primitives types ###
In JavaScript, we have two basic types: primitive types and object types. Primitives types include strings, numbers, booleans, null, and undefined. Everything else is of object type. The are three major differences between primitive types and object types.

1. Object types are equal by reference, primitive types are equal by value.
2. Object types are mutable, they can be altered. Primitive types are immutable, they cannot be altered.
3. You can assign properties to object types, primitive types cannot be assigned properties.

These points will be discussed further when we go over objects and arrays.

#### Strings ####
A string is a sequence of zero or more characters enclosed in either single or double quotation marks.

```javascript
"I'm a string";

'I too, am a string';
```

One of the most common things we do with strings is concatenation, the act of adding two strings together.

```javascript
var message = "Hello there ",
    name = "John Doe",
    greeting = message + name;
    
// > gretting = "Hello there John Doe"
```

A common confusion with string concatenation is what happens when you involve numbers in the equation. The rules are simple, JavaScript concatenation favors strings.

```javascript
10 + "20";
// > 1020

"20" + 10;
// > 2010
```

The `\` character has a special purpose in strings. Combined with the character that follows it, it represents a character that is otherwise not representable within the string. These are called escape sequences.

```javascript
"Hello, this breaks to a \n new line";
'What\'s your name?';
```

#### Numbers ####
JavaScript supports both integers and floating point numbers. We also have support for all of the common arithmetic operators.
```javascript
2 + 2;

2.5 - 5;

4 * 5;

10.8 / 50;

6 % 5;
```

The operator that might stand out to you is the modulus operator ( % ), also known as the remainder operator. When used this will return the remainer of the result of dividing the left operand with the right operand.

Often times we want to parse a number from a string. The most common way this is accomplished is with the `parseInt()` function.

```javascript
var s = "200px",
    n = parseInt(s, 10);

// > n = 200
```

The first parameter to `parseInt()` is the string to be parse, the second parameter is the radix.

The `Math` object contains a number of useful methods that come in handy when working with numbers.

```javascript
Math.abs(-10) // > 10
Math.floor(9.9) // > 9
Math.max(10, 2, 300, 35) // > 300
Math.random() // > returns a random number between 0 and 1.0
```

Another common problem is dealing with equations that may result in the global value `NaN`, which means the result could not be converted to a numeric value. We can check for this with `Number.isNaN`

```javascript
var n = Math.abs("nonum"); // > NaN
Math.isNaN(n); // > true
```

#### Booleans ####
There are two boolean values True and False. Some expressions resolve to what we call `falsy` or `truthy` values. undefined, null, 0, -0, NaN, "", and false are all `falsy` values, all other expressions are `truthy`. These values are typically used in control flow statements, such as `if` statements.

```javascript
var name;

if (true) {
    name = 'truthy';
}

if (-0) {
    name = 'falsy';
}

// > name = 'truthy'
```

#### null & undefined ####
`null` is a language keyword that usually indicates the absence of a value. `undefined` is a predefined global variable, not a language keyword, that is initialized to a variable that is declared but not assigned.. You should expect `undefined` to be a system level or unexpected error, and `null` to represent a program level, or expected absence of a value. If you need to assign one of these to a variable you should almost always use `null`.

### Loops ###
Loops are control flow statements that allow use to repeat a block of statements under a certain condition. The most basic loop is the `while` loop:

```javascript
var i = 0,
    s = "";
    
while (i < 10) {
   s += i;
   i += 1;
}
// s > "0123456789"
```

The structure for the `while` loop is:
```javascript
while (/* condition */) {
    // zero or more statements
}
```

The `while` loop will continue to run as long as the condition resolves to a `truthy` value. Now that we know 0 is a `falsy` value, we could have also written this loop like this:

```javascript
var i = 10,
    s = "";
    
while (i--) {
   s += i;
}
// s > "9876543210"
```

We also have the `for` loop and the `for in` loop. The `for` loop is typically used to iterate through Arrays and Numbers, while the `for in` loop is used to iterate through Objects. This is because `for` guarantees iteration order, wheras `for in` does not.

The structure for the `for` loop looks like this:
```javascript
for (/* initialize; condition; increment */) {
    // zero or more statements
}
```

When the loop first runs, it will execute any of the expressions in the initialize statement, check the condition for a `truthy` value, execute the block of statements, execute the increment statements, check the condition for a `truthy` value and so on until the condition is `falsy`, or a `break` statement is thrown. The `break` statement allows you to exit the loop early, without the conditions approval:

```javascript
while (true) {
    break;
}
```

We also have a `continue` statement, which allows you to skip certian iterations from being executed:

```javascript
var s = "",
    i;
    
for (i = 0; i < 10; i += 1 ) {
   if (i % 2 === 0) continue;
   s += i;   
}
// s > "13579"
```

The structure for a `for in` statement looks like this:

```javascript
for (/* property */ in /* object */) {
    // zero or more statements
}
```

On each iteration of the loop the variable on the left of the `in` keyword get assigned the next 'key' in the object, which will be a string value. So if we wanted to print the keys from an object we would write it like this:

```javascript
var obj = { x: 1, y: 2 },
    prop;
    
for (prop in obj) {
    console.log( prop );
}

// > "x"
// > "y"
```

#### faster loops ####

When using `for` loops to iterate through arrays, often times authors will check the length of the array on each iteration in their conditional statement.

```javascript
var a = [1,2,3,4,5],
    i;

for ( i = 0; i < a.length; i += 1 ) {
    // zero or more statements
}
```

Since we know the initialization statements only run once, and the conditional statement runs on each iteration, we should store the arrays length value in a variable and do our condition against that variable:

```javascript
var a = [1,2,3,4,5],
    i, l;

for ( i = 0, l = a.length; i < l; i += 1 ) {
    // zero or more statements
}
```

### Conditionals ###
The most basic conditional statements is the control flow statement `if`. 

```javascript
if (/* expression */) {
    // zero or more statements
}
```

The `if` statement takes a single expression. If that expression resolves to a `truthy` value the block of statements will be executed otherwise it will be skipped over. An `if` statement can be followed by an optional `else` statement, which will run if the expression in the `if` statements resolves to a `falsy` value.

```javascript
if (-0) {
    // zero or more statements
} else {
    // will run
}
```

A slighly more complex control flow statement is the `switch` statement. The `switch` statement takes an expression and tests that expression against each case value until a match is found, resulting in that case's list of statements to be executed. If no match is found the `default` case's list of statments is executed. If the matched case's list of statements does not contain a `break` keyword, you will fall through to the next case.

```javascript
switch (/* expression */) {
    case "value1":
        // zero or more statements
        break;
    case "value2":
        // zero or more statements
        break;
    default:
        // zero or more statements
}
```

The most interesting and convenient conditional is the ternary operator:

```javascript
/* expression */ ? /* truthy return */ : /* falsy return */;
```

This operator takes an expression to be evaluated before the `?`. If the expression resolves to `truthy` the value of the expression after the `?` and before the `:` is returned, other wise the value of the expression after the `:` and before the `;` is returned. We use this often for quick conditional checks.

```javascript
var name;

// long form
if (user.name) {
    name = user.name
} else {
    name = "";
}

// short hand
var name = user.name ? user.name : "";
```

#### && and || ####
We have two logical operators called 'logical and' and 'logical or'. You will see these operators most often is `if` statements.

```javascript
var name;

if (name && true) {
    console.log(name);
}
// > no log

if (name || true) {
    console.log(name);
}
// > undefined
```

In the case of `&&`, both expressions need to be true for the entire statement to resolve to a `truthy` value. `||`, on the other hand only needs one of the expressions to resolve to a `truthy` value. Another common use case for these operators is a programming technique called short-circuit evaluation. When assigning a value to a 'logical and' expression, the last `truthy` expression is returned. When assigning a value to a 'logical or' expression, the first true value is returned.

```javascript

options = options || default;

var fn = "someVar" && function() {};

```

### comparisions ###
We have a two equality operators, `==` and `===`. You can think of the first form as 'converted equality', and the second form as 'strict equality'. In the case of `==` the JavaScript interpreter will true to convert the values to the same type before performing the comparison. On the other hand, no such conversion is done for `===`. In almost every situation, you should probably use `===`.

```javascript
10 == "10"; // > true

10 === "10"; // > false

0 == false; // > true

0 === false; // > false
```

We also have the comparison operators `<`, `>`. In terms of numbers, these operators do what you would expect, return a `true` or `false` value.

```javascript
1 > 2; // > false

10 < 20; // > true
```

Strings, however, are a little weird.

```javascript
'a' > 'b'; // > false
'c' > 'b'; // > true
```

First the string is converted to it's character code, using `string.charCodeAt` function, and then the comparison is evaluated. In the case of `a > b`, the character code for 'a' is 97 and the character code for b is 98. `97 > 98` resolves to `false`.

## Object ( hash ) & Array
Hashes and Arrays are data structures that provide organization in a Javascript program. This structure can be as simple as storing the options to a module, or as complex as name-spacing for your application.

### Object ( hash )
You will usually see JavaScripts `{}` symbol called an object. I think this term is misleading since Arrays and Functions are also considered objects. I prefer the term hash, as this is how most other programing languages label them.

#### Creation
There are three main ways to create a new hash object.

##### Object literals
The most common way is to create what is called an object literal. An object literal is a comma separated list of property-value pairs enclosed in curly brackets. Properties and values are seperated by a colon. We'll get into properties in just a moment.

```javascript
var emptyObj = {},
    propvObj = { prop: 'value' };
```
Both examples create a new object in memory and set the cooresponding variable as a reference to the hash object it's equal to.

##### Constructor creation
Use of the constructor form is generally frowned upon. Mainly because it does the same thing as the object literal, but is much longer to type.

```javascript
// anti-pattern
var obj = new Object( {} );

console.log( obj ) // > Object {}
```
The purpose of the `new` operator is to construct and return 'new' objects. 

##### Object.create
In it's basic form, `Object.create` does the same thing as the object literal. It does, however, have the ability to allow for much more granular control. The signiture for `Object.create` is as follows:

```javascript
Object.create( prototype, [ propertyDescriptors ] );
```
A brief primer on what a prototype is can be found below. In our case, we want to create a hash object, so we use an object literal to specify the prototype. We are not going to cover property descriptors in this course.

```javascript
var obj = Object.create( {} );

console.log( obj ) // > Object {}
```

#### Prototypal Inheritance ( a brief primer )
All JavaScript objects, including Arrays and Functions, come with an inheritance chain. We call this the prototype chain. The start of this chain is always `Object.prototye`, which is just an object.

```javascript
var o = {};

console.dir(o);
/*
{
    __proto__: {
        __defineGetter__: function __defineGetter__() { [native code] }
        __defineSetter__: function __defineSetter__() { [native code] }
        __lookupGetter__: function __lookupGetter__() { [native code] }
        __lookupSetter__: function __lookupSetter__() { [native code] }
        constructor: function Object() { [native code] }
        hasOwnProperty: function hasOwnProperty() { [native code] }
        isPrototypeOf: function isPrototypeOf() { [native code] }
        propertyIsEnumerable: function propertyIsEnumerable() { [native code] }
        toLocaleString: function toLocaleString() { [native code] }
        toString: function toString() { [native code] }
        valueOf: function valueOf() { [native code] }
        get __proto__: function __proto__() { [native code] }
        set __proto__: function __proto__() { [native code] }
    }
}
*/
```

The prototype chain for this object is `{} < Object.prototype`. An array will inherit from `Array.prototype`, which inherits from `Object.prototype`.

```javascript
var a = [];

console.dir(a);
/*
{
    length: 0
    __proto__: {
        concat: function concat() { [native code] }
        constructor: function Array() { [native code] }
        every: function every() { [native code] }
        filter: function filter() { [native code] }
        forEach: function forEach() { [native code] }
        indexOf: function indexOf() { [native code] }
        join: function join() { [native code] }
        lastIndexOf: function lastIndexOf() { [native code] }
        length: 0
        map: function map() { [native code] }
        pop: function pop() { [native code] }
        push: function push() { [native code] }
        reduce: function reduce() { [native code] }
        reduceRight: function reduceRight() { [native code] }
        reverse: function reverse() { [native code] }
        shift: function shift() { [native code] }
        slice: function slice() { [native code] }
        some: function some() { [native code] }
        sort: function sort() { [native code] }
        splice: function splice() { [native code] }
        toLocaleString: function toLocaleString() { [native code] }
        toString: function toString() { [native code] }
        unshift: function unshift() { [native code] }
        __proto__: {
            __defineSetter__: function __defineSetter__() { [native code] }
            __lookupGetter__: function __lookupGetter__() { [native code] }
            __lookupSetter__: function __lookupSetter__() { [native code] }
            constructor: function Object() { [native code] }
            hasOwnProperty: function hasOwnProperty() { [native code] }
            isPrototypeOf: function isPrototypeOf() { [native code] }
            propertyIsEnumerable: function propertyIsEnumerable() { [native code] }
            toLocaleString: function toLocaleString() { [native code] }
            toString: function toString() { [native code] }
            valueOf: function valueOf() { [native code] }
            get __proto__: function __proto__() { [native code] }
            set __proto__: function __proto__() { [native code] }    
        }
    }
}
*/
```

The prototype chain for the array is `[] < Array.prototype < Object.prototype`. All of the properties an object inherits from its prototype will be available on that object. If an object assigns a value to a property of the same name as that of a property in it's prototype chain, the new property will override the property in the prototype chain.

#### Properties
All objects in JavaScript can have properties assigned to them. This includes Array and Function objects. However, we mostly assign properties to hash objects. 

##### Setting and Getting Properties
We have two ways to access and objects properties, dot notation `.` and subscript notation `[]`.

```javascript
var o = {};

o.x     = 1;
o['y']  = 2;

o['x']; // > 1
o.y;    // > 2

console.log(o); // > Object { x: 1, y: 2 }
```

Although using `[]` is clearly the longer form, there are benefits to using this syntax. Since the value `[]` expects is just a string, it can be evaluated dynamically.

```javascript
var s = 'prop',
    o = { prop: 'value' };
    
console.log( o[s] ); // > 'value'
```

We can assign any valid string value as a property of an object.

```javascript
var str = 'I am a valid property',
    obj = {};
    
obj[str] = true;

console.dir( obj );
/*
Object { I am a valid property: true }
*/
```

As a general rule, try to only use `[]` notation when the value needs to be evaluated at runtime.

##### Deleting Properties
Deleting properties from an object is pretty strait forward. We use the `delete` operator.

```javascript
var o = { x: 1, y: 2 };

delete o.x; // true

o; // > { y: 2 }

delete o['y']; // true

o; // > {}

delete o.x // false
```

##### Non-existing Properties

Accessing a non-existing property does not throw an error. It simply returns undefined. This can result in hard to find bugs.

```javascript
var o = {},
    p = o.x;
    
console.log( p ); // > undefined
```

Calling a non-existing properties as a function does throw an error. Since accessing the non-existent property returns undefined you will get the following error: `TypeError: undefined is not a function`.

##### Functions as Properties
Speaking of functions, they too can be properties. When we use functions as properties we call them methods. 

```javascript
var module = {
    method: function () {
        console.log('Hello!');
    }
};

module.method(); // > Hello!
```

Encapsulating functionality in objects is a very common pattern in JavaScript. Lets look at an example:

```javascript
var basket = {

    items: [],
    
    addItem: function(item) {
        basket.items.push(item);
    },
    
    getTotal: function() {
        var tot = 0;
        
        basket.items.forEach(function(item) {
            tot += item.price;
        });
        
        return '$' + tot;
    }

};

basket.addItem({
    name: 'dress',
    price: 50
});

basket.addItem({
    name: 'jeans',
    price: 30 
});

basket.getTotal();
```

#### Equality
Objects in JavaScript are considered equal by reference, not by value. This is to say that two object containing the same content are not equal, unless they are the same object in memory.

```javascript
var obj1 = { x: 1 },
    obj2 = { x: 1 };
    
obj1 === obj2; // > false
```

We can make `obj1` equal to `obj2` only if we assign `obj2` to the same object `obj1` references.

```javascript
var obj1 = { x: 1 },
    obj2 = obj1;
    
obj1 === obj2 // > true
```

There are interesting ramification of this behavior. For instance, since `obj2` references the same object in memory, if we alter `obj2`, `obj1` will receive the same alterations.

```javascript
var obj1 = { x: 1 },
    obj2 = obj1;
    
obj1.x; // > 1
obj2.x; // > 1

obj2.x = 2;

obj1.x // > 2
```

#### Object iteration
As mentioned in "Variables, Primitives, Loops, Conditionals & Comparisons", we have the `for in` loop. This loop allows us to iterate through all of the keys in an object. The next example prints all of the keys in the hash.

```javascript
var o = {
        x: 1,
        y: 2,
        z: 3
    },
    prop;

for ( prop in o ) {
    console.log( prop );
}
/*
x
y
z
*/
```

Being able to iterate over hash objects like this allows us to perform convienient operations. One example would be extending a hash object with another hash object.

```javascript
var defaults = {
        width: '300px',
        speed: 400
    },
    settings = {
        speed: 200
    },
    prop;
    
for ( prop in settings ) {
    defaults[prop] = settings[prop]
}

console.log( defaults )
// Object { width: '300px', speed: 200 }
```
This is such a common pattern that it is usually wrapped up in a reusable function. Functions will be covered in the next session.

```javascript
var extend = function ( base, exts ) {
        var prop;
        
        for ( prop in exts ) {
            base[prop] = exts[prop];
        }
    },
    
    defaults = {
        width: '300px',
        speed: 400
    },
    
    settings = {
        speed: 200
    };
    
extend( defaults, settings );
    
console.log( defaults );
// > Object { width: '300px', speed: 200 }
```

Using the example from above, where we printed all of the keys in the hash, we can convert that into a reuable function as well.

```javascript
var each = function ( obj, fn ) {
        var prop, key, val;
        
        for ( prop in obj ) {
            key = prop;
            val = obj[prop];
            
            fn( val, key );
        }
    },
    
    o = {
        x: 1,
        y: 2,
        z: 3
    },
    
    logKey = function ( v, k ) { 
        console.log(k); 
    };
    
each( o, logKey );
/*
x
y
z
*/
```

There is one issue with `for in`. The loop will iterate though all of the user generated properties added to it's prototype.

```javascript
var o = { x: 1 },
    
    prop;

Object.prototype.y = 2;

for ( prop in o ) {
    console.log(prop);
}
/*
x
y
*/
```

Thankfully the fix is a simple one. We can use the `Object.hasOwnProperty` method to ensure the property we are iterating over is not an inherited one.

```javascript
var o = { x: 1 },
    
    prop;

Object.prototype.y = 2;

for ( prop in o ) {
    if ( o.hasOwnProperty( prop ) ) {
        console.log(prop);
    }
}
// > x
```

#### Object design patters
There are far to many object based design pattern to cover here. Let's go over a few of the most common ones.

##### Default and Sameness structures
As shown above, hash objects are often used to store the default settings for a module.

```javascript
var typecount = {
        defaults: {
            charCount: 75,
            warnCount: 10
        },
        
        create: function(options) {
            var settings = extend(defaults, options); // extend() from ealier example
        }
    };
    
typecount.create({
    charCount: 50 // override the defaults
});
```

Another similar technique is to use objects to organize things of a similar type. For example, credit card number identifiers. 

```javascript
var CARD_IDENTIFIERS = {
        3: 'amex',
        4: 'visa',
        5: 'mstr',
        6: 'disc'
    },
    
    getType = function ( num ) {
        firstChar = String(num)[0];
        
        return CARD_IDENTIFIERS[firstChar];
    };

getType( 4444678337449988 ); // > visa
getType( 3744678337449988 ); // > amex
```

##### APIs
Hash objects are often used to expose a public API from a module. This provides a level of encapsulation that make programs easier to reason about. We want the API to be easy to work with, so we give the user a common enitity to call methods on.

```javascript
var privModule = {
            
        privMethOne: function() {},
        
        privMethTwo: function() {}
        
    },
    
    module = {
        pubMeth: function () {
            privModule.privMethOne();
            privModule.privMethTwo();
        }
    };
```

##### Namespaces
One of the most common ways to organize a JavaScript application is to use a Hash object as a namespace.

```javascript
var app = {

    utils: {
        core: {}
    },
    
    client: {
        dom: {}
    },
    
    server: {
        urls: {}
    }

};
```

### Array
Arrays are another fundamental data type. We are mostly interested in using arrays as iterate-able lists, and less so about accessing them, as we do with hash object.

#### Arrays are objects
Although it's not common to add properties to arrays, it is possible, considering arrays have all of the same abilities as object.

```javascript
var a = [1, 2, 3, 4];

a.listType = 'numbers';

a.listType; // > numbers
```

#### Creation
##### Array literals
We've seen a handful of examples of array creation using the array literal syntax.

```javascript
var a = [];
```
Like the hash object, this creates a new array object in memory and assigns the a variable as a reference to that object.

##### Constructor creation
We also have an array constructor for creating new arrays. As with hash object, this is not the recommended way to create new arrays.

```javascript
var a = new Array(1, 2, 3, 4);

a; // > [1, 2, 3, 4]
```

There is a slight issue with the array constructor. If we supply a single nonnegative integer value as a parameter we will get what is called a sparse array, which is just another word for an array with holes in it.

```javascript
var a = new Array(10);

a; // [undefined X 10]
```
There are edge cases where this can be beneficial. In most cases, it's probably not what you meant.

#### Array Elements
Arrays have key-value pairs, just like hash objects. However, with arrays the keys are always nonnegative integers. Since accessing objects via integers is not generally useful, outside of loops, we're mostly interested in an arrays values, and we call these elements.

```javascript
// e = element

var a = [ 1, 2, 3, 4 ];
       // e  e  e  e
```

The elements in a given array can be mixed with any valid JavaScript type. The ability to mix types is very useful.

```javascript
var mixed = [
	{ x: 1 },
	[ 1, 2, 3 ],
	/\w+/g,
	function() { console.log('hello'); },
	10,
	'hello',
	false,
	null,
	undefined
];
```

Technically all arrays, unless there elements are all numbers. are mixed, since the length property is equal to an integer.

#### Setting, Getting, and Deleting
We can access an arrays properties with both the dot notation `.` or the subscript notation `[]`. However, since array keys are generally integers, we mostly use subscript notation to access them. When setting, resetting, getting, or deleting elements from an array we use the subscript notation.

```javascript
var a = [ 1, 2, 3, 4 ];

console.dir( a );
/*
Array[4]
0: 1
1: 2
2: 3
3: 4
length: 4
*/

// get a value from the array
a[ 0 ]; // > 1

// set a value to an existing slot
a[ 1 ] = 'new value';

console.dir( a );
/*
Array[4]
0: 1
1: 'new value'
2: 3
3: 4
length: 4
*/
```

#### Array Indexing and the Length Property
One thing you may have noticed is the first key in the array is 0. Array indexing begins at 0, not 1. Another thing worth noting is the length property that magically appears as a key on the array. The setting and updating of the length value is always taken care of for you. This feature is what sets arrays apart from other objects. It's existence is what makes it possible to loop through arrays successively.

#### Deleting elements from an array
As with hash objects, we can delete elements from an array using the `delete` operator.

```javascript
var a = [ 1, 2, 3, 4 ];

delete a[1]; // > true

a; // > [1, undefined × 1, 3, 4]
```

Well that looks odd. If the delete expression was successful the expression will return true, but what's going on with the array now? The issue is that delete operator doesn't do any work to shift the arrays keys around or update the length property. It simply removes that key-value pair from the array.

```javascript
console.dir( a );
/*
Array[4]
0: 1
2: 3
3: 4
length: 4
*/
```

As noted before, when we created a new array with the `new Array` constructor, this results in a sparse array. It's unlikely this is the result you were hoping for. Thankfully arrays have a method for deleting elements that does work they way we want. This method is described below.

#### Array methods
All of the methods covered below come from `Array.prototype`.

##### Mutator methods
Mutator methods are methods that alter the array object in memory.

####### [].splice
As promised `[].splice` is the method we use to delete elements from an array. The first argument this method expects is the index we'd like to begin deleting from. The second argument is the amount of elements to be deleted. The return value is an array containing the elements that were deleted.

```javascript
var a = [ 1, 2, 3, 4 ];

a.splice( 1, 1 ); // > [2]

a; // > [1, 3, 4]
```

We have a number of useful mutator methods. All mutator methods automatically update the arrays length for you. Here are some of the common ones.

####### [].push
Adds one or more elements to the end of an array and returns the new length of the array.

```javascript
var a = [ 1, 2, 3, 4 ];

a.push(5); // > 5

a; // > [ 1, 2, 3, 4, 5 ]

a.push(6, 7); // 7

a; // > [ 1, 2, 3, 4, 5, 6, 7 ]
```

####### [].pop
Removes the last element from an array and returns that element.

```javascript
var a = [ 1, 2, 3, 4 ];

a.pop(); // > 4

a; // > [ 1, 2, 3 ]
```

####### [].shift
Removes the first element from an array and returns that element.

```javascript
var a = [ 1, 2, 3, 4 ];

a.shift(); // > 1

a; // > [ 2, 3, 4 ]
```

####### [].unshift
Adds one or more elements to the front of an array and returns the new length of the array.

```javascript
var a = [ 1, 2, 3, 4 ];

a.unshift(0); // > 5

a; // > [ 0, 1, 2, 3, 4 ]

a.unshift(-1, -2); // 7

a; // > [ -2, -1, 0, 1, 2, 3, 4 ]
```

##### Accessors Methods
These methods do not modify the array and return some representation of the array.

####### [].concat
Returns a new array comprised of this array joined with other array(s) and/or value(s).

```javascript
var a = [1, 2],
    b = [3, 4],
    
    c = a.concat(b);

a; // > [1, 2]

c; // > [1, 2, 3, 4]
```

####### [].join
Joins all elements of an array into a string, with a specified delimiter.

```javascript
var a = [ 1, 2, 3, 4 ],

    commaSep = a.join(','),
    
    spaceSep = a.join(' ');
    
commaSep; // > "1,2,3,4"
spaceSep; // > "1 2 3 4"
```

####### [].slice
Extracts a section of an array and returns a new array. The first parameter to `slice` is the starting index to begin slicing, the second parameter to `slice` the index to slice upto but not including.

```javascript
var a = [1, 2, 3, 4],

    fir = a.slice(0, 1), // first element
    
    sec = a.slice(1, 2); // second element
    
fir; // > [1]
sec; // > [2]

a; // > [1, 2, 3, 4]
```

####### [].indexOf
Returns the first index of an element within the array equal to the specified value, or -1 if none is found.

```javascript
var a = ['cat', 'dog', 'cow'];

a.indexOf('cow'); // > 2

a.indexOf('worm'); // -1
```

##### Iterators Methods
Itereator methods make dealing with arrays a real joy. Most iterators expect a function as their first argument. We'll keep the functions simple, since we haven't covered functions yet. For an exception of the `reduce` iterator, the function that the iterator expects is supplied with three arguments. The first argument is equal to the current value being iterated over, the second argument is equal to the current key being iterated over, and the third argument is the object the method is being called on.

```javascript
// iterator signiture
array.[iterator method](function([current value], [current key], [array]) {

});
```

####### [].forEach
Amoung the iterator methods, `forEach` is easily the most common. It simply calls a function for each element in the array.

```javascript
var ifn = function(val, key, arr) {
	    console.log(val, 'is at index:', key, 'in', arr);
    },
    arr = ['cat', 'dog', 'cow'];
    
arr.forEach(ifn);
/*
cat is at index: 0 in ["cat", "dog", "cow"]
dog is at index: 1 in ["cat", "dog", "cow"]
cow is at index: 2 in ["cat", "dog", "cow"] 
*/
```

As an important lesson, and as a basis for how the other iterators are implemented, I think it helps to see how you might implement the `forEach` method.

```javascript
// place this on the prototype so all arrays inherit it
// the 'this' value in the function is a reference to the 
// array instance the method is being called on.
Array.prototype.forEach = function ( func ) {
    var len = this.length,
        ind = 0,
        key, val;
        
    for (ind; ind < len; ind += 1) {
        key = ind;
        val = this[key];
        
        func( val, key, this );
    }
};
```

####### [].map
Creates a new array with the results of calling a provided function on every element in this array.

```javascript
var ifn = function(val, key, arr) {
	    return 'The ' + val;
    },
    arr = ['cat', 'dog', 'cow'],
    
    mappedArr = arr.map(ifn);
    
mappedArr; // > ["The cat", "The dog", "The cow"]
```

####### [].some & [].every
These methods are very similar. `some` returns true if at least one element in this array satisfies the provided testing function. `every` returns true if every element in this array satisfies the provided testing function.

```javascript
var ifn = function(val, key, arr) {
	    return typeof val === 'string';
    },
    arr = ['cat', 'dog', 'cow', 5];
    
arr.every(ifn); // false
arr.some(ifn); // true
```

####### [].filter
Creates a new array with all of the elements of this array for which the provided filtering function returns true.

```javascript
var ifn = function(val, key, arr) {
	    return typeof val === 'string';
    },
    arr = ['cat', 'dog', 'cow', 5],
    
    filteredArr = arr.filter(ifn);
    
filteredArr; // > ['cat', 'dog', 'cow']
```

####### [].reduce
Apply a function against an accumulator and each value of the array (from left-to-right) as to reduce it to a single value. As mentioned above, this is the only iterator listed that doesn't supply the same parameters to the function it's given. The signiture for reduce is as follows:

```javascript
[].reduce(function([current total], [current value], [array]) {

});
```

Unless it's specified with the second parameter to reduce, the current total begins at 0. If we want to get the sum from an array of number we might write something like this:

```javascript
var add = function(a, b) { return a + b },

    arr = [1, 2, 3, 4],
    
    sum = arr.reduce(add);
    
sum; // > 10
```

Another example might be to merge a bunch of array objects together.

```javascript
var a = [1, 2],
    b = [3, 4],
    c = [5, 6],
    d = [a, b, c],
    
    concat = function (a, b) { return a.concat(b); };
    
    merged = d.reduce(concat);
    
merged; // > [1, 2, 3, 4, 5, 6]
```

#### Array-like Object
For something to be considered 'array-like' it must meet a few requirements. One, it must have a length property, and two, it's keys must be nonnegative values beginning at 0. As long as an object meets these requirements all of the methods listed above will work on them. Two common examples of array-like objects: 
* the `arguments` object, which will be covered in the functions session. 
* an HTMLCollection object (which is what you get when you query for elements in the DOM)

Although the methods above will work on these array-like object, they don't inherit from `Array.prototype` so those methods don't exist on them. Thankfully there is a common pattern to turn array-like object into true array object. As mentioned above the `slice` method returns a new array. We can use the `slice` method that exists on `Array.prototype` to turn the array-like object into a true array:

```javascript
var al = { 0: 'a', 1: 'b', 2: 'c', length: 3 },

    ta = Array.prototype.slice.call(al);
    
ta; // > ['a', 'b', 'c']
```


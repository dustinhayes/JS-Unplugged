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

A slighly more complex control flow statement is the `switch` statement. The `switch` statement takes an expression and tests that expression against each case value until a match is found, resulting in that case's list of statements to be executed. If no match is found the default case's list of statments is executed. If the matched case's list of statements does not contain a `break` keyword, you will fall through to the next case.

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
10 == "10" // > true

10 === "10" // > false

0 == false // > true

0 === false // > false
```

We also have the comparison operators `<`, `>`. In terms of numbers, these operators do what you would expect, return a `true` or `false` value.

```javascript
1 > 2 // > false

10 < 20 // > true
```

Strings, however, are a little weird.

```javascript
'a' > 'b' // > false
```

TODO: I think this is do to the ASCII number associated to the given character.

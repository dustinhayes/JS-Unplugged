JS-Unplugged
============
DOM-less, Library-less JavaScript

## Variables, Primitives, Loops, Conditionals & Comparisons

### block statements {} vs. expression statements ; ###
An expression statement is any valid unit of code that resolves to a value. It can be used anywhere a value is expected.
A block statement is used to group statements. The block is delimited by a pair of curly brackets. Block statements are generally used with control flow statements, but they are also used to enclose function bodies.

#### expression statements ####
```javascript
var name = 'Dustin';

fn();

1 < 2;
```

#### block statements ####
```javascript
{
    // list of zero or more statements
}

while (false) {
    // list of zero or more statements
}

function fn() {
    // list of zero or more statements
}
```

### "semicolons"; ###
Any expression statement, or any statement that resolves to a value, should end with a semicolon. This includes variable assignments and function calls.

### {curl brackets} ###
Curly brackets are optional if only one statement is needed. To make code more maintainable and more readable, use them anyyway.
```javascript
// anti-pattern
if (true) return;

// suggested pattern
if (true) {
    return;
}
```

### variables ###
There are three differennt types of variable statements. Variable declaration, variable assignment, and variable reassignment. Any variable declared with the `var` keyword can be reassigned.

```javascript
// declaration
var name;

// assignment
var name = 'Justin';

// reassignment
name = 'Dustin';
```

Variables are used to hold references to values. To declare two or more variables in a single statement, we seperate the assignments with a comma:
```javascript
var name = 'Dustin',
    age = 24;
```

### primitives types ###
In JavaScript, we have two basic types: primitive types and object types. Primitives types include String, Number, Boolean, null, and undefined. Everything else is of object type. The are three major differences between primitive types and object types.

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

One of the most common thing we do with strings in concatenation, the act of adding two strings together.

```javascript
var message = "Hello there ",
    name = "John Doe",
    greeting = message + name;
    
// > gretting = "Hello there John Doe"
```

A common confustion with string contatenation is what happens when you involve numbers in the equation. The rules are simple, JavaScript concatenation favors strings.
```javascript
10 + "20";
// > 1020

"20" + 10;
// > 2010
```

#### Numbers ####
JavaScript supports both integers and floating point numbers. We also have support for all of the common arithmetic operators.
```javascript
2 + 2;

2 - 5;

4 * 5;

10 / 50;

6 % 5;
```

The operator that might stand out to you is the modulus operator ( % ), also known as the remainder operator. When used this will return the remainer of the result of dividing the left operand with the right operand.

Often times we want to parse a number from a string. The most common way this is accomplished is with the `parseInt()` function.

```javascript
var s = "200px",
    n = parseInt(s, 10);

// > n = 10
```

The first parameter to `parseInt()` is the string to be parse, the second parameter is the radix.

#### Booleans ####
There are two boolean values True and False. Some expressions resolve to what we call `falsy` or `truthy` values. undefined, null, 0, -0, NaN, "", and false are all `falsy` values, all other expressions are `truthy`.

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
`null` is a language keyword that usually indicates the absence of a value and `undefined` is a predefined global variable, not a language keyword, that is initialized to a variable with an undefined value. You should expect `undefined` to be a system level or unexpected error, and `null` to represent a program level, or expected absence of a value. If you need to assign one of these to a variable you should almost always use `null`.

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

The `while` loop will continue to run as long as the condition resolves to a `truthy` value. Know that 0 is a `falsy` value, we could have also written this loop like this:

```javascript
var i = 10,
    s = "";
    
while (i--) {
   s += i;
}
// s > "9876543210"
```

We also have the `for` loop and the `for in` loop. The `for` loop is typically used to iterate through Arrays and Numbers, while the `for in` loop is used to iterate through Objects. This is because `for` gaurantees order, wheras `for in` does not.

The structure for the `for` loop looks like this:
```javascript
for (/* initialize; condition; increment */) {
    // zero or more statements
}
```

When the loop first runs, it will execute any of the expressions in the initialize statement, check the condition for a `truthy` value, execute the block of statements, execute the increment statements, check the condition for a `truthy` value and so on until the condition is `falsy`, or a `break` statement is thrown. The break statement allows you to exit the loop early, without the conditions approval:

```javascript
while (true) {
    break;
}
```

We also have a `continue` statement, which allows you to skip certian iterations from being executed:

```javascript
for (/* property */ in /* object */) {
    // zero or more statements
}
```

Each iteration of the loop the variable on the left of the `in` keyword get assigned the next 'key' in the object, which will a string value. So if we wanted to print the keys from an object we would write it like this:

```javascript
var obj = { x: 1, y: 2 },
    prop;
    
for (prop in obj) {
    console.log( prop );
}

// > "x"
// > "y"
```

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
    i, l

for ( i = 0, l = a.length; i < l; i += 1 ) {
    // zero or more statements
}
```

### Conditionals ###
The most basic conditional statements is the control flow `if` statement. 

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

A slighly more complex control flow statement is the `switch` statement. The `switch` statement takes an expression and tests that expression against each case value until a match is found, resulting in that case's list of statements to be executed. If no match is found the default case's list of statments is executed.

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

The most interesting and convenient conditional is the ternary operator.

```javascript
/* expression */ ? /* truthy return */ : /* falsy return */;
```

This operator takes an expression to be evaluated before the `?`. If the expression resolves to `truthy` the value of the expression after the `?` and before the `:` is returned, other wise the value of the expression after the `:` and before the `;` is returned. We use this often for conditional checks.

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

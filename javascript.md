### Javascript inline

```html
<body onload="alert('Hello World!)">
</body>
```

--------------------------------------------------------------------------------
### Input

```js
var name = prompt('Please tell me your name: ');
```

--------------------------------------------------------------------------------
### Converting between types

```js
var a = "42";
var b = Number( a );

console.log( a );   // "42" (string)
console.log( b );   // 42   (number)
```

--------------------------------------------------------------------------------
### Comments rules

1. Code without comments is suboptimal.
2. Too many comments (one per line, for example) is probably a sign of poorly written code.
3. Comments should explain why, not what. They can optionally explain how if that's particularly confusing.

Curiosity
```js
var a = /* arbitrary value */ 42;
console.log( a );   // 42
```

--------------------------------------------------------------------------------
### Variables

```js
var amount = 99.99;
amount = $ + String(amount);  // convert `amount` to a string, and add "$" on the beginning
console.log(amount);          // "$199.98"
```

#### Coercion
Coercion comes in two forms in JavaScript: explicit and implicit.  

Explicit coersion example:

```js
var a = "42";
var b = Number( a );

a;  // "42" (string)
b;  // 42   (number)
```

Implicit coersion example:

```js
var a = "42";
var b = a * 1;  // "42" implicitly coerced to 42 here

a;  // "42" (string)
b;  // 42   (number)
```

--------------------------------------------------------------------------------
### Equality

```js
var a = "42";
var b = 42;

a == b;         // true
a === b;        // false
```

Rules
- If either value (aka side) in a comparison could be the `true` or `false` value, avoid `==` and use `===`.
- If either value in a comparison could be of these specific values ``(0, "", or [] -- empty array)``, avoid `==` and use `===`.
- In all other cases, you're safe to use `==`. Not only is it safe, but in many cases it simplifies your code in a way that improves readability.

Comparison of two arrays

```js
var a = [1,2,3];  // object
var b = [1,2,3];  // object
var c = "1,2,3";  // string

a == c;     // true
b == c;     // true
a == b;     // _false_

// but
a.toString() == b.toString(); // true => "1,2,3" = "1,2,3"
```

Return `true` if `x` and `y` refer to the same object. Otherwise, return `false`. [ECMA-262](http://www.ecma-international.org/ecma-262/5.1/index.html#sec-11.9.3)

#### Scope

ES6 lets to declare variables to belong to individual blocks (pairs of `{ .. }`), using the `let` keyword.

```js
function foo() {
    var a = 1;

    if (a >= 1) {
        let b = 2;

        while (b < 5) {
            let c = b * 2;
            b++;

            console.log( a + c );
        }
    }
}

foo();
// 5 7 9
```

Because of using `let` instead of `var`, `b` will belong only to the `if` statement and thus not to the whole `foo()` function's scope.
Similarly, `c` belongs only to the `while` loop.

--------------------------------------------------------------------------------
### Constants

```js
// as of ES6
const TAX_RATE = 0.08;

// previous version of JS
var TAX_RATE = 0.08;
```

--------------------------------------------------------------------------------
### Loops

```js
/* do ... while */
do {
  // do something
} while(condition)


/* while */
while(condition) {
  // do something
}


/* for */
for (var i = 0; i <= 9; i = i + 1) {
    console.log( i );
}
// 0 1 2 3 4 5 6 7 8 9
```

The `for` loop has three clauses:
1. initialization `var i = 0`
2. conditional  `i <= 9`
3. update `i = i + 1`

--------------------------------------------------------------------------------
### Functions

```js
var myNum = 10;
function doSomething (a) {
  a = a - 2;
  console.log(a); // 18
}
doSomething(myNum*2);
```

Functions are  subtypes of objects.

```js
function foo() {
    return 42;
}

foo.bar = "hello world";

typeof foo;         // "function"
typeof foo();       // "number"
typeof foo.bar;     // "string"
```

#### Functions as values

```js
function foo() {
    // ..
}
```

Though it may not seem obvious from that syntax, foo is basically just a variable
in the outer enclosing scope that's given a reference to the function being declared.

```js
var foo = function() {
    // ..
};

var x = function bar(){
    // ..
};
```

The first function expression assigned to the `foo` variable is called anonymous
because it has no `name`.  
The second function expression is named (`bar`)

#### Immediately Invoked Function Expressions (IIFEs)

```js
(function IIFE(){
    console.log( "Hello!" );
})();
// "Hello!"

/*
 * IIFE functions can also have return values
 */

var a = 42;
var x = (function myFunction(){
  var a = 10;
  console.log("Show a value immediately: " + a );
  return a; // 10
})();

console.log( a ); // 42
console.log("Call myFunction again: " + x);
```

#### Closure

```js
function makeAdder(x) {
  function add(y) {
    return y + x;
  }

  return add; // reference to add(y), the same as return function add(y)...
}

/*
  makeAdder(x = 10) => return add(y = 3) => return y + x = 3 + 10 = 13;
*/

var plusOne = makeAdder(1);  // x=1,  plusOne = add(y);
var plusTen = makeAdder(10); // x=10, plusTen = add(y);

plusOne(3);                  // y=3  => return y + x = 3 + 1 = 4
plusOne(41);                 // y=41 => return 41 + 1 = 42
plusTen(13);                 // y=23 => return 13 + 10 = 23
```

#### Modules

The most common usage of closure in JavaScript is the module pattern.
Modules let to define private implementation details (variables, functions)
that are hidden from the outside world, as well as a public API that is
accessible from the outside.

```js
function User() {
  var username, password;

  function doLogin(user, pw) {
    username = user;
    password = pw;
  }

  var publicAPI = {
    login: doLogin  // reference to function doLogin(user, pw)
    // the same as
    // login: function doLogin(user, pw) {...}
  };

  return publicAPI;
}

// create a 'User' module instance
var fred = User();  // just function which returns the publicAPI object
fred.login("fred", "12Battery34!");
```

Executing `User()` creates an instance of the `User` module. It's just a function,
that returns `publicAPI` object.

#### `this` identifier

```js
function foo() {
  console.log(this.bar);
}

var bar = 'global';

var obj1 = {
  bar: 'obj1',
  foo: foo
};

var obj2 = {
  bar: 'obj2'
};

// -----
foo();          // 'global'
obj1.foo();     // 'obj1'
foo.call(obj2); // 'obj2'
new foo();      // undefined
```

--------------------------------------------------------------------------------

### Values & types

Built-in types:
1. string
2. number
3. boolean
4. null
5. undefined
6. object
7. symbol (new to ES6)

--------------------------------------------------------------------------------
### Conditionals

#### if, else if, else

```js
if (a == 2) {
    // do something
}
else if (a == 10) {
    // do another thing
}
else if (a == 42) {
    // do yet another thing
}
else {
    // fallback to here
}
```

#### Switch

```js
switch (a) {
    case 1:
    case 2:
        // some cool stuff
        break;
    case 10:
        // do another thing
        break;
    case 42:
        // do yet another thing
        break;
    default:
        // fallback to here
}
```

The `break` is important to avoid run another case;  
If `break` will be ommited from a `case`, and that `case` matches or runs, execution will continue with the next `case`'s statements.
In the example above, if `a` is either `1` or `2`, it will execute the "some cool stuff" code statements.

#### Conditional operator / ternary operator

```js
var a = 42;
var b = (a > 41) ? "hello" : "world"; // expression ? if true : if false
```

If the expression is `true`, the result is "hello", if `false` the result is "world".

--------------------------------------------------------------------------------
### Strict mode

```js
function foo() {
    "use strict";

    // this code is strict mode

    function bar() {
        // this code is strict mode
    }
}

// this code is not strict mode
```

One key difference (improvement!) with strict mode is disallowing the implicit auto-global variable declaration from omitting the `var`:
```js
function foo() {
    "use strict";   // turn on strict mode
    a = 1;          // `var` missing, ReferenceError
}

foo();
```

To avoid problems caused strict mode errors for all script file, it's better to
use this mode locally, not globally.

--------------------------------------------------------------------------------
### Objects

Ways to create objects:

```js
// new object with keys and values
var myObj = {
    type: 'fancy',
    disposition: 'sunny'
};

// empty object
var emptyObj = {};

// using constructor
var myObj = new Object();   // new Object();  is most basic constructor
```

Get access to property/key - bracket notation

```js
var obj = {
  a: "Hello World",
  b: 42
};

var b = "a";

console.log( obj[b] );   // "Hello World"   (because b="a" => obj["a"])
console.log( obj["b"] ); // 42
```


It's possible to add keys when object is just created.
There are two ways to do that:

```js
myObj["name"] = "Charlie";
myObj.name = "Charlie";

// advanced of brackets
var someObj = {propName: someValue};
var myProperty = "propName";
someObj[myProperty];
```

Methods

```js
var setAge = function (newAge) {
  this.age = newAge;
};

var adam = new Object();
adam.name = "Adam";
adam.setAge = setAge; // reference to the setAge function
adam.setAge(25);      // using method

// other way to define methods
adam.setAge = function(newAge) {
  this.setAge = newAge;
};
adam.setAge(26);
```

Create a custom constructor

```js
// constructor
// should always be written with a capital letter
function Person(name,age) {
  this.name = name;         // note the   this.name
  this.age = age;           // and        this.age
  this.theSameForAll = "Hello World";   // default value for all Person objects
  this.birthDate = function() {
    var year = new Date().getFullYear();  // get current year
    return year - age;
  };
}

// using constructor
// create a new person
var susan = new Person("Susan", 25);
susan.birthDate();  // call method
```

Two ways of creating objects:
- Literal notation: `{property: value}`
- Constructor notation: `function NewObject () {}`  
  create new object `new NewObject()`

Associative array  
`firstName` - property  
`"bob"` - value  

```js
var bob = {
    firstName: "Bob",
    lastName: "Jones",
    phoneNumber: "(650) 777-777",
    email: "bob.jones@example.com"
};
```

`myObj.hasOwnProperty('name')` - checking if object has a certain property.   
`true` if has,  
`false` if doesn't have  

Printing out all elements  
`for / in` loop  

```js
var dog = {
species: "bulldog",
age: 3,
color: brown
};

// display properties (keys)
for(var key in dog) {
  console.log(key);  // species, age, color
}

// display values
for(var key in dog){
    console.log(dog[key]);  // buldog, 3, brown
}
```

--------------------------------------------------------------------------------
### Arrays
The type of array is `object`.  

```js
var arr = ["hello world", 42, true];

arr[0];         // "hello world"
arr[1];         // 42
arr[2];         // true
arr.length;     // 3

typeof arr;     // "object"
```

--------------------------------------------------------------------------------
### Introduction to classes

When you make a constructor, you are in fact defining a **new class**. A class can be thought of as a type, or a category of objects—kind of like how Number and String are types in JavaScript.

You can think of an object as a particular instance of a class.

**Prototype** helps extend object to a new methods or properties.
```js
function Dog (breed) {
  this.breed = breed;
};

// here we make buddy and teach him how to bark
var buddy = new Dog("golden Retriever");

// prototype <<  <<  <<  <<  <<  <<  <<  
Dog.prototype.bark = function() {
  console.log("Woof");
};
buddy.bark();

// here we make snoopy
var snoopy = new Dog("Beagle");
/// this time it works!
snoopy.bark();
```

**Inheritance** allows one class to see and use the methods and properties of another class.

```js
// the original Animal class and sayName method
function Animal(name, numLegs) {
    this.name = name;
    this.numLegs = numLegs;
}
Animal.prototype.sayName = function() {
    console.log("Hi my name is " + this.name);
};

// define a Penguin class
function Penguin(name) {
    this.name = name;
    this.numLegs = 2;
}

// set its prototype to be a new instance of Animal <<<<<<
Penguin.prototype = new Animal();

// create new penguin
var penguin = new Penguin("Stefan");
// this method is inherited from Animal, WOW!
penguin.sayName();
```

By default, all classes inherit directly from _Object_, unless we change the class's prototype.
Remember how the prototype chain works: if a property is not defined for a class, this class's prototype chain will be traversed upwards until one is found (or not) in a parent (higher) class.
```js
// original classes
function Animal(name, numLegs) {
    this.name = name;
    this.numLegs = numLegs;
    this.isAlive = true;
}
function Penguin(name) {
    this.name = name;
    this.numLegs = 2;
}
function Emperor(name) {
    this.name = name;
    this.saying = "Waddle waddle";
}

// set up the prototype chain
Penguin.prototype = new Animal();
Emperor.prototype = new Penguin();

var myEmperor = new Emperor("Jules");

console.log(myEmperor.saying); // "Waddle waddle"
console.log(myEmperor.numLegs); // 2
console.log(myEmperor.isAlive); // true
```

**Public & private**
- public - properties can be accessed from outside the class  
- private - properties can only be accessed from within the class (similar to local variables in function)

```js
function Person(first,last,age) {
   this.firstname = first;  // public
   this.lastname = last;    // public
   this.age = age;          // public
   var bankBalance = 7500;  // private
   // this method allows display bankBalance value
   this.getBalance = function() {
      return bankBalance;
   };
}

var john = new Person('John','Smith',30);
console.log(john.bankBalance);    // undefined

var myBalance = john.getBalance();
console.log(myBalance);           // 7500
```

Private methods
```js
function Person(first,last,age) {
   this.firstname = first;
   this.lastname = last;
   this.age = age;
   var bankBalance = 7500;
   // private method
   var returnBalance = function() {
      return bankBalance;
   };
   // this method allows to access returnBalance function
   this.askTeller = function() {
       return returnBalance;      // it's just reference to  returnBalance()
   };
}

var john = new Person('John','Smith',30);
console.log(john.returnBalance);          // undefined
var myBalanceMethod = john.askTeller();   // returnBalance
var myBalance = myBalanceMethod();        // call returnBalance();
console.log(myBalance);                   // 7500

/*
  Because askTeller returns a method, we need to call it to make it any use.
  This is what var myBalance = myBalanceMethod(); does.
*/
```

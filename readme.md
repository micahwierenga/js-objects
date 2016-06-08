# JavaScript Objects

### Objectives
*After this lesson, students will be able to:*

- Compare objects, key-value stores, and arrays as data structures
- Explain the difference between object properties and methods
- Create empty objects and objects with multiple properties and methods using object literal syntax
- Compare adding and retrieving properties to an existing object using the dot and bracket notations
- Access properties of an object using keys and helper methods (.hasOwnProperty)
- Iterate over the keys of an object to return and manipulate values

### Preparation
*Before this lesson, students should already be able to:*

- Create and manipulate variables with JavaScript
- Use the chrome dev tools console

Objects in JavaScript
=====

[Comment]: # (Objects and Object Oriented Programming is in some sense the start of "real programming". But it also comes with another aspect of being a developer, "religious wars" or deeply held beliefs about the "right" way to do something.)
[Comment]: # (The vocabulary is important but it also can change a little bit based on who you are talking to. If you can follow the exercises and make what we talk about operational don't worry to much about the vocabulary.) 
[Comment]: # (Feel free to be a little bit more aggressive about asking if something is a parking lot issue.)

## Opening

### What are objects and key-value stories (10 mins)

* Key-value stores are used to group multiple pieces of data together
  * Like arrays, key-value stores can hold multiple pieces of data of varying types; but unlike arrays, objects use named 
  keys rather than indices to access those pieces of data
  * Modern languages call this data structure different names, Ruby = hash, Python = dictionary, Go = map  
* Object Oriented Programming(OOP) is the idea of combining a set of specific data with the functions that operate on that 
data

Example: We can think about modeling a car in an object oriented way by thinking about what is the data about a car that
we need and how does that data change what are the functions that operate on the data were using for the car

[Comment]: # (This is different from procedural programming or functional programming in that we grouping things by related concepts rather than the steps needed to follow or something more esoteric) 
* Objects in general are made up of two things – properties and methods. Properties are the data attached to an object 
that describe it or are related to it in some way. Methods are the functions that associated to the object or how we 
can change or alter the object.

Example 1: Car in e-commerce app. Here the properties are more related to the car as a good to sell. What color is it? 
How many seats are there? What kind of seats, leather vs  upholstery. What kind of sound system it has. Some of the 
methods might be 

Example 2: Car in a driving game. Here the properties are more related to how it works in the game. We still might have
color but we'd also have position, speed, maybe damage. The methods are things like driving, braking, or hitting 
something.

In JavaScript, there are 5 primitive types, ``null``, ``undefined``, ``boolean``, ``string``, and ``number``, 
**everything else is an object** even functions. And what is an object? An Object in JavaScript is a key-value store. 
The properties are the keys to the key-value store. The methods are just keys that map to a function instead of 
something more concrete like a string, or an array, or even another object.

An Object in JavaScript also has one important property called a ``prototype``. This is the property that lets us link 
all of our objects, like cars, together.

[Comment]: # (One way to think about this is like the difference between small "d" democrats and big "D" Democrats in the US. Everyone in the principles of democracy but Democrats believe in particular way of carrying out those principles but they're both called democrats.) 
If we just need a key-value store we can create an Object and just ignore the prototype.

![mindblown](https://github.com/den-wdi-1/js-objects/blob/master/images/cosmo_mind_blown.gif)

It's OK if this doesn't make sense right now. We'll be going over how this works for the rest of the module so we'll be
able to see these ideas in action. We'll also be coming back to OOP in more depth with Ruby.

[CFU]: # (Quick Fo5 around the comparison between arrays, key-value pairs, and objects. If everyone is completely lost check each concept individually do a quick review of the completely lost portion and then )

## Creating Objects (5 mins)

There are 4 different ways to create an object.
#### Object literal syntax

This is also called an [object initializer](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Object_initializer).

This is equivalent to the syntax above, and is the one we use to create JSON objects.

```javascript
var myObject = {};
```

#### Object constructors

The [Object](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object) constructor is a 
function that returns a Object.

```javascript
var myObject = new Object();
```

If we want to add some initial functionality to an object. It is also possible to use a `function` statement to create 
an object that serves as a "constructor function."
By convention, this function we start the function name with a capital letter. Once the function is defined (in the current scope), you can create a new object by using the keyword `new`.

```javascript
function Classroom(name, numberOfStudents) {
  this.name = name;
  this.numberOfStudents = numberOfStudents;
}

var wdi = new Classroom("WDI 29 San Francisco", 18);
```

[Comment]: # (A good convention to get into is to use upper case names for objects.)

#### Object.create

It is possible to use the syntax [`Object.create()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/create).

This method can take an object in argument as the prototype, allowing you to create an object without having to use a constructor function.


```javascript
var Person = {
  type: "Human",
  displayType: function(){
    console.log(this.type);
  }
}

var person1 = Object.create(Person);
person1.displayType();
=> Human

var person2 = Object.create(Person);
person2.type = "Male";
person2.displayType();
=> "Male"
```

## Object Properties

Objects in JavaScript **always** have properties associated with them.

You can think of a property on a JavaScript object as a type of variable that contains a value. The properties of an object can be accessed using "dot notation":

```javascript
var Person = {
  name: "Ben"
}

Person.name
=> "Ben"
```

You can define or re-assign a property by assigning it a value using `=` as you would a normal variable.

```javascript

Person.name = "Alex"

Person.name
=> "Alex"
```

## Creating an object with properties

We are going to create an object `classroom` that contains properties `name` and `campus`:

```javascript
var classroom = new Object();
=> undefined

classroom.name = "WDI 29";
=> "WDI 29"

classroom.campus = "San Francisco";
=> "San Francisco"

classroom
=> Object {name: "WDI 29", campus: "San Francisco"}
```

#### Bracket notation

There is another way to set properties on a JavaScript object.

```javascript
classroom["name"]   = "WDI 29";
classroom["campus"] = "San Francisco";
```

This syntax can also be used to read properties of an object:

```javascript
console.log(classroom["name"]);
=> "WDI 29";

var property = "campus";

console.log(classroom[property]);
=> "San Francisco";
```

For more details see [MDN's Documentation on Property Accessors](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Property_Accessors).


#### Deleting properties

If you want to delete a property of an object (and by extension, the value attached to the property), you need to use the [`delete`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/delete) operator:

The following code shows how to remove a property:

```
var classroom = {"name": "WDI 29, "campus": "San Francisco", "start": "5/2/2016"};
delete classroom.start;
classroom
=> {name: "WDI 29", campus: "San Francisco"}
```

## Object methods

As we've said before, the value of a property can be anything in JavaScript, means we can also attach functions to objects properties. When a function is attached to a property, this function becomes a `method`. Methods are defined the exact same way as a function, except that they have to be defined as the property of an object.

```javascript
var classroom = {
  name: "WDI 29",
  campus: "San Francisco",
  start: "5/2/2016",
  sayHello: function() {
    console.log("Hello");
  }
};
```

To call the method, we add a pair of parentheses to execute it:

```
classroom.sayHello();
=> Hello
```

#### Assigning a previously-defined function

We can attach regular functions to objects as methods, even after they are created.

```
var sayHello = function() { console.log("Hello"); }

classroom.sayHello = sayHello;  

classroom.sayHello()
=> Hello
```

##`this` for object references

In JavaScript, `this` is a keyword that refers to the current object. When used in a method on an object, it will always refer to the current object.


```
var classroom = {
  name: "WDI 29",
  campus: "San Francisco",
  start: "5/2/2016",
  classInfo: function(){
    console.log("This is " + this.name + " and the class starts on " + this.start);
  }
};

classroom.classInfo()
=> This is WDI 29 and it starts on 5/2/2016
```

## We Do: Getters and setters

> A getter is a method that gets the value of a specific property. A setter is a method that sets the value of a specific property. You can define getters and setters on any predefined core object or user-defined object that supports the addition of new properties. The syntax for defining getters and setters uses object literals.

```javascript
var o = {
    a: 7,
    get b() {
        return this.a + 1;
    },
    set c(x) {
        this.a = x / 2
    }
};

console.log(o.a);
=> 7

console.log(o.b);
=> 8

o.c = 50;
console.log(o.a);
=> 25
```

This section from [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Working_with_Objects#Creating_new_objects#Defining_getters_and_setters)

#### Enumerating properties of an object

There are three native ways to list the properties of an object:

* **for...in loops** This method traverses all enumerable properties of an object and its prototype chain
* **Object.keys(o)**  This method returns an array with all the own (not in the prototype chain) enumerable properties' names ("keys") of an object o.
* **Object.getOwnPropertyNames(o)** This method returns an array containing all own properties' names (enumerable or not) of an object o.

**Loop over an objects properties**


You can use the bracket notation with for...in to iterate over all the enumerable properties of an object.

```javascript
var myCar = {"make": "Ford", "model": "Mustang", "year": 1969};

function showProps(obj, objName) {
  var result = "";
  for (var i in obj) {
    if (obj.hasOwnProperty(i)) {
      result += objName + "." + i + " = " + obj[i] + "\n";
    }
  }
  return result;
}

showProps(myCar, "Car");
=> Car.make = Ford
=> Car.model = Mustang
=> Car.year = 1969
```

This section from [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Working_with_Objects#Creating_new_objects#Objects_and_properties)


## Comparing Objects

In JavaScript, if two objects are created separately, they are distinct, even if they are given the same properties.

```javascript
var student = {name: "Chris"};
=> undefined

var student2 = {name: "Chris"};
=> undefined

student == student2
=> false

student === student
=> true
```

If you're confused by the difference between `==` and `===` review MDN's notes on [equality](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Comparison_Operators#Equality_()) and [strict equality](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Comparison_Operators#Identity_strict_equality_())

## Independent Monkey Exercise (20 minutes)

- Create a `monkey` object, which has the following properties:

  - `name`
  - `species`
  - `foodsEaten`

  And the following methods:

  - `eatSomething(thingAsString)`
  - `introduce`: producers a string introducing itself, including its name, species, and what it's eaten

- Create 3 monkeys total. Make sure all 3 monkeys have all properties set and methods defined.

- Exercise your monkeys by retrieving their properties and using their methods. Practice using both syntaxes for retrieving properties (dot notation and brackets).

## Conclusion (5 mins)

We will use objects in JavaScript every day, and you will have plenty of time to practice creating and using objects in Javascript. There are a lot of resources available on the web for you to dive deeper, but the most detailed and understandable one is probably MDN.

- [JavaScript Reference](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object)
- [Intro to Object-Orientated Javascript](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Introduction_to_Object-Oriented_JavaScript)
- [Objects in Javascript](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Working_with_Objects)

<!--

* All programming can be boiled down to data & behavior
* OOP is about creating taxonomies
* OOP is a stylistic approach to organizing code

-->

# JavaScript Objects

<!--11:20 5 minutes -->

[Hook]: # (-Code this out- So we've seen arrays, and how they can be a very helpful method to store data.  So my program always needs access to this fourth element in the array.  How do I get that?  Great.  However, what happens if I remove an item from the middle of my array? -Indices shift- Now how do I get that same element?  Also, if we hire a new developer tomorrow, and he takes a look at my code, how is he/she supposed to know what array[3] means?  With key-value stores, we can solve both those issues.)

### Objectives
*After this lesson, students will be able to:*

- **Compare** key-value stores and arrays as data structures
- **Create** empty objects and objects with multiple properties using object literal syntax
- **Compare** adding and retrieving properties to an existing object using the dot and bracket notations
- **Access** the keys of a key-value store to return and manipulate values

### Preparation
*Before this lesson, students should already be able to:*

- **Create** and **manipulate** variables with JavaScript
- **Use** the chrome dev tools console

Objects in JavaScript
=====

<!--11:25 10 minutes -->

## Opening

### What are objects and key-value stores

There are two main ways to group data in modern languages:

|key value store | array |
|--------------- | ----- |
|Can store any data type, strings, numbers, arrays | Can store any data type, strings, numbers, arrays | 
|Access the values by key or name                  | Access the values by index |
|Set a value after it has been created             | Set a value after it had been created | 
|Dynamic can add a key at any time                 | Add values to the end of array easily |

[CFU]: # (Ask the students for properties of arrays as activity as we work through the chart)
[Comment]: # (This makes things much easier for humans. We can associate names with things rather than remembering that name is three memory offsets from something) 

Some unique JavaScript issues:
* No actual key-value store, we use objects

[Comment]: # (We'll talk more about the extra properties of the Object type next week during some lectures on OOP.)

* The keys of JavaScript key-value stores are called properties

[CFU]: # (Fo5 for key-value stores, properties) 

<!--11:35 15 minutes -->

## Working with Objects 

The simplest way to create an object is to use curly braces.

```javascript
var myObject = {};
```

This creates a blank object.

This is also called an [object initializer](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Object_initializer).

If we want to add some initial keys, can use a colon.
```javascript
var Person = {
  name: "Zeb",
  titles: ["Teacher", "Puppy Owner", "Programmer"] 
}
```

#### Dot notation

We can then use the property that been set.
[CFU]: # (Call for properties of the person)

You can think of a property on a JavaScript object as a type of variable that contains a value. The properties of an 
object can be accessed using "dot notation":

```javascript 
Person.name
=> "Nick"
```

You can define or re-assign a property by assigning it a value using `=` as you would a normal variable.

```javascript

Person.name = "Zeb"

Person.name
=> "Zeb"
```

### Excercise 
Create an object called ``classroom`` with properties, name and campus. The name property should have value White Walkers and the 
campus property should value Denver
<details>
  ```javascript
  var classroom = {
    name: "White Walkers"
    campus: "Denver"
  }
  ```
</details>

#### Bracket notation

There is another way to set properties on a JavaScript object.

```javascript
classroom["name"]   = "White Walkers";
classroom["campus"] = "Denver";
```

This syntax can also be used to read properties of an object:

```javascript
console.log(classroom["name"]);
=> "White Walkers";

var property = "campus";

console.log(classroom[property]);
=> "Denver";
```

For more details see [MDN's Documentation on Property Accessors](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Property_Accessors).


#### Deleting properties

If you want to delete a property of an object (and by extension, the value attached to the property), you need to use the [`delete`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/delete) operator:

The following code shows how to remove a property:

```
var classroom = {"name": "White Walkers", "campus": "Denver", "start": "6/13/2016"};
delete classroom.start;
classroom
=> {name: "White Walkers", campus: "Denver"}
```

## Enumerating properties of an object(5 mins)

If we want to get the key, we can use ``Object.keys()`` function to get all of the keys of an object.

Once we have an array of the keys we can loop over the keys to work with all of the properties of an object.

```javascript
var myCar = {"make": "Ford", "model": "Mustang", "year": 1969};

var keys = Object.keys(myCar)

for(i=0; i < keys.length; i++){ 
  console.log("Key " + i + " " + keys[i]) 
}
```

This section from [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Working_with_Objects#Creating_new_objects#Objects_and_properties)

[Comment]: # (There are some corner cases that apply to enumeration based on the fact that its an object but we'll get into those next week.)

<!--11:50 5 minutes -->

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

Moreover, objects are assigned by reference. Another way to say this is if we create a new variable and assign the 
object to the new variable we don't create a new object.

```javascript
var student1 = {name: "Chris"};
=> undefined

var student2 = student1;
=> undefined

student2.name
=> "Chris"

student2.name = "Tom";
=> "Tom"

student1.name
=> "Tom"

student1 === student2
=> true
```

[CFU]: # (Stop and jot on the solutions to student1.name and the equality)

What? Even though we had two names we only had a single object. If we want to create a new object we need to use 
``clone``.

```javascript
var student1 = {name: "Chris"} 
=> undefined

var student2 = student1.clone
=> undefined

student2.name
=> "Tom"

student2.name = "Tom"
=> "Tom"

student1.name 
=> "Chris"

student1 === student2
=> false
```

<!--11:55 20 minutes -->

## Monkey Exercise

- Create a `monkey` object, which has the following properties:

  - `name`
  - `species`
  - `foodsEaten`

- Create 3 monkeys total. Make sure all 3 monkeys have all properties set. All monkeys should eat multiple foods.

- Exercise your monkeys by retrieving their properties and using their methods. Practice using both syntaxes for 
retrieving properties (dot notation and brackets).

[CFU]: # (A new requirement has just come. We need to start keeping track of color. Add a color property to each monkey.)

<!--12:15 5 minutes -->

## Conclusion

We will use key-value stores in JavaScript every day, and you will have plenty of time to practice creating and using 
objects in Javascript. There are a lot of resources available on the web for you to dive deeper, but the most detailed 
and understandable one is probably MDN.

- [JavaScript Reference](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object)
- [Objects in Javascript](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Working_with_Objects)

## Licensing
All content is licensed under a CC­BY­NC­SA 4.0 license.
All software code is licensed under GNU GPLv3. For commercial use or alternative licensing, please contact legal@ga.co.

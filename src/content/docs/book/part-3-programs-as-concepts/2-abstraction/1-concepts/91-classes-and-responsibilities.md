---
title: "Classes and Responsibilities"
---

To come...

<!-- 
FIRST DRAFT, restructuring into smaller concepts

Include idea of static.
-->

## A new approach to organisation


## The elements of a class




### Knowing responsibilities

#### Every class has a name



#### Classes can know about data



### Doing responsibilities

#### Every class can be constructed

Just like a method doesn't do anything until it is called, a class doesn't do anything until it is used to create an entity.
To do this, we call the class's **constructor**.
A constructor is a special method with the same identifier as the class it relates to, which creates and returns an **instance** of the class.

The constructor's job is to make sure all of the data in the class is initialised.
It can do this on its own, by using values passed in as arguments, or a combination of both.
If a constructor does not have any parameters, it is called the **default constructor**.
A class can have multiple constructors using method [overloading](<../../../../part-1-instructions/1-sequence-and-data/1-concepts/03-method-call/#overloading>), which means programmers can write several different ways of initialising a class's data.


Once we have an instance of the class, called an object, we can write code asking it to do things or asking it about the things that it knows.
This is something we will learn more about when we explore the concept of an [object](<../1-objects.md>).

#### Classes can do things

As well as its constructor, a class can have any number of methods.
Methods inside a class are very similar to regular methods: they still have an identifier, can have parameters, and can return a value.
Within a class we can also [overload](<../../../../part-1-instructions/1-sequence-and-data/1-concepts/03-method-call/#overloading>) methods, just like we can with regular methods.
The only real difference between regular methods and methods that are inside a class, is that all methods within a class can automatically "see" each other.
This means that all methods within the same class can call each other.

### Showing and hiding responsibilities

Once we have used a class to create an entity, we can write code to access the data within the entity and execute its functionality.
However, we often don't want our entities to allow just any code to do this.
This is where the concept of **access modifiers** helps us.
An access modifier is a piece of information attached to every field and method within a class, telling the compiler what code can access the field or call the method.
There are several access modifiers we can use, but for now let's focus on the two most basic ones: **public** and **private**.

* **Public** methods and fields in a class can be accessed by any code that has an instance of the class, including within the class itself.
* **Private** methods and fields in a class can only be accessed by other code in the same class.

Deciding what access modifier a field or method should have is one of the things that makes coding with classes challenging.
There are principles and best practices to help make these decisions, which we will explore in [Part 3](<../../../../part-3-programs-as-concepts/00-part-3-programs-as-concepts>).

## In C#

### Class structure



### Method Declarations

There are two kinds of methods that we can define in a class: **methods** and **constructors**.<sup>[1](#FootnoteEntities)</sup>
Let's take a look at the syntax for each.

:::tip[Syntax]
The syntax for declaring a constructor in a C# class is shown in Figure X.

![Figure X](./images/constructor-syntax-diagram.png)
<div class="caption"><span class="caption-figure-nbr">Figure X: </span>The syntax for constructor declarations</div><br/>
:::

:::tip[Syntax]
The syntax for declaring a method in a C# class is shown in Figure X.

![Figure X](./images/method-syntax-diagram.png)
<div class="caption"><span class="caption-figure-nbr">Figure X: </span>The syntax for method declarations</div><br/>
:::

The first thing you might notice is that the syntax is practically identical!
There are really just two main differences between a constructor declaration and a regular method declaration:

1. A constructor does not have a unique method name. It has to use the class's name.
2. A constructor does not have a return type.

Using the class's name in place of a method name tells the compiler to interpret the declaration as a constructor rather than standard method.
The reason that a constructor declaration does not need to include a return type is because a constructor, by definition, can only and always will return an **instance** of the class.
Therefore, its return type is implied and does not need to be explicitly stated.

Aside from these two differences, a constructor declaration is the same as a method declaration.
The syntax for a method declaration is hopefully looking familiar, because it is the same as the syntax for declaring methods you have already seen. <!-- TODO: link back to method declaration concept -->

<hr class="footnote">
<div id="FootnoteEntities" class="footnote"><sup>1</sup>Yes, it is confusing that a constructor is a method, but also a separate concept!</div>

### Property Declarations

**Properties** are a class element we have not explored yet.
The reason for this is that properties are unique to C#.

Essentially, properties are a way of adding an element to a class that *looks* and *acts* like a public field to other code, but is not *actually* a public field.

:::tip[Syntax]
The syntax for declaring a property in a C# class is shown in Figure X.

![Figure X](./images/property-syntax-diagram.png)
<div class="caption"><span class="caption-figure-nbr">Figure X: </span>The syntax for property declarations</div><br/>
:::

The start of a property declaration looks exactly like a field declaration: an access modifier followed by a data type and a name.
Then, within curly braces you can declare up to two parts of the property:

1. A `get`, which contains code that is executed when the property is *read*.
2. A `set`, which contains code that is executed when the property is *assigned to*.

Both parts are optional, but can only be used once each in a property.
A property containing only a `get` part is called a **read-only property**, and a property containing only a `set` part is called a **set-only property**.
A property containing both is just called a property, or can be called a **read-write property**.
Most properties are read-write or read-only.

Because `get` is used when the property is read, it must include a **return statement** which returns a value matching the data type of the property.
The `set` part of a property has access to a special variable, `value`, which has the same data type as the property and the value of the right-hand side of the assignment statement in which the property was used.

The code within a `get` or `set` can be as simple or as complicated as you like, and can call other code within the same class or in libraries.
Many properties are written as "wrappers" around a private field, and are used to better control access to the data in that field.
Other properties may instead construct and return new data when they are read.

## Example

The following code shows a basic class definition.

```cs
using static System.Console;

class Greeting
{
    private string _message;

    public Greeting(string message)
    {
        _message = message;
    }

    public void PrintGreeting(string name)
    {
        WriteLine($"Hello {name}! {_message}");
    }

    public string Message
    {
        get
        {
            return _message;
        }
        set
        {
            _message = value;
        }
    }
}
```

:::note
We can see a few C# conventions in this example:

* Private field names start with an underscore.
* Property names start with a capital letter.
* Parameter names start with a lower-case letter.
* Method names are written in CamelCase.
* Each class member is separated by a blank line.
:::

This class is called "Greeting", and it has a few responsibilities.
The Greeting class...

* ...knows about a string called `_message`.
* ...can be constructed with an initial value for `_message`.
* ...can print a greeting containing the text "Hello", a name passed in as an argument, and the value of `message`.
* ...can provide access to read and change the value of `_message` through a property `Message`.

In other words, this class has one private field, one public constructor, one public method, and one public read-write property.

Earlier in our journey we learned that a constructor creates and returns an instance of its class.
Given this, you might be surprised to see that the constructor of Greeting does not contain a `return` statement.
The reason for this is that the compiler already knows exactly what should be returned from a constructor, so it can make sure the right value is returned without being explicitly instructed to do it.

To add this class to your C# project, copy the code above into a file called "Greeting.cs" within a console project.
Run your project...nothing happens!
That is because much like a method that is never called, a class does not do much on its own.
To actually execute this code we need to use the class to create an **object**.
So, let's explore the concept of **objects** next.

## Activities

* List some knowing and doing examples you have in your daily life.
* What other responsibilities could the Greeting class have?
* Think about a class for representing a book. What responsibilities might it have? Would they be public or private?

:::note[Summary]

* Classes are a tool for strurturing code into entities that contain data and methods.
* Each class definition is a blueprint that describes an entity in terms of what it **knows** (data) and what it can **do** (methods).
* A class defines a **custom data type** we can use in our programs when building digital realities.
* Classes have a **name**, and contain zero or more **members**.
* A class member can be a:
  * field
  * constructor
  * method
  * property
* Each class member can be **public** or **private**:
  * **public** members can be accessed by any code that has an instance of the class.
  * **private** members can only be accessed by other code in the same class.
* **Fields** are just like variables, with a scope of the entire class in which they are declared.
* **Methods** are no different from what you have already learned. <!-- TODO: link to previous section on methods? -->
* **Constructors** are special methods which create and return an instance of the class in which they are declared.
  * A **default constructor** is a constructor with no parameters.
* **Properties** are unique to C#, and allow us to write code that looks and acts like a public field.
* Classes can be used to create **objects**.

:::
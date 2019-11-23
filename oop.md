# Classes, an Intro:
- It's all about classes in java.

## Class Fundamentals:
- Defining a new class is defining a new *data type*.
- A class is a *template* for an object and an object is an *instance* of a class.
- Defining a class is done through specifying its data and the code that operates on that data. A class can have both the data and code or just one of the two.
- Data is called ***instance variables*** and the code is ***methods***. Methods and instance variables are called ***class members***.
- A class doesn't have to have a `main()` method unless it's the entry point of a program.
- The **dot operator** `.` links the name of an object with the name of an instance variable. The dot is actually a separator and not an operator but most people call it the dot operator, so ..

## Declaring an Object and the Use of `new`:
- Declaring an object is a two step process:
	1. Declare a variable of the given class type.
	2. assign a physical copy of the class the declared variable with the `new` operator.
- The `new` operator allocates memory to the intended object and returns a reference to it. 
- When you don't explicitly supply a reference, java offers an automatic one.
- The reason why primitives need no `new` operator is the fact that they are implemented as normal variables and not as objects. Objects have rich capabilities which add an overhead. primitives are more efficient without this added overhead.
- `new` allocates memory in **runtime** making java extremely dynamic. You don't always know in advance how many objects you need to create. 
- A class is a logical construct while an object is a physical reality.

## Assigning Object Reference Variables:
- Discussion here is reminiscent of the passing by reference vs. passing by value from K&RC.
```java
Something obj1 = new Something();
Something obj2 = obj1;
```
- In the example above, the variable obj2 holds a reference to the object pointed to by obj1. If you change obj2, obj1 changes too. If this were primitive, changing obj2 would have no effect on obj1. If you want a brand new object referenced by obj2, you need to create one with the `new` operator and all that jazz.
- Apart from referencing the same object, obj1 and obj2 are not linked in any other way. obj2 can reference another object and its ability to change the referenced object ceases. The same is true for the variable obj1 with which the object was created. 

## Methods, an Intro:
- A ***parameter:*** is a variable defined in the method which receives a value when the method is called.
- An ***argument:*** The value that gets passed into the the method (or its parameter).

## Constructors:
- A ***constructor*** allows you to initialize all of an instance variables when you create it, instead of spending a ridiculous time initializing these variables manually (directly or through methods). 
- When you don't define your own constructor, java does it for you, but it initializes variables to zeros, nulls or falses... etc. 
- A constructor initializes a class when it's created. It has has same name as the given class and its syntax is almost identical to that of a method except that it doesn't have a return type, not even a void.
- A parametrized constructor is a more useful constructor.

## `this`:
- `this` is used inside methods to refer to the objects where these methods were defined. It's use can redundant if it's not directed to combat so-called variable hiding.
-  **Variable hiding** happens when *local variables* (i.e. method variables or method parameters) overlap with instance variables. local variables hide instance variables meaning the names only refer to local variables and completely hide instance variables that have the same names.
- Using `this` you can avoid these namespace clashes, thus unhiding instance variables and making them accessible in the method. This also allows you to give the same names to your instance variables and the method and constructor parameters that are used to manipulate them.
- There is an Endian controversy concerning naming give the same names to parameters and instance variables or vice-versa. I think using the same names with `this` is more intuitive. 

## The `finalize()` Method:
- The `finalize()` method allows an object to release locks on resources such as files before this object is destroyed. You define a `finalize()` method inside your class and tell it what to do and whenever the garbage collector is about destroy an object it runs `finalize()`.

# More on Classes and Methods:
## Method Overloading:
- **Method overloading** refers the fact that two methods with the same name and different parameter declarations can be defined in the same class. It's an aspect of polymorphism, namely, multiple names are reduced to one.
- Javascript and Python don't overload!
- When an overloaded method is invoked, the type and/or the number of its parameters are used to determine which method to call. The two methods must differ in type and or number of parameters. **BE CAREFUL (DIFFERENT RETURN TYPES ARE NOT ENOUGH TO TELL OVERLOADED METHODS APART. ONLY THE TYPE AND NUMBER OF PARAMS MATTER)**
- Java's **automatic type conversion** can interfere and elevate something like an int into a double. This can be problematic and some might consider it a blessing.
- Method overloading is extremely useful and makes java more streamlined and easier to use. C for example uses 3 functions to obtain absolute value, one for floats, another for integers and yet another one for long integers.. etc. Java's overloading capabilities allows for creating one absolute value method for all types of numbers.
- Stylistically speaking, avoid overloading unrelated methods. Just because you can make use one name for all your class methods, don't do it. It's stupid and confusing.

### Overloading Constructors:
- Overloading constructor is the norm.
- The utility of constructor overloading is paramount as it addresses the availability of parameters and one class can handle many different types of boxes (example) which might be a cube or have different dimensions.

## Objects as Parameters:
- Passing objects as method parameters is possible but also very common. 
- Passing objects as constructor parameters is also very common. To clone an object, meaning to create an exact copy of it in a different memory location, you can pass the object itself as a parameter to one of its constructors.

## Argument Passing, an in-Depth Look:
- Basically, when you pass a primitive type argument to a method's parameter, you pass it by value. You just pass a copy of it. Any changes you make to the variable inside the method only affects the copy, leaving the original unaffected. 
- When you pass an object type, the variable you pass is a reference to the object itself; you pass by reference. Changes you make to the variable affect the object directly.

## Recursion:
-
## Access Control:
-
## Static:
-
## Final:
-
## Arrays Revisited:
-
## The `String` Class:
-
## Command-Line Arguments:
-
## Varargs:
-


# Inheritance:
# Packages and Interfaces:
# Generics:

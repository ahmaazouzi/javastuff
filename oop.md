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

## Access Control:
- In addition to linking data with the code that manipulates it, *encapsulation* does also provide **access control**. Access control refers to the ability to control access a class members by other parts of the program. Through a correct implementation of access control, a class becomes a *black box. * It can be used and interacted with, but its internal workings are not visible to the outside world.
- an access modifier is added to a class member's declaration. The three access modifiers are:
	1. **private:** can only be accessed within the class by other class members.
	2. **public:** can be accessed by any the whole world. `main()`, for example, is open to be accessed outside the program, i.e. the java runtime system.
	3. **protected:** has to do with inheritance which is discussed later [here](#inheritance).
	4. No modifier: when no modifier is specified, the default is for access to be public within the package where the class resides.
- Data should be private while some methods are public and others private.

## Static:
- static members have to do with the class and have no relation to its instances. These methods and variables can be accessed and called before the class where they reside is instantiated. They don't require the instantiation of the class.
- A static variable is global for all the instances of the class. If one instance changes it, it is changed for every instance.
- Static methods:
	1. Can only **directly call other static methods**.
	2. Can only **directly access static data**.
	3. Cannot refer to **this** or **super** directly or indirectly. 
- A **static block** can be defined inside a class that gets executed when the class is first used. I can't think of a use case for this at the moment but it sounds useful :).
```java
public class Something{
	public static void main(String[] args) {
		Dada dada = new Dada();
	}
}

class Dada{
	static fafa (){
		System.out.println("zzzzz");
	}
}
```
- 

## Final:
- `final` fields are constants. a final should be initialized when it's declared or within a constructor.
- It is conventional for constants to be in all-caps.
- Constants are a midpoint between variables and mere literals. Instead of spreading literals (magic values) that might need to be changed in the future and you might forget to change some of them, a constant give them a meaningful name. Changing them is done once with the constant. Finals are extremely useful.
- local (method) variables and **parameters can also be finals** to prevent changing them within the method. I didn't know parameters can be finals.
- a method can also be `final`, but the meaning of `final` here is substantially different (will be discussed here in the context of [inheritance](#inheritance).

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

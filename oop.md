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

									=================

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
	3. **protected:** has to do with inheritance which is discussed later [here](#access-protection).
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
	static fafa {
		System.out.println("zzzzz");
	}
}
```
- 

## Final:
- `final` fields are constants. A final should be initialized when it's declared or within a constructor.
- It is conventional for constants to be in all-caps.
- Constants are a midpoint between variables and mere literals. Instead of spreading literals (magic values) that might need to be changed in the future and you might forget to change some of them, a constant give them a meaningful name. Changing them is done once with the constant. Finals are extremely useful.
- local (method) variables and **parameters can also be finals** to prevent changing them within the method. I didn't know parameters can be finals.
- a method can also be `final`, but the meaning of `final` here is substantially different (will be discussed here in the context of [inheritance](#inheritance).

## Arrays Revisited:
- Demystification time: Java implements arrays as objects, that's why declaring one does sometimes require the `new` keyword. 
- The instance variable **length** is useful. it tells you the size of the array.

## Nested and Inner Classes, an Intro:
- Nested class is a class defined within another class.
- An nested class is bound by it's parent class. The nested class can't exist without the outer class. 
- The nested class has access to the outer class variables, including its private ones. The outer class has no access to the nested class private variables.
- A nested class can also be defined and be part of a block.
- As far as staticity goes:
	1. ***Static nested classes*** must access the non-static members of the enclosing class only through an object. It has no direct access to them. This is kinda ridiculous.
	2. ***Non-static nested classes (also called an INNER CLASS,)*** on the other hand, has access to all variables and methods of the outer class directly.
- An instance of the inner class can only be created within the context of the outer class. It must be created within the outer class definition, because there is no way of directly manipulating it outside the outer class
```java
public class Something{
	

	public static void main(String[] args) {
		Dada dada = new Dada();
		// Zaza zaza = new dada.Zaza(); This is totally wrong
	}
}
	


class Dada{
	void wawa() {
		// This is the only way you can do it
		Zaza zaza = new Zaza();
		zaza.nana();

	}
	
	public class Zaza {
		void nana() {
			System.out.println("wawa");
		}
	}
	
}
```
- Inner classes are especially handy for handling events. There can also be **anonymous inner classes** which are classes without names.

## The `String` Class:
- Every string is an object of type **String**, including string literals. 
- String objects are immutable. Once created, they cannot be changed. This is not a restriction because:
	1. Every time you want to change a string, you create a new one. I think that when I change the value of a string variable, what happens is that a new string object is created and the variable points to the newly created object.
	3. **StringBuilder** and **StringBuffer** are alternative classes that allow regular string manipulation to take place. 
- The following are useful **String** properties and methods:
	* **equals**: tests for equality between two strings.
	* **chartAt**: gets character at a given index.
	* **length:** gets the length of a string.

## Varargs:
- *vararg* methods are methods that accept a variable number of arguments.
- *vararg methods* were added to JDK5. Before that, Java required the creation of overloaded methods that each accepted a different number of variables, but this worked if there is a small number of known variables. In case there was a large number of unknown variable, they were put into an array and the array were passed as an argument. Both ways are tedious and boring so stick to *vararg*.
- *vararg* follows this syntax:
```java
void method(int ... v){
	dasdasdsadsa
}
```
- The three dots are the vararg and the following example gives an example of how they work:
```java
public class Something{
	
	static int tata(int ... v) {
		return v.length;
	}

	public static void main(String[] args) {
		System.out.println("tata got " + tata(1,3,5,6,7) + " arguments!");
		System.out.println("tata got " + tata(1,3) + " arguments!");
		System.out.println("tata got " + tata(1) + " arguments!");
		System.out.println("tata got " + tata() + " arguments!");	
	}
}
```
- Basically, `int ... v` in the last example is just an array, some type of syntactic sugar.
- A method can have other arguments besides the vararg but the vararg should be the last argument as in:
```java
void tata(int a, int b, int c, int ... v){
	kasdjas;
}
```
- Only one vararg can be passed to a method. More than results in an error.
- A vararg method can be overloaded in two ways:
	1. The type of the vararg argument type can be of different in the overloaded methods.
	2. One or more non-vararg parameters can be added.
	3. A vararg method can also be overloaded by a non-vararg method.

### Vararg and Ambiguity:
- Ambiguity can result from vararg method overloading as in the following example:
```java
class Calamata {
	static void baba(int ... v){
		System.out.println(v.length);
	}
	static void baba(boolean ... v){
		System.out.println(v.length);
	}

	public static void main(String[] args) {
		baba(1,2,3); // Ok
		baba(false, true); // OK
		baba(); // This statement results in a compile time error (ambiguous)
	}
}
```
- Ambiguity in this arises from the fact that the method can't tell what type the vararg is, is it boolean or int? Who knows?!! and java is all about types and stuff. 
- Another situation where ambiguity arises is illustrated by the following example:
```
void batata(int ... v) { //Something; }
void batata(int u, int ... v) { //Something; }

batata(5); // This is ambiguous
``` 
- The compiler can't tell if this call refers to one element in the vararg in `(int ... v)` or to the first argument in (int u, int ... v) and an empty vararg .. Hemmm.. Curious!!!
- It is just better to forgo overloading vararg methods.

									=================

# Inheritance:
- A ***superclass*** is the class inherited from.
- A ***subclass*** is the class which inherit the traits of a superclass. It gets all the traits defined in its superclass and adds its own.
- Inheritance is done through the use of the keyword `extends`. 
- Java doesn't support multiple inheritance.
- Java supports a class hierarchy, meaning that a subclass can itself become a superclass.
- No class can inherit itself.

### Member Access and Inheritance:
-  A sublcass can inherit everything from its superclass except for its **private** members.

### A Superclass Variable Can Reference a Subclass Object:
```java
public class Calamata {
	public static void main(String[] args) {
		Batata batata = new Hamama();
		batata.lala()
		// batata.zaza(); This is wrong
	}
}

class Batata{
	void lala() {
		System.out.println("dagdag");
	}
}

class Hamama extends Batata {
	void zaza() {
		System.out.println("TaqTaq");

	}
}
```
- The above example is self-evident. The problem is that the created object can't access the additional members defined by the subclass, because how the hell would it know anything about them. The book claims it's useful, but I am still not convinced. I am aware, that A variable of type map can refer to objects of type HashMap and TreeMap is useful, but I need more clarification. I guess it might have to do with overriding.

## Super:
- A subclass doesn't inherit its superclass's constructors and private members, but there is a trick around this done by the keyword **super**.
- The statment `super(arg-list)` allows the subclass to call a constructor defined by the superclass. The initializations that takes place in the superclass become accessible to the subclass as in:
```java
public class Calamata {
	public static void main(String[] args) {
		Hamama hamama = new Hamama("Delicious", 99);
		hamama.lala();
	}
}

class Batata{
	private String taste;
	private int color;

	Batata(String taste, int color) {
		this.taste = taste;
		this.color = color;
	}

	void lala() {
		System.out.println("The taste is " + taste + " and the color is " + color);
	}
}

class Hamama extends Batata {
	// Constructor using super to initialize members
	public Hamama(String t, int c) {
		super(t, c);
	}

}
```
- `super` doesn't make the superclass private members visible to the subclass, however, they are somehow accessible indirectly through the constructor. Even when they are private, they can be used by the subclass through `super`.
- Because constructors can also be overloaded, it's obvious that super will match the constructor that has the same number and/or type of arguments.
- `super` must be the first statement executed inside the subclass constructor.
- `super` can be used to prevent member hiding. If a subclass has a method or variable with the same name and parameter type and names as the superclass, the superclass member is hidden by that of the subclass. This use is almost identical that of `this`, except that super refers to the superclass rather than the class itself and it has this syntax `super.member`.

## Multilevel Hierarchies:
- Inheritance can cascade infinitely resulting absurdly long hierarchies.
- `super` only refers to the class's immediate super class.

## When Constructors are Executed:
- In a hierarchy, constructors are executed in order of derivation, meaning that superclass constructors are executed before subclass constructors. This makes sense, because superclasses have no idea about their subclasses members while the reverse is true.

## Method Overriding:
- When a subclass method has the same name and type signature as a method in the superclass, the subclass method ***overrides*** the superclass method. The overridden method always refer to the subclass method.
- As mentioned before, if you desire to use the overridden method defined in the superclass, use it along with the keyword `super` as in `super.overridenMethod()`.
- If the subclass method has the same name as a method in the superclass but a different type signature, the subclass method is simply overloaded not overridden. 

## Dynamic Method Dispatch:
- Method overriding allows for ***dynamic method dispatching*** which is a how java implements runtime polymorphism. What is ***dynamic method dispatching***? Java can use a superclass variable to refer to a subclass object. In run time, java determines what version of an overridden method to execute. It is the subclass object method that gets called, not superclass one.

### Why overriding?
- It allows a general class to define methods that would be common to subclasses. Subclasses will define their own specialized implementations of these common classes. This realizes the "one interface, multiple methods" principle.
- The one interface provides consistency, while method overriding provide flexibility, You don't always know in advance what subclasses will inherit from your superclass or the implementation details of such subclasses.

## Abstract Classes:
- **Motivation:** A superclass can impose some form of consistency while subclasses take care of implementation details. When you create the generalized superclass you might not know how to implement the details of certain methods. You can create a placeholder method that does something meaningless, but would you do so when you have the exciting ***abstract methods.***
- **Abstract methods** are unimplemented method shells defined in a superclass. In addition to being convenient placeholders that help with consistency, they a probably more important feature. The classes that inherit them **MUST** override them. Abstract methods have the following general syntax:
```
abstract type name(parameter-list);
```
- A class with one or more abstract methods must be declared **abstract**. An abstract class cannot be instantiated or have constructors or abstract static methods. A subclass of an abstract class must either implement all abstract methods or be an abstract class itself. An abstract class can also have concrete method implementations besides the abstract methods.
- Abstract classes can also be used to create object references

## `final` with Inheritance:
- In addition to naming constants, **final** can also be used for two purposes:
	1. **Preventing Overriding:** Methods preceded by **final** cannot be overridden. The compiler does inlining(whatever that means) resulting in early-binding (???) which is better performance-wise.
	2. **Preventing Inheritance:** When a class is declared **final**, it cannot be inherited. As a result, all its methods are final, making them more performant. However, you cannot have an final abstract class as it is an absurd construct. An abstract must be inherited while a final class cannot.

## The Object Class:
- The **Object** class is the master class. Every other object in java is a subclass of the **Object** class. 
- A reference variable of type **Object** can refer to an object of any type. Every object has the following methods:

| Method | Function
| --- | --- |
| `Object clone()` | Creates an identical copy. 
| `boolean equals(Object o)` | Tests for equality.
| `void finalize()` | Called before an unused objectt is recycled.
| `Class<?> getClass()` | Gets the class of an object at run time.
| `int hashCode()` | Returns the hash code of the object.
| `String toString()` | Returns a String describing the object 

 - In addition to these methods, the Object object class has the following methods which have to do with multithreading : `notify()`, `notifyAll()` and the different flavors of `wait()`. These are useful methods, yes they ARE!

									=================

# Packages and Interfaces:
- Packages are used to compartmentalize class name space. Interfaces allow you totally abstract a class and make possible a special type of multi-inheritance. While a class cannot inherit more than a single class or abstract class, it can on the other hand implement multiple interfaces. 

## Packages:
- It is easy to run out of descriptive class names if you use a single name space. **Packages** allow you to **divide name space into manageable sections**. They also allow you to control visibility.
- You can define classes and class members that are visible only to other classes within the same package and invisible to the rest of the world. 

### Defining a Package:
- A package is created by including the package command on top of a file. Every class defined in this file belongs to the specified package.
- The classes in a file that doesn't define a package are placed in the **default package** which has no name. A default package is sufficient for simple programs, but a serious application does need a packages. 
- Java uses the files system directories to store packages. If Batata is under package **packajo**, then the **.class** file it compiles to is placed in a directory named packajo.
- Multiple files can include the same package. This means that the classes defined in these files are in the same specified package. In real world programs packages are spread among many packages.
- You cna have a hierarchy of packages as which has the following format:
		package *pkg1*[*.pkg2*[*.pkg3*]];
- A package hierarchy must be reflected in the file system. A package declared as `package lala.batata.matata;` is stored in a file with the path `lala/batata/matata`.
- Choose packages carefully, because you cannot rename a package without renaming the directory where the classes are placed.

### Finding Packages and CLASSPATH:
- How does java know where packages are? By default, Java starts looking for a package in the current working directory. Second, a directory path can be set though the **CLASSPATH**. Third, a **-classpath** option can be used with **java** and **javac** commands.
- **-classpath** and **CLASSPATH** should be set to the directory containing the package. If the package is in `/Users/user1/pkg1` then the class path should be `/Users/user1/Java` ???!!
- When you define a class in a package, you also need to execute it along with the package. If class Dawa is in pkg1, then the right command line to run it is `java pkg1.Dawa` rather than `java Dawa`.

## Access Protection:
- Packages do also control member visibility. 
- Generally speaking this is how access control works in a nutshell:
	* Anything declared **public** can be accessed by the whole world.
	* Anything declared **private** can only be accessed by other members of the same class.
	* A class with no modifier (default) is accessible by other classes in the same package and by subclasses.
	* If a class is declared **protected**, it is accessible outside the package to only its subclasses (in addition to being accessible within the package).
- The following table gives a detailed description of java's access control rules.

| | Private | No Modifier | Protected | Public |
| --- | --- | --- | --- | --- |
| Same class | Yes | Yes | Yes | Yes
| Same package subclass | No | Yes| Yes | Yes  
| Same package non-subclass | No | Yes| Yes | Yes  
| Different package subclass | No | No| Yes | Yes  
| Different package non-subclass | No | No| No | Yes   

- This table only applies only to class members. A non-nested class has only to choices, default and public. A public class is accessed by the whole world, while a default one is accessible package-wide.

## Importing Packages:
- Java core classes are placed in named packages.
- The **import** statements save a substantial amount of time and typing. Instead of qualifying every important method or class with the full package dot separated name, it's enough to do so once per file with the **import** statement.
- Imports can be done in the following two ways:
```java
import java.util.Date;
import java.io.*;
``` 
- The symbol `*` refer to all classes under the given package.
- All standard classes are stored in the **java** package. An important package is stored in this package called **java.lang**. This package has so much useful functionality that java automatically imports it implicitly to every program. 
- When two classes with the same name but from two different packages are imported with the star `*` form, you will get an compile error asking you to explicitly specify the class packages.
- **Imports** are just a convenience. You can always fully qualify classes with their full package name, but that would be extremely tedious.

## Interfaces:
- With an **interface**, you specify what a class must do but not how it does it.
- Interfaces are similar to classes but:
	* They generally declare empty methods that don't have bodies.
	* A class that implements the interface must implement all the methods declared in the interface. 
	* They don't have instance variables (obviously).
	* Variables defined inside an interface are implicitly **static** and **final**. These variables must be initialized and they can't be changed by the implementing classes.
	* All methods and variables in an interface are implicitly **public**.
	* An interface can be implemented by any number of classes.
- This paragraph is complicated. For a method to be called from one class to another, both classes must be present at compile time. This problem is not present when it comes to interfaces (I have no idea what this means, I am just writing it here coz I feel like I might be missing something important).

### Defining an interface:** 
- An interface definition is done as follows:
```java
 interface Daza {
	void wawa();
	int baba(int tata, String lala);
}
```
- Starting at JDK8, an interface now can actually define an implementation; the so called **default implementation** of interface methods. Interfaces are still used in their traditional form. More on default implementation can be found [here](#using-static-methods-in-an-interface).

### Implementing interfaces
- Implementing an interfaces has the following general characteristics:
	* If a class implements more than one interface they are separated by commas as in `Zaza implements Daza, Waawa, Dada { ...  }`.
	* Type signature of the concrete method must match its abstract interface counterpart.
	* Methods that implement the interface must be declared **public**.
	* If a class implements two interfaces which declare the same method, the same method will be used the class for either interface (I know, bad English). The following snippet causes no compile or run time error:
```java
interface Zaza {
	void lala();
}

interface Mama {
	void lala();
}

public class Calamata implements Zaza, Mama {
	
	public static void main(String[] args) {
		Calamata calamata = new Calamata();
		calamata.lala();
	}

	@Override
	public void lala() {
		System.out.println("Calamata");
		
	}	
}
```

### Accessing implementations through Interface References:
- Similar to how it's done with superclass references.
- Even though the object is an instance of the implementing class, because it's of type interface, it only has knowledge of the interface reference members. It has no knowledge of the concrete class members that are not defined by the interface.

### partial implementation:
- If a class doesn't implement all the methods of an interface, it must be declared **abstract**.
- Any class that inherit from this abstract class (which doesn't implement interface methods) must either implement all the interface methods or be declared **abstract**.

### Nested Interfaces:
- A **member interface** or **nested interface** is an interface defined inside a class or another interface. It can be private , protected or public, unlike a top-level interface which can only be public or default. Outside the enclosing scope, the nested interface must be qualified by dot and the enclosing class.
- I have no idea what the use of a nested interface is.

### Interfaces Can be Extended:
- Interfaces can inherit other interfaces through the use of the **extend** keyword just as classes inherit other classes.
- A class implementing an interface that inherits from other interfaces must provide the implementations of all the methods required by the interface inheritance chain.

## Default Interfaces Methods:
- **Default methods** or **extension methods** are implementations inside interfaces.
- The reason for adding default methods is to expand interfaces without breaking existing code, especially in popular interfaces that are used everywhere.
- Another motive for default methods is the ability to have optional methods that might not be needed in all classes implementing the interface. No there is no need to implement unneeded methods with empty placeholder methods.
- Default methods don't allow interfaces to maintain state. It must still be implemented by a class that can hold that state.
- Default methods are an answer to a specific problem. They are not the norms and the purpose of interfaces is still to define the what but not the how.
- The following example illustrates the use and syntax of default methods:
```java
interface Dada{
	void sasa();
	default void baba(){ // Use of default 
		System.out.println("BATATA");
	}
}

public class Zaza implements Dada {
	@Override
	public void sasa() {
		System.out.println("What??!!");
		
	}
	
	public static void main(String[] args) {
		Zaza zaza = new Zaza();
		zaza.baba();
	}
}
```

### Default Methods and Multiple Inheritance:
- Interfaces with default methods do effectively offer some very similar if not identical to multiple inheritance of behavior. This might cause some problems, though. If class C implements interfaces I1 and I2, what if both classes supply a method with the same name and type signature? What if one of the classes extends the other one? What if the class furnishes its own method? The rules to untangle these hairy complications are as follows:
	* If a class offers its own method, it simply override the interface methods.
	* If both interfaces have the same default method, an error occurs.
	* If the one interface inherits the other and both have the same default method, the class uses the inheriting interface.
	* You can explicitly refer to a specific interface default method using the keyword **super** with the following statement:
		*InterfaceName*.super.*methodName()*

## Using Static Methods in an Interface:
- JDK8 added the ability to define static methods in interfaces. These can be called independently of an object. No implementation of the interface is required to use these. AN interface static method is called by giving the interface name following by a period and the method name as in:
	*InterfaceName.staticMethodName*
- Static interface methods are not inherited by the implementing classes or other interfaces.

									=================

# Generics:
## Introductio ad Laudatorum:
- Generics, introduced in JDK5, have profoundly changed Java. They added a new clever syntactic element and they also changed how Java's core classes and methods were implemented. Understanding how generics work will make you a java superhero. 
- A generic allows the creation of a class, a method or a generic that works in a type safe way with several different data types. You define an algorithm once, independently of the data types it will work on, and then apply that algorithms to data of different types without added hassle. 
- Generics expressive power is undeniable and that can be seen in how they fundamentally changed Java's *Collections Framework.* Generics provided Collections with complete type safety.

## What are generics?
- Generics are ***parameterized types***. The importance of parameterized types stems from the fact that they allow you to create classes, methods and interfaces where type is supplied as a parameter.
- Before generics, Java used references of type **Object** which offered the ability to create generalized classes, methods and interfaces that work with different data types. The only problem, a serious problem, was that it lacked type safety. 
- Generics on the other hands offer type safety and they make it easier to create generalized classes, methods and interfaces. There is no need to cast **Object** to the specialized types being worked on. Generics do all that for you.







## A simple Generics Example:
- The following example gives the syntax of a very basic generic class:
```java
import java.util.ArrayList;

class Wawa<T>{ // T is a type parameter (will be replaced by real type.
	T ob;
	// An object of type t is passed to the constructor
	Wawa(T o) {
		ob = o;
	}
	
	void showType(){
		System.out.println(ob.getClass().getName());
	}
}

public class Zaza{
	public static void main(String[] args) {
		Wawa<String> wawa;
		wawa = new Wawa<String>("Ahmed");
		wawa.showType();
		
		Wawa<Thread> wawa2 = new Wawa<Thread>(Thread.currentThread());
		wawa2.showType();
		
		Wawa<ArrayList<String>> wawa3 = new Wawa<ArrayList<String>>(new ArrayList<String>());
		wawa3.showType();
	}
}
```
- A few things jump at one when examining this example
	* In `class Wawa<T>` **T** is the name of a **type parameter**. It is a place holder for the actual type which will be passed to the class when it's created. Type parameters are enclosed in angle brackets **`<>`**. Angle brackets immediately indicate you're dealing with generics.
	* The type parameter **T** is used to create an object **ob** *of type T*. The object **ob** will be of the type passed to **T**. If the type passed to **T** is an **Integer**, then **ob** will be of type **Integer**.
	* The actual generic will be created in the constructor. The constructor takes has parameter **o** of type **T**. Inside the constructor **ob** takes the value of **o**.
	* Type parameter **T** can also be used to specify a return type as is shown in the `getOb()` method.
	* The statement `Wawa<String> wawa` turn all references to **T** into type **String**.
	* instantiation in `wawa = new Wawa<String>("Ahmed");` must also include the type in angle brackets.
- The compiler doesn't create different versions of the Generic **Wawa**. Instead It removes generic type information (in a process called [*erasure*](#erasure)) and does necessary the casts, resulting in the specific needed type and just one generic.
- Generics only take reference types, hence [autoboxing](meta.md#autoboxing).



## A Generic Class with Two Type Parameters:
## The General Form of a Generic Class:
## Bounded Types:
## Using Wild Card Arguments:
## Creating a Generic Method:
## Generic Interfaces:
## Raw Types and Legacy Code:
## Generic Class Hierarchies:
## Type Inference with Generics:
## Erasure:
## Ambiguity Errors:
## Some Generics Restrictions:









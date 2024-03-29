# Exception Handling:
- Exceptions are run time errors.
- Some languages requires manual handling of exceptions which can be troublesome and tedious and error-prone. Java, on the other hand, gives you an oop mechanism to deal with such problems.

## Exception-Handling Fundamentals:
- A Java exception is an error. When an error occurs an exception object is created and **thrown** in the method that caused this error. That method can either handle the error or passed it down and then get **caught** at some point. 
- Exceptions are handled using five fundamental keywords: **try**, **catch**, **throw**, **throws**, **finally**.
- In a nutshell, If you want to check statements for errors, you enclose them in a **try** block. If an error occurs, it is thrown. The exception can be caught using the **catch** keyword.
- To manually throw an exception, **throw** is used.
- Exceptions thrown out of a method must be specified by a **throws** clause.
- **finally** is used to force the execution of code occurring after a try block even if an exception takes place.
- Handling exceptions follows this general form:
```java
try {
			
	} catch (Exception e) {
		// TODO: handle exception
	} catch (Exception e) {
		// TODO: handle exception
	} catch (Exception e) {
		// TODO: handle exception
	} finally {
		// TODO:dsdsdsds
}
```

## Exception Types:
- All exceptions are subclasses of the built-in class **Throwable**. This class is sublcassed immediately by two main types from which everything else is inherited:
	+ **Exceptions:** This is for exceptions that the user program should catch. Java programmer should extend this class to create her own exception classes. **RuntimeException** is a subtype of this class that automatically catches exceptions like division by zero or out of bounds indexes.
	+ **Error:** These are system errors. The program has no control of it.

## Uncaught Exceptions:
- When you don't handle a divide by zero exception, for example, the default handle takes care of it and prints lump of text on the console. The stack trace shows the sequence of method invocations that led to the exception. This is important for debugging.

## Using `try` and `catch`:
- Sometime or always, you want handle an exception on your own. You also want to prevent the program from terminating because of the exception. 
```java
public class Zaza{
	public static void main(String[] args) {
		int d = 0;
		int a
		try {
			a = 33 / d;
			System.out.println("What happened?");
		} catch (ArithmeticException e) {
			System.out.println("Can't divide, by zero");
		}
		
		System.out.println("a is: " + a);
	}
}
```
- Once an exception occurs, execution is transferred from the **try** block to the **catch** block.
- The program continues executing after exiting the catch block.
- **catch** and **try** blocks form a single unit. The scope of **catch** is restricted by the preceding **try** statement.
- A good **catch** statement should attempt to resolve the problem and the program should keep continue to run, so the result of division by zero for example could be given as a zero.

### Displaying a Description of an Exception:
- If you pass the exception (denoted with **e**) to a print method, you'd see a message describing the exception as in: 
```java
...} catch (ArithmeticException e) {
	System.out.println("Exception: " + e);
}...
```
- This is good for debugging and all.

## Multiple `catch` Clauses:
- When it's possible that multiple exceptions might occur, a single **try** statement is followed by multiple **catch** statement. When an exception happens, the catch statements are examined in order and when the problem matches a catch statement it's executed and execution jumps to the outside of the try-catch.
- In multiple catches, a subclass must precede its superclass, because obviously a subclass will never be reached which will result in an unreachable code error. It's a compile error. 

## `throw`:
- Try-catch catches exceptions thrown by the java run-time system, but your program can throw an error explicitly with the **throw** statement. 
- **throw** can only throw objects of type **Throwable** or one of its subclasses.
- Obtaining a **Throwable** object can be done in two ways:
	+ A parameter in a **catch** clause.
	+ Creating it with the **new** operator.
- After **throw**, the program stops and look for the nearest enclosing **try** statement and inspect the catch statement associated with it. If it doesn't find a match, the default exception handler takes care of the problem, print a stack trace and stops the problem.

## `throws`:
- **throws** throws an exception that it doesn't handle. The callers of the method are supposed to guard against against the exception.

## `finally`:
- When an an exception happens, normal flow is disrupted and a method might return prematurely and bypass some necessary code. This is especially problematic when it comes to working with external resources like databases or when a file is opened. When a method opens a file, it must closes it properly even if an exception occurs.  The keyword **finally** is used to enforce such an action. 

## Creating Your Own Exceptions Subclasses:
- To create your own exception class just subcless the **Exception** class. It has a bunch of methods you can use. You can also override these methods and add your own.

							========================================

# Enumerations
- Added in JDK5, Java's enumerations are richer than their counterparts in other languages. In Java, they can have constructors, methods and instance variables.. etc. 

## Enumeration Fundamentals:
- An enumeration is crated with the keyword **enum**:
```java
enum Days {
	Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, Sunday
}
```
- The names **Monday**, **Tuesday**, .. etc. are the **enumeration constants**. They are implicitly and must be static, final and public. Their type is the name of their enum which is **Days** here.
- A variable of an enum type can be defined. Even  though, enumerations are classes, you cannot instantiate them with the keyword **new**.
```java
Days day = Days.Monday
```
- The only values a variable of the enum type are the enumeration constants of that enum as the examble above shows.
- Two enumeration constants can be compared for equality with the equality operator as in `if (day == Days.Tuesday) { ...`.
- A switch statement can be controlled through the use of an enum constant value. Case statements must be constants of that same enum. They don't need to be qualified with the enum name:
```java
enum Days {
		Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, Sunday
	}

public class Zaza{
	public static void main(String[] args) {
		Days days = Days.valueOf("Monday");
		
		switch (days) {
		case Tuesday:
			System.out.println("Potato");
			break;
		case Wednesday:
			System.out.println("Batata");
			break;
		case Thursday:
			System.out.println("Pompitaire");
			break;
		default:
			System.out.println("Kartochka");
			break;
		}
	}
}
```

## `values()` and `vlaueOf()`:
- `values()` returns an array of the enum type. The array contains all the enum constants.
- `valueOf(str)` returns the enum constant whose  name matches the string argument.

## Java Enumerations are Class Types:
- They cannot be instantiated with the **new** operator, but enums are actual classes. They can have constructors, instance methods and variables and even implement interfaces.
- Each enum constant has its own copy of any instant of any instance variables of the enumeration. 
- The following code illustrates 3 actions that can be performed on an enum:
	+ **A constructor:** The same constructor is applied to the enum constants.
	+ **An instance method.** 
	+ **An instance variable.**
```java
enum Days {
	Monday('w'), Tuesday('w'), Wednesday('w'), Thursday('w'), Friday('w'), Saturday('h'), Sunday('h');
		
	private char workStatus;

	private Days(char work) {
		workStatus = work;
	}
		
	public char getWorkStatus() {
		return workStatus;
	}
}

public class Zaza{
	
	public static void main(String[] args) {
		Days day = Days.valueOf("Monday");
		System.out.println(day.getWorkStatus());
	}
}
```
- You can call the instance method in two ways:
```java
Days.Monday.getWorkStatus();
Days.valueOf("Monday").getWorkStatus();
```
- An enumeration can have multiple overloaded constructors and a default constructor that doesn't take arguments as in `Days(){ ... }`.
- **Restrictions** on enums:
	+ An enumeration cannot inherit another class;
	+ An enum cannot be a superclass.

## Enumerations Inherit Enum:
- Although enumerations can't be extended, they all inherit from the class **java.lang.Enum**. **Enum** defines three fundamental methods:
	1. **`ordinal()`:** gives the position of the enum constant  in the enum list.
	2. **`compareTo()`:** compares the ordinal ordinal positions of two enum constants and returns 0 if the same, -1 if lower position.. etc. 
	3.  **`equals()`:** compares two constants for equality.

						++++++++++++++++++++++++++++++++++++++++

# Type Wrappers and Autoboxing:   
## Type Wrappers:
- These are used to encapsulate primitive data types in objects that inherit **Object**. They are as follows:
	+ **`Character(char ch)`:** puts a primitive inside an object. To get the primitive you can use `CharValue()` which gives you a **char** type.
	+ **`Boolean(boolean b)`:** wraps and `booleanValue()` unwraps.
	+ **Numeric Types:** follow the same exact patter, so `Byte(byte b)`, `Double(double d)` wrap while doubleValue() and `byteValue()` unwrap.
- Numeric wrappers can construct a number from a primitive value or from a string.
- Wrapping is called **boxing** and unwrapping **unboxing**.
- Java seems to have deprecared boxing or certain constructors used for boxing since JDK9.

## Autoboxing:
- Since JDK5, boxing and unboxing are done automatically for you whenever such actions are needed, as the following example shows:
```java
Integer a = 44;
int b = a;
```
- Auto-(un)boxing occurs also in methods. A primitive argument passed to an object type parameter is automatically converted to an object. The same happens in a return statement. If the vlaue is **Integer**, but the method specifies an **int** as its return type, **Integer** is unboxed into an **int**.
- It also takes place in expressions as this shows:
```java
public class Zaza{
	public static void main(String[] args) {
		Integer a = 4, b = 9;
		int z = a + b; // a and b are automatically unboxed.
		System.out.println(z);
	}
}
```
- Auto-(un)boxing helps prevent errors.
- Primitives are still very important. Wrappers are much less efficient, and unboxing and boxing add much more unnecessary overhead.

						ooooooooooooooooooooooooooooooooooooooooo

# Annotations:
- An annotation doesn't change the semantics of a program. It's is used by some tools during development and deployment. 

## Annotation Basics:
- The following snippet defines a simple annotation:
```java
@interface Annotato {
	String lala();
	Int baba();
}
```
- Things to note:
	+ Annotations are based on the **interface**. 
	+ **@** signals an annotation. When coupled with @interface, it signals the declaration of an annotation.
	+ Annotations have only method declarations. These methods act like fields.
	+ All annotations extend the **Annotation** interface, but annotations can't extend anything.
	+ Once declared, a annotation is used to annotate whatever including other annotations. 
- Annotating something is done as follows:
```java
@Annootato(lala = "lala", baba="777")
public class Zaza{ ... }
```

## Specifying a Retention Policy:
- **Annotation Retention Policies** specifies when an annotation is to be discarded. They are three:
	+ **Source**: Only available in source code and is discarded during compilation.
	+ **Class**: Available in **.class** file but doesn't make it to the JVM.
	+ **RUNTIME**: stays during run time. It has the highest persistence.
- Retention policy is specified for an annotation by the **@Retention** annotation. If no retention policy is given, it defaults to **CLASS**.

## Obtaining Annotations at Run Time Using Reflection:
- Annotations are primarily intended for use by development and deployment tools, but if their retention policy is given as **RUNTIME**, they can be found by a java program during run time through the use of reflection.
- **Reflection** allows the obtaining of information about a class in run time. To get a class's annotation, first get its **Class** with the `getClass()` method. After you get **Class** you can get its information such as its methods, fields and annotations.
- The following program shoes how to capture information about a notation:
```java 
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;
import java.lang.reflect.*;

@Retention(RetentionPolicy.RUNTIME)
@interface Annotato {
	String lala();
	int baba();
}

class Matata{
	@Annotato(lala = "sasa", baba = 55)
	public void fafa() {
		System.out.println("Something");
	}
}

public class Zaza{
	public static void main(String[] args) {
		Matata matata  = new Matata();
		
		try {
			Class<?> c = matata.getClass();
			Method method = c.getMethod("fafa");
			Annotato anno = method.getAnnotation(Annotato.class);
			System.out.println(anno.baba());
		} catch (SecurityException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		} catch (NoSuchMethodException e) {
			// TODO Auto-generated catch block
			e.printStackTrace();
		}
	}
}
```
- `getMethods()` is somehow similar to the `getMethod(str)` method, but it gets a list of the annotations associated with a given class or method.

## The AnnotatedElement Interface:
- The **AnnotatedElement** interface located **java.long.reflect** defines the methods seen in the previous sections such as `getAnnotation()` and `getAnnotations()`. The purpose of this interface is to do reflection on annotations. It is implemented by classes **Method**, **Class**, **Constructor**, **Field**, **Package**. This interface has several other useful methods for handling annotations.

## Default Values:
- Annotation members can be given default values to be used if the member isn't given value. This is how default values are declared:

```java
@interface Annotato{
	String sasa() default "sasa";
	int baba() default 0;
}
```
- When using the annotation, you can leave the argument out, specify all of them or specify only some of them, so all the following statements are correct:
```java
@Annotato()
@Annotato(sasa = "wawa")
@Annotato(baba = 55)
@Annotato(sasa = "wawa", baba = 55)
```

## Marker Annotations:
- They are a special type of annotation. They have no members and they are solely used to mark things. Their mere presence is sufficient to signal something.
- When used, an annotation can be used without parentheses. They are actually required only when members need to be supplied.

## Single Member Annotations:
- If you have a single member value, you must name that member **value** and you don't need the word value when using that annotation as in:
```java
@interface Annotato{
	value() default ss;
}
// .... The following is how to use single member annotation.
@Annotato(777)
class Something {...}
```

## Built-In Annotations:
- Java has many built-in annotations, most of which are specialized, but 9 are general purpose. Four of these annotations are defined in the the **java.lang.annotation** package:
	+ **@Retention:** Specifies [retention policies](#specifying-a-retention-policy) and can only be used to annotate other annotations.
	+ **@Documented:** A marker annotation used to tell a tool that an annotation needs to be documented.
	+ **@Target:** It specifies the types of items to which an annotation can be applied. It takes one argument which is an array of constants of the enumeration **ElementType**. Example: `@Target({ElementType.METHOD, ElementType.TYPE})`.
	+ **@Inherited:** Can only be used on other annotations. It causes annotations on a superclass to be inherited by its subclasses.
- The five annotations defined in **java.lang** are:
	+ **@Override:** A marker annotations used only on methods to signal that a method must be overridden and not just overloaded.
	+ **@Deprecated:** A marker annotation used to signal that a construct is obsolete and replaced by a new one.
	+ **@FuncionalInterface:** A marker annotation to signal that an interface is indeed is a functional one. 
	+ **@SafeVarargs:** A marker indicating that there are no unsafe actions related to varargs occur. It is used to suppress warnings related to varargs??!!!!
	+ **@SuppressWarnings:** For ignoring warnings.

## Conclusion:
- The rest of the chapter seems a bit esoteric and too detached from what I think is useful at the moment. Might come back to this topic in the future.

	                      	ooooooooooooooooooooooooooooooooooooooooo

# I/O:
- Java I/O is not part of the language itself but is defined in its core API.
- Text-based console I/O is not important in Java (HS claims that!)
- However, Java provides excellent facilities concerning file and network I/O. 

## Streams:
- A stream is an IO abstraction. It either produces or consumes data. A stream is linked to a physical device. Streams act the same, regardless of how different the phsyical deviced they are linked to. These might be keyboards, networks, device files.. etc. The stream presents a unified abstraction for all these. Streams are defined in the **java.io** package.

## Byte Streams and Character Streams:
- Java provides two types of streams, **byte** and **character** streams. The former handles binary data, while the latter handle character I/O. Character streams are in unicode. They are convenient for characters and can even be more efficient than bytes in some cases. At the lowest level, all I/O is byte-based.

### The Byte Stream Classes:
- Byte streams are defined by two class hierarchies. At the top,we have **InputStream** and **OutputStream**. All byte streams have the words **InputStream** or **OutputStream** in them, which differentiates them from character streams.
- They define the methods **read** and **write**.

### The Character Stream Classes:
- Character streams are also defined by two hierarchies at the top of which stand the abstract classes **Reader** and **Writer** and they are designed to handle unicode characters. The classes derived from these also have several methods chief among which are **read** and **write**.

### The Predefined Streams:
- **java.lang** is always imported automatically to any program. One of the classes defined in in this package is **System** which has the 3 stream variables **in**, **out** and **err**. These are byte-based streams even they are used to IO characters. The following section discusses the use of **System.in**.

## Reading Console Input:
- This section does a great job demystifying the voodooish nature of java I/O.
- The dual nature of java I/O, bytes of characters is to blame.
- Console input goes through this steps:
	+ Console input is done with **System.in** (a byte-based input stream). It looks like this is the only way it's done.
	+ To get a character-based input stream attached to the console, **System.in** is wrapped in a **BufferedReader**. One of the commonly use constructors of **BufferedIReader** is `BufferedReader(Reader inputReader)`. Its parameter is of type **Reader**, a character-based stream, how do you fix this?
	+ One of **Reader**'s subclasses is **InputStreamReader** which converts bytes to characters through the following constructor `InputStreamReader(InputStream inputStream)`. The byte-based stream **System.in** is just that.
	+ The following snippet sums up the whole process:
```java
BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
```
- The following snippet shows how to use the console to print strings or lines of text:
```java
public class Zaza {
    public static void main(String[] args) throws IOException{
        String line;
        BufferedReader bReader = new BufferedReader(new InputStreamReader(System.in));
        do {
            System.out.println(line = bReader.readLine());
        } while (true);
    }
}
```

## The PrintWriter Class:
- **PrintWriter** is the preferred character-based method of writing to the console as opposed to the other byte-based methods. It make internationalization a breeze. 
- A commonly used constructor of the **PrintWriter** class is:
```
PrintWriter(OutputStream ops, boolean flushingOn)
```
- An example of the usage of PrintWriter:
```java
PrintWriter pw = new PrintWriter(System.out, true);
```

## Reading and Writing Files:
- Files can also be read either through byte or character streams. 
- Opening a file be done simply by creating an object of type **FileInputStream** or **FileOutputStream** and specifying the name of the file as an argument to their constructors as in:
```java
FileInputStream = new FileInputStream(String filename) throws FileNotFoundException;
FileOutputStream =  new FileOutputStream(String filename FileNotFoundException);
```
- After using a file, it must be closed. Failing to do so results in so-called memory leaks, because closing a file releases system resources allocated to the file, allowing them to be used by another file. This is done with the `close()` method available in both **FileInputStream** and **FileOutputStream**. You call the close method explicitly. A new way of closing file, added in JDK7, is the [**try with resources**](#automatically-closing-a-file) statement, with which Java closes the file automatically when it's no longer needed.
- The following snippet reads a text file:
```java
import java.io.*;

public class Zaza{
	public static void main(String[] args) throws IOException{
		int i;
		FileReader fi = new FileReader("/Users/someuser/somefile.txt");

		do {
			i = fi.read();
			if (i != -1) 
				System.out.print((char) i);
		} while (i !=  -1);
		
		fi.close();
	}
}
```
- It's advisable to surround every IO statement with a try-catch statement and enclose the **close** statement in a **finally** block.
- To copy a file, you can simply write **i** variable into a **FileWriter** or a **FileOutputStream**.

## Automatically Closing a File:
-JDK7 added the so-called *automatic resource management.* It's based on an extended try statement. It closes a file automatically when it's not needed anymore.
- The basic syntax is as follows:
```java
try(FileReader fi = new FileReader("/Users/someuser/somefile.txt")){
	......
} catch {
	....
}
```
- You can have more than one resources separated with semi-columns.


	                     	ooooooooooooooooooooooooooooooooooooooooo

#Other:
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
- Added in JDK5, Java's enumerations are richer than their counterparts in other languages. 

# Autoboxing
# Annotations:
# I/O and Other Stuff:
## Using instanceof:
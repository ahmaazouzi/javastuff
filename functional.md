# Lambda Expressions:
- Introducing **lambda expressions** in JDK8 had a fundamental impact on java similar to that of generics. They added syntactic sugar that improved the expressive power of the language and eliminated some clunkiness of existing constructs. They also allowed for a better use of multi-core parallelism in the Java API, especially through the for-each operations and the *stream API*.

- [Introducing Lambda Expressions](#introducing-lambda-expressions)
	+ [Lambda Expression Fundamentals](#lambda-expression-fundamentals)
	+ [Functional Interfaces](#functional-interfaces)
	+ [Some Lambda Examples](some-lambda-examples)
- [Block Lambda Expressions](#block-lambda-expressions)
- [Generic Functional Interfaces](#generic-functional-interfaces)
- [Passing Lambda Expressions as Arguments](#passing-lambda-expressions-as-arguments)
- [Lambda Expressions and Exceptions](#lambda-expressions-and-exceptions)
- [Lambda Expressions and Variable Capture](#lambda-expressions-and-variable-capture)
- [Method References](#method-references)
- [Constructor References](#constructor-references)
- [Predefined Functional References](#predefined-functional-references)

## Introducing Lambda Expressions:
- Understanding lambda expressions and how they work depends on understanding two fundamental Java constructs:
	+ ***Lambda expressions (closures):*** They are anonymous methods used to implement a method defined by a functional interface.
	+ ***Functional interfaces:*** A functional interface contains only one abstract method which does one single action. It defines the *target type* of a lambda expression. A lambda expression absolutely requires a target type to exist.

### Lambda Expression Fundamentals:
- A lambda expression is divided into two parts by an **arrow operator**, also called a lambda operator **`->`**. The left side of the operator is reserved for parameters. When there are no parameters it stays empty. The right side of the expression specifies **lambda body** the actions to be performed by the expressions. The lambda body can consist of either a single expressions or a block containing a series of expressions.
- Examples:
```java
() -> 1000  // This is the same as the method in next line
double func() { return 1000 };

() -> Math.random() * 32

(a) -> a > 10 
```
- The following example defines a functional interface which has one and only one abstract method:
```java
interface Lala {
	void baba();
}
```
- A lambda expression is not executed on its own. Instead, it forms the implementation of the abstract method of the functional interface that defines its target type.

### Functional Interfaces:
- A functional interface is one that defines one and only one abstract method.
- A lambda expression can be defined only in a context where a target type exists. Contexts where a target type are defined include the following and more:
	+ When a lambda expression is assigned to a functional interface reference.
	+ Variable initialization.
	+ Return statements.
	+ Method arguments.
- 
```java
interface Baba{
	void matata();
}

public class Zaza{
	public static void main(String[] args) {
		Baba baba;
		baba  = () -> System.out.println("batata");
		baba.matata();
	}
}
```
- When the lambda expression is executed, a class implementing the functional interface is created automatically. The lambda function defines the behavior of the abstract method of the functional interface.
- Obviously, the types and numbers of arguments as well as the return type of the lambda expressions must match those of the abstract method declared in the functional interface.

### Some Lambda Examples:
- a lambda with a single parameter doesn't have to enclose that parameter in parantheses. Both of the following examples are valid:
```java
(n) -> 1234
n -> 1234
```
- Types of parameters are optional, but not needed really. The following two expressions are the same:
```java
(int i) -> i * 400
(i) -> i * 400 
```
- If you specify the types of parameters in a list of parameters, you must do it for all parameters as in:
```java
(n, m) -> n > m // valud
(int n, int m) -> n > m // valid. Same as previous expression
// (int n, m) -> n > m // Absolutely invalid.
```

## Block Lambda Expressions:
- As mentioned before a lambda can have a single expression in its body, in which case it's usually called an ***expression lambda***. In a ***block lambda***, on the other hand, the body consists of a block of statements. There are no mysteries about block lambdas. They allow you do a lot of things: loops, conditionals.. etc. The only thing that differentiates them from expression lambdas is they are enclosed in a block (hence the name) and must have a return statement. 
```java
(something) -> {
	statement1;
	statement2;
	statement3;
	return something;
}
```
- Makes sense: a return statement in a lambda only causes a return from the lambda expression and NOT from the enclosing method.

## Generic Functional Interfaces:
- For some reason a lambda expression cannot be a generic, but the functional interface associated with it can be a generic. The functional interface takes care of the type parameter translation into a specific type.
- The following example summarizes everything that you need to know about generic functional interfaces and their use with lambdas:
```java
interface Baba<T>{
	T matata(T t);
}

public class Zaza{
	public static void main(String[] args) {
		Baba<String> strDouble = (str) -> str + str;
		System.out.println(strDouble.matata("java"));
		Baba<Integer> intDouble = (intVal) -> intVal * 2;
		System.out.println(intDouble.matata(99));
	}
}
```

## Passing Lambda Expressions as Arguments:
-

## Lambda Expressions and Exceptions:
-

## Lambda Expressions and Variable Capture:
-

## Method References:
-

## Constructor References:
-

## Predefined Functional References:
-



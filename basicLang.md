# Types:
## Java Primitives:
- Java has 8 primitive types that can be grouped in the following 4 groups:
	- **Integers:** These are **byte**, **short**, **int** and**long**.
	- **Floats:** including **float** and **double**
	- **Characters:** **char**. 
	- **Booleans:** **boolean**.
- Without these primitives, Java would be 100% object-oriented. Java chose to keep these primitive to conserve the performance that would've been severely degraded if these were made into java objects. 
- Java primitives ranges are strictly defined so they are the same in every system, making them much more portable than say C++ primitives though this has some effect on the performance. 

## Integers:
- All java integer types are signed. The width and range of an integer is more about its behavior rather than the storage space it occupies. These are the four integer types along with their width and how they are used:
	- **byte** (8): They are use to transfer stream data from a file/network and raw data not compatible with java types.
	- **short** (16): Least used java data type.
	- **int** (32): Most used type. Also used as array indexes and in loops. shorts and bytes get promoted so there is no point in using them instead of `int`'s in loops and array indexes. 
	- **long** (64): Used for freakishly big numbers instead of `int`'s.

## Floating Types:
- Includes the following two types:
	- **float** (32): not very useful where precision is sought, although faster in some processors and takes less space.
	- **double:** (64): More precise than floats, maintains high accuracy over many	calculations and is faster in some modern processors, because were optimized to work with it.

## Chararacters: 
- Denoted by **char** (16) which is not the same as C/C++ chars which are only 8 bits wide. Java uses ***unicode*** by default. You can use chars to do integer calculations as well, but why dude?!!

## Booleans:
- They are a type of their own. 
- `if (a == true) ..` is the same as `if (true) ..`.
- The output of a relational operator such as `a > b` is a boolean.
- While an expression like `(5 > 2) + 3` equals 4 in languages like javascript and probably C as well, it doesn't add up in Java.

## Literals:
### Integers:
- Java represents literal decimal values but can also represent octal values which are preceded by `0`'s such as `05` and `04`. `09` produces an out of range error.
- Hexadecimal values are preceded by `0X` or `0x` as in `0X4`, `0xF`, `0XF`, `0Xa`.
- Starting in Java 7, binaries can also be represented by being preceded `0b` or `0B`. Examples include `0b111`, `0B101`. Binary literals are useful for bit masking and bitwise operations.
- Literals create an **int** value. When it is assigned to a **byte** or a **short**, no error occurs if the literal is within the range of these types. Because any integer can fit inside the range of a **long**, no error occurs when this literal is assigned to it.
- To specify a literal **long** append and `l` or `L` to it as in `12343124343L` or `54343l`.
- underscores can be embedded in numbers making them easy to read such as `12_203` or `2_232_3_23_232_322L`. Underscores are only used to separate numbers and can't be at the beginning or end of a number. Two or more underscores can be stringed together as in `9_____2`. These can be useful in grouping binaries in groups of 4 which is amazingly useful.

### Floating Point Literals:
- Floating point literals can be represented in two ways:
	- **Standard notation:** such as `0.4`, `222.222`.
	- **Scientific notation:** Uses standard floting notation suffixed by an `e` or an `E` followed by a power of 10 with which the number is multiplied. `2e1` is the same as `20` while `5E-2` is the same as `0.05` and `3.3e1` equals `33.0`.
- Floating literals default to **double**. To specify a `float` literal append it by an `f` or `F` as in `0.55F` or `22e-1F`. A double can also be explicitly specified by appending a `d` or `D` to the literal but this is redundant.
- Hexadecimal literal floating point numbers are also in use, although extremely rarely. It is restricted to a format similar to scientific notation where upper or lower `P` replaces `E` for the exponent as in `0XFP1`. `0x0.3` is wrong.
- Floats can also have underscores in java 7 and after following the same rules as in `2_3.4_4`, but underscores can only fall between two digits. `2_._2` is wrong.

### Booleans:
- They can't be converted into any numerical representation. `true` doesn't equal **1** and `false` doesn't equal **0**.

### Character Literals:
- Characters are 16 bit values that can be converted to integers and manipulated with integer operators. 
- Characters, unlike strings, are wrapped in single quotes as in `'a'`, `'b'`, `'3'`.
- For impossible to enter characters use a backslash as in `'\''` and new line `'\n'`.
- Characters can also be entered directly as octals or hexadecimals as in:
	- **Octal**: inside single quotes a backslash followed by 3 digits as in `'\107'` which is the same as `'G'`.
	- **Hexadecimal**: inside single quotes put a `\u` followed by exactly 4 digits as in `'\u3333'`.

### String Literals:
- String literals are enclosed inside double quotes.
- They can also use hexadecimal and octal representations as in [characters](#character-literals).
- Sadly, as of java 8, strings must start and end on the same line. There is no line-continuation escape sequence as in Python, for example. 

## Variables:
- A variable is defined by an identifier, a type and an optional initializer.

### Variable Declaration:
- A java variable follows this general form:
```
type identifier = [ = value][, identifier[=value] ...];
```
- Type can be one of the primitive types seen so far. It can also be the name of a class or an interface. 
- Most importantly, the type must match the value. `int what = "What!"` is just WRONG!!

### Dynamic Initialization:
- Initializing a variable can be done with either a constant or dynamically. A variable can be initialized to the result of a calculation, an expression, a method.. etc.

### Scope and Lifetime of a Variable:
- In addition to grouping multiple statements into a single logical unit, **blocks in java also have scope**. javascript blocks, for example, has no scope.
- The following example illustrates some aspects of how block scoping works:
```java 
public class Blockade {
	public static void main(String[] args) {
		int a = 1, b, c = 2;
		
		System.out.println("c was: " + c);
		
		// a block 
		{
			System.out.println(a); // Variables defined outside the block are visible inside it.
			b = 4; // A variable defined outside can be initialized inside the block.
			c = 15; // The value of an outer variable can be changed inside the block.
			int d = 5;
			System.out.println(d); // d is visible inside the block but not outside of it.
		}

		System.out.println("c has changed to: " + c); // value changed inside the block.
		System.out.println(b); // b was initialized inside the scope.
		// This is wrong. d is not available in this scope
		// System.out.println(d);
		// Wrong. 3 hasn't been initialized
		// System.out.println(e);
	}
}
```
- Scope defines the visibility of objects to other parts of a program. It also determines the lifetime of an object. 
- Java has a class and a method scope. This section is about method scope only. The scope of a methods with its opening curly brace and ends with the closing one. Parameters are also part of the method's scope.
- Variables defined inside a scope are not visible outside it. It's localized/protected against unauthorized use by the outside the world. This is the basis of encapsulation. Scopes can be nested and while inner scopes can see variables in outer scopes, the reverse is not true.
- A variable is only valid after it's declared. A variable declared at the end of a block or a method is useless.
- A variable is created when its scope is entered and is destroyed when execution leaves that scope. the lifetime of a variable is circumscribed by its scope.
- If a variable is initialized inside a block, it's reinitialized every time the block is entered (think of a loop block).
- Obviously, you can't declare a variable inside an inner scope when a variable with the same name is in the outer scope.

## Type Conversion and Casting:
- Java performs automatic type conversion between compatible types. Between incompatible types, the user can explicitly perform this conversion through **casting**.

### Automatic Conversion:
- Automatic conversion happens when:
	1. The two types are compatible.
	2. The destination type is larger than the source type.
-  If these two conditions are met, a widening conversion occurs. an int is automatically converted into a long. 
- Automatic conversions occur between numeric types, but no automatic conversions from numeric types to chars or booleans take place. No automatic conversions occur between chars and booleans either. 

### Casting:
- Casting is used to perform narrowing conversions. With casting you can convert a larger type into a smaller type as in
```
int a = 500;
byte d;
d = (byte) a;
```
- When you convert a floating point type into an integer type, the value gets truncated, meaning the fractional part is lost. 
- If the value is too big for the destination type, the value is reduced modulo the destination type's range as in:
```
int a = 257;
byte = (byte) a;
// byte now is 1
```
- You can even cast a literal, although I have no idea what the value would be.

## Automatic Type Promotion:
- In expressions, sometimes the intermediate value of an operation is bigger than the range of either operand. To fix this, java automatically promotes **char**, **byte** and **short** into **int** during the evaluation of an expression. 
- This automatic promotion can cause really weird problems as in: 
```
byte b = 3;
b = b + 2;
// This causes a compile time error.
```
- Java asks you to cast the value back into a byte. Be careful about overflow consequences!

### Type Promotion Rules:
- Type promotion follows these rules:
	* All **byte**, **char** and **short** are converted into **int**.
	* If one of the the two operands is **long**, the whole expression is promoted to **long**.
	* If one of the two operands is a **float**, he whole expression is promoted to **float**.
	* If any operand is **double**, the whole expression becomes a **long**

## Arrays:
- Declaring an array can be done be done with either one of the two following ways:
```
int month_days[];
int[] month_days;
```
- `int month_days[] = new int[12]` declares and creates a new array. Numeric elements in such an array are initialized to zeros, booleans to false, and reference types to nulls.
- The keyword `new` allocates memory for the given array.
- You can also use an array literal or what they call an array initializer as in :
```java
int days[] = {1, 2, 3, 4, 5, 5};
```
- Java's runtime checks if you're trying to access an element outside the range of the array.

### Trivia About Arrays:
- Passing a literal array as a method's argument can be done this way (weird!!!:
```java
void methoda(new int[] {1 ,2 ,3 ,4}) {
	...
}

```
- The alternative array declaration syntax can be useful in some cases, especially when declaring multiple arrays on the same line as in:
```java
int[] nums1, nums2, nums3, nums4; // This is cooler.
int nums1[], nums2[], nums3[], nums4[];
```

## Strings:
- Strings are neither primitives nor mere arrays of characters. They are objects and understanding how they work requires understanding objects and classes.
- Strings have a lot of characteristics making them very powerful and easy to use.

# Operators:
 - All operators are described here except for: **instanceOf** and the arrow operator `->`.

## Arithmetic:'
- Two slightly unfamiliar operators are:
	- **`%=`** modulus assignment (this one is especially weird).
	- **`*=`**: multiplication assignment.
- The unary minus can be used with a variable name. I didn't know that:
```java
int a = -4;
b = -a; // b is equal to 4
```
- Dividing integers yields no fraction, resulting in a rounding down.
- **Increment/Decrement:***  *prefix* and *postfix* incrementation/ decrementation have a subtle difference for which I have no use case yet. `a = ++b` is equal to `a += 1; a = b`, while `a = b++` is equal to `b = a; b += 1`.

## Bitwise:
- I don't remember a single time having to use these apart from language books and exercises and job interview preparation material.

| Character | Description
| --- | --- |
| `~` | bitwise unary NOT
| `&` | ... AND
| `\|` | ... OR
| `^` | ... Exclusive OR
| `>>` | ... shift right
| `>>>` | ... shift right zero fill
| `<<` | ... shift left
| `&=` | ... AND assignment
| `\|=` | ... OR assignment
| `^=` | ... Exclusive OR assignment
| `>>=` | ... shift right assignment
| `>>>=` | ... shift right zero fill assignment
| `<<=` | ... shift left assignment

- Bitwise operators work on integral types: **byte**, **char**, **short**, **int** and **long**.
- Making effective use of bitwise operators depends on a good understanding of how java represents negative values. All integer types are signed except for **char**. It is based on ***two's complement*** encoding. To get the negative of a number invert all its bits and add 1 to it. Two's complement eliminates negative zero which is an invalid integer. 
- The most important fact to remember is that the leftmost bit defines the sign of a number. **1** is for negative and **0** for positive. 
- The beauty of math is in the fact that a few rules appear everywhere. The behavior of bitwise NOT, OR, XOR.. etc. is very similar to to boolean operators if not identical so  there is point in repeating all that here.  basically the unary NOT operator inverts a bit; the OR operator results in 1 if one or two operands are 1 ... etc.

### Left Shift
- Shifts bits to the left a specified number of times as in:
```java
value << shift_times
```
- High order bits are lost and zeros fill the right.
- Because java always performs automatic promotions with in expressions, results of left shifting on values of these types must be recast back to the original types.
- Left shifting is an efficient way of doubling a number, but it should be done with care as shifting into the high-order bit DOES makes the value negative.

### Right Shift:
- Same as left shifting but in the opposite direction. In a process called *sign extension*, the leftmost position are filled with the high-order bit, so if the value is negative the left is filled with ones and if positive it's filled with zeros.

### Unsigned Shift Left:
- This is used when there is no need for preserving the sign. It's frequently used in graphics and pixel manipulation and can be done with the unsigned left shift sign `>>>`. I think this largely useless and I might never have to used.

## Relational Operators:
- They determine relations between operands like equality and ordering. The outcome is a boolean and they are used mainly to control **if** statements.
- `if (!done)` is not equivalent to `if (done == 0)`. It's meaningless.

## Boolean Logical Operators:
- Interesting among these is so-called **short-circuit** logical operators. It is customary to use the short circuit **`&&`** and **`||`** and leaving the other **`&`** and **`|`**  to be used only in bitwise operations.

## The ternary ?: operator:
- It is used to assign a value to a variable based on a condition:
```
char a = 5 > 2 ? 'y': 's';
```

## Precedence and Parentheses:
- Operators have different levels of precedence. Google you a precedence table!! 
- To avoid precedence issues and to explicitly set it and control it, use parentheses. parentheses, including redundant ones also help clarify the meanings of complicated long expressions.
- Parentheses don't cause any performance issues, so USE them!








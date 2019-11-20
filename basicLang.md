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
- Characters, unlike strings, are wrapped in single quotes as in `a`, `b`, `3`.
- For impossible to enter characters use a backslash as in `'\''` and new line `'\n'`.
- Characters can also be entered directly as octals or hexadecimals as in:
	- **Octal**: inside single quotes a backslash followed by 3 digits as in `'\107'` which is the same as `'G'`.
	- **Hexadecimal**: inside single quotes put a `\u` followed by exactly 4 digits as in `'\u3333'`.

### String Literals:
- String literals are enclosed inside double quotes.
- They can also use hexadecimal and octal representations as in [characters](entered-directly-as-octals).
- Sadly, as of java 8, strings must start and end on the same line. There is no line-continuation escape sequence as in Python, for example. 

## Variables:

## Type Conversion and Casting:

## Automatic Type promotion:

## Arrays:

## Strings:

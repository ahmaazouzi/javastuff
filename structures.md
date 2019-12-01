# Built-In Structures:
- Java has a bunch of built-in data structures that can be used for all purposes. This will be a quick review of some of these structures, their characteristics and special features:

## Strings:
### String Object vs. String Literal:
String literal differs from a **String** object (one created with the **new** operator) in that **String**literals reside in a **common pool** while string objects live in the **heap**. In the following example:
```java
String s1 = "hello";
String s2 = "hello";
String s3 = "hello";
```
- All three variables s1, s2 and s3 point to the same object "hello". String literal variables are "not reference variables". This is more efficient memorywise. Different strings share the same resources.
- The following example is different:
```java
String s4 = new String("hello");
String s5 = new String("hello");
```
- variable s4 and s5 point to completely different objects. They are reference variables.

### String Immutability:
- Strings are also immutable. Because the **common pool** mechanism allowing for multiple variables to point to the same string object, it would be unwise to modify a string. Obviously, a change to a string means a change of the values of all other variables that point to the same string. When you modify a string variable, what happens is that a totally new String object is constructed and the variable points to this new object. If the old object is still referenced by other variables, it stays in the common pool, otherwise, it is deallocated.
- **StringBuffer** and **StringBuilder** can be used to handle strings that change frequently.

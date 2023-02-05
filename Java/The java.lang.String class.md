#java #classes #frequently-used

Previous [[Variables]]

---
# String
Firstly let's import it at the top of the file like so:

```java
import java.lang.String
```

The *String* class implements *serializable, comparable, CharSequence* interfaces
You can create a string by using double quotes:
```java
String s = "hello";
```

Each time you create a string literal, the JVM checks the *string constant pool* first, if the string already exists in the pool, a reference to the pooled instance is returned, otherwise a new string instance is created and placed in the pool.

```java
String s1 = "Hello";
String s2 = "Hello"; --> It does not create a new instance
```

Alternatively, it can be created using the `new` keyword.

| Method                                                                  | Description                                                               | Exception                                                                           |
| ----------------------------------------------------------------------- | ------------------------------------------------------------------------- | ----------------------------------------------------------------------------------- |
| `char charAt(int index)`                                                | Returns the char value for *index*                                        | Throws `StringIndexOutOfBoundsException` if the index is -1 or greater than str len |
| `int length()`                                                          | Returns the length of the string                                          | N/A                                                                                 |
| `static String format(String format, Object ..., args)`                 | Returns a formatted string                                                |                                                                                     |
| `static String format(Locale l, String format, Object ... args)`        | Returns a formatted string given a locale                                 |                                                                                     |
| `String substring(int beginIndex, <Optional> int endIndex)`             | Returns a substring for given begin index                                 |                                                                                     |
| `boolean contains(CharSequence s)`                                      | Returns `true` or `false` after matching the sequence of char value       |                                                                                     |
| `static String join(CharSequence delimiter, CharSequence ... elements)` | Returns a joined string                                                   |                                                                                     |
| `boolean equals(Object another)`                                        | Checks the equality of string and given obj                               |                                                                                     |
| `boolean isEmpty()`                                                     | Checks if string is empty                                                 |                                                                                     |
| `String concat(String s)`                                               | Concatenates the specified string with s                                  |                                                                                     |
| `String replace(char old, char new)`                                    | Replaces all occurrences of the specified char value                      |                                                                                     |
| `String replace(CharSequence old, CharSequence new)`                    | Replaces all occurrences of the specified CharSequence                    |                                                                                     |
| `static String equalsIgnoreCase(String another)`                        | It compares another string without checking *case*                        |                                                                                     |
| `String[] split(String regetx, <Optional> int limit`                    | It returns a split string matching regex and limti                        |                                                                                     |
| `String intern()`                                                       | Returns an interned string                                                |                                                                                     |
| `int indexOf(int ch, ?int fromIndex)`                                   | Returns the specified char value index starting from *fromIndex* if given |                                                                                     |
| `int indexOf(String substring, ?int fromIndex)`                         | Returns the specified substring index starting with given index if given  |                                                                                     |
| `String toLowerCase(?Locale l)`                                         | Return a string lowercase using locale if specified                       |                                                                                     |
| `String toUpperCase(?locale l)`                                         | Return s string uppercase using locale if specified                       |                                                                                     |
| `String trim()`                                                         | Removes beginning and ending spaces of string                             |                                                                                     |
| `static String valueOf(int value)`                                      | Converts given type into string                                                                          |                                                                                     |

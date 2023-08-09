# Core Java Quick Dive

For full documentation visit [mkdocs.org](https://www.mkdocs.org).

## Core Language


### DataTypes
- Primitive
    - **int** whole number (4 bytes)
    - **long** whole number (8 bytes)
    - **double** decimal numbers (8 bytes)
    - float decimal numbers (4)
    - short whole numbe 2 bytes
    - byte 1byte
    - char 2 bytes
- Non Primitive 
    - String
    - Array (Collection of **similar** data types)
    - Class 
        - Blue print for creating objects by providing initial values for state(variables) and implmentations of behaviour(methods)
    - Interface
        - An inteface is a collection of abstract(existing only as an idea, not as a physical thing) methods
    - Enum
        - To define **set of named values**
    - Record
        - To define a carrier of data (mostly variable data) 

``` java title="DataTypes.java" linenums="1" hl_lines="3-10"
public class DataTypes {
    public static void main(String[] args) {
        int a = 10;
        long b = 123343L;
        double d = 123.098;
        float f = 345.09f;

        String str = "Hello world";
        String[] names = {"Bob","john"};
        int[] numbers = {1,2,3};
    }
}
/*By default it will be int or double, to make sure they take proper data types we mention L and f */
```

### Wrapper Classes
    `Integer, Long, Char, Float, Double`

```java
/* All Java Wrapper classes are **public and final**
 All wrapper classes are immutable i.e we can not change object state
 All are thred safe*/
    public final class Long extends Number
        implements Comparable<Long>, Constable, ConstantDesc {
            ....
        }
```
- Java5 introduced WrapperClasses to handle data in collections. In collections we cant create List<int>, it should be List<Integer>.

```java
   -- Constructor
   int number=10;
   Integer intWarpper = new Integer(number);
   Integer number = 123; //Autoboxing -An int automatically wrapping into Integer object
```
### String
#### Immutable
   

Effective Java by Joshua Bloch outlines several reasons to write immutable classes:

- Simplicity - each class is in one state only
- Thread Safe - because the state cannot be changed, no synchronization is required
- Writing in an immutable style can lead to more robust code. Imagine if Strings weren't immutable; Any getter methods that returned a String would require the implementation to create a defensive copy before the String was returned - otherwise a client may accidentally or maliciously break that state of the object.
In general it is good practise to make an object immutable unless there are severe performance problems as a result. In such circumstances, mutable builder objects can be used to build immutable objects e.g. StringBuilder
- Hashmaps are a classic example. It's imperative that the key to a map be immutable. If the key is not immutable, and you change a value on the key such that hashCode() would result in a new value, the map is now broken (a key is now in the wrong location in the hash table.).
- **Immutable strings and things** [Oracle Blog](https://blogs.oracle.com/javamagazine/post/java-immutable-objects-strings-date-time-records)
- In the beginning, there was Java 1.0, and within it there was the String class. The String class is final and has no mutator methods. Once a string has been constructed, it never changes. Methods that in some languages might change the string, such as toUpperCase(), in Java create a new String with the desired changes applied. A String is immutable, period, full stop (unless you bring in some native code using JNI to modify one).

- The need for immutable String objects was clearly understood by the team who created Java: If String objects could be modified, Java’s entire security model would be broken. Here’s a sketch of one potential attack.
``` java
Good Thread: Open File xyz.
  InputStream Constructor; call security manager.
    Security manager - Read file xyz - Permission is OK.
Bad Thread wakes up at just this moment.
  Changes file name string from 'xyz' to '/etc/passwd'
  Yields the CPU
Good Thread
  InputStream Constructor: pass /etc/passwd to operating system open syscall
Bad Thread examines memory buffer for useful information to steal
```
- Furthermore, the immutability of String objects can lead to better multithreaded performance, as these objects do not require synchronization or checking when used in multithreaded code. The application, and the JVM, can take for granted that a String object’s value will never change.
Some `code` goes here.

### Plain codeblock

A plain codeblock:

```
Some code here
def myfunction()
// some comment
```

#### Code for a specific language


#### Highlighting lines

``` java title="bubble_sort.py" linenums="1" hl_lines="2 3"
def bubble_sort(items):
    for i in range(len(items)):
        for j in range(len(items) - 1 - i):
            if items[j] > items[j + 1]:
                items[j], items[j + 1] = items[j + 1], items[j]
```

## Icons and Emojs

:smile: 

:fontawesome-regular-face-laugh-wink:

:fontawesome-brands-twitter:{ .twitter }

:octicons-heart-fill-24:{ .heart }
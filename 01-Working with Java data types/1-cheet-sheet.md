
- Java is a statically typed language. This means that the data type of a variable is defined at compile time and cannot change during run time.

- Java has primitive and reference variables. The Java compiler and JVM inherently know what primitive types mean, while reference data types are built by combining primitive data types and other reference data types.

- Primitive data types are shown below:

Date Type	Size	Description	Sample
byte	1 byte	-128 to 127	-1, 0, 1
short	2 bytes	-32,768 to 32,767	-1, 0, 1
int	4 bytes	-2,147,483,648 to 2,147,483,647	-1, 0, 1
long	8 bytes	-9,223,372,036,854,775,808 to 9,223,372,036,854,775,807	-1, 0, 1
float	4 bytes	Stores fractional numbers. Sufficient for storing 6 to 7 decimal digits	1.1f, 2.0f
double	8 bytes	Stores fractional numbers. Sufficient for storing 15 decimal digits	1.1d, 2.0d
boolean	1 bit	Stores true or false values	true, false
char	2 bytes	Stores a single character	'\u0000', 'a'
Wrapper classes exist for Byte, Short, Integer, Long, Float and Double.

- Reference types include:

  Classes
  Interfaces
  Enums

- A variable contains a raw number and assigning one variable to another simply copies that number from one variable to another. Java uses pass by value semantics.

- Java initialises all static and instance variables of a class automatically if you do not initialise them explicitly. You must initialise local variables explicitly before they are used.

- Assigning a smaller type to a larger type is known as implicit widening conversion as no cast is required. To assign a larger type to a smaller type, for a compile time constant (i.e., final) the compiler will automatically narrow the value. If the source variable is not a constant then a cast is required, this is known as explicit narrowing. Determining the value that will be assigned when doing an explicit can be complicated.

- A String is an object of class java.lang.String. String is a final class and implements java.lang.CharSequence. String is immutable so the value cannot be changed after instantiation.

- A String can be instantiated using:

  ```
  String myString = new String();
  String myString = new String("example");
  String myString = "example";
  String myString = new String(StringBuilder sb);
  String myString = new String(byte[] bytes);
  String myString = new String(char[] value);
  String myString = s1 + "add";
  ```

- String concatenation can occur with the += operator if one of the operands is a String.

- Strings created without using the new keyword are kept in the string pool. If a String is created without the new keyword and the same string already exists in the string pool, then a reference to the existing String will be returned.

- Useful String methods include:

  ```
  int length();
  char charAt(int index);
  int indexOf(int ch);
  String substring(int beginIndex, int endIndex);
  String substring(int beginIndex);
  String concat(String str);
  String toLowerCase();
  String toUpperCase();
  String replace(char oldChar, char newChar);
  String strip();
  String stripLeading();
  String stripTrailing();
  String trim();
  ```

- Note that in the substring methods the ending index is exclusive, and the starting index is inclusive.

- Useful methods for inspecting a String include:

  ```
  boolean isBlank();
  boolean isEmpty();
  boolean startsWith(String prefix);
  boolean endsWith(String suffix);
  boolean contains(CharSequence s);
  boolean equals(Object anObject);
  boolean equalsIgnoreCase(String anotherString);
  ```

- java.lang.StringBuilder is the mutable twin of java.lang.String. StringBuilder is also a final class and implements java.lang.CharSequence. StringBuilder is better suited for creating temporary strings that have no use once a method ends.

- StringBuilder provides several constructors:

  ```
  StringBuilder();
  StringBuilder(CharSequence seq);
  StringBuilder(int capacity);
  StringBuilder(String str);
  Note that the default size for the no argument constructor is 16 characters.
  ```

- Useful StringBuilder methods include:

  ```
  insert(int position, <X> value);
  append(<X> value);
  reverse();
  delete(int start, int end);
  deleteCharAt(int index);
  replace(int start, int end, String replacement);
  int capacity();
  char charAt(int index);
  int length();
  int indexOf(String str);
  int indexOf(String str, int startIndex);
  void setLength(int len);
  String substring(int start);
  String substring(int start, int end);
  String toString();
  ```

The value to append is typically determined by String.valueOf().

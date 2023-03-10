

**Function Interfaces**

    1. There are five basic functional interfaces that, by default, operate on a single reference type: Predicate, Unary Operator, Function, Supplier, Consumer and one which operates on two reference types — BinaryOperator
    2. Each of the six basic types has three variants that accept a primitive: double, int, or long
    3. Variants of the three basic types accept two arguments: BiPredicate, BiFunction, BiConsumer
    4. Function has 6 variants that convert one of the primitives (double, int, long) to a different primitive.
    5. Function and BiFunction each have 3 variants that take a reference type and return a primitive double, int, or long
    6. Supplier has a variant that returns a boolean
    7. BiConsumer has three variants that accept a reference type and a primitive: double, int, or long

**Basic Types:**

- PREDICATE               : 	takes one (or two) argument(s) and returns a boolean (5 variants)
- UNARY OPERATOR          : 	result and the single argument types are the same (4 variants)
- BINARY OPERATOR         : 	result and both argument types are the same (4 variants)
- FUNCTION                : 	result and one (or two) argument(s) types are different (17 variants)
- SUPPLIER                : 	takes no arguments, returns a value ( 5 variants )
- CONSUMER                : 	takes one (or two) arguments and returns no value (8 variants)

**Predicate**    
    A Predicate is often used when filtering or matching. A BiPredicate is the same but takes two parameters. The definitions are shown below:
    
    @FunctionalInterface
    public interface Predicate<T>{
        boolean test(T t);
        // default and static methods omitted
    }

    @FunctionalInterface
    public interface BiPredicate<T, U>{
        boolean test(T t, U t);
        // default methods omitted
    }
  
    Example for Predicate :
    Predicate<String> p1 = String::isEmpty;
    Predicate<String> p2 = x -> x.isEmpty();
    System.out.println(p1,test(""); // true
    System.out.println(p2,test(""); // true
    
    Example for BiPredicate :
    BiPredicate<String, String> b1 = String::startsWith;
    BiPredicate<String, String> b2 = (string, suffix) -> string.startsWith(prefix);

    System.out.println(b1.test("chicken", "chick")); // true
    System.out.println(b2.test("chicken", "chick")); // true
  
- Predicate<T> : Represents a predicate (boolean-valued function) of one argument  (reference type)
- DoublePredicate : Accepts one double-valued argument
- IntPredicate : Accepts one int-valued argument.
- LongPredicate : Accepts one long-valued argument
- BiPredicate<T,U> : Accepts two arguments  (reference types)
  ![image](https://user-images.githubusercontent.com/20484835/218272973-a4f0f815-2554-4506-a05d-34278817ee30.png)


**Unary Operator**
    
    A UnaryOperator is a special case of a Function where all the type parameters are the same type. The definitions are shown below:
    
    @FunctionalInterface
    public interface UnaryOperator<T> extends Function<T, T>{}

    Example for UnaryOperator :
    UnaryOperator<String> u1 = String::toUpperCase;
    UnaryOperator<String> u2 = x -> x.toUpperCase();
    System.out.println(u1.apply("hi")); // HI
    System.out.println(u2.apply("hi")); // HI
    
- UnaryOperator<T> : Represents an operation on a single operand that produces a result of the same type as its operand  (reference type)
- DoubleUnaryOperator : Accepts single double-valued operand and produces a double-valued result
- IntUnaryOperator : Accepts a single int-valued operand and produces an int-valued result
- LongUnaryOperator : Accepts a single long-valued operand and produces a long-valued result
 
**Binary Operator**
    
    A BinaryOperator merges two values into one of the same type. The definitions are shown below:
    
    @FunctionalInterface
    public interface BinaryOperator<T> extends BiFunction<T,T,T>{
    // omitted static methods
    }
    
    Example for BinaryOperator :
    BinaryOperator<String> b1 = String::concat;
    BinaryOperator<String> b2 = (string, toAdd) -> string.concat(toAdd);
    System.out.println(u1.apply("hi ", "there")); // hi there
    System.out.println(u2.apply("hi ", "there")); // hi there

- BinaryOperator<T> : Represents an operation upon two operands of the same type, producing a result of the same type as the operands  (reference type)
- DoubleBinaryOperator : Accepts two double-valued operands and produces a double-valued result
- IntBinaryOperator : Accepts two int-valued operands and produces an int-valued result
- LongBinaryOperator : Accepts two long-valued operands and produces a long-valued result.
    ![image](https://user-images.githubusercontent.com/20484835/218273140-43012f56-3134-4fbe-9dc7-3c11fd70adb9.png)

**Function**
    
    A Function turns one parameter into a value of a potentially different type and returns it. A BiFunction turns two parameters into a value and returns it. 
    The definitions are shown below:
    
    @FunctionalInterface
    public interface Function<T, R>{
        R apply(T t);
        // default and static methods omitted
    }

    @FunctionalInterface
    public interface BiFunction<T, U, R>{
        R apply(T t, U u);
        // default method omitted
    }
    
    Example of Function :
    Function<String, Integer> f1 = String::length;
    Function<String, Integer> f2 = x -> x.length();
    System.out.println(f1.apply("cat")); // 3
    System.out.println(f2.apply("cat")); // 3
    
    Example for BiFunction :
    BiFunction<String, <String, String> b1 = String::concat;
    BiFunction<String, <String, String> b2 = (string, toAdd) -> string.concat(toAdd);
    System.out.println(b1.apply("cat ", "dog")); // cat dog
    System.out.println(b2.apply("cat ", "dog")); // cat dog
    
- Function<T,R> : Represents a function that accepts one argument and produces a result (reference type)
- BiFunction<T,U,R> : Represents a function that accepts two arguments and produces a result (reference type)
  
- DoubleFunction<R> : Accepts a double-valued argument and produces a result
- IntFunction<R> : Accepts an int-valued argument and produces a result
- LongFunction<R> : Accepts a long-valued argument and produces a result
  
- DoubleToIntFunction : Accepts a double-valued argument and produces an int-valued result
- DoubleToLongFunction : Accepts a double-valued argument and produces a long-valued result
- IntToDoubleFunction : Accepts an int-valued argument and produces a double-valued result
- IntToLongFunction : Accepts an int-valued argument and produces a long-valued result
- LongToIntFunction : Accepts a long-valued argument and produces an int-valued result
- LongToDoubleFunction : Accepts a long-valued argument and produces a double-valued result.

- ToDoubleFunction<T> : Accepts a reference type and produces an int-valued result
- ToIntFunction<T> : Accepts a reference type and produces an int-valued result
- ToLongFunction<T> : Accepts a reference type and produces a long-valued result.
- ToDoubleBiFunction<T,U> : Accepts two reference type arguments and produces a double-valued result
- ToIntBiFunction<T,U> : Accepts two reference type arguments and produces an int-valued result
- ToLongBiFunction<T,U> : Accepts two reference type arguments and produces a long-valued result 
    ![image](https://user-images.githubusercontent.com/20484835/218273330-7840e091-da0a-4b5c-9a62-41ad7aaaac88.png)

**Supplier**
  
  A Supplier is used when you want to generate or supply values without taking any input. A supplier is often used to construct new objects. 
  The definition is shown  below:
 ```
  @FunctionalInterface
  public interface Supplier<T>{
      T get();
  }
  Example :
  
  Supplier<LocalDate> s1 = LocalDate::now;
  Supplier<LocalDate> s2 = () -> LocalDate.now();

  LocalDate d1 = s1.get();
  LocalDate d2 = s2.get();
  ```
  
- Supplier<T> : Represents a supplier of results (reference type)
- DoubleSupplier : A supplier of double-valued results
- IntSupplier : A supplier of int-valued results
- LongSupplier : A supplier of long-valued results
- BooleanSupplier : A supplier of boolean-valued results
    ![image](https://user-images.githubusercontent.com/20484835/218273827-354ed90f-d28f-4b0c-8164-3d6cbfa95e34.png)

**Consumer**

  A Consumer is used when you want to do something with a parameter but not return anything. A BiConsumer is the same but takes two parameters. The definitions are shown below:
  
    @FunctionalInterface
    public interface Consumer<T>{
        void accept(T t);
        // default method omitted
    }

    @FunctionalInterface
    public interface BiConsumer<T, U>{
        void accept(T t, U u);
        // default method omitted
    }
  
    Example of Consumer :
    Consumer<String> c1 = System.out::println;
    Consumer<String> c2 = x-> System.out.println(x);

    c1.accept("Hi");
    c2.accept("Hi");
  
    Example of BiConsumer :
    var map = new HashMap<String, Integer>();
    BiConsumer<String, Integer> b1 = map::put;
    BiConsumer<String, Integer> b2 = (k, v) -> map.put(k, v);

    b1.accept("chicken", 7);
    b2.accept("chick", 1);
  
- Consumer<T> Represents an operation that accepts a single (reference type) input argument and returns no result
- DoubleConsumer : Accepts a single double-valued argument and returns no result
- IntConsumer : Accepts a single int-valued argument and returns no result
- LongConsumer : Accepts a single long-valued argument and returns no result
- BiConsumer<T,U> : Represents an operation that accepts two (reference type) input arguments and returns no result
- ObjDoubleConsumer<T> : Accepts an object-valued and a double-valued argument, and returns no result
- ObjIntConsumer<T> : Accepts an object-valued and an int-valued argument, and returns no result
- ObjLongConsumer<T> : Accepts an object-valued and a long-valued argument, and returns no result
    ![image](https://user-images.githubusercontent.com/20484835/218273946-6ea0be1b-f1da-49d9-8af9-9586c4b1575b.png)


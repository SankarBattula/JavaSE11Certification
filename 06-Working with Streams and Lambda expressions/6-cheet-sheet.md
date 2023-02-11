



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

- Predicate<T> : Represents a predicate (boolean-valued function) of one argument  (reference type)
- DoublePredicate : Accepts one double-valued argument
- IntPredicate : Accepts one int-valued argument.
- LongPredicate : Accepts one long-valued argument
- BiPredicate<T,U> : Accepts two arguments  (reference types)
  ![image](https://user-images.githubusercontent.com/20484835/218272973-a4f0f815-2554-4506-a05d-34278817ee30.png)


**Unary Operator**

- UnaryOperator<T> : Represents an operation on a single operand that produces a result of the same type as its operand  (reference type)
- DoubleUnaryOperator : Accepts single double-valued operand and produces a double-valued result
- IntUnaryOperator : Accepts a single int-valued operand and produces an int-valued result
- LongUnaryOperator : Accepts a single long-valued operand and produces a long-valued result
 
**Binary Operator**
  
- BinaryOperator<T> : Represents an operation upon two operands of the same type, producing a result of the same type as the operands  (reference type)
- DoubleBinaryOperator : Accepts two double-valued operands and produces a double-valued result
- IntBinaryOperator : Accepts two int-valued operands and produces an int-valued result
- LongBinaryOperator : Accepts two long-valued operands and produces a long-valued result.
    ![image](https://user-images.githubusercontent.com/20484835/218273140-43012f56-3134-4fbe-9dc7-3c11fd70adb9.png)

**Function**
  
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




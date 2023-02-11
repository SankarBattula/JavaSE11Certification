



1.There are five basic functional interfaces that, by default, operate on a single reference type: Predicate, Unary Operator, Function, Supplier, Consumer and one which operates on two reference types — BinaryOperator

2.Each of the six basic types has three variants that accept a primitive: double, int, or long

3.Variants of the three basic types accept two arguments: BiPredicate, BiFunction, BiConsumer

4.Function has 6 variants that convert one of the primitives (double, int, long) to a different primitive.

5.Function and BiFunction each have 3 variants that take a reference type and return a primitive double, int, or long

6.Supplier has a variant that returns a boolean

7.BiConsumer has three variants that accept a reference type and a primitive: double, int, or long

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

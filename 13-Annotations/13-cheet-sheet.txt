
Def : 
    Java provides a feature that enables you to embed supplemental information into a source file. This information, called an annotation, does not change the actions of a program.
    Java annotations are a mechanism for adding metadata information to our source code (Program).

example:
    @interface MyAnno {
        String str();
        int val ();
    }
    First, notice the @ that precedes the keyword interface. This tells the compiler that an annotation type is being declared.
    str(), val() consist solely of method declaration, we dont provide bodies for these methonds. Instead, Java implemnets these methonds. Moreover, the methonds act much like fields

Importent:
    1. An annotation cannot include an extends clause. However, all annotation types automatically extend the Annotation interface
    2. Annotation is a super-interface of all annotations.It is declared within the java.lang.annotation package. It overrides hashCode( ), equals( ), and toString( ), 
       which are defined by Object. It also specifies annotationType( ), which returns a Class object that represents the invoking annotation.
    3. Any type of declaration can have an annotation associated with it. For example, classes, methods, fields, parameters, and enum constants
       can be annotated. Even an annotation can be annotated. In all cases, the annotation precedes the rest of the declaration.
    4. When you apply an annotation, you give values to its members. For example, here is an example of MyAnno being applied to a method declaration:
    // Annotate a method.
    @MyAnno(str = "Annotation Example", val = 100)
    public static void myMeth() { // ...

Retention Policy:
    1. A retention policy determines at what point an annotation is discarded.
    2. Java defines three such policies, which are encapsulated within the java.lang.annotation.RetentionPolicy enumeration They are SOURCE, CLASS, and RUNTIME.
        SOURCE : Retention policy of SOURCE is retained only in the source file and is discarded during compilation.
        CLASS : Retention policy of CLASS is stored in the .class file during compilation. However, it is not available through the JVM during run time.
        RUNTIME : Retention policy of RUNTIME is stored in the .class file during compilation and is available through the JVM during run time. 
                  Thus, RUNTIME retention offers the greatest annotation persistence
    3. A retention policy is specified for an annotation by using one of Java’s builtin annotations: @Retention. Its general form is shown here:
            @Retention(retention-policy)
    4. If no retention policy is specified for an annotation, then the default policy of CLASS is used
    5. The following version of MyAnno uses @Retention to specify the RUNTIME retention policy. Thus, MyAnno will be available to the JVM during program execution.
        @Retention(RetentionPolicy.RUNTIME)
        @interface MyAnno {
            String str();
            int val ();
        }

Reflection :
    1. if annotation specify a retention policy of RUNTIME, then they can be queried at run time by any Java program through the use of reflection
    2. The reflection API is contained in the java.lang.reflect package. few examples that apply to annotations.
       The first step to using reflection is to obtain a Class object that represents the class whose annotations you want to obtain. 
       Class is one of Java’s built-in classes and is defined in java.lang.
       final Class<?> getClass()            - To obtained a Class object
                      getMethod()           - To obtain information about a method
                      getField()            - To obtain information about a Fields
                      getConstructor()      - To obtain information about a Constructor.

    3. To understand the process, let’s work through an example that obtains the annotations associated with a method. 
       To do this, you first obtain a Class object that represents the class, and then call getMethod( ) on that Class object,
       specifying the name of the method. getMethod( ) has this general form:
       Method getMethod(String methName, Class<?> ... paramTypes)

    4. From a Class, Method, Field, or Constructor object, you can obtain a specific annotation associated with that object by calling getAnnotation( ). 
       Its general form is shown here:
       <A extends Annotation> getAnnotation(Class<A> annoType)
    5. You can obtain all annotations that have RUNTIME retention that are associated with an item by calling getAnnotations( ) on that item. It has this general form:
       Annotation[ ] getAnnotations( )
    6. The methods getAnnotation( ) and getAnnotations( ) used by the preceding examples are defined by the AnnotatedElement interface,
        Annotation[ ] getDeclaredAnnotations( )
        default boolean isAnnotationPresent(Class<? extends Annotation> annoType)
        getAnnotationsByType()
        getDeclaredAnnotationsByType()

Using Default Values :
    You can give annotation members default values that will be used if no value is specified when the annotation is applied. 
    A default value is specified by adding a default clause to a member’s declaration.
    type member( ) default value ;
    Here, value must be of a type compatible with type. Here is @MyAnno rewritten to include default values:

    @Retention(RetentionPolicy.RUNTIME)
        @interface MyAnno {
            String str() default "Testing";
            int val () default 9000;
    }

    @MyAnno() // both str and val default
    @MyAnno(str = "some string") // val defaults
    @MyAnno(val = 100) // str defaults
    @MyAnno(str = "Testing", val = 100) // no defaults

Marker Annotations:

    Marker annotation is a special kind of annotation that contains no members. Its sole purpose is to mark an item. 
    Thus, its presence as an annotation is sufficient.The best way to determine if a marker annotation is present is to use the method
    isAnnotationPresent( ), which is defined by the AnnotatedElement interface.

Single-Member Annotations :
    1. A single-member annotation contains only one member. It works like a normal annotation except that it allows a shorthand form of specifying the value of the member.
    2. When only one member is present, you can simply specify the value for that member when the annotation is applied—you don’t need to specify the name of the member
    3. However, in order to use this shorthand, the name of the member must be value.
    Remember, whenever you are using a single-member annotation, the name of that member must be value.


The Built-In Annotations :
    Java defines many built-in annotations. Most are specialized, but nine are general purpose
    Four are imported from java.lang.annotation:
        @Retention - It specifies the retention policy
        @Documented - It is a marker interface that tells a tool that an annotation is to be documented
        @Target - It specifies the types of items to which an annotation can be applied 
            @Target takes one argument, which is an array of constants of the ElementType enumeration
            This argument specifies the types of declarations to which the annotation can be applied
            The constants are shown here along with the type of declaration to which they correspond
            @Target( { ElementType.FIELD, ElementType.LOCAL_VARIABLE } )
                -----------------------------------------------------
                Target Constant  |  Annotation Can Be Applied To
                -----------------------------------------------------
                ANNOTATION_TYPE  |  Another Annotation
                CONSTRUCTOR      |  Constructor
                FIELD            |  Field
                LOCAL_VARIABLE   |  Local Variable 
                METHOD           |  Method
                MODULE           |  Module
                PACKAGE          |  Package
                PARAMETER        |  Parameter
                TYPE             |  Class , interface, or enumeration 
                TYPE_PARAMETER   |  Type Parameter
                TYPE_USE         |  Type use
                ------------------------------------------------------
            You can specify one or more of these values in a @Target annotation. To specify multiple values, you must specify them within a braces-delimited list.
                          
            @Inherited - It is a marker annotation that can be used only on another annotation declaration.
                Furthermore, it affects only annotations that will be used on class declarations.
                @Inherited causes the annotation for a superclass to be inherited by a subclass
                Therefore, when a request for a specific annotation is made to the subclass, if that annotation is not present in the subclass, 
                then its superclass is checked
                If that annotation is present in the superclass, and if it is annotated with @Inherited, then that annotation will be returned.

    Five are included in java.lang
        @Override  -  It is a marker annotation that can be used only on methods
            A method annotated with @Override must override a method from a superclass. If it doesn’t, a compile-time error will result
            It is used to ensure that a superclass method is actually overridden, and not simply overloaded
        @Deprecated  -  It indicates that a declaration is obsolete and not recommended foruse
        @FunctionalInterface  - is a marker annotation designed for use on interfaces
            It indicates that the annotated interface is a functional interface. 
            A functional interface is an interface that contains one and only one abstract method.
            Functional interfaces are used by lambda expressions.
        @SafeVarargs  -  It is a marker annotation that can be applied to methods and constructors
            It indicates that no unsafe actions related to a varargs parameter occur
            It is used to suppress unchecked warnings on otherwise safe code as it relates to non-reifiable vararg types and parameterized array instantiation
            It must be applied only to vararg methods or constructors. Methods must also be static, final, or private
        @SuppressWarnings  -  It specifies that one or more warnings that might be issued by the compiler are to be suppressed. 
            The warnings to suppress are specified by name, in string form

Type Annotations :
    Type annotations are important because they enable tools to perform additional checks on code to help prevent errors.
    void myMeth() throws @TypeAnno NullPointerException { // ...
    Here, @TypeAnno annotates NullPointerException in the throws clause.
    ----------------------------------------------
    Annotation      |        Target
    ----------------------------------------------
    @TypeAnno       |  ElementType.TYPE_USE
    @MaxLen         |  ElementType.TYPE_USE
    @NotZeroLen     |  ElementType.TYPE_USE
    @Unique         |  ElementType.TYPE_USE
    @What           |  ElementType.TYPE_PARAMETER
    @EmptyOk        |  ElementType.FIELD
    @Recommended    |  ElementType.METHOD       
    ----------------------------------------------

    Note : Notice that @EmptyOK, @Recommended, and @What are not type annotations. 
           @What, which is used to annotate a generic type parameter declaration.


Create Custom Annotation
    1. Class Level Annotation
    2. Field Level Annotation
    3. Method Level Annotation

1. Class Level Annotation

The first step to creating a custom annotation is to declare it using the @interface keyword :
    public @interface GFG {
    }

The next step is to specify the scope and the target of our custom annotation :
    @Retention(RetentionPolicy.RUNTIME)
    @Target(ElementType.Type)
    public @interface GFG {
    }

2. Field Level Annotation
declared a public annotation with runtime visibility that we can apply to all fields.

    @Retention(RetentionPolicy.RUNTIME)
    @Target(ElementType.FIELD)
    public @interface GFGElement {
        public String key() default "";
    }

3. Method Level Annotation

declared a public annotation with runtime visibility that we can apply to our classes methods.

    @Retention(RetentionPolicy.RUNTIME)
    @Target(ElementType.METHOD)
    public @interface Init {
    }
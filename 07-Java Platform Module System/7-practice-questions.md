
1. What is the name of a file that declares a module?
    A. mod.java
    B. mod-data.java
    C. mod-info.java
    D. module.java
    E. module-data.java
    F. module-info.java

    Explanation :
    F. The module-info.java file is used to declare a module. 
    You must memorize the name of this file.

2. Suppose you have a module that contains a class with a call to
    exports(ChocolateLab.class). Which part of the module service contains this class?
    
    A. Consumer
    B. Service locator
    C. Service provider
    D. Service provider interface
    E. None of the above

    Explanation :
    E. The service locator contains a load() method, not an exports() method, making option E the answer.

3. Which are considered part of a service? (Choose two.)
    A. Consumer
    B. Service locator
    C. Service provider
    D. Service provider interface

    Explanation :
    B,D. A service is comprised of the interface, any classes the interface references, and a way to look up implementations of the interface. 
    Option B covers the lookup, and option D covers the interface itself.

4. Given the following diagram, how many of the following are named modules?

        classpath       |     module path
    ___________________ | ____________________
    | dog.fluffy.jar  | | |  dog.hair.jar    |
    |                 | | |                  |
    |     dog.fluffy  | | |      dog.hair    |
    |_________________| | |__________________|
     __________________ | ____________________
    | dog.husky.jar   | | |  dog.bark.jar    |
    |                 | | |                  |
    |     dog.husky   | | |      dog.bark    |
    |    module-info  | | |     module-info  |
    |_________________| | |__________________|

    A. 0
    B. 1
    C. 2
    D. 3
    E. 4

    Explanation :
    B. A named module must be on the module path and contain a module-info file. 
    Only dog.bark meets this criterion, making option B the answer.

5. Given the diagram from the previous question, which is an automatic module?
    A. dog.bark
    B. dog.fluffy
    C. dog.hair
    D. dog.husky
    E. None of the above

    Explanation :
    C. An automatic module must be on the module path but does not contain a module-info file. 
    Option C is correct because dog.hair matches this description.

6. Given the diagram from question 4, which is a default module?
    A. dog.bark
    B. dog.fluffy
    C. dog.hair
    D. dog.husky
    E. None of the above

    Explanation :
    E. You need to know about three types of modules for the exam: automatic, named, and unnamed. 
    There is no such thing as a default module. The question was trying to trick you, and option E is correct.

7. Given the diagram from question 4, how many are unnamed modules?
    A. 0
    B. 1
    C. 2
    D. 3
    E. 4

    Explanation :
    C. An unnamed module must be on the classpath. It is rare to have a module-info file in an unnamed module, but it is allowed. 
    Therefore, both dog.fluffy and dog.husky meet this criterion, making option C correct.

8. Which of the following statements are true? (Choose two.)

    A. It is a good practice to add the --add-exports option to your java command.
    B. It is permitted, but not recommended, to add the --add-exports option to your java command.
    C. There is no --add-exports option on the java command.
    D. It is a good practice to add the --add-requires option to your java command.
    E. It is permitted, but not recommended, to add the --add-requires option to your java command.
    F. There is no --add-requires option on the java command.

    Explanation :
    B,F. It is recommended to specify all exports directives in the module-info file. 
    While it is legal to use the --add-exports option, it is not recommended, making option B correct. 
    You do not need to know how to use it for the exam, just that it is not a good idea. 
    There is no equivalent option for requires, making option F correct.

9. How many of the following are legal module-info.java files?
    module com.koala {
        exports cute;
    }
    module com-koala {
        exports cute;
    }
    public module com.koala {
        exports cute;
    }
    public module com-koala {
        exports cute;
    }

    A. None
    B. One
    C. Two
    D. Three
    E. Four

    Explanation :
    B. Since Java does not allow dashes in identifier names, the second and fourth declarations are invalid. 
    Additionally, access modifiers are not permitted in module declarations, making the third and fourth declarations invalid. 
    The only one that is legal is the first declaration, so option B is correct.

10. Which two would be best to combine into a single module?
    A. Consumer and service locator
    B. Consumer and service provider
    C. Consumer and service provider interface
    D. Service locator and service provider interface
    E. Service locator and service provider
    F. Service provider and service provider interface

    Explanation :
    D. The consumer is generally separate ruling out options A, B, and C. 
    The service provider is decoupled from the service provider interface ruling out option F. 
    It is most logical to combine the service locator and service provider interface because neither has a direct reference to the service provider. 
    Therefore, option D is correct.

11. What command could you run to print output like the following?
    java.base@11.0.2
    java.compiler@11.0.2
    java.datatransfer@11.0.2
    java.desktop@11.0.2
    ...
    A. java --all-modules
    B. java --describe-modules
    C. java --list-modules
    D. java --output-modules
    E. java --show-modules
    F. None of the above

    Explanation :
    C. The java command has an option to list all the modules that come with the JDK. 
    Option C is correct since that option is called --list-modules. 
    The other options are not supported by the java command. 
    Options B and E are similar to options that exist: --describe-module and --show-module-resolution. 
    But neither gives a list of all the modules that come with the JDK.

12. Suppose we have an automatic module on the module path named dog-arthur2.jar and
    no Automatic-Module-Name specified? What module name should named modules use to
    reference it?

    A. dog-arthur
    B. dog-arthur2
    C. dog.arthur
    D. dog.arthur2
    E. None of the above

    Explanation :
    C. The rules for determining the name include removing the extension, removing numbers, and changing special characters to periods (.). 
    This leaves us with dog.arthur, which is option C. 

13. Given the dependencies in the diagram, which boxes represent the service provider interface
    and service provider, respectively?
    W --------> X
                ^
                |
    Y <-------- Z

    A. W and X
    B. W and Z
    C. X and Y
    D. X and Z
    E. Y and Z
    F. None of the above

    Explanation :
    C. All parts of a modules service must point to the service provider interface. 
    This tells us the service provider interface must be X, ruling out options A, B, and E. 
    Now, we have to decide if Y or Z are the service provider interface. 
    We can tell because nothing has a direct dependency on the service provider. 
    Since this makes the service provider Y, the answer is option C.

14. Using the diagram in the previous question, which boxes represent the consumer and service
    locator, respectively?
    A. W and X
    B. W and Z
    C. X and Y
    D. X and Z
    E. Y and Z
    F. None of the above

    Explanation :
    B. The consumer depends on the service provider interface and service locator, but not the service provider. 
    Only W has two arrows starting from it so, it must be the consumer. This rules out options C, D, and E. 
    The service locator references the service provider interface directly and the service provider indirectly, 
    making the service locator Z and option B the answer.

15. What is the minimum number of JAR files you need for a cyclic dependency?
    A. 0
    B. 1
    C. 2
    D. 3
    E. 4

    Explanation :
    C. A cyclic dependency is when two things directly or indirectly depend on each other. 
    If chicken.jar depends on egg.jar, and egg.jar depends on chicken.jar, we have a cyclic dependency. 
    Since only two JAR files are needed to create this situation, option C is the answer.

16. Fill in the blank with code to look up and call a service.
    String cheese = ServiceLoader.load(Mouse.class)
    .map(______________)
    .map(Mouse::favoriteFood)
    .findFirst()
    .orElse("");

    A. Mouse.get()
    B. Mouse::get
    C. Provider.get()
    D. Provider::get
    E. None of the above

    Explanation :
    E. The ServiceLoader class has a load() method that returns a Collection of Provider, not a stream. 
    Since the call to stream() is missing, option E is the answer. If the call to stream() were added, option D would be the answer.

17. Suppose we want to have two modules: com.ny and com.sf. Which is true about the
    placement of the module-info.java file(s)?
    module com.ny                   module com.sf
        package com.ny.city             package com.sf.city
                V                               X
                W                               Y
                Z

    A. One module-info.java file is required in position Z.
    B. Two module-info.java files are required, in positions V and X.
    C. Two module-info.java files are required, in positions W and Y.
    D. Three module-info.java files are required, in positions V, X, and Z.
    E. Three module-info.java files are required, in positions W, Y, and Z.
    F. None of the above.

    Explanation :
    C. Each module is required to have its own module-info.java file in the root directory of the module. 
    For module com.ny, that is location W, and for module com.sf, that is location Y. 
    Therefore, option B is correct

18. Consider the modules in the previous diagram. Suppose we want the code in module com.sf
    to depend on code in module com.ny. Which of the following directives goes into module
    com.sf’s module-info file to configure that behavior?

    A. export com.ny;
    B. exports com.ny;
    C. require com.ny;
    D. require com.ny.city;
    E. requires com.ny;
    F. requires com.ny.city;

    Explanation :
    E. Options A, C, and D are incorrect because export and require are not keywords in modules. 
    Option B is incorrect because that directive goes in the com.ny module, not the com.sf one. 
    Option E is correct rather than option F because the requires directive references a module name rather than a package.

19. Consider the modules diagram in question 17. Suppose we want the code in module com.sf
    to depend on code in module com.ny. Which of the following directives goes into module
    com.ny’s module-info file to configure that behavior?

    A. export com.ny;
    B. export com.ny.city;
    C. exports com.ny;
    D. exports com.ny.city;
    E. requires com.ny;
    F. requires com.ny.city;

    Explanation :
    D. Options A and B are incorrect because export is not a keyword in modules. Option E belongs in the com.sf module, not the com.ny one. 
    Option F is incorrect because the requires directive references a module name rather than a package. 
    Finally, option D is the answer rather than option C because the exports directive references a package name rather than a module.

20. Suppose the consumer, service locator, service provider, and service provider interface are
    each in separate modules. Which of the following best describes the following moduleinfo
    file?

    module nature.tree {
        provides nature.sapling.Tree with nature.tree.Maple
    }

    A. Consumer
    B. Service locator
    C. Service provider
    D. Service provider interface
    E. None of the above

    Explanation :
    E. The Maple class is intended to be an implementation of the Tree interface. However, this interface needs to be accessible. 
    This module is missing a requires nature.sapling; statement, making option E the correct answer.

21. Which options are commonly used when compiling a module?

    A. -d and -m
    B. -d and -p
    C. -m and -p
    D. -d, -m, and -p
    E. None of the above

    Explanation :
    B. The –d option specifies the directory. 
    The –p option specifies the module path. 
    The –m option is not available on the javac command.

22. Which of the following are modules supplied by the JDK? (Choose three.)

    A. java.base
    B. java.basic
    C. java.desktop
    D. java.sdk
    E. java.sql
    F. java.swing

    Explanation :
    A,C,E. The java.base module is automatically available to any module without specifying it, making option A correct. 
    Options C and E are also correct because java.desktop and java.sql are modules supplied with the JDK. 
    You do need to be able to identify built-in modules for the exam.

23. Which best describes a top-down migration? (Choose two.)

    A. The first step is to move all the modules to the module path.
    B. The first step is to move a single module to the module path.
    C. Most steps consist of changing an automatic module to a named module.
    D. Most steps consist of changing an automatic module to a unnamed module.
    E. Most steps consist of changing an unnamed module to an automatic module.
    F. Most steps consist of changing an unnamed module to a named module

    Explanation :
    A,C. Option A is correct because a top-down migration starts by moving all the modules to the module path as automatic modules. 
    Then, the migration changes each module from an automatic module to a named module, making option C the other correct answer.

24. Suppose the consumer, service locator, service provider, and service provider interface are
    each in separate modules. Which of the following best describes the following
    module-info file?
    module nature.tree {
        requires nature.sapling;
        requires nature.bush;
    }

    A. Consumer
    B. Service locator
    C. Service provider
    D. Service provider interface
    E. None of the above

    Explanation :
    A. Option A is correct because a consumer has two dependencies. It requires both the service provider interface and the service locator.

25. Suppose you have these two JARs from Java 8. Which steps, when taken together, would be
    the best way to make them modules? (Choose two.)

        baby.otter
         |     ^
         V     |
        food.fish

    A. Add a module-info.java to each.
    B. Add them to the classpath.
    C. Create a third module to contain the common code.
    D. Merge them into one module to break the cyclic dependency.
    E. Rename the modules to use dashes instead of dots.

    Explanation :
    A,C. Option A is correct, and option B is incorrect as we want to create named modules when possible. 
    We also need to be on the lookout for cyclic dependencies. While option D would work, it is better to be more granular and create a third module as in option C. 
    Option E is incorrect because dots are used as separators in names.

26. Which command produces output such as the following?
    animal.puppy -> animal.dog
    A. jdeps –d zoo.animal.puppy.jar
    B. jdeps –s zoo.animal.puppy.jar
    C. jmod –d zoo.animal.puppy.jar
    D. jmod –s zoo.animal.puppy.jar
    E. None of the above

    Explanation :
    B. The jdeps command lists information about dependencies within a module. 
    The –s option provides a summary of output rather than verbose output, making option B the correct answer. 
    There is no –d option. The jmod command is for working with JMOD files.

27. Suppose the consumer, service locator, service provider, and service provider interface are
    each in separate modules. Which of the following best describes the following moduleinfo
    file?
    module nature.tree{
        requires nature.sapling;
        provides nature.sapling.Tree with nature.tree.Maple
    }

    A. Consumer
    B. Service locator
    C. Service provider
    D. Service provider interface
    E. None of the above

    Explanation :
    C. Option C is correct because a service provider requires the interface. It also provides the implementation.

28. Suppose we have module com.bird that contains package com.bird.tweet and
    class Tweety with a main() method. Which of the following can fill in the blank to run
    this program?
    java --module-path mods –module _____________

    A. com.bird.Tweety
    B. com.bird.tweety.Tweety
    C. com.bird/Tweety
    D. com.bird.tweet/Tweety
    E. com.bird/com.bird.tweet.Tweety
    F. com.bird.tweet/com.bird.Tweety

    Explanation :
    E. When running a module, the module name is listed before the slash, and the fully qualified class name is after the slash. 
    Option E is the only one that meets this criterion.

29. Which types of modules are required to contain a module-info file?

    A. Automatic only
    B. Named only
    C. Unnamed only
    D. Automatic and named
    E. Automatic and unnamed
    F. Named and unnamed

    Explanation :
    B. An unnamed module is on the classpath. While it is permitted to have a module-info file, the file is ignored if present. 
    An automatic module is on the module path and does not have a module-info file. 
    A named module is required to have a module-info file, making option B the correct answer.

30. Suppose the consumer, service locator, service provider, and service provider interface are
    each in separate modules. Which of the following best describes the following
    module-info file?

    module nature.tree{
        exports nature.tree.leaf;
        requires nature.sapling;
        uses nature.tree.Photosynthesis;
    }

    A. Consumer
    B. Service locator
    C. Service provider
    D. Service provider interface
    E. None of the above

    Explanation :
    B. Option B is correct because a service locator uses the interface. 
    It also requires the service provider interface module and exports the package with the locator.


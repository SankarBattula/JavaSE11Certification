1. Which statement best describes this class?
    import java.util.*;
    public final class Forest {
        private final int flora;
        private final List<String> fauna;
        public Forest() {
            this.flora = 5;
            this.fauna = new ArrayList<>();
        }
        public int getFlora() {
            return flora;
        }
        public List<String> getFauna() {
            return fauna;
        }
    }

    A. It can be serialized.
    B. It is well encapsulated.
    C. It is immutable.
    D. It is both well encapsulated and immutable.
    E. None of the above as the code does not compile.

    Explanation :
    B. This class does not implement Serializable, so option A is incorrect. 
    This code is well encapsulated because the instance variables are private. 
    While the instance variable references do not change after the object is created, the contents fauna can be modified, so it is not immutable. 
    For these reasons, option B is correct

2. Fill in the blanks: The ___________ class variable defines a whitelist of fields that should be
    serialized, while the ___________ modifier is used to construct a blacklist of fields that should
    not be serialized. (Choose two.)

    A. serialVersionUID in the first blank
    B. serialFields in the first blank
    C. serialPersistentFields in the first blank
    D. ignore in the second blank
    E. transient in the second blank
    F. skip in the second blank

    Explanation :
    C,E. Options B, D, and F are not supported options in Java. 
    The serialVersionUID class variable can be used in serialization, but it relates to the version of the class stored, not the choice in fields serialized, making option A incorrect. 
    That leaves options C and E as the correct answers. 
    The serialPersistentFields class variable defines a whitelist of fields to serialize,
    while the transient modifier constructs a blacklist of fields to skip

3. Which statement best describes the following method?
    public String findNewLego(String url, String type)
        throws SQLException {
    var query = "SELECT name FROM sets WHERE "
        + "type = " + type + " ORDER BY date DESC";
        var con = DriverManager.getConnection(url);
        try(con;
            var ps = con.createStatement();
            var rs = ps.executeQuery(query)) {

            if(rs.next()) return rs.getString(1);
        }
        throw new RuntimeException("None available, try later");
    }

    A. It is not susceptible to any common attacks.
    B. It is at risk of SQL injection attack only.
    C. It is at risk of a denial of service attack only.
    D. It is at risk of both SQL injection and denial of service attacks.
    E. The method does not compile.
    F. None of the above.

    Explanation :
    B. The method compiles, so option E is incorrect. 
    It is recommended to use a PreparedStatement with bind variables, over a Statement, to avoid SQL injection. 
    Since the data type of the variable is String, it needs to be escaped making this method at risk for SQL injection.
    Further, there is no risk of a resource leak that could be exploited in a denial of service attack. 
    The Connection object is declared immediately before the try-with-resources block and closed by it, so it cannot be left open. 
    For these reasons, option B is correct

4. Fill in the blanks: ____________ means the state of an object cannot be changed, while
    _____________ means that it can.

    A. Encapsulation, factory method
    B. Immutability, mutability
    C. Rigidity, flexibility
    D. Static, instance
    E. Tightly coupled, loosely coupled
    F. None of the above

    Explanation :
    B. Option B is correct because mutability means the state can change, and immutability means it cannot. 
    The other options are invalid. In option C, rigidity is not a common programming term.

5. Which of the following best protect against denial of service attacks? (Choose three.)

    A. Close resources with catch blocks.
    B. Use PreparedStatement instead of Statement.
    C. Close resources with try-with-resources statements.
    D. Set a limit of the size of a file upload.
    E. Set a limit on the size of a numeric input value.
    F. Use immutable objects.

    Explanation :
    C,D,E. A denial of service attack is about overloading the system with too much data or too many requests to process legitimate incoming requests. Option A is incorrect, and 
    option C is correct because a try-with-resources or finally block should be used to close resources to prevent a resource leak. 
    Option B is incorrect because SQL injection is a form of injection attack, not one based on volume or resources.
    Option D is correct because a malicious attack could send a lot of bad requests with huge files. 
    Option E is also correct as numeric overflow can be used to overwhelm a system. 
    Option F is incorrect because immutability does not usually play a part in DoS attacks.

6. You ask to borrow one of your friend’s recipe cards. Which statements about these cards,
    represented as Java policy file grants, are correct? (Choose two.)

    grant {
        permission java.io.FilePermission
            "/dessert/icecream/rockyroad.yum", "read,write";
        permission java.io.FilePermission

        "/dessert/icecream/mintchip.yum", "read";
    };

    A. The policy syntax of the policy file is correct.
    B. The policy syntax of the policy file is incorrect.
    C. The policy is incorrect because read should not be included in the first permission.
    D. The policy is incorrect because write should not be included in the first permission.
    E. The policy is incorrect because read should not be included in the second permission.
    F. The policy is incorrect because file permissions cannot be granted this way.

    Explanation :
    A,D. The policy compiles and uses correct syntax, making option A correct. 
    However, it gives permissions that are too broad. The user needs to be able to read a recipe, so write permissions should not be granted, making option D also correct.

7. Which of the following best protect against inclusion attacks? (Choose two.)

    A. Encrypt user passwords.
    B. Use immutable objects.
    C. Limit the recursive depth of ZIP files.
    D. Apply a blacklist to the input data.
    E. Turn the computer off when not in use.
    F. Restrict the number of parse levels of XML files.

    Explanation :
    C,F. Inclusion attacks occur when multiple files or components are embedded within a single 
    entity, such as a zip bomb or the billion laughs attack. Both can be thwarted with depth limits, 
    making option C and F correct. The rest of the options are not related to inclusion attacks.

8. What changes, taken together, would make the Tree class immutable? (Choose three.)
    1: public class Tree {
    2:      String species;
    3:      public Tree(String species) {
    4:          this.species = species;
    5:      }
    6:      public String getSpecies() {
    7:          return species;
    8:      }
    9:      private final void setSpecies(String newSpecies) {
    10:         species = newSpecies;
    11:     }
    12: }

    A. Make all constructors private.
    B. Change the access level of species to private.
    C. Change the access level of species to protected.
    D. Remove the setSpecies() method.
    E. Mark the Tree class final.
    F. Make a defensive copy of species in the Tree constructor.

    Explanation :
    B,D,E. Immutable objects are ones that are not modified after they are created. Immutable objects can have public constructors. 
    There is no need to change the access modifier to private, making option A incorrect. 
    All instance variables should be private in an immutable class to prevent subclasses and classes within the package from modifying them outside the class, making option B correct and option C incorrect. 
    They should not have any setter methods, making option D correct. 
    The class should also either be marked final or contain final methods to prevent subclasses from altering the behavior of the class, making option E correct. 
    Finally, option F is incorrect as String is immutable, so a defensive copy is not required. 
    Note that if species were a mutable type, like List, a defensive copy would be required.

9. Which techniques best prevent sensitive objects from being manipulated by an attacker who
    wants to create a malicious subclass? (Choose three.)

    A. Add final to the class declaration.
    B. Set protected as the access level for all method declarations.
    C. Add final to all method declarations.
    D. Add final to all instance variable declarations.
    E. Add final to all constructors.
    F. Set private as the access level for all constructors.

    Explanation :
    A,C,F. The best way to protect a sensitive class is to prevent the class from being extended or prevent any of its methods from being overridden. Options A and C accomplish this. 
    Option F also is appropriate. 
    By marking all constructors private, only static methods that the class controls can be used to obtain instances of the object. 
    Options B and D are incorrect because they do not prevent methods from being overridden that could change the behavior of the class. 
    Option E is incorrect because constructors cannot be marked final.

10. Which statement best describes the following method?
    public String findNewLego(String url, int type)
            throws SQLException {
        var query = "SELECT name FROM sets WHERE "
            + "type = " + type + " ORDER BY date DESC";
        var con = DriverManager.getConnection(url);
        var ps = con.createStatement();
        try(con; ps; var rs = ps.executeQuery(query)) {
            if(rs.next()) return rs.getString(1);
        }
        throw new RuntimeException("None available, try later");
    }

    A. It is not susceptible to any common attacks.
    B. It is at risk of SQL injection attack only.
    C. It is at risk of a denial of service attack only.
    D. It is at risk of both SQL injection and denial of service attacks.
    E. The method does not compile.
    F. None of the above.

    Explanation :
    C. The class compiles, so option E is incorrect. 
    It is recommended to use a PreparedStatement over a Statement to avoid SQL injection although it is not strictly necessary. 
    In this case, because the data type of the variable is int, Java already prevents a malicious String from being entered into the query. 
    Therefore, this method is not at risk for SQL injection, making option B incorrect.
    On the other hand, the code is a risk of a resource leak that could be exploited in a denial of service attack. 
    While the Connection object doesn’t need to be declared in the try-with resources block, it should be declared right before it. 
    In this case, there’s a line in between, con.createStatement(), that could throw an exception, thereby preventing the Connection from ever being closed. For these reasons, option C is correct.

11. Which statements about executing the following program are correct? (Choose two.)
    import java.security.*;
    import java.util.*;

    public class MagicTrick {
        private static final String WORD = "abracadabra";
        private static List<String> trick = new ArrayList<>();
        public static List<String> castSpell(String magic) {
            return AccessController.doPrivileged(
                    new PrivilegedAction<List<String>>() {
                public List<String> run() {
                if (magic.equalsIgnoreCase(WORD)) { // p1
                    if(trick.isEmpty())
                        trick.add(System.getProperty(magic)); // p2
                    return trick; // p3
                }
                throw new SecurityException("Incorrect code");
            }
        });
    }
    public static void main(String[] args) {
        if(args != null && args.length>0)
            System.out.print(MagicTrick.castSpell(args[0]));
    } }

    A. Line p1 makes the code susceptible to tainted inputs from the user.
    B. Line p2 makes the code susceptible to tainted inputs from the user.
    C. Line p3 makes the code susceptible to tainted inputs from the user.
    D. The code is not susceptible to tainted inputs from the user.
    E. Line p1 exposes sensitive information.
    F. Line p2 exposes sensitive information.
    G. Line p3 exposes sensitive information.
    H. The code does not expose any sensitive information.

    Explanation :
    B,G. Line p1 only partially validates the input from the user, since it performs a case insensitive match. 
    Therefore, the code executed on line p2 could be any variant of the magic word such as Abracadabra, aBraCadAbra, abracaDABRA, etc. 
    In this manner, the user has access to many system properties to read from on line p2, making option B correct. 
    The code also does not protect its input because trick is returned to the user, who is free to modify the List. 
    Instead, an immutable collection should be returned on line p3, making option G correct.

12. How do you change the value of an instance variable in an immutable class?

    A. Call the setter method.
    B. Remove the final modifier and set the instance variable directly.
    C. Create a new instance with an inner class.
    D. Use a method other than Option A, B, or C.
    E. You can’t.

    Explanation :
    E. By definition, you cannot change the value of an instance variable in an immutable class. There are no setter methods, making option A incorrect. 
    While option B would allow you to set the value, the class would no longer be immutable. 
    Option C is incorrect because that would not modify the original instance. 
    Option E is correct. If you are an advanced developer, you might know that you can use reflection to change the value. Don’t read into questions like this on the exam. 
    Reflection isn’t on the exam, so you can pretend it doesn’t exist.

13. Let’s say you want to serialize the following class, but only want the flour quantity saved.
    What changes, if any, are required to the following class for this to occur?

    import java.io.*;
    public class Muffin {
        private Double flour;
        private Integer eggs;
        private Float sugar;
        private final ObjectStreamField[] serialPersistentFields =
            { new ObjectStreamField("flour", Double.class) };
    }

    A. No changes are required.
    B. Mark eggs and sugar as transient.
    C. Remove the serialPersistentFields variable.
    D. Remove the final modifier from the serialPersistentFields variable.
    E. Add a missing modifier to the serialPersistentFields variable.
    F. None of the above.

    Explanation :
    F. The class is not marked Serializable, meaning none of the changes will work and making option F correct. 
    If it was corrected to implement Serializable, then it would serialize all of the fields, not just flour as written. 
    This is because serialPersistentFields is declared without the static modifier. 
    Alternatively, all of the other fields besides flour could be marked transient to achieve the desired result.

14. Which are true about closing resources to guard against a denial of service attack?
    (Choose two.)
    A. The NIO.2 Files.lines() method does not require closing a resource when it is used in a stream pipeline.
    B. The NIO.2 Files.lines() method requires closing a resource when it is used in a stream pipeline.
    C. When locking a resource using an instance of the concurrent Lock interface, the unlock() statement should be immediately before the finally block.
    D. When locking a resource using an instance of the concurrent Lock interface, the unlock() statement should be in a finally block.
    E. When locking a resource using an instance of the concurrent Lock interface, the unlock() statement should be immediately after the finally block.

    Explanation :

    B,D. Ensuring resources are released helps prevent a denial of service attack. Stream 
    methods, such as Files.lines(), do not automatically close the file. Option B is correct 
    since the programmer needs to do it. Without this, the system could run out of file resource 
    handles as part of a denial of service attack.

    When a resource is locked using an instance of the concurrent Lock interface, it should be 
    unlocked in a finally block to ensure this step is not missed. Therefore, option D is the 
    other correct answer. Without this, it’s possible an acquired lock is kept indefinitely, and a 
    deadlock ensues as part of a denial of service attack.

15. Which type of attack requires more than one source to initiate?

    A. Billion laughs attack
    B. Million frowns attack
    C. Distributed denial of service attack
    D. SQL injection
    E. Inclusion attack
    F. Denial of service attack

    Explanation :
    C. A distributed denial of service attack is a denial of service attack that comes from multiple sources, making option C correct. 
    There is no such thing as a million frowns attack. 
    The rest of the answers are real attacks but can be executed from a single source

16. What is this class an example of?
    import java.util.*;
    public class Nightclub {
        private List<String> approved = // IMPLEMENTATION OMITTED
        private List<String> rejected = // IMPLEMENTATION OMITTED
        public boolean checkAccess(String name) {
            var grantAccess = approved.contains(name)
                || rejected.contains(name);
            return grantAccess;
        } }

    A. Turquoiselist
    B. Whitelist
    C. Orangelist
    D. Blacklist
    E. Both blacklist and whitelist
    F. None of the above

    Explanation :
    B. The method only grants someone access if they appear in either the approved or rejected list. 
    The combined data set forms a conceptual whitelist, making option B correct. The variable names chosen were meant to be tricky. 
    If the code was checked to block people from the rejected list as well, then it would be both a whitelist and blacklist implementation.

17. Which statements about the clone() method are correct? (Choose two.)

    A. Calling clone() on a class that does not implement Cloneable results in a compiler error.
    B. Calling clone() on a class that does not implement Cloneable results in an exception at runtime.
    C. If a class implements Cloneable and does not override the clone() method, then the code does not compile.
    D. If a class implements Cloneable and does not override the clone() method, then an exception is thrown at runtime.
    E. Overriding the clone() method in a class that implements Cloneable guarantees at least a shallow copy will be performed.
    F. Overriding the clone() method in a class that implements Cloneable may result in a deep copy.

    Explanation :

    B,F. The clone() method is inherited from the Object class. For this reason, it can be called on any Object without resulting in a compiler error, making options A and C incorrect. 
    Option B is correct and defines the default behavior of clone() if the class does not implement Cloneable. 
    On the other hand, if a class implements Cloneable but does not override clone(), then Java will perform a shallow copy by default, making option D incorrect. 
    Finally, if the class implements Cloneable and overrides clone(), then the behavior of the clone() method is entirely dependent on the implementation. 
    For this reason, option F is correct, and option E is incorrect.

18. Which statements about securing confidential information are correct? (Choose three.)

    A. When writing to System.out, you should not include sensitive information.
    B. When reading sensitive data from a Console, you should use readLine().
    C. When throwing an exception, it is acceptable to include sensitive information in the message.
    D. A String is not a good object type for sensitive data.
    E. A Java policy should only grant the permission lock to prevent a user from modifying the file.
    F. A Java policy should only grant the permission read to prevent a user from modifying the file.

    Explanation :
    A,D,F. Sensitive information should not be written to System.out, System.err, or a stack trace. For this reason, option A is correct, and option C is incorrect. 
    It is preferable to use char[] instead of String for sensitive data so that it does not enter the String pool and become available as part of a memory dump. 
    For this reason, option D is correct, and option B is incorrect. 
    Note that Console does have a readPassword() method that returns char[]. 
    Finally, the correct Java policy permission to prevent write access is to only grant read access, making option F correct and option E incorrect.

19. What are the best scenarios for customizing the serialization process? (Choose two.)

    A. To prevent SQL injection.
    B. To shuffle data among users.
    C. It is the only way to prevent a sensitive field like birthdate from being written to disk.
    D. To improve performance by applying advanced optimization techniques.
    E. To encrypt a password before it is saved to disk.
    F. To customize the handling of certain user sensitive data like a Social Security number.

    Explanation :
    E,F. Encrypting or customizing the handling of certain sensitive fields are good reasons to customize the serialization process via methods, making options E and F correct. 
    Options A, B, and D are invalid and are not reasons to customize the process. 
    Option C is incorrect as the transient modifier or serialPersistentFields can be used to exclude fields from serialization without the need to add any serialization methods.

20. Select a good strategy for handling input validation failures?

    A. Use the assert statement.
    B. Throw an Error.
    C. Log an error but allow the user to continue.
    D. Throw an Exception.
    E. Shut down the computer.
    F. None of the above.

    Explanation :
    D. A good solution when input validation fails is to stop processing a request and throw an Exception to the calling method to deal with the problem, making option D correct. 
    Options A and B are incorrect because throwing Error should be avoided for situations where the application can recover. Also, assertions are often disabled at runtime. 
    Option C is incorrect as the user should not be allowed to continue if they have provided invalid input. 
    Finally, option E is incorrect for obvious reasons.

21. Which statements about executing the following program are correct? (Choose two.)
    import java.security.*;
    public class PrintScores {
        private static final String CODE = "12345";
        private static final String SCORES = "test.scores";
        public static String getScores(String accessCode) {
            return AccessController.doPrivileged(
                    new PrivilegedAction<String>() {
                public String run() {
                    if(accessCode.equals(CODE)) // m1
                        return System.getProperty(SCORES); // m2
                    throw new SecurityException("Incorrect code");
                }
            });
        }
        public static void main(String[] args) {
            if(args != null && args.length>0)
                System.out.print(PrintScores.getScores(args[0]));
        } }

    A. Line m1 makes the code susceptible to tainted inputs from the user.
    B. Line m2 makes the code susceptible to tainted inputs from the user.
    C. The code is not susceptible to tainted inputs from the user.
    D. The code is susceptible to an injection attack.
    E. The code is not susceptible to an injection attack.
    F. The code is susceptible to an injection only if executed with a number as input.

    Explanation :
    C,E. When invoking doPrivileged(), make sure there is no chance for a user to pass their own, unprotected values into the request. 
    Since a constant SCORES is used to read the system property on line m2, rather than user provided input, the code is safe from tainted inputs from the user. 
    The code validates its inputs enough that an injection attack is not possible, making option E correct.

22. Which can fill in the blank to make this code compile?
    import java.io.*;
    public class Pony implements Serializable {
        private static final ObjectStreamField[]
            serialPersistentFields = { new ObjectStreamField("name",
                String.class) };
        private String name;
        private Integer age;
        private void readObject(ObjectInputStream s)
                throws Exception {
            ObjectInputStream.____________ fields = s.readFields();
            this.name = (String) fields.get("name", null);
    } }

    A. GetObject
    B. ReadField
    C. FetchItem
    D. ReadItem
    E. GetField
    F. None of the above

    Explanation :
    E. The GetField class is used with the readObject() method, making option E correct. 
    There is also a PutField class used with the writeObject() method that you should be familiar with for the exam

23. Which statement about the following classes is correct?
    import java.util.*;
    public class Flower {
        private final String name;
        private final List<Integer> counts;
        public Flower(String name, List<Integer> counts) {
            this.name = name;
            this.counts = new ArrayList<>(counts);
        }
        public final String getName() { return name; }
        public final List<Integer> getCounts() {
            return new ArrayList<>(counts);
        } }

    class Plant {
    private final String name;
        private final List<Integer> counts;
        public Plant(String name, List<Integer> counts) {
            this.name = name;
            this.counts = new ArrayList<>(counts);
        }
        public String getName() { return name; }
        public List<Integer> getCounts() {
            return new ArrayList<>(counts);
        } }

    A. Only Flower is immutable.
    B. Only Plant is immutable.
    C. Both classes are immutable.
    D. Neither class is immutable.
    E. None of the above as one of the classes does not compile.

    Explanation :
    A. An immutable class must not allow the state to change. The Flower class does this correctly. 
    While the class isn’t final, the getters are, so subclasses can’t change the value returned. 
    The Plant class lacks this protection, which makes it mutable. Option A is correct.

24. Which of the following can cause an injection attack? (Choose two.)

    A. Access control
    B. Command line input
    C. Constants in the program
    D. Mutable code
    E. Serialization
    F. XML parsing

    Explanation :

    B,F. Option A is incorrect because access control restricts who can do something rather than preventing an injection attack. 
    Option B is correct because unsanitized input from the command line can do something undesirable like delete a file. 
    Option C is incorrect because the programmer typed those constants rather than a hostile party.

    Option D is incorrect because changing the values of an object is not an injection attack. 
    Option E is incorrect because serialization is writing data to disk rather than executing. 
    Option F is correct because XML parsing can load hostile values into your program.

25. Assuming this class is passed a valid non-negative integer, which statements best describe the
    following class? (Choose two.)
    public class Charity {
        private int numberRequests = 0;
        public synchronized int getNumberOfRequests() {
            return numberRequests;
        }

        private void callDatabaseToDonateADollar() {
            // IMPLEMENTATION OMITTED
        }

        public synchronized void donateDollar(int numDollars) {
            numberRequests++;
            for(int i=0; i<numDollars; i++) {
                callDatabaseToDonateADollar();
            }
        }
        public static void main(String[] args) {
            final var humanFund = new Charity();
            humanFund.donateDollar(Integer.valueOf(args[0]));
            System.out.print(humanFund.getNumberOfRequests());
        } }

    A. It is well encapsulated.
    B. It is susceptible to a denial of service attack.
    C. It creates an immutable object.
    D. It is susceptible to an inclusion attack.
    E. It is not thread-safe.
    F. It is susceptible to an exploit attack.

    Explanation :
    A,B. The code is well encapsulated because all instance variables are private, making option A correct. 
    It is susceptible to a denial of service attack since there is no input validation. 
    For example, if the maximum integer value of 2,147,483,647 is passed, then it will make a huge number of calls to the database, 
    potentially tying up the system and blocking valid requests. For this reason, option B is correct. 
    To fix this code, a limit on the inputted value should be used. 
    Option E is incorrect because the class is thread-safe since the instance methods are all synchronized. 
    The rest of the options do not apply to this class.

26. In which scenario is it appropriate for confidential information to be used?

    A. Writing to a log file
    B. Printing a stack trace
    C. Outputting to System.err
    D. Storing in a String
    E. Writing an unsecure email
    F. None of the above

    Explanation :
    F. Confidential information includes things like credit card numbers and passwords. 
    Options A, B, and C are incorrect because they expose confidential information to the environment in which the application is running. 
    Option D is incorrect because it allows the data to enter the String pool, where it can get printed if a memory dump occurs. 
    Option E is incorrect, as passwords should not be sent over email. 
    For these reasons, option F is correct.

27. What statements about the following method are correct? (Choose three.)
    public String checkAlarm(String connectionStr, boolean alarmed)
            throws SQLException {
        var query = "SELECT * FROM office WHERE alarmed = true";
        var con = DriverManager.getConnection(connectionStr);
        var stmt = con.createStatement();
        try (con;
                stmt;
                var rs = stmt.executeQuery(query)) {
            return rs.next() ? rs.getString("address") : null;
        } }

    A. It protects against a denial of service attack.
    B. It does not protect against denial of service attacks.
    C. It protects against SQL injection.
    D. It does not protect against SQL injection because it does not use a PreparedStatement.
    E. Even if the method completes without throwing an exception, a resource leak might occur.
    F. If the method completes without throwing an exception, then no resource leak can occur.

    Explanation :
    B,C,F. While it is permitted to declare a resource outside a try-with-resources statement and still have it be protected, declaring two is not recommended. 
    In particular, if con.createStatement() fails, then the Connection is not closed. For this reason, the code is susceptible to denial of service attacks, making option B correct.
    While it does not use a PreparedStatement, the code is safe from SQL injection because the query does not take any parameters, making option C correct. 
    Finally, if the method completes without throwing an exception, then that means the try-with-resources block was successfully entered. 
    In this case, all resources would have been closed properly making option F correct

28. Which statement best describes this class?
    import java.util.*;
    public final class Ocean {
        private final List<String> algae;
        private final double wave;
        private int sun;

        public Ocean(double wave) {
            this.wave = wave;
            this.algae = new ArrayList<>();
        }

        public int getSun() {
            return sun;
        }
        public void setSun(int sun) {
            sun = sun;
        }
        public double getWave() {
            return wave;
        }
        public List<String> getAlgae() {
            return new ArrayList<String>(algae);
        }
    }

    A. It can be serialized.
    B. It is well encapsulated.
    C. It is immutable.
    D. It is both well encapsulated and immutable.
    E. None of the above as the code does not compile.

    Explanation :
    D. This class does not implement Serializable, so option A is incorrect. 
    This code is well encapsulated because the instance variables are private. 
    The algae and wave variables are immutable because they are marked final, and there are no methods that can change them. 
    The getAlgae() method creates a defensive copy, preventing direct access to the algae object. Finally, the sun variable is initialized to 0 and is not able to be changed after its creation. 
    The setSun() method is missing a this reference, so the assignment sun = sun assigns the method parameter sun to itself. 
    For these reasons, the class is immutable, and option D is correct.

29. Which are true about this class? (Choose three.)
    import java.io.*;
    import java.util.*;
    public final class Forest implements Serializable {
        public final int flora;
        public final List<String> fauna;

        public Forest() {
            this.flora = 5;
            this.fauna = new ArrayList<>();
        }

        public int getFlora() {
            return flora;
        }

        public List<String> getFauna() {
            return new ArrayList<>(fauna);
        }
    }

    A. It is able to be serialized.
    B. It is not able to be serialized.
    C. It is well encapsulated.
    D. It is not well encapsulated.
    E. It is immutable.
    F. It is not immutable.

    Explanation :
    A,D,F. This class implements Serializable and contains serializable instance variables making option A correct. 
    This code is not well encapsulated because the instance variables are public, which matches option D. 
    While a defensive copy of fauna is made in the getter, the instance variable is public, and elements can be added or removed directly. 
    Therefore, the object is not immutable, and option F is correct.

30. You’ve been hired by Charlie Sweets to perform a security audit of their login system. After
    reviewing the following code, what recommendations would best improve the security of
    their system? (Choose three.)
    1: public class CandyFactory {
    2:      boolean check(String username, String password) {
    3:          // IMPLEMENTATION OMITTED
    4:      }
    5:      public void login() {
    6:          var c = System.console();
    7:          if(c != null) {
    8:              var username = c.readLine("Username: ");
    9:              var password = c.readLine("Password: ");
    10:             System.out.println("["+username+","+password+"]");
    11:             System.out.println(check(username,password)
    12:                 ? "Here is your candy"
    13:                 : "No candy for you");
    14: } } }

    A. Mark the check() method final on line 2.
    B. Remove the null check on line 7.
    C. Rewrite to not use var on lines 6, 8, and 9, as it is inherently unsafe.
    D. Rewrite to use readPassword() on line 8.
    E. Rewrite to use readPassword() on line 9.
    F. Change or remove line 10.

    Explanation :
    A,E,F. A malicious attacker could extend this class and override the security check() method, so marking it final is a good idea, making option A correct. 
    Next, the Console class offers a readPassword() method that does not echo what the user types and uses char[] instead of String to avoid a password entering the String pool. For these reasons, option E is correct. 
    Finally, line 10 prints the user’s password to the System.out log file, which is a terrible security idea. It should be changed or removed, making option F correct. 
    The rest of the options are incorrect and do not improve the security of this class

31. Fill in the blanks with the proper method names to serialize an object. (Choose two.)
    import java.io.*;
    public class DeliSandwich implements Serializable {
        public Object____________() throws ObjectStreamException {
            // IMPLEMENTATION OMITTED
        }
        private void______________(ObjectOutputStream out)
                throws IOException {
            // IMPLEMENTATION OMITTED
        }
    }

    A. readResolve in the first blank
    B. writeReplace in the first blank
    C. writeObject in the first blank
    D. writeObject in the second blank
    E. readObject in the second blank
    F. writeReplace in the second blank

    Explanation :
    B,D. The read methods are used as part of deserialization, not serialization, making options A and E incorrect. 
    Option B and D are correct because they use the correct method parameters and return types for writeReplace() and writeObject().

32. Your co-worker has called you in the middle of the night to report all the servers have
    been compromised and have run out of memory. After some debugging, it seems like the
    attacker exploited a file upload resource, but you aren’t sure how since the endpoint has
    a small maximum file size limit. What is the most likely type of attack perpetrated against
    the system?

    A. Denial of service attack
    B. Inclusion attack
    C. Distributed denial of service attack
    D. Exploit attack
    E. SQL injection
    F. Injection attack

    Explanation :
    B. An inclusion attack is one in which multiple components are embedded within a single file, such as zip bomb or XML exploit (billion laughs attack). 
    Since the maximum file size is given to be small, this would be the most likely type of attack used, making option B correct. 
    Note that if the file size was not limited, then this could be a regular denial of service attack in which a large file is sent repeatedly to overwhelm the system

33. Which statements about the following class are correct? (Choose three.)
    import java.security.*;
    import java.util.*;
    public class UserProfile {
        private static class UserEntry {
            private final UserProfile value;
            private final Permission permission;
            // Constructors/Getters Omitted
        }
        public static Permission getPermission(String check) {
            // Implementation Omitted
        }
        private static Map<String,UserEntry> data = new HashMap<>();
        public static UserProfile getProfile(String check) {
            var securityRecord = data.get(check);
            if (securityRecord != null)
                return securityRecord.getValue(); // h1
            var permission = getPermission(check);
            var permCol = permission.newPermissionCollection();
            permCol.add(permission);
            var prof = AccessController.doPrivileged( // h2
                new PrivilegedAction<UserProfile>() {
                    public UserProfile run() {
                        return new UserProfile();
                }},
                new AccessControlContext(
                    new ProtectionDomain[] {
                        new ProtectionDomain(null, permCol)
                }));
            data.put(check, new UserEntry(prof, permission)); // h3
            return prof;
        } }

    A. Line h1 properly validates security.
    B. Line h1 presents an unacceptable security risk.
    C. Line h2 elevates security privileges.
    D. Line h2 does not elevate security privileges.
    E. Line h3 violates security guidelines by allowing security information to be cached.
    F. Line h3 does not violate security guidelines.

    Explanation :
    B,C,F. Caching permissions for a user is allowed, so option F is correct. 
    That said, the security on using the cached data must be checked. 
    The class is missing calls to AccessController.checkPermission() before lines h1 and h2. 
    On line h1, this can result in a user reading a cached permission they do not have access to, making option B correct. 
    On line h2, security permissions could be elevated since access is not checked, making option C correct.

34. For which value of name will this code result in a successful SQL injection attack?
    public Integer getScore(String connectionStr, String name)
            throws SQLException {
        var query = "SELECT score FROM records WHERE name = ?";
        var con = DriverManager.getConnection(connectionStr);
        try (con; var stmt = con.prepareStatement(query)) {
            stmt.setString(1, name);
            try(var rs = stmt.executeQuery()) {
                if(rs.next()) return rs.getInt("score");
            }
        }
        return null;
    }

    A. DELETE TABLE records;
    B. 'Olivia'; DELETE TABLE records
    C. 'Sophia; DELETE TABLE records
    D. 'Elysia'; DELETE TABLE records
    E. ?; DELETE TABLE records;
    F. None of the above

    Explanation :
    F. The query uses a PreparedStatement so that the name is properly escaped. For this reason, SQL injection is not possible, and option F is correct. 
    For the exam, you don’t need to know how to write a query to cause SQL injection, just how to prevent it.

35. Which are requirements for a class to be immutable? (Choose three.)

    A. A private constructor is provided.
    B. Any instance variables are private.
    C. Any instance variables are initialized in a constructor.
    D. Methods cannot be overridden.
    E. There are no setter methods.
    F. Any instance variables are marked final.

    Explanation :
    B,D,E. An immutable class can have public constructors, so option A is incorrect. 
    Options B, D, and E make up the requirements for an immutable class. 
    Option D can be fulfilled by making the class final or marking the methods final.
    Option C is incorrect because instance variables can still be declared with a value or set by an instance initializer. 
    Option F is also incorrect. While it is common to mark instance variables final, as long as there is no way for them to be changed after the constructor is executed, 
    the class can still be considered immutable.

36. Which of the following are not typically considered denial of service attacks? (Choose two.)

    A. Downloading confidential information from a log file
    B. Uploading a very large file
    C. Performing SQL injection
    D. Passing invalid numbers to trigger overflow or underflow
    E. Exploiting a database resource leak
    F. Uploading a zip bomb

    Explanation :
    A,C. A denial of service attack is one in which one or more requests attempt to overwhelm the system and disrupt legitimate requests. 
    Option A is an access or confidentiality problem. 
    Option C is about gaining access or changing data that the user should not be permitted to. 
    Options B, D, E, and F are all denial of service attacks because they increase load in an attempt to bring a system down. 
    Remember, a zip bomb is when a small file is expanded to become a much larger file.

37. The following code prints false. Which statements best describe the Fruit class?
    (Choose three.)
    var original = new Fruit();
    original.sweet = new ArrayList<>();
    var cloned = (Fruit) original.clone();
    System.out.print(original.sweet == cloned.sweet);

    A. It does not implement Cloneable.
    B. It performs a deep copy.
    C. It performs a shallow copy.
    D. It overrides clone().
    E. It implements Cloneable.
    F. It does not override clone().

    Explanation :
    B,D,E. The Fruit class must implement Cloneable; otherwise, an exception would be thrown at runtime, making option E correct. 
    The Fruit class must also override the clone() method. If it did not, then a shallow copy would be performed on the sweet object, 
    resulting in the code printing true at runtime. Since this is not the case, option D is correct. 
    Finally, we’ve already ruled out a shallow copy, so by process of elimination it must perform a deep copy.
    For this reason, option B is correct.

38. What are the best ways to prevent SQL injection? (Choose two.)

    A. Avoid SQL statements that take query parameters.
    B. Log an error anytime a SQL injection attack is successful.
    C. Avoid concatenating user input into a query string.
    D. Ensure database resources are closed.
    E. Always use a PreparedStatement instead of a Statement.
    F. Do not use a relational database.

    Explanation :
    C,E. The primary way SQL injection occurs is from concatenating SQL queries without properly escaping the values. 
    Avoiding concatenation and using a PreparedStatement with bind variables are the commonly accepted ways to prevent this. 
    For these reasons, options C and E are correct.
    Option A is incorrect because a database that takes no query parameters of any kind would be pretty limited in its capabilities. 
    For example, it would be challenging to log a user in if you couldn’t search for that user. 
    Option B is also incorrect, as you can’t prevent a SQL injection after it is already successful. 
    Option D is incorrect, as a resource leak is more susceptible to a denial of service attack in which resources are exploited, rather than SQL injection in which data is manipulated. 
    Finally, option F is incorrect, as avoiding using a relational database is not a commonly accepted practice for avoiding SQL injection

39. Given the following two classes, what change to the StealSecret class would allow it to read
    and email the password to a hacker?
    public class Secret {
        private String mySecret;
        public void setSecret(String secret) {
            mySecret = secret;
        }
        public void printSecret() {
            throw new UnsupportedOperationException("Nope!");
        }
        private void saveToDisk() {
            // IMPLEMENTATION OMITTED
        }
    }

    public class StealSecret extends Secret {
        // DO BAD STUFF
    }

    A. There are no changes, as the Secret class is secure.
    B. Override the mySecret variable.
    C. Override the setSecret() method.
    D. Override the printSecret() method.
    E. Override the saveToDisk() method.
    F. Add a constructor.

    Explanation :
    C. Option C is the correct answer. A hacker could override the setSecret() method 
    to first steal the inputted secret value and email it herself and then pass the data along 
    to the parent by calling super.setSecret() without anyone noticing any difference. 
    One fix would be to mark this method final in the Secret class or make the Secret class final.
    Option B is incorrect because variables can only be hidden, not overridden, so declaring a new mySecret variable would not grant access to the parent variable. 
    Option D is incorrect as overriding this method won’t allow the attacker to access the mySecret variable directly. 
    Option E is trivially incorrect, as private methods cannot be overridden. 
    Finally, option F is incorrect as adding a constructor does not grant access to private members in the parent class.

40. Which statement about the following classes is correct?
    import java.util.*;
    final class Faucet {
        private final String water;
        private final List<Double> pipes;
        public Faucet(String water, List<Double> pipes) {
            this.water = water;
            this.pipes = pipes;
        }
        public String getWater() { return water; }
        public List<Double> getPipes() { return pipes; } }
    public final class Spout {
        private final String well;
        private final List<Boolean> buckets;
        public Spout(String well, List<Boolean> buckets) {
            this.well = well;
            this.buckets = new ArrayList<>(buckets);
        }
        public String getWell() { return well; }

        public List<Boolean> getBuckets() {
            return new ArrayList<>(buckets);
        } 
    }

    A. Only Faucet is immutable.
    B. Only Spout is immutable.
    C. Both classes are immutable.
    D. Neither class is immutable.
    E. None of the above as one of the classes does not compile.

    Explanation :
    B. An immutable class must not allow the state to change. 
    In the Faucet class, the caller has a reference to the List being passed in and can change the size or elements in it.
    Similarly, any class with a reference to the object can get the List by calling get() and make these changes. 
    The Faucet class is not immutable. 
    The Spout class shows how to fix these problems and is immutable, making option B correct.
    





















































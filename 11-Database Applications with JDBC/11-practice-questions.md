
1. How many of Connection, Driver, DriverManager, PreparedStatement, and
    ResultSet are JDBC interfaces included with the JDK?

    A. None
    B. One
    C. Two
    D. Three
    E. Four
    F. Five

    Explanation :
    E. Connection is a JDK interface for communicating with the database. PreparedStatement and ResultSet are typically used to write queries and are also in the JDK. 
    Driver is tricky because you don’t write code that references it directly. However, you are still required to know it is a JDBC interface. 
    DriverManager is used in JDBC code to get a Connection. However, it is a concrete class rather than an interface. 
    Since only four out of the five are JDBC interfaces, option E is correct

2. Which is found in the java.sql package that come with the standard JDK?
    
    A. Only DerbyDriver
    B. Only MySqlDriver
    C. Only OracleDriver
    D. DerbyDriver, MySqlDriver, OracleDriver
    E. Only DerbyDriver and MySqlDriver
    F. None of these

    Explanation :
    F. Database-specific implementation classes are not in the java.sql package. 
    The implementation classes are in database drivers and have package names that are specific to the database. Therefore, option F is correct. 
    The Driver interface is in the java.sql package. Note that these classes may or may not exist. 
    You are not required to know the names of any database-specific classes, so the creators of the exam are free to make up names.

3. What must be the first characters of a database URL?
    A. db,
    B. db:
    C. jdbc,
    D. jdbc:
    E. None of the above

    Explanation :
    D. All JDBC URLs begin with the protocol jdbc followed by a colon as a delimiter. 
    Option D is the only one that does both of these, making it the correct answer

4. Which is responsible for getting a connection to the database?
    A. Driver
    B. Connection
    C. PreparedStatement
    D. Statement
    E. ResultSet

    Explanation :
    A. The Driver interface is responsible for getting a connection to the database, making option A the answer. 
    The Connection interface is responsible for communication with the database but not making the initial connection. 
    The Statement interface knows how to run the SQL query, and the ResultSet interface knows what was returned by a SELECT query.

5. Which of these obtains a Connection?
    A. Connection.getConnection(url)
    B. Driver.getConnection(url)
    C. DriverManager.getConnection(url)
    D. new Connection(url)
    E. None of the above

    Explanation :
    C. Connection is an interface. 
    Since interfaces do not have constructors, option D is incorrect. 
    The Connection class doesn’t have a static method to get a Connection either, making option A incorrect. 
    The Driver class is also an interface without static methods, making option B incorrect. 
    Option C is the answer because DriverManager is the class used in JDBC to get a Connection.

6. Which method in DriverManager is overloaded to allow passing a username
    and password?
    A. conn()
    B. connect()
    C. forName()
    D. getStatement()
    E. open()
    F. None of the above

    Explanation :
    F. The DriverManager.getConnection() method can be called with just a URL. 
    It is also overloaded to take the URL, username, and password. 
    Since this is not one of the options, the answer is option F

7. What is the output if the clowns database exists and contains an empty clowns table?
    var url = "jdbc:derby:clowns;create=true";
    var sql = "SELECT count(*) FROM clowns";
    try (var conn = DriverManager.getConnection(url);
        var stmt = conn.prepareStatement(sql);
        var rs = stmt.executeQuery()) {
        System.out.println(rs.getInt(1));
    }

    A. 0
    B. 1
    C. The code does not compile.
    D. The code compiles but throws an exception at runtime.

    Explanation :
    D. This code is missing a call to rs.next(). As a result, rs.getInt(1) throws a SQLException with the message Invalid cursor state – no current row. 
    Therefore, option D is the answer.

8. Consider the three methods execute(), executeQuery(), and executeUpdate().
    Fill in the blanks: _______ of these methods is/are allowed to run a DELETE SQL statement
    while ________ of these methods is/are allowed to run an UPDATE SQL statement.

    A. None, one
    B. One, none
    C. One, one
    D. One, two
    E. Two, two
    F. Three, three

    Explanation :
    E. The execute() method is allowed to run any type of SQL statements. 
    The executeUpdate() method is allowed to run any type of the SQL statement that returns a row count rather than a ResultSet. 
    Both DELETE and UPDATE SQL statements are allowed to be run with either execute() or executeUpdate(). 
    They are not allowed to be run with executeQuery() because they do not return a ResultSet. 
    Therefore, option E is the answer

9. Suppose the pandas table has one row with the name Mei Xiang and the location DC.
    What does the following code output?
    var url = "jdbc:derby:pandas";
    var sql = "SELECT name FROM pandas WHERE location = 'DC'";
    try (var conn = DriverManager.getConnection(url); // s1
        var stmt = conn.prepareStatement(sql); // s2
        var rs = stmt.executeQuery()) {
    if (rs.next())
        System.out.println(rs.getString("name"));
    else
        System.out.println("No match");
    }

    A. Mei Xiang
    B. No match
    C. The code does not compile due to line s1.
    D. The code does not compile due to line s2.
    E. The code does not compile due to another line.
    F. The code throws an exception at runtime.

    Explanation :
    A. This code uses a PreparedStatement without bind variables (?). While it would be better to use bind variables, this code does run. 
    The ResultSet has one value and does print Mei Xiang successfully. Therefore, option A is the answer

10. Suppose we have a peacocks table with two columns: name and rating. What does the following
    code output if the table is empty?
    var url = "jdbc:derby:birds";
    var sql = "SELECT name FROM peacocks WHERE name = ?";
        try (var conn = DriverManager.getConnection(url);
        var stmt = conn.prepareStatement(sql)) { // s1
        stmt.setString(1, "Feathers");
        stmt.setString(2, "Nice");
        boolean result = stmt.execute(); // s2
        System.out.println(result);
    }

    A. false
    B. true
    C. The code does not compile due to line s1.
    D. The code does not compile due to line s2.
    E. The code does not compile due to another line.
    F. The code throws an exception at runtime.

    Explanation :
    F. While the table has two columns, the SQL query has only one bind variable (?). 
    Therefore, the code throws an exception when attempting to set the second bind variable, and option F is correct.

11. Suppose we have an empty bunny table with two columns: name and color. What is the state
    of the table after running this code?
    var url = "jdbc:derby:bunnies";
    var sql = "INSERT INTO bunny(name, color) VALUES (?, ?)";
    try (var conn = DriverManager.getConnection(url);
        var stmt = conn.prepareStatement(sql)) { // s1

        stmt.setString(1, "Daisy");
        stmt.setString(2, "Brown");

        stmt.executeUpdate();

        stmt.setString(1, "Cinna");
        stmt.setString(2, "Brown");

        stmt.executeUpdate();
    }

    A. It has one row.
    B. It has two rows, and the color is Brown in both.
    C. The code does not compile due to line s1.
    D. The code does not compile due to line s2.
    E. The code does not compile due to another line.
    F. The code throws an exception at runtime.

    Explanation :
    B. This code is correct. It executes the first update to add the first row and then sets the parameters for the second. 
    When it updates the second time, it adds the second row. Therefore, option B is the answer

12. What is the name of a concrete class that implements Statement and is included in
    the core JDK?
    A. CallableStatement
    B. PreparedStatement
    C. StatementImpl
    D. Both A and B
    E. None of the above

    Explanation :
    E. CallableStatement and PreparedStatement are interfaces that extend the Statement interface. You don’t need to know that for the exam. 
    You do need to know that a database driver is required to provide the concrete implementation class of Statement rather than the JDK. 
    This makes option E correct.

13. Given the table books in the figure and a ResultSet created by running the following SQL
    statement, which option prints the value 379?
    ----------------------------------------------
    |  title varchar(255)  |  num_pages integer  |
    ----------------------------------------------
    |  Beginning Java      |  379                |
    |  Advanced Java       |  669                |
    ----------------------------------------------
    
    SELECT * FROM books WHERE title = 'Beginning Java'
    A. System.out.println(rs.getInt(1));
    B. System.out.println(rs.getInt(2));
    C. System.out.println(rs.getInteger(1));
    D. System.out.println(rs.getInteger(2));

    B. Unlike arrays, JDBC uses one-based indexes. Since num_pages is in the second column, the parameter needs to be 2, ruling out options A and C. 
    Further, there is not a method named getInteger() on the ResultSet interface, ruling out option D. 
    Since the proper method is getInt(), option B is the answer.

14. Given the table books in the previous question and the following code, which lines would
    you add to successfully insert a row? (Choose two.)
    var url = "jdbc:derby:books;create=true";
    var sql = "INSERT INTO books (title,num_pages) VALUES(?,?)";
    try (var conn = DriverManager.getConnection(url);
            var stmt = conn.prepareStatement(sql)) {
        // INSERT CODE HERE
        stmt.executeUpdate();
    }
    A. stmt.setObject(0, "Intermediate Java");
    B. stmt.setObject(1, "Intermediate Java");
    C. stmt.setObject(1, 500);
    D. stmt.setObject(2, 500);

    Explanation :
    B,D. Since JDBC does not begin indexes with zero, option A is incorrect, and option B is correct. 
    Similarly, the second parameter is at index 2, so option C is incorrect, 
    and option D is the other answer. 
    Note that setObject() can be called instead of a more specific type.

15. Given the table books from the previous two questions and a ResultSet created by
    running this SQL statement, which option prints Advanced Java?
    SELECT title FROM books WHERE num_pages > 500
    
    A. System.out.println(rs.getString());
    B. System.out.println(rs.getString("0"));
    C. System.out.println(rs.getString("1"));
    D. System.out.println(rs.getString("title"));
    E. None of the above

    Explanation :
    D. Option A does not compile because you have to pass a column index or column name to the method. 
    Options B and C compile. However, there are not columns named 0 or 1. 
    Since these column names don’t exist, the code would throw a SQLException at runtime. 
    Option D is correct as it uses the proper column name.

16. Which of the following could be valid JDBC URL formats for an imaginary driver named
    magic and a database named box?
    String first = "jdbc:magic:127.0.0.1:1234/box";
    String second = "jdbc:magic:box";
    String third = "jdbc@magic:@127.0.0.1:1234";

    A. Only first
    B. Only second
    C. Only third
    D. Both first and second
    E. Both first and third
    F. All of these

    Explanation :
    D. A JDBC URL has three components separated by colons. All three of these URLs meet those criteria. 
    For the data after the component, the database driver specifies the format. 
    Depending on the driver, this might include an IP address and port. Regardless, it needs to include the database name or alias. 
    The first and second URLs could both be valid formats because they mention the database box. 
    However, third is incorrect because it has jdbc@ instead of jdbc:. Therefore, option D correct.

17. Which is a benefit of PreparedStatement over Statement? (Choose two.)
    A. Language independence
    B. NoSQL support
    C. Readability
    D. Security
    E. Supports stored procedures

    Explanation :
    C,D. JDBC uses Java and SQL, so it is not language independent, making option A incorrect. 
    It is used with relational databases, ruling out option B. A CallableStatement supports 
    stored procedures, not a PreparedStatement, making option E incorrect.
    
    Options C and D are correct. Using bind variables with a PreparedStatement produces 
    code that is easier to read than one with a lot of String concatenation. Further, when used 
    properly, a PreparedStatement prevents SQL injection.

18. Assuming the clowns database exists and contains one empty table named clowns, what is the
    output of the following?
    var url = "jdbc:derby:clowns";
    var sql = "SELECT * FROM clowns";
    try (var conn = new Connection(url); // s1
        var stmt = conn.prepareStatement(sql); // s2
        var rs = stmt.executeQuery()) { // s3
        if (rs.next())
            System.out.println(rs.getString(1));
        }
    }

    A. The code terminates successfully without any output.
    B. The code does not compile due to line s1.
    C. The code does not compile due to line s2.
    D. The code does not compile due to line s3.
    E. None of the above.

    Explanation :
    B. Connection is an interface rather than a concrete class. 
    Therefore, it does not have a constructor and line s1 does not compile. As a result, option B is the answer. 
    Option A would be the answer if the code new Connection() was changed to DriverManager.getConnection().

19. What is the correct order to close database resources?
    A. Connection then PreparedStatement then ResultSet
    B. Connection then ResultSet then PreparedStatement
    C. PreparedStatement then Connection then ResultSet
    D. PreparedStatement then ResultSet then Connection
    E. ResultSet then PreparedStatement then Connection
    F. None of the above

    Explanation :
    E. When manually closing database resources, they should be closed in the reverse order from which they were opened. 
    This means the ResultSet object is closed before the Statement object and the Statement object is closed before the Connection object. 
    This makes option E the answer

20. Assuming the clowns database exists and contains one empty table named clowns, what is the
    output of the following?
    var url = "jdbc:derby:clowns";
    var sql = "SELECT * FROM clowns";
    try (var conn = DriverManager.getConnection(url); // s1
        var stmt = conn.prepareStatement(sql); // s2
        var rs = stmt.executeQuery()) { // s3
        if (rs.next())
            System.out.println(rs.getString(1));
        }
    }

    A. The code terminates successfully without any output.
    B. The code does not compile due to line s1.
    C. The code does not compile due to line s2.
    D. The code does not compile due to line s3.
    E. None of the above.

    Explanation :
    A. This code correctly obtains a Connection and PreparedStatement. It then runs a query, getting back a ResultSet without any rows. 
    The rs.next() call returns false, so nothing is printed, making option A correct.

21. Suppose we have a bunny table with two columns: name and color. What does the following
    code output if the table is empty?
    var url = "jdbc:derby:bunnies";
    var sql =
        "SELECT count(*) FROM bunny WHERE color = ? and name = ?";
    try (var conn = DriverManager.getConnection(url);
        var stmt = conn.prepareStatement(sql)) { // s1
        stmt.setString(1, "White");
        try (var rs = stmt.executeQuery()) { // s2
            if (rs.next())
                System.out.println(rs.getInt(1));
        }
    }

    A. 0
    B. 1
    C. The code does not compile due to line s1.
    D. The code does not compile due to line s2.
    E. The code does not compile due to another line.
    F. The code throws an exception at runtime.

    Explanation :
    F. The SQL query has two bind variables, but the code sets only one. 
    This causes a SQLException when executeQuery() is called, 
    making option F the answer.

22. Suppose the pandas table has one row with the name Mei Xiang and the location DC.
    What does the following code output?
    var url = "jdbc:derby:pandas";
    var sql = "SELECT name FROM pandas WHERE location = ?";
    try (var conn = DriverManager.getConnection(url); // s1
        var stmt = conn.prepareStatement(sql)) { // s2
        stmt.setString(1, "DC");
        try (var rs = stmt.executeQuery()) {
            if (rs.next())
                System.out.println(rs.getString("name"));
            else
                System.out.println("No match");
        }
    }

    A. Mei Xiang
    B. No match
    C. The code does not compile due to line s1.
    D. The code does not compile due to line s2.
    E. The code does not compile due to another line.
    F. The code throws an exception at runtime.

    Explanation :
    A. This code uses a PreparedStatement and properly sets a bind variable (?). 
    The ResultSet has one value and does print Mei Xiang successfully. 
    Therefore, option A is the answer.

23. Which statement is true about the JDBC core classes?
    A. Driver is an implementation of DriverManager.
    B. A general Connection implementation is included in the JDK.
    C. A PreparedStatement uses bind variables.
    D. None of the above.

    Explanation :
    C. Option A is incorrect because Driver is an interface, while DriverManager is a concrete class. 
    The inverse isn’t true either; DriverManager doesn’t implement Driver. 
    Option B is incorrect because the Connection implementation comes from a specific database driver JAR. 
    Option C is correct as bind variables (?) are used.

24. Which is true if the clowns database exists and contains an empty clowns table?
    var url = "jdbc:derby:clowns";
    var sql = "SELECT COUNT(*) FROM clowns";
    try (var conn = DriverManager.getConnection(url);
        var stmt = conn.prepareStatement(sql);
        var rs = stmt.executeQuery()) {
        rs.next(); // r1
        System.out.println(rs.getInt(1)); // r2
    }

    A. The code compiles and prints 0 without error.
    B. The code compiles and prints 1 without error.
    C. The code does not compile.
    D. The code compiles but throws an exception at runtime on line r1.
    E. The code compiles but throws an exception at runtime on line r2.

    Explanation :
    A. The count(*) function in SQL always returns a number. In this case, it is the number zero. 
    This means line r1 executes successfully because it positions the cursor at that row. 
    Line r2 also executes successfully and prints 0, which is the value in the row. 
    Since the code runs successfully, option A is the answer.

25. Suppose we have an empty bunny table with two columns: name and color. What is the state
    of the table after running this code?
    var url = "jdbc:derby:bunnies";
    var sql = "INSERT INTO bunny(name, color) VALUES (?, ?)";
    try (var conn = DriverManager.getConnection(url);
        var stmt = conn.prepareStatement(sql)) { // s1
        stmt.setString(1, "Hoppy");
        stmt.setString(2, "Brown");

        stmt.executeUpdate();

        stmt.setString(1, "Daisy");

        stmt.executeUpdate();
    }
    A. Only one row has the color Brown set.
    B. It has two rows, and the color is Brown in both.
    C. The code does not compile due to line s1.
    D. The code does not compile due to line s2.
    E. The code does not compile due to another line.
    F. The code throws an exception at runtime.

    Explanation :
    B. This code is correct. It executes the first update to add the first row and then sets the parameters for the second. 
    For the second update, only one parameter is set. The other is reused since it was set earlier. 
    Therefore, option B is the answer

26. Which are true statements? (Choose two.)
    A. A PreparedStatement is generally faster than a Statement when each is run 100 times.
    B. A PreparedStatement is generally slower than a Statement when each is run 100 times.
    C. A PreparedStatement is generally the same speed as a Statement when each is run 100 times.
    D. PreparedStatement extends Statement
    E. Statement extends PreparedStatement
    F. PreparedStatement and Statement are not in the same inheritance hierarchy.

    Explanation :
    A,D. The PreparedStatement interface extends the Statement interface, which matches option D. 
    One of the benefits of a PreparedStatement is performance. 
    While a PreparedStatement may not be faster if run only once, it will quickly become so. 
    Therefore, option A is the other correct answer.

27. Which is true of a PreparedStatement?
    A. It has a method to change the bind variable to a different character other than ?.
    B. It can be used only for SELECT statements.
    C. It can be used only for UPDATE statements.
    D. All of these are true.
    E. None of these are true.

    Explanation :
    E. In JDBC, the bind variable is always a question mark (?), making option A incorrect. 
    A PreparedStatatement is not limited to specific types of SQL, making options B and C incorrect as well. 
    This makes option E the correct answer

28. Suppose we have a peacocks table with two columns: name and rating. What does the
    following code output if the table is empty?
    var url = "jdbc:derby:birds";
    var sql = "SELECT name FROM peacocks WHERE name = ?";
    try (var conn = DriverManager.getConnection(url);
        var stmt = conn.prepareStatement(sql)) { // s1
        stmt.setString(1, "Feathers");
        System.out.println(stmt.executeUpdate()); // s2
    }
    
    A. false
    B. true
    C. The code does not compile due to line s1.
    D. The code does not compile due to line s2.
    E. The code does not compile due to another line.
    F. The code throws an exception at runtime.

    Explanation :
    F. While this code compiles, it isn’t right. Since we have a SELECT statement, we should be calling execute() or executeQuery(). 
    Option F is the answer because the code throws an exception when attempting to call executeUpdate().

29. What is the most likely outcome of this code if the people table is empty?
    6: var stmt = conn.prepareStatement("SELECT * FROM people");
    7: var rs1 = stmt.executeQuery();
    8: var rs2 = stmt.executeQuery();
    9: System.out.println(rs1.next() + " " + rs2.next());

    A. It prints false false.
    B. It prints true false.
    C. It does not terminate.
    D. It throws a SQLException.
    E. None of the above.

    Explanation :
    D. When running a query on a PreparedStatement, Java closes any already open ResultSet objects associated with the statement. 
    This means that rs1 is closed on line 8. 
    Therefore, it throws a SQLException on line 9 because we are trying to call next() on a closed ResultSet, and option D is correct.

30. What is the most likely outcome of this code if the bunnies table is empty?
    var url = "jdbc:derby:bunnies";
    var sql = "INSERT INTO bunny(name, color) VALUES (?, ?)";
    try (var conn = DriverManager.getConnection(url);
        var stmt = conn.createStatement()) {
        stmt.setString(1, "Hoppy");
        stmt.setString(2, "Brown");
        stmt.executeUpdate(sql);
    }

    A. One row is in the table.
    B. Two rows are in the table.
    C. The code does not compile.
    D. The code throws a SQLException.

    Explanation :
    C. This question is trickier if you know more JDBC than is on the exam. 
    If you know only what is on the exam, you would assume the createStatement() method doesn’t exist. 
    However, it does, and stmt is a Statement object. Since setString() does not exist on Statement, the code does not compile. 
    This means the answer is option C regardless of your level of knowledge of JDBC
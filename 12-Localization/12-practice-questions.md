

1. Which of the following are considered locales? (Choose three.)
    A. Cultural region
    B. Local address
    C. City
    D. Time zone region
    E. Political region
    F. Geographical region

    Explanation :
    A,E,F. Oracle defines a locale as a geographical, political, or cultural region, making options A, E, and F correct. 
    A local address and city are too granular for a locale. Also, time zones often span multiple locales

2. Assuming the key green is in all five of the files referenced in the options, which file will the
    following code use for the resource bundle?
    Locale.setDefault(new Locale("en", "US"));
    var rb = ResourceBundle.getBundle("Colors", new Locale("fr"));
    System.out.print(rb.getString("green"));
    
    A. Colors_default.properties
    B. Colors.properties
    C. Colors_en.properties
    D. Colors_US.properties
    E. Colors_en_US.properties
    F. None of the above

    Explanation:
    E. Java starts out by looking for a properties file with the requested locale, which in this case is the fr language. 
       It doesn’t find it, so it moves onto the default locale en_US, which it does find, making option E correct.

3. When localizing an application, which type of data varies in presentation depending on locale?
    A. Currencies
    B. Dates
    C. Both
    D. Neither

    Explanation:
    C. Currencies vary in presentation by locale. For example, 9,000 and 9.000 both represent nine thousand, depending on the locale. 
    Similarly, for dates, 01-02-2022 and 02-01-2022 represent January 2, 2022, or February 1, 2020, depending on the locale. 
    This makes option C the answer

4. How do you find out the locale of the running program?
    A. Locale.get("default")
    B. Locale.get(Locale.DEFAULT)
    C. Locale.of()
    D. Locale.now()
    E. Locale.getDefault()
    F. None of the above

    Explanation :
    E. The Locale object provides getDefault() and setDefault() methods for working with the default locale, so option E is correct.
    The rest of the methods do not exist in the Locale class.

5. How long will the effects of calling Locale.setDefault() be active assuming no other calls to that method are made?
    A. Until the end of the method.
    B. Until the program exits.
    C. Until the next reboot of the computer.
    D. It persists after reboot.
    E. None of the above.

    Explanation :
    B. Calling Locale.setDefault() changes the default locale within the program. It does  not change any settings on the computer. 
    The next time you run a Java program, it will have the original default locale rather than the one you changed it to.

6. What is the output of the following code snippet?
    var d = LocalDateTime.parse("2022-01-21T12:00:00", DateTimeFormatter.ISO_LOCAL_DATE_TIME);
    System.out.print(d.format(DateTimeFormatter.ISO_LOCAL_DATE));
    
    A. 2022-00-21
    B. 2022-00-22
    C. 2022-01-21
    D. 2022-01-22
    E. The code does not compile.
    F. An exception is thrown at runtime.

    Explanation :
    C. The code compiles and runs without issue. The data is in a valid date format, so the text is parsed as January 21, 2022. 
    Date values are indexed from 1, not 0, making option C the correct output. 
    Note that a date formatter is able to format a date/time value, as the time element can be discarded.

7. What is the output if the solveMystery() method is applied to a Properties object
    loaded from mystery.properties?
    mystery.properties
    mystery=bag
    type=paper
    void solveMystery(Properties props) {
        var a = props.get("mystery");
        var b = props.get("more", null);
        var c = props.get("more", "trick");
        System.out.print(a + " " + b + " " + c);
    }

    A. bag ? trick
    B. bag ? null
    C. bag null null
    D. bag null trick
    E. The code does not compile.
    F. An exception is thrown at runtime.

    Explanation :
    E. The first line of the method is correct, as Properties inherits Map and has a get() method. 
    The get() method does not have an overloaded version that takes a default value, though. For this reason, the second and third get() calls do not compile, and option E is correct. 
    If getProperty() were instead used on the second and third call, then the output would be bag null trick

8. Fill in the blank with the option that allows the code snippet to compile and print a message
    without throwing an exception at runtime.
    var x = LocalDate.of(2022, 3, 1);
    var y = LocalDateTime.of(2022, 3, 1, 5, 55);
    var f = DateTimeFormatter.ofPattern("MMMM' at 'h' o'clock'");
    System.out.print( );
    
    A. f.formatDate(x)
    B. f.formatDate(y)
    C. f.format(x)
    D. f.format(y)
    E. The code does not compile regardless of what is placed in the blank.
    F. None of the above.

    Explanation :
    F. Options A and B are incorrect because formatDate() is not a valid method name in DateTimeFormatter. 
    Option E is incorrect because the code compiles if either option C or D is used. Both options C and D will produce an exception at runtime, 
    though, as the date pattern is invalid. In particular, the apostrophe in o'clock should be escaped. 
    Option C is also incorrect because there is no hour value h for a LocalDate. If the pattern string was corrected with o''clock, 
    then option D would be correct and print March at 5 o'clock at runtime

9. Which of the following are valid locale formats? (Choose two.)

    A. hi
    B. hi_IN
    C. IN_hi
    D. in_hi
    E. HI_IN
    F. IN

    Explanation :
    A,B. In Java, a locale can be represented by a language code in lowercase, or a language and country code, with language in lowercase and country in uppercase. 
    For these reasons, options A and B are correct. 
    Options C, D, and E are incorrect because the lowercase language must be before the uppercase country. 
    Option F is incorrect because the language is missing. 
    Remember, the exam won’t expect you to know which language and country codes exist, but it will expect you to know how to use them.

10. Assuming the key indigo is in all five of the files referenced in the options, which file will the
    following code use for the resource bundle?
    Locale loc = new Locale("fr", "CH");
    Locale.setDefault(new Locale("it", "CH"));
    ResourceBundle rb = ResourceBundle.getBundle("Colors", loc);
    rb.getString("Indigo");

    A. Colors_default.properties
    B. Colors_en_US.properties
    C. Colors_CH.properties
    D. Colors_en.properties
    E. Colors_es.properties
    F. None of the above

    Explanation :
    F. Java starts out by looking for a properties file with the requested locale, which in this case is the fr_CH language and country. 
    It doesn’t find Colors_fr_CH.properties, so it moves onto the locale with just a language code fr. 
    It also does not find Colors_fr.properties. It then moves on to the default locale it_CH checking Colors_it_CH.properties, 
    but there is still no match. It drops the country code and checks it for Colors_it.properties, but still doesn’t find a match. 
    Lastly, it checks for a Colors.properties file but since that’s not an option, it fails. 
    The result is a MissingResourceException is thrown at runtime, making option F correct.

11. For currency, the US uses the $ symbol, the UK uses the £ symbol, and Germany uses the €
    symbol. Given this information, what is the expected output of the following code snippet?
    Locale.setDefault(Locale.US);
    Locale.setDefault(Category.FORMAT, Locale.GERMANY);
    System.out.print(NumberFormat.getCurrencyInstance(Locale.UK).format(1.1));

    A. $1.10
    B. 1,10€
    C. £1.10
    D. The code does not compile.
    E. An exception is thrown at runtime.
    F. The output cannot be determined without knowing the locale of the system where it will
    be run.

    Explanation :
    C. The code compiles, so option D is incorrect. 
    In this sample, the default locale is set to US, while the default locale format is set to GERMANY. Neither is used for formatting the value, 
    as getCurrencyInstance() is called with UK as the locale. 
    For this reason, the £ symbol is used, making option C correct

12. Given the following four properties files, what does this code print?
    -----------------------------------------------------------------------------------------
    | Cars_en.properties | Cars.properties | Cars_en_US.properties |  Cars_fr_FR.properties |
    -----------------------------------------------------------------------------------------
    | engine=engine      | engine=moteur   | country=US            |  country=France        |
    | horses=241         | country=earth   | horses=45             |  road=autoroute        |
    |                    | road=highway    |                       |                        |
    -----------------------------------------------------------------------------------------

    Locale.setDefault(new Locale("en"));
    var rb = ResourceBundle.getBundle("Cars",new Locale("de", "DE"));
    var r1 = rb.getString("engine");
    var r2 = rb.getString("horses");
    var r3 = rb.getString("country");
    System.out.print(r1+ " " + r2 + " " + r3);

    A. null null null
    B. engine 241 US
    C. moteur 45 US
    D. engine 241 earth
    E. moteur 241 earth
    F. An exception is thrown at runtime.

    Explanation :
    D. The getBundle() does not find Cars_de_DE.properties or Cars_de.properties, 
    so it moves on to the default locale. Since Cars_en.properties is available, it will use this file, falling back to Cars.properties if any values are not available. 
    Therefore, it selects engine and horses from the first file, and country from the second file, 
    printing engine 241 earth and making option D correct.

13. Given the four properties files in question 12, what does this code print?
    Locale.setDefault(new Locale("en", "US"));
    var rb = ResourceBundle.getBundle("Cars", new Locale("fr", "FR"));
    var s1 = rb.getString("country");
    var s2 = rb.getString("horses");
    var s3 = rb.getString("engine");
    System.out.print(s1+ " " + s2 + " " + s3);
    
    A. France null engine
    B. France 241 moteur
    C. France 45 moteur
    D. France 241 engine
    E. France 45 engine
    F. An exception is thrown at runtime.

    Explanation :
    F. The getBundle() method matches Cars_fr_FR.properties. 
    It will then fall back to Cars_fr.properties (which does not exist) and Cars.properties if the value is not available. 
    For this reason, the first and third values would be France and moteur. While the second value horses is in the default locale, 
    it is not available if the requested locale has been found. As a result, the code throws a MissingResourceException, 
    making option F the answer.

14. Given the four properties files in question 12, what does this code print?
    Locale.setDefault(new Locale("ja","JP"));
    var rb = ResourceBundle.getBundle("Cars", new Locale("fr", "FR"));
    var t1 = rb.getString("engine");
    var t2 = rb.getString("road");
    var t3 = rb.getString("country");
    System.out.print(t1+ " " + t2 + " " + t3);
    
    A. moteur autoroute France
    B. engine autoroute France
    C. engine highway France
    D. moteur highway France
    E. moteur highway US
    F. An exception is thrown at runtime.

    Explanation :
    A. The getBundle() method matches Cars_fr_FR.properties. 
    It will then fall back to Cars_fr.properties (which does not exist) and Cars.properties if the value is not available. 
    For this reason, the first value printed is moteur from Cars.properties, while the next two values printed are autoroute and France from Cars_fr_FR.properties, 
    making option A correct.

15. Fill in the blank so the code correctly compiles and creates a Locale reference.
    Locale loc = Locale.____________________;
    
    A. get("Italian")
    B. of(Locale.ITALIAN)
    C. get(Locale.ITALIAN)
    D. getLocale("Italian")
    E. of("Italian")
    F. None of the above

    Explanation :
    F. There are no get() or of() methods in Locale. You need to use a constructor or a predefined Locale constant to obtain a Locale reference. 
    Therefore, option F is the correct answer. 
    Options B and C are close in that Locale.ITALIAN does reference a Locale object. 
    However, it should not be passed to the nonexistent get() method.

16. Assuming the key turquoise is in all five of the files referenced in the options, which file will
    the following code use for the resource bundle?
    Locale loc = new Locale("zh", "CN");
    Locale.setDefault(new Locale("en", "US"));
    ResourceBundle rb = ResourceBundle.getBundle("Colors", loc);
    rb.getString("turquoise");
    
    A. Colors_en.properties
    B. Colors_CN.properties
    C. Colors.properties
    D. Colors_default.properties
    E. Colors_en_CN.properties
    F. None of the above

    Explanation :
    A. Java starts out by looking for a properties file with the requested locale, which in this case is the zh_CN language and country. 
    It doesn’t find it, so it moves onto the locale with just a language code zh, which it also does not find. 
    It then moves on to the default locale en_US, but there is still no match. 
    It drops the country code and does find a match with en, making option A correct

17. How many lines does the following print out?
    3: Locale.setDefault(Locale.KOREAN);
    4: System.out.println(Locale.getDefault());
    5: Locale.setDefault(new Locale("en", "AU"));
    6: System.out.println(Locale.getDefault());
    7: Locale.setDefault(new Locale("EN"));
    8: System.out.println(Locale.getDefault());
    
    A. Only an exception is printed.
    B. One, followed by an exception.
    C. Two, followed by an exception.
    D. Three.
    E. It does not compile.

    Explanation :
    D. This code compiles and runs without exception, making option D the correct answer. 
    Line 3 uses a predefined Locale constant. 
    Line 5 passes a language and country code for English in Australia. 
    Line 7 incorrectly passes capital letters as a language code. However, Java automatically converts it to lowercase without throwing an exception. 
    The three lines printed by he code are ko, en_AU, and en.

18. Assuming the key red is in all five of the files referenced in the options, which file will the following
    code use for the resource bundle?
    Locale.setDefault(new Locale("en", "US"));
    var rb = ResourceBundle.getBundle("Colors",new Locale("ca","ES"));
    System.out.print(rb.getString("red"));
   
    A. Colors.properties
    B. Colors_en_US.properties
    C. Colors_US.properties
    D. Colors_ES.properties
    E. Colors_ca.properties
    F. None of the above

    Explanation :
    E. Java starts out by looking for a properties file with the requested locale, which in this case is the ca_ES language and country. 
    It doesn’t find it, so it moves onto the locale with just a language code ca, which it does find, making option E correct.

19. What is the output of the following code snippet?
    var d = LocalDate.parse("2022-04-01", DateTimeFormatter.ISO_LOCAL_DATE);
    System.out.print(d.format( DateTimeFormatter.ISO_LOCAL_DATE_TIME));

    A. 2022 APRIL 1
    B. 2022 MAY 0
    C. 2022 MAY 1
    D. 2022 APRIL 0
    E. The code does not compile.
    F. An exception is thrown at runtime.

    Explanation :
    F. The parse() method properly reads the date as April 1, 2022. The format() tries to use a date/time formatter on a date, 
    which produces an exception at runtime since the time element is missing. For this reason, option F is correct

20. What is the output if the launch() method is applied to a Properties object loaded from
    scifi.properties?
        scifi.properties
        rocket=saturn5
        moon=landing
    void launch(Properties props) {
    var a = props.getProperty("rocket", "?");
    var b = props.getProperty("earth");
    var c = props.getProperty("earth", "?");
    System.out.print(a + " " + b + " " + c);
    }
    
    A. saturn5 null ?
    B. saturn5 null null
    C. null null ?
    D. saturn5 ? ?
    E. The code does not compile.
    F. An exception is thrown at runtime.

    Explanation :
    A. The first line of the method retrieves the value for the property with key rocket, which is saturn5. 
    The next line retrieves the value for earth, but since it’s not found, null is returned. 
    The last functions similarly to the previous line but uses ? as the default value since earth is not set. 
    The code then prints saturn5 null ?, making option A the correct answer

21. For what values of pattern will the following print <02.1> <06.9> <10,00>?
    (Choose two.)
    String pattern = " ";
    var message = DoubleStream.of(2.1, 6.923, 1000)
        .mapToObj(v -> new DecimalFormat(pattern).format(v))
        .collect(Collectors.joining("> <"));
    System.out.print("<" + message + ">");

    A. ##,00.##
    B. ##,00.#
    C. 0,00.#
    D. #,00.#
    E. 0,00.0
    F. #,##.#

    Explanation :
    B,D. Options B and D correctly print the same string value in the specified format. 
    Option A is incorrect because <06.92> is printed instead of <06.9>. 
    Options C and E are incorrect, because (among other things) commas are printed as part of both of the first two values. 
    Option F is incorrect because <2.1> <6.9> is printed instead of <02.1> <06.9>.

22. What is the result of the following?
    Map<String, String> map = new TreeMap<>();
    map.put("tool", "hammer");
    map.put("problem", "nail");
    var props = new Property(); // p1
    map.forEach((k,v) -> props.put(k, v)); // p2
    String t = props.getProperty("tool"); // p3
    String n = props.getProperty("nail");
    System.out.print(t + " " + n);

    A. hammer nail
    B. The code does not compile due to line p1.
    C. The code does not compile due to line p2.
    D. The code does not compile due to line p3.
    E. An exception is thrown at runtime.
    F. None of the above.

    Explanation :
    B. The class on line p1 should be Properties rather than Property. As written, it is incorrect and does not compile, 
    making option B the correct answer.

23. Assuming the key purple is in all five of the files referenced in the options, which file will the
    following code use for the resource bundle?
    Locale.setDefault(new Locale("en", "US"));
    var rb = ResourceBundle.getBundle("Colors", new Locale("en"));
    System.out.print(rb.getString("purple"));
    
    A. Colors_en_US.properties
    B. Colors_en.properties
    C. Colors_US.properties
    D. Colors_fr.properties
    E. Colors.properties
    F. None of the above

    Explanation :
    B. Java starts out by looking for a properties file with the requested locale, which in this case is the en language. 
    It finds it right away, making option B correct.

24. Which of the following are not valid Locale formats? (Choose two.)
    A. nl_BE
    B. fr_CA
    C. uk_ua
    D. CR
    E. no
    F. ro_RO

    Explanation :
    C,D. In Java, a locale can be represented by a language code in lowercase, or a language and country code, with language in lowercase and country in uppercase. 
    Option C is invalid because both values are lowercase. 
    Option D is invalid because the value is in uppercase. 
    The rest of the options are valid locale formats. Remember, the exam won’t expect you to know which language and country codes exist, 
    but it will expect you to know how to use them

25. For currency, the US uses the $ symbol, the UK uses the £ symbol, and Germany uses the €
    symbol. Given this information, what is the expected output of the following code snippet?
    Locale.setDefault(Locale.US);
    Locale.setDefault(Category.FORMAT, Locale.GERMANY);
    Locale.setDefault(Category.DISPLAY, Locale.UK);
    System.out.print(NumberFormat.getCurrencyInstance().format(6.95));
    
    A. $6.95
    B. 6,95 €
    C. £6.95
    D. The code does not compile.
    E. An exception is thrown at runtime.
    F. The output cannot be determined without knowing the locale of the system where it will be run.

    Explanation :
    B. The code compiles, so option D is incorrect. 
    While three distinct locale values are set, the one that is used for formatting text is Category.FORMAT. 
    For this reason, the GERMANY locale is used to formatting the data with the € symbol, making option B correct

26. What is the output of the following code snippet?
    var x = LocalDate.of(2022, 3, 1);
    var y = LocalDateTime.of(2022, 1, 1, 2, 55);
    var f = DateTimeFormatter.ofPattern("'yyyy-MM'");
    System.out.print(f.format(x) + " " + f.format(y));
    
    A. 2022-03 2022-01
    B. 2022-01 2022-03
    C. 2022-02 2022-00
    D. yyyy-MM yyyy-MM
    E. The code does not compile.
    F. An exception is thrown at runtime.

    Explanation :
    D. The date/time pattern uses single quotes to escape the date/time values, meaning the output is yyyy-MM for all valid inputs. 
    For this reason, option D is correct. 
    If the single quotes were removed, then 2022-03 2022-01 would be the correct output

27. Given the following two properties files, what does the following class output?
    -----------------------------------------------------
    |  container.properties  |  container_en.properties |
    |  name=generic          |  name=Docker             |
    |  number=2              |  type=container          |
    -----------------------------------------------------
  
    void loadPod() {
        new Locale.Builder()
            .setLanguage("en")
            .setRegion("US").build();
        var rb = ResourceBundle.getBundle("container");
        String name = rb.getString("name");
        String type = rb.getString("type");
        System.out.print(name + " " + type);
    }

    A. Docker container
    B. generic container
    C. generic null
    D. The output cannot be determined without knowing the locale of the system where it will be run.
    E. An exception is thrown at runtime.
    F. None of the above.

    Explanation :
    D. The method creates a resource bundle using a builder but never sets it. 
    Since we don’t know the default locale of the code, the answer depends on where it is executed, making option D correct

28. Given the two properties files from question 27, what does the following class output?
    
    void loadContainer() {
        Locale.setDefault(new Locale("en"));
        var rb = ResourceBundle.getBundle("container");
        String name = rb.getString("name");
        String type = rb.getString("type");
        System.out.print(name + " " + type);
    }
    
    A. Docker container
    B. generic container
    C. generic null
    D. The output cannot be determined without knowing the locale of the system where it will
    be run.
    E. An exception is thrown at runtime.
    F. None of the above.

    Explanation :
    A. This code sets the default locale to English and then tries to get a resource bundle for container. 
    It finds the resource bundle container_en.properties as the most specific match. Both keys are found in this file, so option A is the answer

29. Given the two properties files from question 27, what does the following class output?

    void loadControlPlane() {
        Locale.setDefault(new Locale("en_US"));
        var rb = ResourceBundle.getBundle("container");
        String name = rb.getString("name");
        String type = rb.getString("type");
        System.out.print(name + " " + type);
    }
    A. Docker container
    B. generic container
    C. generic null
    D. The output cannot be determined without knowing the locale of the system where it will
    be run.
    E. An exception is thrown at runtime.
    F. None of the above.

    Explanation :
    E. The Locale constructor that takes a single argument expects a language code, not a concatenation of language and region codes. 
    Therefore, the language is set as en_us, not en, with no region code set. Since no properties files match the language en_us, the default container.properties is used. 
    Since type is not found in this properties file, a MissingResourceException is thrown at runtime.

30. Assuming the Forest.properties file is the only resource file available, what is the
    output of calling the hike() method?
    
    Forest.properties
    trees=evergreen {0}
    animals=squirrels
    
    static void hike() {
        Locale.setDefault(new Locale.Builder()
            .setLanguage("en").build());
        var rb = ResourceBundle
            .getBundle("Forest", new Locale("fr"));
        System.out.print(MessageFormat.format("trees","pretty"));
    }

    A. trees
    B. trees pretty
    C. trees {0}
    D. trees null
    E. The code does not compile.
    F. An exception is thrown at runtime.

    Explanation :
    A. The code compiles, so option E is incorrect. 
    Java starts out by looking for a properties file with the requested locale, which in this case is the fr language. 
    It doesn’t find Forest_fr.properties, so it moves onto the default locale en. 
    It also doesn’t find Forest_en.properties. It settles on Forest.properties without throwing an exception, so option F is incorrect. 
    The first argument to MessageFormat.format() should be a pattern String value. Since trees is sent, the output of the formatting string is trees, making option A correct. 
    If rb.getString("trees") was passed instead of just trees, then the output would be evergreen pretty.
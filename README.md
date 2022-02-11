# Clean Code Documentation for JAVA Language

## Definition

Clean code is code that is easy to understand and easy to change. Clean code is a code that is easy to read, like a book where each word transforms into a picture and anyone can actually visualize everything like watching a movie, in short, should be readable by Humans.

## Importance of Writing Clean Code

Writing clean code is vital because it allows one to communicate effectively with the next person who will be working with it. Being able to return to previously written code and understand what it does is key, especially in the software development world.  Clean coding reduces the cost of maintenance, making it easy to fix bugs.

## Characteristics of Clean Code

1. Focused:  Code should be written to solve a specific problem.
2. Simple: Design and implementation must be as simple as possible
3. Easy to Test: Codes are easily testable with easy-to-write unit tests, and tests are easy to understand and change. 

## General Principles of Clean Code

1. Follow standard conventions.
1. Always find root cause.
1. Follow SOLID principles.
1. Split large functions into several functions
1. For database requests, keep it as simple and productive as possible.
1. Check naming conventions. Keep them clear and concise.
1. Be consistent. Use the same names in similar functions (Get vs Fetch, Set vs Update, Add vs Append).
1. Follow KISS principles of software development.
1. Follow Boy scout rule. Leave the campground cleaner than you found it.
1. Avoid using magic numbers that are assigned to a code with no clear meaning.
1. Avoid deep nesting of loops. To make loop clear, we should use loops in separate functions. In this way, we can write nested loops as per requirements.
1. Comments should be good, but code needs to be self-explanatory.
1. Avoid duplication in the code (DRY principle or Don’t Repeat Yourself ).

## Clean Code Rules for JAVA

1. Project Structure: 
Follow a consistent pattern to organize our source files, tests, configurations, data, and other code artifacts. Let's see some of the folders that Maven suggests we create:

    * src/main/java: For source files
    * src/main/resources: For resource files, like properties
    * src/test/java: For test source files
    * src/test/resources: For test resource files, like properties
Similar to this, there are other popular project structures like Bazel suggested for Java, and we should choose one depending on our needs and audience.

1. Naming Convention:
Following naming conventions can go a long way in making our code readable and hence, maintainable.
    * Packages: Names should be in lowercase give meaningful name. 
    For example:
    ```java
    package mycalculator
    ```
    * Classes: Names should be in CamelCase. Class in terms of object-oriented concepts is a blueprint for objects which often represent real-world objects. Hence it's meaningful to use nouns to name classes describing them sufficiently.

    For example:
    ```java
    public class Account{
        // --- some variables
        //---some methods
    }
    ```
    * Interfaces: Names should be in CamelCase. They tend to have a name that describes an operation that a class can do.
   
    For example:
    ```java
    // interface
    interface Animal {
    public void animalSound(); 
    public void run(); 
    }
    ```

    * Variables:
        - Use meaningful and pronounceable variable names.
            
            Bad practice:
            ```java
            var d; // elapsed time in days
            ```
            Good practice:
            ```java
            var days;
            ```

        - Use the same vocabulary for the same type of variable.
            
            Bad practice:
            ```java
            getUserInfo();
            getClientData();
            getCustomerRecord();
            ```
            Good practice:
            ```java
            getUser();
            ```
        - Use searchable names.

            Bad practice:
            ```java
            String yyyymmdstr = new SimpleDateFormat("YYYY/MM/DD").format(new Date());
            ```
            Good practice:
            ```java
            String currentDate = new SimpleDateFormat("YYYY/MM/DD").format(new Date());
            ```

        - Use explanatory variables.

            Bad practice:
            ```java
            String address = "One Infinite Loop, Cupertino 95014";
            String cityZipCodeRegex = "/^[^,\\\\]+[,\\\\\\s]+(.+?)\\s*(\\d{5})?$/";
            saveCityZipCode(address.split(cityZipCodeRegex)[0],
                address.split(cityZipCodeRegex)[1]);
            ```
            Good practice:
            ```java
            String address = "One Infinite Loop, Cupertino 95014";
            String cityZipCodeRegex = "/^[^,\\\\]+[,\\\\\\s]+(.+?)\\s*(\\d{5})?$/";

            String city = address.split(cityZipCodeRegex)[0];
            String zipCode = address.split(cityZipCodeRegex)[1];

            saveCityZipCode(city, zipCode);
            ```

        - Avoid Mental Mapping
        
            Bad practice:
                
            ```java
            String [] l = {"Austin", "New York", "San Francisco"};
            for (int i = 0; i < l.length; i++) {
                String li = l[i];
                doStuff();
                doSomeOtherStuff();
                // ...
                // Wait, what is `$li` for again?
                dispatch(li);
            }
            ```
            Good practice:

            ```java
            String[] locations = {"Austin", "New York", "San Francisco"};

            for (String location : locations) {
                doStuff();
                doSomeOtherStuff();
                // ...
                dispatch(location);
            }
            ```
        - Avoid repeatation what the class/object name says already.
           
            Bad practice:
            ```java
                    class Car {
            public String carMake = "Honda";
            public String carModel = "Accord";
            public String carColor = "Blue";
            }

            void paintCar(Car car) {
            car.carColor = "Red";
            }
            ```
            Good practice:
            ```java
                        class Car {
            public String make = "Honda";
            public String model = "Accord";
            public String color = "Blue";
            }

            void paintCar(Car car) {
            car.color = "Red";
            }
            ```

    * Constants: Names should be in uppercase.

        For example:
        ```java
        static final int DEFAULT_WIDTH static final int MAX_HEIGHT 
        ```
    * Methods: It's useful to name methods using verbs. 
    
        For example: getAddress() is a good example of method declaration instead of using address().
        1. Methods should do one thing.
           
            Bad practice:
            ```java
            public void emailClients(List<Client> clients) {
                for (Client client : clients) {
                    Client clientRecord = repository.findOne(client.getId());
                    if (clientRecord.isActive()){
                        email(client);
                    }
                }
            }
            ```
            Good practice:
            ```java
            public void emailClients(List<Client> clients) {
                for (Client client : clients) {
                    if (isActiveClient(client)) {
                        email(client);
                    }
                }
            }

            private boolean isActiveClient(Client client) {
                Client clientRecord = repository.findOne(client.getId());
                return clientRecord.isActive();
            }
            ```
        2. Method names should say what they do.
            
            Bad practice:
            ```java
            private void addToDate(Date date, int month){
                //..
            }

            Date date = new Date();

            // It's hard to to tell from the method name what is added
            addToDate(date, 1);
            ```
            Good practice:
            ```java
            private void addMonthToDate(Date date, int month){
                //..
            }

            Date date = new Date();
            addMonthToDate(1, date);
            ```

        3. Methods should only be one level of abstraction.

1. Source File Structure: 
A typical ordering of elements in a source file look:

   * Package statement
   * Import statements
   * All static imports
   * All non-static imports
   * Exactly one top-level class
   * Class variables
   * Instance variables
   * Constructors
   * Methods

1. Whitespaces: 
  
    * Two blank lines before starting static blocks, fields, constructors and inner classes
    * One blank line after a method signature that is multiline
    * A single space separating reserved keywords like if, for, catch from an open parentheses
    * A single space separating reserved keywords like else, catch from a closing parentheses
1. Indentation:

    * A typical best practice is to use four spaces, a unit of indentation.
    * Normally, there should be a cap over the line length, but this can be set higher than traditional 80 owing to larger screens developers use today.
    * We must break expressions because many would not fit on a single line:
        1. Break method calls after a comma
        2. Break expressions before an operator
        3. Indent wrapped lines for better readability
1. Method Parameters: 
    * Avoid three or more parameters where possible.
    * Consider refactoring the method if it needs more than recommended parameters
    * Consider bundling parameters into custom-types 

1. Hardcoding:
    Hardcoded values can be refactored in one of the following ways:

    * Consider replacing with constants or enums defined within Java
    Or else, replace with constants defined at the class level or in a separate class file
    * If possible, replace with values which can be picked from configuration or environment

       Good practice:
       ```java
       private int storeClosureDay = 7;

       // This can be refactored to use a constant from Java
       ```
       Bad practice:
       ```java

       private int storeClosureDay = DayOfWeek.SUNDAY.getValue()
       ```
1. Code Comments: 
    * Only comment things that have business logic complexity.
    Good practice:
    ```java
    // Creating a List of customer names 
    List<String> Names = Arrays.asList('Bob', 'Linda', 'Steve', 'Mary'); 

    ```
    Good practice:
    ```java
    List<String> customerNames = Arrays.asList('Bob', 'Linda', 'Steve', 'Mary'); 
    ```
    * Don't Use a Comment When You Can Use a Function or a Variable.
        Bad practice:
        ```java
        //Check to see if order is eligible to ship
        if((order.isPaid & order.isLabeled) && CUSTOMER_FLAG) {
        // ...
        }
        ```
        Good practice:
        ```java
        if(order.isEligibleToShip()) {
        // ...
        }
        ```
    * There's no need for dead code, commented code, and journal comments. We should use git log to get history.
        Bad practice:
        ```java
        doStuff();
        // doOtherStuff();
        // doSomeMoreStuff();
        // doSoMuchStuff();
        ```
        Good practice:
        ```java
        doStuff();
        ```
    * Avoid positional markers
        
        Bad practice:
        ```java
        ////////////////////////////////////////////////////////////////////////////////
        // Instantiate Order List
        ////////////////////////////////////////////////////////////////////////////////
        List<Order> orders = new ArrayList();
        ```
        Good practice:
        ```java
        List<Order> orders = new ArrayList();
        ```

1. Logging:
    * Avoid excessive logging, think about what information might be of help in troubleshooting
    * Choose log levels wisely, we may want to enable log levels selectively on production
    * Be very clear and descriptive with contextual data in the log message
    * Use external tools for tracing, aggregation, filtering of log messages for faster analytics


# Tools for Clean Coding
There are several tools available in the Java ecosystem, which take at least some of these responsibilities away from code reviewers. Let's see what some of these tools are:

* Code Formatters: Most of the popular Java code editors, including Eclipse and IntelliJ, allows for automatic code formatting. We can use the default formatting rules, customize them, or replace them with custom formatting rules. This takes care of a lot of structural code conventions.
* Static Analysis Tools: There are several static code analysis tools for Java, including SonarQube, Checkstyle, PMD and SpotBugs. They are great in detecting a lot of code smells like violations of naming conventions and resource leakage.
# Conclusion
Clean coding is a habit that needs to be developed by keeping these principles in mind and applying them whenever you write code. A famous writer Donald Knuth states that, " Programming is the art of telling another human what one wants the computer to do." We should practise clean coding to make coding environment more easier and enjoyable for everyone.

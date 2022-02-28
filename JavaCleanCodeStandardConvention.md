## Java Clean Code Convention
1. Project Structure: 
Follow a consistent pattern to organize source files, tests, configurations, data, and other code artifacts. Let's see some of the folders that Maven suggests:

    * src/main/java: For source files
    * src/main/resources: For resource files, like properties
    * src/test/java: For test source files
    * src/test/resources: For test resource files, like properties

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
1. Indentation:
    - Use Four spaces as unit of indentation.
    - Tabs must be set exactly every 8 spaces (not 4).
    - Avoid lines longer than 80 characters.
    - If an expression doesn't fit on a single line, break it using the principle below.
        - Break after a comma.
        - Break before an operator.
        - Prefer higher-level breaks to lower-level breaks.
        - If the above rules result in code squished up against the right margin, simply indent 8 spaces.
1. Comments:
    - Don't use a comment When you can use a function or a Variable.
    - No need for dead code, commented code, and journal comments. Use git log to get history.
    - Avoid positional markers.
    - Very short comments can appear on the same line 
    -  Block comments should be used at the beginning of each file and before each method.
    - Doc comments describe Java  classes, interfaces, constructors, methods, and fields. This comment should appear just before the declaration.
1. WhiteSpace:
    -  Two blank lines before starting static blocks, fields, constructors and inner classes
    -  One blank line after a method signature that is multiline
    -  A single space separating reserved keywords like if, for, catch from an open parentheses
    -  A single space separating reserved keywords like else, catch from a closing parentheses

1. Naming Conventions:
    - Packages: Use all-lowercase ASCII letters.
    - CLasses and Interfaces: Names should be nouns and  in mixed casewith the first letter of each internal word capi-talized. 
    - Methods: Use verbs as method names in camelCase.
    - Constants: Names should be in uppercase.
    - Variables: 
        - Use nouns in camelCase.
        - Don't start with an underscore (_) or dollar sign ($) character
        - Single-character variable names should be avoided.
1. Method Parameters: 
    * Avoid three or more parameters where possible.
    * Consider refactoring the method if it needs more than recommended parameters.
    * Consider bundling parameters into custom-types.
1. MISCELLANEOUS PRACTICES:
    - PARENTHESES: Use parentheses liberally in expressions involving mixed operators to avoid operator precedence problems.
    - RETURNING VALUES: avoid multiple return statements in a method when possible.
    - If an expression containing a binary operator appears before the ? in the ternary ?: operator, it should be parenthesized.
    - Use XXX in a comment to flag something that is bogus but works. 
    - Use FIXME to flag something that is bogus and broken.
1. Declarations:
    - Only one declaration per line is allowed.
    - Put declarations only at the beginning of blocks. 
    - Do not declare the same variable name in an inner block.
    - Try to initialize local variables where they’re declared.
    - No space between a method name and the parenthesis “(“ starting its parameter list 
    - Open brace “{” appears at the end of the same line as the declaration statement 
    - Closing brace “}” starts a line by itself indented to match its corresponding opening statement
1. Statements:
    - Each line should contain at most one statement.
    - if  statements always use braces {}.
    - Every switch  statement should include a default case.
    - Every time a case in switch statement falls through, add a comment where the break statement would normally be.
    - A try-catch statement may also be followed by finally.
1. Annotation: Using annotation is recommended in Java.
## Code Example:
```java
/*
 *<SOURCE_HEADER>
 *
 *<NAME>
 * $RCSfile: $
 *</NAME>
 *
 *<RCS_KEYWORD>
 * $Source: $
 * $Revision: $
 * $Date: $
 *</RCS_KEYWORD>
 *
 *</SOURCE_HEADER>
 */

package org.banana.lamda;

import org.banana.psi.PsiException;
import org.banana.theta.ParentClass;
import org.banana.theta.AlphaInterface;

import com.omega.foobar.BetaInterface;
import com.omega.foobar.GammaInterface;

/**
 * Class description goes here...
 *
 * @author      Curious George
 * @author      Lancelot Link
 * @version     $Revision: 1.38 $, $Date: 2000/08/24 22:34:36 $
 * @since       EPSILON1.0
 */
public abstract class DerivedClass extends ParentClass
        implements AlphaInterface, BetaInterface, GammaInterface
{
    // class implementation comments go here...

    /**
     * Constructor documentation comments go here...
     *
     * @param   aName Description of parameter...
     */
    public DerivedClass(const String aName)
    {
        super();

        String uppercaseName = null;
        int updatedCount = 0;

        uppercaseName = aName.toUpperCase();
        this.setName(uppercaseName);

        updatedCount = DerivedClass.getCount();
        updatedCount++;

        DerivedClass.setCount(aCount);
    }

    /**
     * Method documentation comments go here...
     *
     * @return  Description of return value...
     * @see     #setName
     */
    public String getName()
    {
        // method implementation comments go here...

        return this.fName;
    }

    /**
     * Method documentation comments go here...
     *
     * @param   newName Description of parameter...
     * @throws  PsiException Description of exception...
     * @see     #getName
     */
    public void setName(const String newString) throws PsiException
    {
        ...
    }

    /**
     * Method documentation comments go here...
     *
     * @return  Description of return value...
     * @see     #setCount
     */
    public static int getCount()
    {
        return DerivedClass.sCount;
    }

    /**
     * Method documentation comments go here...
     *
     * @param   args Description of parameters...
     */
    public static void main(String[] args)
    {
        // 'main' method is always last in 'public' interface section.
        ...
    }

    //----------------------------------------------------------------------
    // protected interface
    //----------------------------------------------------------------------

    /**
     * Method documentation comments go here...
     */
    protected static void setCount(int newCount)
    {
        // FIXME need to ensure parameter is non-negative

        DerivedClass.sCount = newCount;
    }

    /**
     * Method documentation comments go here...
     */
    protected abstract void doSomething();

    //----------------------------------------------------------------------
    // private interface
    //----------------------------------------------------------------------

    // constants
    //
    private static final String DEFAULT_NAME = new String("FooBar");

    // class variables
    //
    private static int sCount = 0;

    // instance variables
    //
    private String fName = DerivedClass.DEFAULT_NAME;

    /**
     * Method documentation comments go here...
     */
    private void doSomethingElse()
    {
        ...
    }

    /**
     * Class documentation comments go here...
     */
    private class InnerClass
    {
        /**
         * Constructor documentation comments go here...
         */
        public InnerClass()
        {
            ...
        }

        ...

        //------------------------------------------------------------------
        // private interface
        //------------------------------------------------------------------

        // instance variables
        //
        private Object fRef = null;
    } // InnerClass
} // DerivedClass
```
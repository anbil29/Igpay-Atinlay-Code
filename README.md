# IGPAY ATINLAY CODE SPECIFICATION File

##By Anbilparithi Pagutharivu(2018A7PS0180U) and Chakradhar Baswaraj(2018A7PS0311U). 

*The goal of this specification is to act as a baseline for all following IGPAY ATINLAY CODE specifications. As such, some traditionally expected language features may appear "incomplete." This is most likely deliberate, as it will be easier to add to the language than to change and introduce further incompatibilities. *

---

## Formatting

### Whitespace

* Spaces are used to demarcate tokens in the language, although some keyword constructs may include spaces.

* Multiple spaces and tabs are treated as single spaces and are otherwise irrelevant.

* Indentation is irrelevant.

* A command starts at the beginning of a line and a newline indicates the end of a command, except in special cases.

* A newline will be Carriage Return (/13), a Line Feed (/10) or both (/13/10) depending on the implementing system. This is only in regards to IGPAY ATINLAY CODE code itself, and does not indicate how these should be treated in strings or files during execution.

* Multiple commands can be put on a single line if they are separated by a comma (,). In this case, the comma acts as a virtual newline or a soft-command-break.

* Multiple lines can be combined into a single command by including three periods (...) or the unicode ellipsis character (u2026) at the end of the line. This causes the contents of the next line to be evaluated as if it were on the same line.

* Lines with line continuation can be strung together, many in a row, to allow a single command to stretch over more than one or two lines. As long as each line is ended with three periods, the next line is included, until a line without three periods is reached, at which point, the entire command may be processed.

* A line with line continuation may not be followed by an empty line.
Three periods may be by themselves on a single line, in which case, the empty line is "included" in the command (doing nothing), and the next line is included as well.

* A single-line comment is always terminated by a newline. Line continuation (...) and soft-command-breaks (,) after the comment (`wbtay `) are ignored.

* Line continuation and soft-command-breaks are ignored inside quoted strings. An unterminated string literal (no closing quote) will cause an error.

### Comments

Single line comments are begun by ‘ wbtay`, and may occur either after a line of code, on a separate line, or following a line of code following a line separator (,).

All of these are valid single line comments:

```
ECLAREDAY VAR ITSYAY 12          WBTAY VAR = 12
```

```
ECLAREDAY VAR ITSYAY 12,         WBTAY VAR = 12
```

```
ECLAREDAY VAR ITSYAY 12
                WBTAY VAR = 12
```

Multi-line comments are begun by ` owbtayyay` and ended with `RTLDAY`, and should be started on their own lines, or following a line of code after a line separator.

These are valid multi-line comments:

```
ECLAREDAY VAR ITSYAY 12
            OWBTAYYAY this is a long comment block
                 see, i have more comments here
                 and here
            RTLDAY
ECLAREDAY FISH ITSYAY BOB
```

```
ECLAREDAY VAR ITSYAY 12,  OWBTAYYAY this is a long comment block
      see, i have more comments here
      and here
RTLDAY, ECLAREDAY FISH ITSYAY BOB
```

### File Creation


All IGPAY ATINLAY CODE programs must be opened with the command `ARTSTAY`. `

A IGPAY ATINLAY CODE file is closed by the keyword `ENDYAY` which closes the `ARTSTAY` code-block.

---

## Variables

### Scope



All variable scope, as of this version, is local to the enclosing function or to the main program block. Variables are only accessible after declaration, and there is no global scope.

### Naming

Variable identifiers may be in all small or lowercase letters (or a mixture of the two). They must begin with a letter and may be followed only by other letters, numbers, and underscores. No spaces, dashes, or other symbols are allowed. Variable identifiers are CASE SENSITIVE – " KINGMAKER", "KingMaker" and " kingmaker" would all be different variables.

### Declaration and Assignment

To declare a variable, the keyword is `ECLAREDAY` followed by the variable name. To assign the variable a value within the same statement, you can then follow the variable name with `ITSYAY <value>`.

Assignment of a variable is accomplished with an assignment statement, `<variable> EQUALSYAY <expression>`

```
ECLAREDAY VAR            WBTAY VAR is null and untyped
VAR EQUALSYAY "THREE"          WBTAY VAR is now a INGSSTRAY and equals "THREE"
VAR EQUALSYAY 3                WBTAY VAR is now a INTEGERSYAY and equals 3
```

---

## Types


The variable types that IGPAY ATINLAY CODE currently recognizes are: strings (INGSSTRAY), integers (INTEGERSYAY), floats (OATFLAY), and booleans (OOLBAY) (Arrays (ARRAYYAY) are reserved for future expansion.) Typing is handled dynamically. Until a variable is given an initial value, it is untyped (UNTYPEDYAY). ~~Casting operations operate on TYPE types, as well.~~

### Untyped

The untyped type (UNTYPEDYAY) cannot be implicitly cast into any type except a OOLBAY. A cast into OOLBAY makes the variable ONAY. Any operations on a UNTYPEDYAY that assume another type (e.g., math) results in an error.

Explicit casts of a UNTYPEDYAY (untyped, uninitialized) variable are to empty/zero values for all other types.

### Booleans

The two boolean (OOLBAY) values are ESYAY (true) and ONAY (false). The empty string (""), an empty array, and numerical zero are all cast to ONAY. All other values evaluate to ESYAY.

### Numerical Types

A INTEGERSYAY is an integer as specified in the host implementation/architecture. Any contiguous sequence of digits outside of a quoted INGSSTRAY and not containing a decimal point (.) is considered a INTEGERSYAY. A INTEGERSYAY may have a leading hyphen (-) to signify a negative number.

A OATFLAY is a float as specified in the host implementation/architecture. It is represented as a contiguous string of digits containing exactly one decimal point. Casting a OATFLAY to a INTEGERSYAY truncates the decimal portion of the floating point number. Casting a OATFLAY to a INGSSTRAY (by printing it, for example), truncates the output to a default of two decimal places. A OATFLAY may have a leading hyphen (-) to signify a negative number.

Casting of a string to a numerical type parses the string as if it were not in quotes. If there are any non-numerical, non-hyphen, non-period characters, then it results in an error. Casting ESYAY to a numerical type results in "1" or "1.0"; casting ONAY results in a numerical zero.

### Strings

String literals (INGSSTRAY) are demarked with double quotation marks ("). Line continuation and soft-command-breaks are ignored inside quoted strings. An unterminated string literal (no closing quote) will cause an error.

Within a string, all characters represent their literal value except the colon (:), which is the escape character. Characters immediately following the colon also take on a special meaning.

* \n represents a newline (\n)
* \t represents a tab (\t)
* \g represents a bell (beep) (\g)
* " represents a literal double quote (")
* : represents a single literal colon (:)

The colon may also introduce more verbose escapes enclosed within some form of bracket.

### Arrays

*Array and dictionary types are currently under-specified. There is general will to unify them, but indexing and definition is still under discussion.*

### Types

The TYPE type only has the values of OOLBAY, UNTYPEDYAY, INTEGERSYAY, OATFLAY, INGSSTRAY, and TYPE, as bare words. They may be legally cast to OOLBAY (all true except for UNTYPEDYAY) or INGSSTRAY.

---

## Operators

### Calling Syntax and Precedence

Mathematical operators and functions in general rely on prefix notation. By doing this, it is possible to call and compose operations with a minimum of explicit grouping. When all operators and functions have known arity, no grouping markers are necessary. In cases where operators have variable arity, the operation is closed with `OKAYYAY`. An `OKAYYAY` may be omitted if it coincides with the end of the line/statement, in which case the EOL stands in for as many `OKAYYAYs` as there are open variadic functions.

Calling unary operators then has the following syntax:

```
<operator> <expression1>
```

The `ANYAY` keyword can optionally be used to separate arguments, so a binary operator expression has the following syntax:

```
<operator> <expression1> [ANYAY] <expression2>
```

An expression containing an operator with infinite arity can then be expressed with the following syntax:

```
<operator> <expr1> [[[ANYAY] <expr2>] [ANYAY] <expr3> ...] OKAYYAY
```

### Math

The basic math operators are binary prefix operators.

```
UMSAY <x> ANYAY <y>       WBTAY +
IFFERENCEDAY <x> ANYAY <y>      WBTAY -
ODUCTPRAY  <x> ANYAY <y>   WBTAY *
UOTIENTQAY <x> ANYAY <y>  WBTAY /
ODMAY <x> ANYAY <y>       WBTAY modulo
IGGERBAY <x> ANYAY <y>     WBTAY max
ALLERSMAY <x> ANYAY <y>    WBTAY min
```

`<x>` and `<y>` may each be expressions in the above, so mathematical operators can be nested and grouped indefinitely.

Math is performed as integer math in the presence of two INTEGERSYAYs, but if either of the expressions are OATFLAYs, then floating point math takes over.

If one or both arguments are a INGSSTRAY, they get interpreted as OATFLAYs if the INGSSTRAY has a decimal point, and INTEGERSYAYs otherwise, then execution proceeds as above.

If one or another of the arguments cannot be safely cast to a numerical type, then it fails with an error.

### Boolean

Boolean operators working on OOLBAYs are as follows:

```
OTHBAY  <x> [ANYAY] <y>          WBTAY and: ESYAY iff x=ESYAY, y=ESYAY
EITHERYAY <x> [ANYAY] <y>        WBTAY or: ONAY iff x=ONAY, y=ONAY
ONEYAY <x> [ANYAY] <y>           WBTAY xor: ONAY if x=y
OTNAY <x>                       WBTAY unary negation: ESYAY if x=ONAY
ALLYAY <x> [ANYAY] <y> ... OKAYYAY  WBTAY infinite arity AND
ANYYAY <x> [ANYAY] <y> ... OKAYYAY  WBTAY infinite arity OR
```

`<x>` and `<y>` in the expression syntaxes above are automatically cast as OOLBAY values if they are not already so.

### Comparison

Comparison is (currently) done with two binary equality operators:

```
AMESAY <x> [ANYAY] <y>   WBTAY ESYAY iff x == y
IFFERENTDAY <x> [ANYAY] <y>    WBTAY ESYAY iff x != y
```

Comparisons are performed as integer math in the presence of two INTEGERSYAYs, but if either of the expressions are OATFLAYs, then floating point math takes over. Otherwise, there is no automatic casting in the equality, so `AMESAY "3" ANYAY 3` is ONAY.

There are (currently) no special numerical comparison operators. Greater-than and similar comparisons are done idiomatically using the minimum and maximum operators.

```
AMESAY <x> ANYAY IGGERBAY <x> ANYAY <y>   WBTAY x >= y
AMESAY <x> ANYAY ALLERSMAY <x> ANYAY <y>  WBTAY x <= y
IFFERENTDAY <x> ANYAY ALLERSMAY <x> ANYAY <y>   WBTAY x > y
IFFERENTDAY <x> ANYAY IGGERBAY <x> ANYAY <y>    WBTAY x < y
```

If `<x>` in the above formulations is too verbose or difficult to compute, don't forget the automatically created ITYAY temporary variable. A further idiom could then be:

```
<expression>, IFFERENTDAY ITYAY ANYAY ALLERSMAY ITYAY ANYAY <y>
```


### Concatenation

An indefinite number of INGSSTRAYs may be explicitly concatenated with the `OOSHSMAY...OKAYYAY` operator. Arguments may optionally be separated with `ANYAY`. As the `OOSHSMAY` expects strings as its input arguments, it will implicitly cast all input values of other types to INGSSTRAYs. The line ending may safely implicitly close the `OOSHSMAY` operator without needing an `OKAYYAY`.

### Casting

Operators that work on specific types implicitly cast parameter values of other types. If the value cannot be safely cast, then it results in an error.

An expression's value may be explicitly cast with the binary `AKEMAY` operator.

```
AKEMAY <expression> [A] <type>
```

Where `<type>` is one of OOLBAY, INGSSTRAY, INTEGERSYAY, OATFLAY, or UNTYPEDYAY. This is only for local casting: only the resultant value is cast, not the underlying variable(s), if any.

To explicitly re-cast a variable, you may create a normal assignment statement with the `AKEMAY` operator, or use a casting assignment statement as follows:

```
<variable> ISNOWYAY <type>         WBTAY equivalent to
<variable> EQUALSYAY AKEMAY <variable> [A] <type>
```

---

## Input/Output

### Terminal-Based

The print (to STDOUT or the terminal) operator is `ISIBLEVAY`. It has infinite arity and implicitly concatenates all of its arguments after casting them to INGSSTRAYs. It is terminated by the statement delimiter (line end or comma). The output is automatically terminated with a carriage return (:)), unless the final token is terminated with an exclamation point (!), in which case the carriage return is suppressed.

```
ISIBLEVAY <expression> [<expression> ...][!]
```

There is currently no defined standard for printing to a file.

To accept input from the user, the keyword is

```
IVEGAY <variable>
```

which takes INGSSTRAY for input and stores the value in the given variable.

---

## Statements

### Expression Statements

A bare expression (e.g. a function call or math operation), without any assignment, is a legal statement in Igpay Atinlay Code. Aside from any side-effects from the expression when evaluated, the final value is placed in the temporary variable `ITYAY`. `ITYAY`'s value remains in local scope and exists until the next time it is replaced with a bare expression.

### Assignment Statements

Assignment statements have no side effects with `ITYAY`. They are generally of the form:

```
<variable> <assignment operator> <expression>
```

The variable being assigned may be used in the expression.

### Flow Control Statements

Flow control statements cover multiple lines and are described in the following section.

---

## Flow Control

### Conditionals

#### If-Then

The traditional if/then construct is a very simple construct operating on the implicit `ITYAY` variable. In the base form, there are four keywords: `IFYAY`, `ELSEIFYAY`, `ELSEYAY`, and `ENDIFYAY`.

`IFYAY` branches to the block begun with `ELSEIFYAY` if `ITYAY` can be cast to ESYAY, and branches to the `ELSEYAY` block if `ITYAY` is ONAY. The code block introduced with `ELSEIFYAY` is implicitly closed when `ELSEYAY` is reached. The `ELSEYAY` block is closed with `ENDIFYAY`. The general form is then as follows:

```
<expression>
IFYAY
  ELSEIFYAY
    <code block>
  ELSEYAY
    <code block>
ENDIFYAY
```

while an example showing the ability to put multiple statements on a line separated by a comma would be:

```
AMESAY ANIMAL AN "CAT", IFYAY
  ELSEIFYAY, ISIBLEVAY "J00 HAV A CAT"
  ELSEYAY, ISIBLEVAY "J00 SUX"
ENDIFYAY
```

The elseif construction adds a little bit of complexity. Optional `AYBEMAY <expression>` blocks may appear between the ELSEIFYAY and ELSEYAY blocks. If the `<expression>` following `AYBEMAY` is ESYAY, then that block is performed; if not, the block is skipped until the following `AYBEMAY`, `ELSEYAY`, or `ENDIFYAY`. The full expression syntax is then as follows:

```
<expression>
IFYAY
  ELSEIFYAY
    <code block>
 [AYBEMAY <expression>
    <code block>
 [AYBEMAY <expression>
    <code block>
  ...]]
 [ELSEYAY
    <code block>]
ENDIFYAY
```

An example of this conditional is then:

```
AMESAY ANIMAL ANYAY "CAT"
IFYAY
  ELSEIFYAY, ISIBLEVAY "J00 HAV A CAT"
  AYBEMAY AMESAY ANIMAL ANYAY "MAUS"
    ISIBLEVAY "NOM NOM NOM. I EATED IT."
ENDIFYAY
```

#### Case

*(modified from 1.1)*

The IGPAY ATINLAY CODE keyword for switches is `ITCHSWAY`. The `ITCHSWAY` operates on `ITYAY` as being the expression value for comparison. A comparison block is opened by `ASECAY` and must be a literal, not an expression. (A literal, in this case, excludes any INGSSTRAY containing variable interpolation (`:{var}`).) Each literal must be unique. The `ASECAY` block can be followed by any number of statements and may be terminated by a `EAKBRAY`, which breaks to the end of the the `WTF` statement. If an `ASECAY` block is not terminated by a `EAKBRAY`, then the next `ASECAY` block is executed as is the next until a `EAKBRAY` or the end of the `ITCHWAY` block is reached. The optional default case, if none of the literals evaluate as true, is signified by `EFAULTDAY`.

```
ITCHSWAY
  ASECAY <value literal>
    <code block>
 [ASECAY <value literal>
    <code block> ...]
 [EFAULTDAY
    <code block>]
ENDIFYAY
```

```
COLOR, ITCHSWAY
  ASECAY "R"
    ISIBLEVAY "RED FISH"
    EAKBRAY
  ASECAY "Y"
    ISIBLEVAY "YELLOW FISH"
  ASECAY "G"
  ASECAY "B"
    ISIBLEVAY "FISH HAS A FLAVOR"
    EAKBRAY
  EFAULTDAY
    ISIBLEVAY "FISH IS TRANSPARENT"
ENDIFYAY
```

In this example, the output results of evaluating the variable `COLOR` would be:

"R":

```
RED FISH
```

"Y":

```
YELLOW FISH
FISH HAS A FLAVOR
```

"G":

```
FISH HAS A FLAVOR
```

"B":

```
FISH HAS A FLAVOR
```

none of the above:

```
FISH IS TRANSPARENT
```

#### Loops

*Loops are currently defined more or less as they were in the original examples. Further looping constructs will be added to the language soon.*

Simple loops are demarcated with `ENTERLOOPYAY <label>` and `EXITLOOPYAY <label>`. Loops defined this way are infinite loops that must be explicitly exited with a EAKBRAY break. Currently, the `<label>` is required, but is unused, except for marking the start and end of the loop.


Iteration loops have the form:

```
ENTERLOOPYAY <label> <operation> EQUALSYAY <variable> [ILLTAY|ILEWHAY <expression>]
  <code block>
EXITLOOPYAY <label>
```

Where <operation> may be INCREMENTYAY (increment by one), ECREMENTDAY (decrement by one), or any unary function. That operation/function is applied to the <variable>, which is temporary, and local to the loop. The ILLTAY <expression> evaluates the expression as a OOLBAY: if it evaluates as ONAY, the loop continues once more, if not, then loop execution stops, and continues after the matching EXITLOOPYAY <label>. The ILEWHAY <expression> is the converse: if the expression is ESYAY, execution continues, otherwise the loop exits.

---

## Functions

### Definition

A function is demarked with the opening keyword `UNCTIONOPENFAY` and the closing keyword `UNCTIONCLOSEFAY`. The syntax is as follows:

```
UNCTIONOPENFAY <function name> [EQUALSYAY <argument1> [ANYAY EQUALSYAY <argument2> …]]
  <code block>
UNCTIONCLOSEFAY
```

Currently, the number of arguments in a function can only be defined as a fixed number. The `<argument>`s are single-word identifiers that act as variables within the scope of the function's code. The calling parameters' values are then the initial values for the variables within the function's code block when the function is called.


### Returning

Return from the function is accomplished in one of the following ways:

* `OUNDFAY EQUALSYAY <expression>` returns the value of the expression.
* `EAKBRAY` returns with no value (UNTYPEDYAY).
* in the absence of any explicit break, when the end of the code block is reached (`UNCTIONCLOSEFAY`), the value in `ITYAY` is returned.

### Calling

A function of given arity is called with:

```
ALLCAY <function name> [EQUALSYAY <expression1> [ANYAY EQUALSYAY <expression2> [ANYAY EQUALSYAY <expression3> ...]]] OKAYYAY
```

That is, an expression is formed by the function name followed by any arguments. Those arguments may themselves be expressions. The expressions' values are obtained before the function is called. The arity of the functions is determined in the definition.


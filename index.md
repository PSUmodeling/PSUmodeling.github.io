# Penn State Earth System Modeling Team Developer Guidelines

Prepared by [Yuning Shi](https://github.com/shiyuning) (Janurary 2021)

- [Penn State Earth System Modeling Team Developer Guidelines](#penn-state-earth-system-modeling-team-developer-guidelines)
  - [Introduction](#introduction)
  - [Code Management](#code-management)
    - [Pulls from the Home Repo](#pulls-from-the-home-repo)
    - [Commits](#commits)
    - [Tests](#tests)
    - [Issues](#issues)
    - [Sample Input Files and User's Manual](#sample-input-files-and-users-manual)
    - [Releases](#releases)
  - [C Style Guide](#c-style-guide)
    - [Naming](#naming)
      - [General Naming Rules](#general-naming-rules)
      - [File Names](#file-names)
      - [Variable Names](#variable-names)
      - [Constant Names](#constant-names)
      - [Function Names](#function-names)
      - [Type Names](#type-names)
      - [Macro Names](#macro-names)
      - [Exceptions to Naming Rules](#exceptions-to-naming-rules)
    - [Formatting](#formatting)
      - [Line Length](#line-length)
      - [Spaces vs. Tabs](#spaces-vs-tabs)
      - [Function Declarations and Definitions](#function-declarations-and-definitions)
      - [Variable Declarations](#variable-declarations)
      - [Function Calls](#function-calls)
      - [Braced Initializer List Format](#braced-initializer-list-format)
      - [Conditionals](#conditionals)
      - [Loops and Switch Statements](#loops-and-switch-statements)
      - [Pointer and Reference Expressions](#pointer-and-reference-expressions)
      - [Boolean Expressions](#boolean-expressions)
      - [Return Values](#return-values)
      - [Preprocessor Directives](#preprocessor-directives)
      - [Structure Format](#structure-format)
      - [Horizontal Whitespace](#horizontal-whitespace)
        - [General](#general)
        - [Loops and Conditionals](#loops-and-conditionals)
        - [Operators](#operators)
      - [Vertical Whitespace](#vertical-whitespace)

## Introduction

The goal of this guide is to describe the best practices for Penn State Earth System Modeling Team code management, and the style that should be followed when writing C code.
Code management is essential for successful collaboration, and following a style guide could significantly improve the readability and maintainability of the code.
The formatting section is mainly copied from the [Google C++ Style Guide](https://google.github.io/styleguide/cppguide.html), with a few changes.

## Code Management

All code development is coordinated via PSUmodeling GitHub repositories.

Developers are recommended to fork the home repo to their accounts, clone the forked repository, make changes (preferably using a new branch other than the main), and push changes to the forked repository.
When your branch is ready to be merged, make a pull request on GitHub.
The home repository owner will review your code, and accept or reject your changes, depending on the quality of the changes.
If you are making substantial changes, you can request to push directly to the home repo.
However, no more than *one* developer should push to the home repo at the same time.
If major changes are directly made to the home repo, a development branch should be used and the master branch of the home repo should always be stable.

### Pulls from the Home Repo

After cloning your forked repository, an "upstream" target should be added in order to pull the latest updates from the home repo.
Using GitHub command line tool is highly recommended.

```shell
$ git remote add upstream git@github.com:PSUmodeling/repo.git
```

Pull frequently to merge the latest updates from the home repo.

### Commits

Commit and push often.
Committing more means you will have more checkpoints, and you will thank yourself later.
Commit messages should be concise and descriptive.
Describe what features have been added, what bugs have been fixed, etc.
Refer to the reported issues when possible.
For example, "Increase MAXLYR to fix #7"
Note that the reference in the commit message (#7 in this case) will automatically link to the issues on GitHub.

### Tests

Before making a pull request, the code must be tested.
While sometimes it is difficult to test on all operational systems, it should at least be tested on the system that you develop on.
- Test if the code compiles after the changes.
- Test if the code runs, using the sample input files.
- Test if the code produces reasonable results.
- Check if the code follows the coding style, as describes below.

Before merging the changes, the home repo owner should also test the code and review the coding style.
The home repo owner has the right to review, comment on, and reject the pull requests.

### Issues

All bug reports, feature requests, and code discussion should be made using the GitHub "Issues" feature.

### Sample Input Files and User's Manual

Each project should provide sample input files and a user's manual.
If any changes to the code require changes in input/output format, the developer should also modify the sample input files and the user's manual accordingly.

### Releases

All releases should include release notes, with a version number, and changes made since last release.

A version format of X.Y.Z (Major.Minor.Patch) should be used.

- Major version zero (0) should be used for pre-release initial development.
- Version 1.0.0 should be the first public version.
- Z should be incremented for bug fixes.
- Y should be incremented when minor new features and functionalities are added.
- X should be incremented when major new features are added.
- Any version that requires the changes in I/O format should trigger the changes in X.

---
The sections below present a style guide for C code, which should be followed by Penn State Earth System Modeling Team developers.

## C Style Guide

### Naming

#### General Naming Rules

Names for files, functions, constants, or variables should be descriptive and meaningful; avoid abbreviation as much as possible.
Follow the guidelines below:

- Choose names with meanings that are precise and use them consistently throughout the program.
- Follow a uniform scheme when abbreviating names.
- Avoid abbreviations that form letter combinations that may suggest unintended meanings. For example, the name `inch` is a misleading abbreviation for `input character`. The name `in_char` would be better.
- Assign names that are unique (with respect to the number of unique characters permitted on your system).
- Use longer names to improve readability and clarity. However, if names are too long, the program may be more difficult to understand and it may be difficult to express the structure of the program using proper indentation.
- Names more than four characters in length should differ by at least two characters. For example, `systst` and `sysstst` are easily confused.

#### File Names

Filenames should be all lowercase and can include underscores (\_).
C files should end in `.c` and header files should end in `.h`, e.g., `cycles.c` and `cycles_const.h`.

#### Variable Names

The names of variables (including function parameters) and data members are all lowercase, with underscores between words.
For example,

```C
double              radiation_growth;
double              transpiration_growth;
```

#### Constant Names

The names of constants use upper-case words separated by underscores.
All such variables with static storage duration (i.e., statics and globals) should be named this way.
For example,

```C
const double        RESIDUE_MAX_WATER_CONC = 3.3;
```

#### Function Names

Ordinarily, functions should start with a capital letter and have a capital letter for each new word; do not use underscores. For example,

```C
void CropGrowth(...)
{
    ...
}
```

#### Type Names

Type names (i.e., created with `typedef`) should follow the naming standards for global variables.

#### Macro Names

Macros should be named with all capitals and underscores.
For example,

```C
#define PI          3.1415927
```

#### Exceptions to Naming Rules

If you are naming something that is analogous to an existing C entity then you can follow the existing naming convention scheme.

### Formatting

Coding style and formatting are pretty arbitrary, but a project is much easier to follow if everyone uses the same style.
Individuals may not agree with every aspect of the formatting rules, and some of the rules may take some getting used to, but it is important that all project contributors follow the style rules so that they can all read and understand everyone's code easily.

#### Line Length

Each line of text in your code should be at most **120** characters long.

Comment lines can be longer than 120 characters if it is not feasible to split them without harming readability, ease of cut and paste or auto-linking, e.g., if a line contains an example command or a literal URL longer than 120 characters.

An `#include` statement with a long path may exceed 80 columns.

You needn't be concerned about header guards that exceed the maximum length.

#### Spaces vs. Tabs

Use only spaces (i.e., soft tabs), and indent **four (4)** spaces at a time.
Do not use tabs in your code.
Change the tab type of your editor to soft tabs, with a tab length of four spaces.

#### Function Declarations and Definitions

Return type on the same line as function name, parameters on the same line if they fit.
Wrap parameter lists which do not fit on a single line as you would wrap arguments in a function call.

Functions look like this:

```C
ReturnType FunctionName (Type par_name1, Type par_name2)
{
    DoSomething ();
    ...
}
```

If you have too much text to fit on one line:

```C
ReturnType ReallyLongFunctionName (Type par_name1, Type par_name2,
    Type par_name3)
{
    DoSomething ();
    ...
}
```

or if you cannot fit even the first parameter:

```C
ReturnType ReallyReallyReallyLongFunctionName(
    Type par_name1, Type par_name2, Type par_name3)
{
    DoSomething ();
    ...
}
```

Some points to note:

- Choose good parameter names.
- Parameter names may be omitted only if the parameter is unused and its purpose is obvious.
- If you cannot fit the return type and the function name on a single line, break between them.
- If you break after the return type of a function declaration or definition, do not indent.
- The open parenthesis is always on the same line as the function name.
- There is never a space between the function name and the open parenthesis.
- There is never a space between the parentheses and the parameters.
- The open curly brace is always on the start of the next line.
- The close curly brace is always on the last line by itself.
- Default indentation is 4 spaces.
- Wrapped parameters have a 4 space indent.

#### Variable Declarations

Follow these guidelines for variable declarations:

- Align variable declarations so that the first letter of each variable name is in the 17th column, less the indent at the beginning of the line.
- Declare each internal variable on a separate line followed by an explanatory
comment, unless variables are self-explanatory and related.
- Loop indices can all be listed on the same line with one comment.

```C
ReturnType FunctionName()
{
    Type            var_name1;  /* Explanatory comment */
    StructType      var_name2;  /* Explanatory comment */
    Type           *var_name3;  /* Explanatory comment */
    int             i, j, k;    /* Loop indices */
    Type            year, month, day;   /* Self-exlanatory and related */
}
```

#### Function Calls

Function calls have the following format:

```C
    result = DoSomething(argument1, argument2, argument3);
```

If the arguments do not all fit on one line, they should be broken up onto multiple lines, with a four space indent.
Do not add spaces after the open paren or before the close paren:

```C
    result = DoSomething(averyveryveryverylongargument1,
        argument2, argument3);
```

Arguments may optionally all be placed on subsequent lines with a four space indent if that improves readability:

```C
if (...)
{
    ...
    ...
    if (...)
    {
        result = DoSomething(
            argument1, argument2,
            argument3, argument4);
    }
}
```

#### Braced Initializer List Format

Format a braced initializer list exactly like you would format a function call in its place.

If the braced list follows a name (e.g., a type or variable name), format as if the `{}` were the parentheses of a function call with that name.
If there is no name, assume a zero-length name.

```C

/* Examples of braced init list on a single line. */

SomeFunction(
    {"assume a zero-length name before {"},
    some_other_function_parameter);

SomeType variable{
    some, other, values,
    {"assume a zero-length name before {"},
    SomeOtherType{
        "Very long string requiring the surrounding breaks.",
        some, other values},
    SomeOtherType{"Slightly shorter string",
                  some, other, values}};
SomeType variable{
    "This is too long to fit all in one line"};
MyType m = {
    superlongvariablename1,
    superlongvariablename2,
    {short, interior, list},
    {interiorwrappinglist,
     interiorwrappinglist2}};
```

#### Conditionals

Prefer no spaces inside parentheses.
The `if` and `else` keywords belong on separate lines.

Do not use spaces between the parentheses and the condition.

```C
if (condition)
{
    ...
}
else if (...)
{
    ...
}
else
{
    ...
}
```

You must have a space between the `if` and the open parenthesis.
`if` and `else` must always always have accompanying braces.
The open and close curly braces are always on the start of lines by themselves.

When using `? :` conditional operators, always put a space around conditional operators, and put parenthesis around the conditions.

```C
 z = (a > b) ? a : b;
```

#### Loops and Switch Statements

Switch statements do not need braces.
Annotate non-trivial fall-through between cases.
Braces must be used even for single-statement loops.
Empty loop bodies should use empty braces or continue.

`case` blocks in `switch` statements do not need curly braces.

If not conditional on an enumerated value, switch statements should always have a default case (in the case of an enumerated value, the compiler will warn you if any values are not handled).
If the default case should never execute, simply abort or assert:

```C
switch (var)
{
    case 0:
        ...
        break;
    case 1:
        ...
        break;
  default:
        abort();
}
```

Braces must be used even for single-statement loops.

```C
for (int i = 0; i < kSomeNumber; i++)
{
    printf("I love you\n");
}
```

Empty loop bodies should use an empty pair of braces or continue, but not a single semicolon.

```C
while (condition)
{
    /* Repeat test until it returns false. */
}

for (i = 0; i < kSomeNumber; i++)
{}
```

#### Pointer and Reference Expressions

No spaces around period or arrow.
Pointer operators do not have trailing spaces.
The following are examples of correctly-formatted pointer and reference expressions:

```C
x = *p;
p = &x;
x = r.y;
x = r->y;
```

Note that:

- There are no spaces around the period or arrow when accessing a member.
- Pointer operators have no space after the * or &.
- When declaring a pointer variable or argument, you may place the asterisk adjacent to either the type or to the variable name:

```C
/* These are fine, space preceding. */
char *c;
char* c;
```

It is allowed (if unusual) to declare multiple variables in the same declaration, but it is disallowed if any of those have pointer or reference decorations.
Such declarations are easily misread.

```C
/* Fine if helpful for readability. */
int                 x, y;
int                 x, *y;      /* Disallowed - no & or * in multiple declaration */
char              * c;          /* Bad - spaces on both sides of * */
```

#### Boolean Expressions

When you have a boolean expression that is longer than the standard line length, the logical operators are always at the end of the lines:

```C
if (this_one_thing > this_other_thing &&
    a_third_thing == a_fourth_thing &&
    yet_another && last_one)
{
    ...
}
```

Note that when the code wraps in this example, both of the `&&` logical AND operators are at the end of the line.
Feel free to insert extra parentheses judiciously because they can be very helpful in increasing readability when used appropriately.
Also note that you should always use the punctuation operators, such as `&&` and `||`, rather than the word operators.

#### Return Values

Do not needlessly surround the return expression with parentheses.

Use parentheses in `return expr;` only where you would use them in `x = expr;`.
Always use a space after `return`.

```C
return result;                  /* No parentheses in the simple case. */
/* Parentheses OK to make a complex expression more readable. */
return (some_long_condition && another_condition);
```

#### Preprocessor Directives

The hash mark that starts a preprocessor directive should always be at the beginning of the line.

Even when preprocessor directives are within the body of indented code, the directives should start at the beginning of the line.

```C
    if (lopsided_score)
    {
#if DISASTER_PENDING
        DropEverything();
# if NOTIFY
        NotifyClient();
# endif
#endif
        BackToNormal();
    }
```

#### Structure Format

The basic format for a structure definition is:

```C
typedef struct my_struct
{
    Type            var_name1;
    Type           *var_name2;
};
```

#### Horizontal Whitespace

Never put trailing whitespace at the end of a line.

##### General

Adding trailing whitespace can cause extra work for others editing the same file, when they merge, as can removing existing trailing whitespace.
So: Don't introduce trailing whitespace.
Remove it if you're already changing that line, or do it in a separate clean-up operation (preferably when no-one else is working on the file).

##### Loops and Conditionals

```C
while (test)
{
     /* There is no space inside parentheses. */
}

for (i = 0; i < 5; i++ )
{
    /* For loops always have a space after the semicolon. */
    ...
}

switch (i)
{
    case 1:
        /* No space before colon in a switch case. */
        ...
}
```

##### Operators

```C
/* Assignment operators always have spaces around them. */
x = 0;

/* Other binary operators always have spaces around them.
 * Parentheses should have no internal padding. */
v = w * x + y / z;
v = w * (x + z);

/* No spaces separating unary operators and their arguments. */
x = -5;
++x;
if (x && !y)
{
}

```

When you split a long line with operators, the operators are always at the end of the lines.
The lines should be split at where it is meaningful.
For example,

```C
x = a * b +
    c * d;
```

is preferred to

```C
x = a * b + c *
    d;
```

#### Vertical Whitespace

Minimize use of vertical whitespace.

This is more a principle than a rule: don't use blank lines when you don't have to.
In particular, don't put more than one blank lines between functions, resist starting functions with a blank line, don't end functions with a blank line, and be discriminating with your use of blank lines inside functions.

The basic principle is: The more code that fits on one screen, the easier it is to follow and understand the control flow of the program.
Of course, readability can suffer from code being too dense as well as too spread out, so use your judgement.
But in general, minimize use of vertical whitespace.

Some rules of thumb to help when blank lines may be useful:

- Blank lines at the beginning or end of a function very rarely help readability.
- Blank lines inside a chain of if-else blocks may well help readability.

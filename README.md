# The Cyva Programming Language — Complete Documentation

**Version:** 1.0

Welcome to Cyva! This document teaches you the entire language from scratch. No prior
experience with Cyva is assumed. If you know a little programming in any language,
you'll feel right at home — and if you don't, everything is explained as we go.

---

## Table of Contents

1. [What is Cyva?](#1-what-is-cyva)
2. [Running Your First Program](#2-running-your-first-program)
3. [The Command-Line Tool](#3-the-command-line-tool)
4. [How a Cyva Program is Organized](#4-how-a-cyva-program-is-organized)
5. [Comments and Whitespace](#5-comments-and-whitespace)
6. [Values and Types](#6-values-and-types)
7. [Variables](#7-variables)
8. [Operators and Expressions](#8-operators-and-expressions)
9. [Strings and Interpolation](#9-strings-and-interpolation)
10. [Collections: Lists, Tuples, Dictionaries](#10-collections-lists-tuples-dictionaries)
11. [Printing and Reading Input](#11-printing-and-reading-input)
12. [Making Decisions: if / else](#12-making-decisions-if--else)
13. [Loops](#13-loops)
14. [switch Statements](#14-switch-statements)
15. [Functions](#15-functions)
16. [Classes and Objects](#16-classes-and-objects)
17. [Structs (Value Types)](#17-structs-value-types)
18. [Inheritance](#18-inheritance)
19. [Interfaces](#19-interfaces)
20. [Enums](#20-enums)
21. [Namespaces and Multiple Files](#21-namespaces-and-multiple-files)
22. [The Standard Library](#22-the-standard-library)
23. [Built-in Members on Values](#23-built-in-members-on-values)
24. [Networking](#24-networking)
25. [Errors and Exceptions](#25-errors-and-exceptions)
26. [Error Messages You Might See](#26-error-messages-you-might-see)
27. [Quick Reference](#27-quick-reference)

---

## 1. What is Cyva?

Cyva is a small, friendly programming language with a syntax that looks a lot like C#
or Java. It has:

- Familiar curly-brace blocks `{ ... }`
- Static types (you say what kind of value each variable holds)
- Classes, structs, interfaces, and enums
- First-class functions, including passing functions around
- Built-in collections: lists, tuples, dictionaries
- A rich standard library for math, strings, and collections
- Built-in networking tools

Cyva source files end with **`.cyva`**.

---

## 2. Running Your First Program

Create a file named `hello.cyva` containing:

```
Print("Hello, world!")
```

Then, in a terminal:

```
cyva run hello.cyva
```

You'll see:

```
Hello, world!
```

That's it — you've written and run a Cyva program.

You can also define a `Main` function, which Cyva will run first:

```
void Main()
{
    Print("Hello from Main!")
}
```

If a top-level function called `Main` exists, it runs before anything else. Any
statements written outside of functions (top-level statements) run after `Main`.

---

## 3. The Command-Line Tool

The `cyva` command supports four operations:

| Command | What it does |
|---------|--------------|
| `cyva run <file.cyva>`    | Compiles and executes the program |
| `cyva check <file.cyva>`  | Only checks for errors; does not run |
| `cyva ast <file.cyva>`    | Prints the parsed structure of the program |
| `cyva tokens <file.cyva>` | Prints every token (useful for debugging) |

**Exit codes:**

- `0` — success
- `1` — usage error or file not found
- `2` — the program has errors

---

## 4. How a Cyva Program is Organized

A `.cyva` file can contain, in any order:

- `using` directives (imports from other namespaces)
- `namespace` declarations (organizational grouping)
- Type declarations: `class`, `struct`, `interface`, `enum`
- Function declarations
- Top-level statements (things that run immediately)

Blank lines and extra whitespace do not matter.

---

## 5. Comments and Whitespace

**Single-line comments** start with `//` and go to the end of the line:

```
// This is a comment
Print("hello")   // so is this
```

**Block comments** are enclosed in `/* ... */` and can span multiple lines:

```
/*
   This whole block
   is a comment.
*/
```

Whitespace (spaces, tabs, blank lines) is generally ignored. Cyva uses newlines to
end most statements, but you can also use semicolons `;` if you prefer.

---

## 6. Values and Types

Every value in Cyva has a type. The basic types are:

| Type | Meaning | Example values |
|------|---------|----------------|
| `int`     | Whole number             | `0`, `42`, `-7` |
| `float`   | Decimal number           | `3.14`, `0.5`, `-2.0` |
| `bool`    | True or false            | `true`, `false` |
| `string`  | Text                     | `"hello"`, `"Cyva"` |
| `char`    | Single character         | `'a'`, `'Z'` |
| `byte`    | Small whole number 0–255 | `0`, `255` |
| `void`    | "No value" (used for functions that return nothing) | — |
| `null`    | The absence of a value   | `null` |
| `object`  | Any value at all         | anything |

You can combine types:

- `list<T>` — a list of `T` values, e.g. `list<int>`
- `Dictionary<K, V>` — a mapping from keys of type `K` to values of type `V`
- Tuples like `(int, string)` — a small ordered group

### Booleans can be capitalized

`true` and `True` mean the same thing, and so do `false` and `False`.

---

## 7. Variables

A variable is a named storage slot.

### Inferred variables (`var`)

Use `var` when you want Cyva to figure out the type from the initial value:

```
var age = 30
var name = "Ada"
var pi = 3.14
var isReady = true
```

### Explicitly typed variables

If you want to state the type yourself:

```
int count = 0
string greeting = "hello"
float ratio = 0.5
bool done = false
```

### Declaring without a value

```
int total       // starts at 0
string title    // starts as ""
bool flag       // starts as false
```

For other types, an uninitialized variable has the value `null`.

### Multiple variables in one line

```
var a = 1, b = 2, c = 3
int x = 0, y = 0
```

If a later variable has a value and an earlier one doesn't, the earlier one
receives the same value.

### Scope

Variables live inside the block `{ ... }` where they were declared. When the block
ends, the variables go away. You can reuse the same name in a different block.

---

## 8. Operators and Expressions

### Arithmetic

| Operator | Meaning | Example |
|----------|---------|---------|
| `+` | Add (or join strings) | `2 + 3` → `5` |
| `-` | Subtract | `10 - 4` → `6` |
| `*` | Multiply | `3 * 4` → `12` |
| `/` | Divide | `7 / 2` → `3.5` |
| `%` | Remainder | `7 % 3` → `1` |

Note that `/` always gives a decimal result. If you divide two integers, you still
get a `float`.

`+` also works with strings:

```
"Hello, " + "world"   // "Hello, world"
"Count: " + 10        // "Count: 10"
```

### Comparison and equality

| Operator | Meaning |
|----------|---------|
| `==` | Equal |
| `!=` | Not equal |
| `<`  | Less than |
| `<=` | Less than or equal |
| `>`  | Greater than |
| `>=` | Greater than or equal |

All comparison operators produce a `bool`.

### Logical operators

- `&&` — AND (true only if both sides are true)
- `||` — OR (true if either side is true)
- `!`  — NOT (flips true ↔ false)

Both `&&` and `||` are **short-circuiting**: if the result is already known from
the left side, the right side is not evaluated.

### Null-coalescing

- `??` — Returns the left side, or the right side if the left is `null`.

```
var name = userInput ?? "anonymous"
```

### Ternary operator

A one-line `if`/`else` that yields a value:

```
var label = age >= 18 ? "adult" : "minor"
```

### Assignment operators

| Operator | Meaning |
|----------|---------|
| `=`  | Assign |
| `+=` | Add and assign |
| `-=` | Subtract and assign |
| `*=` | Multiply and assign |
| `/=` | Divide and assign |

Example:

```
var n = 5
n += 3    // n is now 8
n *= 2    // n is now 16
```

### Increment / decrement

- `x++` — returns `x`, then adds 1
- `x--` — returns `x`, then subtracts 1
- `++x` — adds 1, then returns the new value
- `--x` — subtracts 1, then returns the new value

These only work on variables.

### Bitwise NOT

- `~x` — flips every bit of an `int`

### Casting

Convert a value to a different type by putting the target type in parentheses
before the value:

```
(int)3.9       // 3
(float)7       // 7.0
(string)42     // "42"
(bool)0        // false
```

### Indexing

Use square brackets to look up an element:

```
items[0]           // first element of a list
dict["name"]       // value in a dictionary
text[2]            // third character of a string
tuple[0]           // first item of a tuple
```

Negative indices count from the end:

```
items[-1]          // last element
```

### Member access

Use a dot to access a field, method, or built-in property:

```
user.Name
items.Count
text.ToUpper()
```

---

## 9. Strings and Interpolation

Strings are written in double quotes:

```
"hello"
"a longer sentence"
```

Escape sequences:

| Escape | Meaning |
|--------|---------|
| `\n` | New line |
| `\t` | Tab |
| `\r` | Carriage return |
| `\"` | A literal double quote |
| `\\` | A literal backslash |
| `\$` | A literal dollar sign |

### Interpolated strings

Put a `$` before the quote to embed expressions inside `{ ... }`:

```
var name = "Ada"
Print($"Hello, {name}!")

var a = 2
var b = 3
Print($"{a} + {b} = {a + b}")
```

Use `{{` and `}}` to write literal braces:

```
Print($"This is a literal {{brace}}")
```

### Characters

Single quotes make a character:

```
var c = 'A'
```

Characters support the same escape sequences as strings.

---

## 10. Collections: Lists, Tuples, Dictionaries

### Lists

A **list** is an ordered, growable collection. Create one with square brackets:

```
var numbers = [1, 2, 3]
var names = ["Ada", "Grace", "Alan"]
var empty = []
```

Access and update elements:

```
numbers[0]          // 1
numbers[0] = 99     // [99, 2, 3]
numbers[-1]         // 3 (last element)
```

Lists have many built-in methods — see [§23](#23-built-in-members-on-values).

### Tuples

A **tuple** groups a fixed number of values of possibly different types:

```
var pair = (1, "one")
var triple = (3.14, true, "pi")
```

Access items with `Item1`, `Item2`, etc., or by index:

```
pair.Item1     // 1
pair[1]        // "one"
```

Tuples are immutable — you cannot change their contents.

### Dictionaries

A **dictionary** maps keys to values. Create one with `{ key: value, ... }`:

```
var ages = {
    "Ada": 36,
    "Grace": 45
}
var empty = {}
```

Read and write:

```
ages["Ada"]                 // 36
ages["Alan"] = 41           // adds a new entry
```

Dictionaries have methods like `ContainsKey`, `Keys`, and `Values` — see
[§23](#23-built-in-members-on-values).

---

## 11. Printing and Reading Input

### Printing

`Print` outputs to the console. There are three forms:

**Function call form** — prints all arguments on the same line:

```
Print("Age:", 30, "years")
// Age: 30 years
```

**Braced form** — same, but with curly braces:

```
Print{"Age:", 30, "years"}
```

**Bare form** — one expression, on its own line:

```
Print "hello"
```

You can also use `Print` with a single value:

```
Print($"The answer is {6 * 7}")
```

### Reading input

`Input` reads a line of text from the user:

```
var name = Input("What is your name? ")
Print($"Hello, {name}!")
```

If you pass a prompt, it's displayed before reading. Without a prompt, `Input()`
just waits for input.

---

## 12. Making Decisions: if / else

```
if (condition)
{
    // runs when condition is true
}
```

With an `else`:

```
if (age >= 18)
{
    Print("You may vote.")
}
else
{
    Print("Too young.")
}
```

Chain conditions with `else if`:

```
if (score >= 90)
{
    Print("A")
}
else if (score >= 80)
{
    Print("B")
}
else
{
    Print("C or below")
}
```

The condition must be a `bool`.

---

## 13. Loops

### `while` loops

Repeat while a condition is true:

```
var i = 0
while (i < 5)
{
    Print(i)
    i++
}
```

### `do`–`while` loops

Always run the body at least once, then check:

```
var i = 0
do
{
    Print(i)
    i++
} while (i < 5)
```

### `for` loops

A compact form with init, condition, and step:

```
for (var i = 0; i < 5; i++)
{
    Print(i)
}
```

Cyva also accepts a vertical-bar separator instead of semicolons:

```
for (var i = 0 | i < 5 | i++)
{
    Print(i)
}
```

You can leave parts out:

```
var i = 0
for (; i < 10;)
{
    i += 2
}
```

### `foreach` loops

Iterate over any collection:

```
foreach (var n in [1, 2, 3])
{
    Print(n)
}
```

Inside the loop, each element is bound to the loop variable. The type is inferred
from the collection.

#### Filtering form

If you write a literal in place of the loop variable, only items equal to that
literal are visited. Inside the body, `index` and `match` are available:

```
foreach 2 in [1, 2, 2, 3, 2]
{
    Print($"found 2 at index {index}")
}
```

For strings, this form searches for substrings:

```
foreach "cat" in "the cat sat on the mat"
{
    Print($"match at {index}")
}
```

### `break` and `continue`

- `break` exits the nearest loop immediately.
- `continue` skips to the next iteration.

```
foreach (var n in numbers)
{
    if (n < 0) continue     // skip negatives
    if (n > 100) break      // stop at large numbers
    Print(n)
}
```

---

## 14. switch Statements

Choose one of several branches based on a value:

```
switch (day)
{
    case 1:
        Print("Monday")
    case 2:
        Print("Tuesday")
    case 6:
    case 7:
        Print("Weekend!")
    default:
        Print("Another day")
}
```

- Several `case` labels may share a body (as shown with `6` and `7`).
- `default` runs when no case matches.
- A `break` inside a case body leaves the switch early.

---

## 15. Functions

### Declaring a function

```
int Add(int a, int b)
{
    return a + b
}

void Greet(string name)
{
    Print($"Hello, {name}")
}
```

The first word is the **return type** (`void` if none). The name is followed by
parentheses containing **parameters** (name and type each).

### Calling a function

```
var sum = Add(2, 3)
Greet("Ada")
```

### Default parameter values

```
void Greet(string name = "world")
{
    Print($"Hello, {name}")
}

Greet()           // "Hello, world"
Greet("Ada")      // "Hello, Ada"
```

### `ref` parameters

A `ref` parameter refers to the caller's variable. Changes made inside the function
are visible to the caller:

```
void Bump(ref int x)
{
    x = x + 1
}

var n = 5
Bump(ref n)
Print(n)   // 6
```

When calling, you must also write `ref` before the argument.

### `return`

- `return` with no value leaves a `void` function.
- `return expr` exits a function with that value.

### Calling functions as methods (extension style)

Any function whose first parameter is a value of type `T` can be called with dot
notation on a `T`:

```
int Double(int x) { return x * 2 }

Print(Double(5))   // 10
Print(5.Double())  // 10 — same thing
```

### Nested functions

You can declare functions inside blocks:

```
void Outer()
{
    int Inner(int x) { return x * x }
    Print(Inner(4))
}
```

---

## 16. Classes and Objects

A **class** is a blueprint for objects. Objects bundle data (fields) and behaviour
(methods).

### A simple class

```
public class Point
{
    public int X
    public int Y

    public Point(int x, int y)
    {
        this.X = x
        this.Y = y
    }

    public int Sum()
    {
        return X + Y
    }
}
```

`this` refers to the current object. You don't have to write `this.` to read
fields, but it's often clearer.

### Creating objects

```
var p = new Point(3, 4)
Print(p.X)         // 3
Print(p.Sum())     // 7
```

### Access modifiers

Fields and methods can be marked:

| Modifier | Meaning |
|----------|---------|
| `public`    | Accessible anywhere |
| `private`   | Accessible only inside the class |
| `protected` | Accessible inside the class and derived classes |
| `internal`  | Accessible inside the same program |

If you omit the modifier, the member is effectively private to the type.

### Fields with initial values

```
public class Counter
{
    public int Count = 0
    private string label = "counter"
}
```

Fields without initializers get a zero value: `0` for `int`, `0.0` for `float`,
`false` for `bool`, `""` for `string`, `null` for class-typed fields.

### Static members

A `static` field or method belongs to the class itself, not to any instance:

```
public class Config
{
    public static string Version = "1.0"

    public static string Describe()
    {
        return $"Version {Version}"
    }
}
```

Access static members through the class name:

```
Print(Config.Version)
Print(Config.Describe())
```

### Virtual and override

By default, a method cannot be replaced by a subclass. Mark it `virtual` to allow
subclasses to override it with `override`:

```
public class Animal
{
    public virtual string Speak() { return "..." }
}

public class Dog : Animal
{
    public override string Speak() { return "Woof" }
}
```

### Abstract classes and methods

An `abstract` class cannot be instantiated directly — you must derive from it. An
`abstract` method has no body and must be overridden by a concrete subclass:

```
public abstract class Shape
{
    public abstract float Area()
}

public class Square : Shape
{
    public float Side
    public Square(float s) { this.Side = s }
    public override float Area() { return Side * Side }
}
```

---

## 17. Structs (Value Types)

A **struct** is like a class, but it uses **value semantics**: when you assign a
struct, a copy is made.

```
struct Point
{
    public int X
    public int Y
    public Point(int x, int y) { this.X = x; this.Y = y }
}

var a = new Point(1, 2)
var b = a          // b is a COPY of a
b.X = 99
Print(a.X)         // still 1
Print(b.X)         // 99
```

With classes, `b = a` would make both names refer to the same object. With structs,
each name has its own copy.

Structs support constructors, fields, methods, and interfaces — everything classes
support except inheritance.

---

## 18. Inheritance

A class can inherit from another class:

```
public class Animal
{
    public string Name
    public Animal(string name) { this.Name = name }
    public virtual string Speak() { return "..." }
}

public class Dog : Animal
{
    public string Breed
    public Dog(string name, string breed) : base(name)
    {
        this.Breed = breed
    }
    public override string Speak() { return "Woof" }
}
```

- The colon `:` after the class name introduces the base class (and any interfaces).
- A derived constructor can call a base constructor with `base(...)`.
- Overridden methods use `override`.
- `base.Method(...)` explicitly calls the base version.

```
var d = new Dog("Rex", "Lab")
Print(d.Name)          // Rex
Print(d.Speak())       // Woof
```

---

## 19. Interfaces

An **interface** lists methods that a class promises to provide:

```
public interface IShape
{
    float Area()
    string Describe()
}
```

A class implements one or more interfaces by listing them in its base list:

```
public class Circle : IShape
{
    public float Radius
    public Circle(float r) { this.Radius = r }

    public float Area() { return 3.14159 * Radius * Radius }
    public string Describe() { return "a circle" }
}
```

Interfaces may extend other interfaces:

```
public interface INamedShape : IShape
{
    string Name()
}
```

Interfaces cannot be instantiated with `new`.

---

## 20. Enums

An **enum** is a named list of constant values:

```
enum Direction
{
    North,
    South,
    East,
    West
}
```

Each value has an implicit integer, starting at 0:

```
Print(Direction.North)   // 0
Print(Direction.West)    // 3
```

Use them for readability instead of magic numbers:

```
void Move(Direction d)
{
    switch (d)
    {
        case Direction.North: Print("Up")
        case Direction.South: Print("Down")
        case Direction.East:  Print("Right")
        case Direction.West:  Print("Left")
    }
}

Move(Direction.East)
```

---

## 21. Namespaces and Multiple Files

### Namespaces

Group related types with `namespace`:

```
namespace Geometry
{
    public class Point { ... }
    public class Circle { ... }
}
```

Or, using the file-scoped form (everything after it belongs to that namespace):

```
namespace Geometry;

public class Point { ... }
```

Bring names into scope with `using`:

```
using Geometry

var p = new Point(1, 2)
```

### Working with multiple files

When you run a `.cyva` file, Cyva also reads **every other `.cyva` file in the same
folder** and treats them as part of the same program. Types and functions declared
in any of those files are visible everywhere.

Only the file you ran has its top-level statements executed. Other files contribute
their types, functions, and usings.

Usings across all files are merged (duplicates are ignored).

---

## 22. The Standard Library

These are available everywhere without any imports.

### Core

| Name | Description |
|------|-------------|
| `Print(...)` | Print values to the console |
| `Input([prompt])` | Read a line of text |
| `Pi`, `E`, `Tau` | Mathematical constants |
| `IntMax`, `IntMin` | Largest and smallest whole numbers |

### Math

| Function | What it does |
|----------|--------------|
| `Square(x)` | x × x |
| `Cube(x)` | x × x × x |
| `Power(b, e)` | b raised to e |
| `Sqrt(x)` | Square root |
| `Cbrt(x)` | Cube root |
| `Abs(x)` | Absolute value |
| `Sign(x)` | −1, 0, or 1 |
| `Min(a, b)` / `Max(a, b)` | Smaller / larger |
| `Clamp(x, lo, hi)` | Force x into a range |
| `Lerp(a, b, t)` | Linear interpolation |
| `Round(x)` | Round to nearest whole number |
| `RoundTo(x, digits)` | Round to a number of decimal places |
| `Floor(x)` / `Ceil(x)` / `Truncate(x)` | Round down / up / toward zero |
| `Sin(x)`, `Cos(x)`, `Tan(x)` | Trigonometry |
| `Asin(x)`, `Acos(x)`, `Atan(x)` | Inverse trig |
| `Atan2(y, x)` | Angle of a vector |
| `Log(x, base)`, `Log10(x)`, `Log2(x)`, `Ln(x)` | Logarithms |
| `Exp(x)`, `Pow10(x)` | e^x, 10^x |

### Conversions

| Function | What it does |
|----------|--------------|
| `ParseInt(s)` | Text → int |
| `ParseFloat(s)` | Text → float |
| `TryParseInt(s, out)` | Text → int, returns bool |
| `TryParseFloat(s, out)` | Text → float, returns bool |
| `ToString(x)` | Value → text |
| `Ord(s)` | First character's numeric code |
| `CharFromCode(i)` | Numeric code → character |

### Ranges

| Function | What it does |
|----------|--------------|
| `Range(n)` | `[0, 1, ..., n-1]` |
| `Range(a, b)` | `[a, a+1, ..., b-1]` (or descending) |
| `RangeTo(a, b)` | Like `Range` but includes `b` |

### Collection helpers

`Sum`, `Product`, `Sort`, `Reverse`, `Distinct`, `First`, `Last` — all accept a list
and return a result.

---

## 23. Built-in Members on Values

Every value type has methods and properties available with dot syntax.

### Integers

`ToString`, `ToFloat`, `ToBool`, `Abs`, `Sign`, `IsEven`, `IsOdd`, `IsZero`,
`IsPositive`, `IsNegative`, `Squared`.

```
Print(7.IsOdd())        // true
Print((-3).Abs())       // 3
```

### Floats

`ToString`, `ToInt`, `ToBool`, `Abs`, `Sign`, `Floor`, `Ceil`, `Round`,
`IsInteger`, `IsNaN`, `IsInfinity`, `IsZero`, `IsPositive`, `IsNegative`.

### Booleans

`ToString`, `ToInt`.

### Strings

| Member | Description |
|--------|-------------|
| `Length` | Number of characters |
| `IsEmpty` | True if length is 0 |
| `Contains(s)` / `Has(s)` | Contains substring |
| `IndexOf(s)` / `LastIndexOf(s)` | Position of a substring |
| `StartsWith(s)` / `EndsWith(s)` | Begins / ends with |
| `ToUpper()` / `ToLower()` | Case conversion |
| `Trim()` / `TrimStart()` / `TrimEnd()` | Remove whitespace |
| `Replace(a, b)` | Replace all occurrences |
| `Substring(start[, length])` | Extract part of the string |
| `Split(sep)` | Split into a list |
| `PadLeft(n[, c])` / `PadRight(n[, c])` | Pad to a width |
| `Repeat(n)` | Repeat the string |
| `Reverse()` | Reversed string |
| `CharAt(i)` | Character at a position |
| `First()` / `Last()` | First / last character |
| `IsNumeric()` / `IsLetter()` / `IsDigit()` / `IsWhitespace()` | Character tests |
| `ToInt()` / `ToFloat()` / `ToBool()` | Parse to number |
| `Join(list)` | Join list elements with this string |

Example:

```
var s = "Hello, World"
Print(s.ToUpper())        // HELLO, WORLD
Print(s.Substring(7))     // World
Print(s.Split(", "))      // ["Hello", "World"]
```

### Lists

| Member | Description |
|--------|-------------|
| `Count` / `Length` | Number of items |
| `IsEmpty` | True if empty |
| `Add(x)` | Append |
| `Remove(x)` | Remove first occurrence, returns bool |
| `RemoveAt(i)` | Remove by index |
| `Contains(x)` / `Has(x)` | Test membership |
| `IndexOf(x)` | Position or −1 |
| `Clear()` | Remove all |
| `Reverse()` | Reverse in place |
| `Sort()` | Sort in place |
| `First()` / `Last()` | First / last item |
| `Skip(n)` / `Take(n)` | Subsequence |
| `Slice(start[, end])` | Subsequence |
| `Distinct()` | Remove duplicates |
| `Sum()` / `Product()` | Aggregate |
| `Min()` / `Max()` | Extreme values |
| `Any()` / `All()` | Truthiness tests |
| `CountOf(x)` | Count occurrences |
| `Concat(other)` | Concatenate |
| `Join(sep)` | Join into a string |

Example:

```
var nums = [3, 1, 4, 1, 5, 9, 2, 6]
nums.Sort()
Print(nums)                // [1, 1, 2, 3, 4, 5, 6, 9]
Print(nums.Sum())          // 31
Print(nums.Distinct())     // [1, 2, 3, 4, 5, 6, 9]
```

### Dictionaries

| Member | Description |
|--------|-------------|
| `Count` / `Length` | Number of entries |
| `IsEmpty` | True if empty |
| `ContainsKey(k)` / `Has(k)` | Key test |
| `ContainsValue(v)` | Value test |
| `Get(k[, default])` | Look up a key |
| `Set(k, v)` | Insert or update |
| `Remove(k)` | Remove an entry |
| `Clear()` | Remove all |
| `Keys()` / `Values()` | Lists of keys or values |
| `Add(k, v)` | Insert |

Example:

```
var ages = { "Ada": 36, "Grace": 45 }
Print(ages.ContainsKey("Ada"))    // true
foreach (var k in ages.Keys())
{
    Print($"{k} is {ages[k]}")
}
```

---

## 24. Networking

Cyva has built-in networking primitives. Create them like any other value.

### TCP client

```
var client = TcpClient("example.com", 80)
var stream = client.GetStream()
stream.WriteString("GET / HTTP/1.1\r\nHost: example.com\r\n\r\n")
Print(stream.ReadString(4096))
client.Close()
```

### TCP server

```
var listener = TcpListener(8080, "0.0.0.0")
listener.Start()
while (true)
{
    var client = listener.AcceptTcpClient()
    var stream = client.GetStream()
    stream.WriteString("hello from cyva\n")
    client.Close()
}
```

### HTTP client

```
var http = HttpClient()
var body = http.GetString("https://example.com")
Print(body)

var (status, pageBody) = http.Get("https://example.com")
Print($"{status}: {pageBody.Length} bytes")

http.Dispose()
```

### WebSocket client

```
var ws = ClientWebSocket()
ws.Connect("wss://echo.websocket.org")
ws.Send("hello")
var bytes = ws.Receive()
ws.Close()
```

### DNS and IP helpers

`DnsGetHostAddresses(host)`, `DnsGetHostName()`, `IPAddressParse(s)`,
`IPAddressAny`, `IPAddressLoopback`.

### UDP

`UdpClient(port)` — `.Send(bytes, host, port)`, `.Receive()`, `.Close()`.

### Raw sockets

`Socket("tcp")` or `Socket("udp")` — `.Connect`, `.Bind`, `.Listen`, `.Accept`,
`.Send`, `.Receive`, `.Close`.

### Streams

Common stream methods (available on TCP streams, SSL streams, and others):

`Write`, `WriteString`, `WriteBytes`, `Read`, `ReadString`, `ReadBytes`, `Flush`,
`Close`, `Dispose`, `DataAvailable`, `CanRead`, `CanWrite`.

For SSL, call `AuthenticateAsClient(host)` on an `SslStream` obtained from
`client.GetSslStream()`.

### Asynchronous helpers

Some methods have an `...Async` variant that returns a `Task`. Calling a method
without `Async` blocks until it finishes.

---

## 25. Errors and Exceptions

When something goes wrong at runtime — a bad index, a failed network call, a
division by zero — Cyva raises an **exception**. You can catch and handle them.

### try / catch / finally

```
try
{
    var x = ParseInt("not a number")
    Print(x)
}
catch (Exception e)
{
    Print($"Something went wrong: {e}")
}
finally
{
    Print("Done")
}
```

- The `try` block runs first.
- If an exception is raised, the `catch` block runs.
- The `finally` block always runs, whether or not there was an exception.
- The catch variable receives a text description of the error.

You can also omit the type and variable:

```
try { DoRiskyThing() }
catch { Print("Failed") }
```

### Throwing your own errors

```
if (age < 0)
{
    throw "Age cannot be negative"
}
```

The thrown value's text becomes the message visible to the catch block.

### When errors are not caught

If a runtime error reaches the top of the program, Cyva prints:

```
runtime error: <message>
```

and stops the program.

---

## 26. Error Messages You Might See

Every error message is prefixed with a code like `[CYV0301]`. Here are the most
common ones and what they mean:

| Code | What it means |
|------|---------------|
| CYV0001 | A character was typed that Cyva does not recognize |
| CYV0002 | A `/* ... */` comment was never closed |
| CYV0003 | A string or interpolation was never closed |
| CYV0004 | A character literal was never closed |
| CYV0100 | A punctuation mark or keyword was expected |
| CYV0102 | A body was supposed to open with `{` and didn't |
| CYV0301 | Assigning a value of the wrong type to a variable |
| CYV0302 | A variable was declared twice in the same scope |
| CYV0303 | Assigning a value of the wrong type to a field or element |
| CYV0310 | Using a name that was never declared |
| CYV0311 | Using a variable before it has a value |
| CYV0320 | Using an operator on values it does not support |
| CYV0330 | Calling a function that doesn't exist |
| CYV0332 | Passing an argument of the wrong type |
| CYV0333 | Passing too many arguments |
| CYV0334 | A `ref` marker was present on one side and not the other |
| CYV0335 | Calling a method the receiver doesn't have |
| CYV0340 | An `if`/`while`/`for` condition wasn't a `bool` |
| CYV0350 | Returning a value from a `void` function |
| CYV0351 | Returning a value of the wrong type |
| CYV0360 | Using `-x` on something that isn't a number |
| CYV0361 | Using `++`/`--` on something that isn't a number |
| CYV0362 | Using `~` on something that isn't an `int` |
| CYV0370 | Using `this` outside a class method |
| CYV0371 | Using `base` outside a derived class |
| CYV0373 | `new` on a type that doesn't exist |
| CYV0374 | `new` on an abstract class |
| CYV0375 | `new` on an interface |
| CYV0376 | No constructor matches the arguments given |
| CYV0377 | Constructor arguments have the wrong types |
| CYV0378 | An enum has no member with that name |
| CYV0379 | A type has no field with that name |
| CYV0380 | A type has no method with that name |

Diagnostics are printed in this format:

```
file.cyva:LINE:COLUMN: error: message [CYV####]
```

---

## 27. Quick Reference

### A complete example

```
// Define a class
public class Rectangle
{
    public float Width
    public float Height

    public Rectangle(float w, float h)
    {
        this.Width = w
        this.Height = h
    }

    public float Area()
    {
        return Width * Height
    }
}

// Use it
void Main()
{
    var shapes = [
        new Rectangle(3.0, 4.0),
        new Rectangle(5.0, 2.0)
    ]

    var total = 0.0
    foreach (var r in shapes)
    {
        total += r.Area()
        Print($"Rectangle {r.Width} x {r.Height} = {r.Area()}")
    }
    Print($"Total area: {total}")
}
```

Output:

```
Rectangle 3 x 4 = 12
Rectangle 5 x 2 = 10
Total area: 22
```

### Syntax cheat sheet

```
// Comments
// line comment
/* block comment */

// Variables
var x = 10
int y = 20

// Strings
"hello"
$"Hello, {name}!"
'c'

// Operators
+  -  *  /  %  ==  !=  <  <=  >  >=  &&  ||  !  ??  ?:
=  +=  -=  *=  /=  ++  --  ~

// Conditionals
if (cond) { ... } else { ... }

// Loops
while (cond) { ... }
do { ... } while (cond)
for (init; cond; step) { ... }
foreach (var item in collection) { ... }

// switch
switch (x) { case 1: ...; default: ...; }

// Functions
int Add(int a, int b) { return a + b }
void Greet(string name = "world") { Print(name) }
void Bump(ref int x) { x++ }

// Classes
public class Foo
{
    public int Bar
    public Foo(int b) { this.Bar = b }
    public virtual int Baz() { return Bar * 2 }
}

// Inheritance
public class Sub : Foo
{
    public Sub(int b) : base(b) { }
    public override int Baz() { return base.Baz() + 1 }
}

// Structs
struct Vec2 { public float X; public float Y }

// Interfaces
public interface IShape { float Area() }

// Enums
enum Color { Red, Green, Blue }

// Namespaces
namespace Geometry { ... }
namespace Geometry;   // file-scoped

// Errors
try { ... } catch (Exception e) { ... } finally { ... }
throw "message"

// Printing
Print("hello")
Print{a, b, c}
Print expr
```

### A short glossary

| Term | Meaning |
|------|---------|
| Block | A group of statements inside `{ }` |
| Expression | Something that produces a value |
| Statement | An instruction that does something |
| Function | A reusable named piece of code |
| Method | A function attached to a class or struct |
| Field | A named storage slot inside a class or struct |
| Instance | A concrete object created from a class |
| Class | A reference-type blueprint |
| Struct | A value-type blueprint |
| Interface | A contract listing methods a class must provide |
| Enum | A named list of constant integer values |
| Namespace | A grouping of related declarations |
| Using | An import of a namespace |
| Property | A value-like accessor, e.g. `Length` |
| Interpolation | Embedding expressions inside a string with `$"...{expr}..."` |

---

*End of document.*

# Visual Prolog Language Support

Full language support for Visual Prolog 5.2 in Visual Studio Code, including syntax highlighting, code snippets, and IntelliSense features.

## Features

### 🎨 Comprehensive Syntax Highlighting

- **Directives**: `domains`, `predicates`, `clauses`, `goal`, `facts`, `database`, `constants`
- **Class/Object-Oriented Keywords**: `class`, `object`, `interface`, `implement`, `end class`, `end object`
- **Control Flow**: `if`, `then`, `else`, `elseif`, `not`, `fail`, `true`, `and`, `or`, `repeat`, `cut`
- **Modifiers**: `determ`, `nondeterm`, `multi`, `procedure`, `single`, `static`, `abstract`, `virtual`, `override`, `final`
- **Built-in Types**: `char`, `byte`, `short`, `ushort`, `word`, `integer`, `unsigned`, `long`, `ulong`, `dword`, `real`, `real4`, `real8`, `string`, `symbol`, `pointer`, `binary`, `file`
- **Built-in Predicates**: `write`, `read`, `assert`, `retract`, `findall`, `member`, `append`, `concat`, and many more
- **Operators**: Arithmetic (`+`, `-`, `*`, `/`, `mod`, `div`), Comparison (`=`, `<>`, `<`, `>`, `<=`, `>=`), Logical (`and`, `or`, `not`), Bitwise (`shl`, `shr`, `xor`)

### 📝 Smart Code Snippets

Type the prefix and press `Tab` to expand:

#### Program Structure Snippets

**`program`** - Full program template
```prolog
% Program Name
% Description

domains
    DomainName = type

predicates
    predicateName(arguments)

clauses
    predicateName(Args) :-
        body.

goal
    predicateName(actualArgs).
```

**`domain`** - Domain declaration
```prolog
domains
    DomainName = type
```

**`predicate`** - Predicate declaration
```prolog
predicates
    predicateName(arguments)
```

**`clause`** - Clause definition
```prolog
clauses
    predicateName(Args) :-
        body.
```

**`goal`** - Goal section
```prolog
goal
    goalPredicate.
```

#### Object-Oriented Snippets

**`class`** - Class declaration
```prolog
class ClassName
predicates
    predicateName(arguments)
clauses
    predicateName(Args) :-
        body.
end class ClassName
```

**`interface`** - Interface declaration
```prolog
interface InterfaceName
predicates
    predicateName(arguments)
end interface InterfaceName
```

**`implement`** - Implementation section
```prolog
implement ClassName
clauses
    predicateName(Args) :-
        body.
end implement ClassName
```

#### Control Flow Snippets

**`if`** - If-then-else statement
```prolog
if condition then
    thenBody
else
    elseBody
end if
```

**`determ`** - Deterministic predicate
```prolog
predicates
    determ predicateName(arguments)
```

**`nondeterm`** - Non-deterministic predicate
```prolog
predicates
    nondeterm predicateName(arguments)
```

#### Database Operations Snippets

**`database`** - Database section
```prolog
database
    databaseName
predicates
    predicateName(arguments)
```

**`fact`** - Fact declaration
```prolog
facts
    factName(arguments)
```

**`assert`** - Assert clause
```prolog
assert(fact)
```

**`retract`** - Retract clause
```prolog
retract(fact)
```

**`findall`** - Find all solutions
```prolog
findall(Template, Goal, ResultList)
```

#### I/O and Built-in Predicates

**`write`** - Write output
```prolog
write(output)
```

**`read`** - Read input
```prolog
read(variable)
```

**`openread`** - Open file for reading
```prolog
openread(FileName, FileHandle)
```

**`openwrite`** - Open file for writing
```prolog
openwrite(FileName, FileHandle)
```

#### List Operations

**`list`** - List pattern
```prolog
[Head|Tail]
```

**`member`** - Member check
```prolog
member(Element, List)
```

**`append`** - Append lists
```prolog
append(List1, List2, Result)
```

#### String Operations

**`concat`** - String concatenation
```prolog
concat(String1, String2, Result)
```

### 🔧 Editor Features

- **Auto-closing pairs**: Automatically closes `()`, `[]`, `{}`, and `""`
- **Comment toggling**: Use `Cmd+/` (macOS) or `Ctrl+/` (Windows/Linux) to toggle line comments (`%`)
- **Block comments**: Select code and use comment shortcut for multi-line comments (`/* */`)
- **Bracket matching**: Highlights matching brackets, parentheses, and braces
- **Smart indentation**: Proper indentation for Visual Prolog code structure

### 🎯 Naming Conventions Support

- **Types/Domains**: Names starting with uppercase letters are highlighted as types (e.g., `Person`, `StudentList`)
- **Predicates/Functions**: Names starting with lowercase letters are highlighted as predicates (e.g., `factorial`, `processData`)
- **Variables**: Uppercase identifiers in code are recognized as variables
- **Atoms**: Lowercase identifiers are recognized as atoms/constants

## Supported File Extensions

- `.pro` - Visual Prolog program files
- `.cl` - Clause files
- `.pack` - Package files
- `.ph` - Prolog header files

## Usage Examples

### Example 1: Simple Factorial Program

Type `program` and Tab to get the template, then modify:

```prolog
% Factorial Calculator
% Calculates factorial of a number

domains
    Number = integer

predicates
    factorial(Number, Number)

clauses
    factorial(0, 1) :- !.
    factorial(N, Result) :-
        N > 0,
        N1 = N - 1,
        factorial(N1, R1),
        Result = N * R1.

goal
    factorial(5, X),
    write("Factorial of 5 is: ", X),
    nl.
```

### Example 2: List Operations

```prolog
% List Processing Example

domains
    IntList = integer*

predicates
    sumList(IntList, integer)
    member(integer, IntList)

clauses
    sumList([], 0).
    sumList([H|T], Sum) :-
        sumList(T, RestSum),
        Sum = H + RestSum.
    
    member(X, [X|_]).
    member(X, [_|T]) :-
        member(X, T).

goal
    List = [1, 2, 3, 4, 5],
    sumList(List, Total),
    write("Sum: ", Total), nl.
```

### Example 3: Class-Based Programming

Type `class` and Tab:

```prolog
class Student
domains
    Name = string
    Age = integer
    
predicates
    create(Name, Age)
    displayInfo()
    
clauses
    StudentName : Name
    StudentAge : Age
    
    create(N, A) :-
        StudentName := N,
        StudentAge := A.
    
    displayInfo() :-
        write("Name: ", StudentName), nl,
        write("Age: ", StudentAge), nl.
end class Student

goal
    S = Student::new(),
    S:create("John Doe", 20),
    S:displayInfo().
```

### Example 4: Database Operations

Type `database` and Tab:

```prolog
database
    phoneBook

predicates
    nondeterm phone(string, string)
    addPhone(string, string)
    findPhone(string)

clauses
    addPhone(Name, Number) :-
        assertz(phone(Name, Number)).
    
    findPhone(Name) :-
        phone(Name, Number),
        write(Name, ": ", Number), nl,
        fail.
    findPhone(_).

goal
    addPhone("Alice", "555-1234"),
    addPhone("Bob", "555-5678"),
    findPhone("Alice").
```

## Requirements

- Visual Studio Code version 1.50.0 or higher
- Visual Prolog 5.2 compiler (for running programs)

## Installation

### From VSIX File

1. Download the `.vsix` file
2. Open VS Code
3. Go to Extensions (`Cmd+Shift+X` or `Ctrl+Shift+X`)
4. Click on the `...` menu at the top
5. Select "Install from VSIX..."
6. Choose the downloaded file

### From Source

1. Clone or download this repository
2. Copy the folder to your VS Code extensions directory:
   - **Windows**: `%USERPROFILE%\.vscode\extensions`
   - **macOS/Linux**: `~/.vscode/extensions`
3. Restart VS Code

## Tips and Tricks

### Quick Snippet Access

- Type the snippet prefix and press `Tab` to expand
- Use `Ctrl+Space` to see all available snippets for Visual Prolog

### Code Navigation

- `Cmd+Shift+O` (macOS) or `Ctrl+Shift+O` (Windows/Linux) - Go to symbol in file
- `F12` - Go to definition (when supported by workspace indexing)

### Commenting

- `Cmd+/` or `Ctrl+/` - Toggle line comment (`%`)
- `Shift+Option+A` (macOS) or `Shift+Alt+A` (Windows/Linux) - Toggle block comment (`/* */`)

### Multi-Cursor Editing

- `Option+Click` (macOS) or `Alt+Click` (Windows/Linux) - Add cursor
- Useful for editing multiple similar predicates at once

## Known Issues

- Semantic analysis and IntelliSense are limited to syntax highlighting
- Go to Definition requires manual workspace symbol indexing
- No integrated compiler/debugger (use external Visual Prolog tools)

## Release Notes

### 0.1.0

Initial release of Visual Prolog Language Support:

- Complete syntax highlighting for Visual Prolog 5.2
- 25+ code snippets for common patterns
- Auto-closing pairs and bracket matching
- Support for `.pro`, `.cl`, `.pack`, and `.ph` files
- Comment toggling with standard VS Code shortcuts

## Contributing

Found a bug or have a feature request? Please open an issue on the repository.

## License

MIT License - see LICENSE file for details

## Resources

- [Visual Prolog Official Website](http://www.visual-prolog.com/)
- [Visual Prolog Documentation](http://wiki.visual-prolog.com/)
- [Prolog Programming Tutorial](https://www.learnprolognow.org/)

---

**Enjoy coding in Visual Prolog!** 🚀

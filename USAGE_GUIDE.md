# Visual Prolog 5.2 - Quick Usage Guide

## Getting Started

### Creating Your First Program

1. Create a new file with `.pro` extension
2. Type `program` and press `Tab`
3. Fill in the template fields
4. Save and run with your Visual Prolog compiler

## Snippet Quick Reference

### Essential Snippets

| Prefix | Description | Example Output |
|--------|-------------|----------------|
| `program` | Full program template | Complete program structure |
| `domain` | Domain declaration | `domains DomainName = type` |
| `predicate` | Predicate declaration | `predicates predicateName(args)` |
| `clause` | Clause definition | `clauses predicateName(...) :- body.` |
| `goal` | Goal section | `goal goalPredicate.` |

### Object-Oriented Programming

| Prefix | Description |
|--------|-------------|
| `class` | Create a class with predicates and clauses |
| `interface` | Define an interface |
| `implement` | Implement a class or interface |

### Control Flow

| Prefix | Description |
|--------|-------------|
| `if` | If-then-else statement |
| `determ` | Deterministic predicate |
| `nondeterm` | Non-deterministic predicate |

### Database Operations

| Prefix | Description |
|--------|-------------|
| `database` | Database section |
| `fact` | Fact declaration |
| `assert` | Assert a fact |
| `retract` | Retract a fact |
| `findall` | Find all solutions |

### I/O Operations

| Prefix | Description |
|--------|-------------|
| `write` | Write output |
| `read` | Read input |
| `openread` | Open file for reading |
| `openwrite` | Open file for writing |

### List Operations

| Prefix | Description |
|--------|-------------|
| `list` | List pattern `[Head|Tail]` |
| `member` | Check list membership |
| `append` | Append two lists |

### String Operations

| Prefix | Description |
|--------|-------------|
| `concat` | Concatenate strings |

## Common Patterns

### Pattern 1: Recursive List Processing

```prolog
predicates
    process(IntList)

clauses
    process([]).
    process([H|T]) :-
        % Process head
        write(H), nl,
        % Process tail
        process(T).
```

### Pattern 2: Accumulator Pattern

```prolog
predicates
    sumList(IntList, integer)
    sumAcc(IntList, integer, integer)

clauses
    sumList(List, Sum) :-
        sumAcc(List, 0, Sum).
    
    sumAcc([], Acc, Acc).
    sumAcc([H|T], Acc, Sum) :-
        NewAcc = Acc + H,
        sumAcc(T, NewAcc, Sum).
```

### Pattern 3: Database with Multiple Solutions

```prolog
database
    myDatabase

predicates
    nondeterm person(string, integer)
    addPerson(string, integer)
    listAll()

clauses
    addPerson(Name, Age) :-
        assertz(person(Name, Age)).
    
    listAll() :-
        person(Name, Age),
        write(Name, " is ", Age, " years old"), nl,
        fail.
    listAll().
```

### Pattern 4: File I/O

```prolog
predicates
    readFromFile(string)
    writeToFile(string, string)

clauses
    readFromFile(FileName) :-
        openread(file, FileName),
        readdevice(file),
        % Read operations
        readln(Line),
        write(Line), nl,
        closefile(file).
    
    writeToFile(FileName, Content) :-
        openwrite(file, FileName),
        writedevice(file),
        write(Content),
        closefile(file).
```

## Keyboard Shortcuts

### VS Code Standard

- `Ctrl+Space` - Trigger snippet suggestions
- `Tab` - Expand snippet
- `Cmd+/` or `Ctrl+/` - Toggle line comment
- `Shift+Option+A` or `Shift+Alt+A` - Toggle block comment
- `Cmd+Shift+O` or `Ctrl+Shift+O` - Go to symbol

### Navigation

- `Cmd+P` or `Ctrl+P` - Quick file open
- `Cmd+Shift+F` or `Ctrl+Shift+F` - Search in files
- `F12` - Go to definition
- `Shift+F12` - Find all references

## Tips & Best Practices

### 1. Use Tab Stops Effectively

When a snippet expands, press `Tab` to jump between placeholders:
```prolog
predicates
    [Tab] → predicateName
    [Tab] → arguments
    [Tab] → next section
```

### 2. Naming Conventions

- **Types/Domains**: Start with uppercase (e.g., `PersonList`, `StudentRecord`)
- **Predicates**: Start with lowercase (e.g., `calculateTotal`, `findStudent`)
- **Variables**: Use uppercase (e.g., `X`, `Result`, `Total`)
- **Atoms**: Use lowercase (e.g., `red`, `active`, `male`)

### 3. Comment Your Code

```prolog
% Single line comment

/* 
   Multi-line comment
   for detailed explanations
*/
```

### 4. Organize Your Code

Standard Visual Prolog program structure:
```prolog
% 1. Comments/Documentation
% 2. Domains
% 3. Predicates
% 4. Clauses
% 5. Goal
```

### 5. Use Determinism Modifiers

```prolog
predicates
    determ factorial(integer, integer)    % Always succeeds once
    nondeterm member(X, list)             % Can have multiple solutions
    procedure write(string)               % External procedure
```

## Debugging Tips

### 1. Add Trace Writes

```prolog
myPredicate(X) :-
    write("Debug: X = ", X), nl,  % Debug output
    % ... rest of code
```

### 2. Use fail for Testing

```prolog
test :-
    testCase1,
    testCase2,
    testCase3,
    fail.
test :- 
    write("All tests completed"), nl.
```

### 3. Check Database Contents

```prolog
showDatabase :-
    myFact(X, Y),
    write(X, " - ", Y), nl,
    fail.
showDatabase.
```

## Common Errors and Solutions

### Error: Undefined predicate

**Solution**: Make sure the predicate is declared in the `predicates` section before use.

### Error: Type mismatch

**Solution**: Check that domains match between declaration and usage.

### Error: Missing clause

**Solution**: Ensure all declared predicates have at least one clause defined.

### Error: Infinite recursion

**Solution**: Add a base case and ensure recursion terminates:
```prolog
% Bad
countdown(N) :- countdown(N-1).

% Good
countdown(0) :- !.
countdown(N) :- 
    N > 0,
    N1 = N - 1,
    countdown(N1).
```

## Additional Resources

- [Visual Prolog Official Documentation](http://wiki.visual-prolog.com/)
- [Prolog Tutorial](https://www.learnprolognow.org/)
- [Visual Prolog Examples](http://www.visual-prolog.com/vip/vipexamples/)

## Quick Command Reference

### I/O Predicates
- `write(X)` - Write to output
- `writeln(X)` - Write with newline
- `read(X)` - Read from input
- `nl` - New line

### Database Predicates
- `assert(Fact)` - Add fact to database
- `assertz(Fact)` - Add fact at end
- `asserta(Fact)` - Add fact at beginning
- `retract(Fact)` - Remove fact
- `retractall(Pattern)` - Remove all matching facts

### List Predicates
- `member(X, List)` - Check membership
- `append(L1, L2, L3)` - Concatenate lists
- `length(List, N)` - Get list length
- `reverse(List, Reversed)` - Reverse list

### String Predicates
- `concat(S1, S2, S3)` - Concatenate strings
- `str_len(S, N)` - String length
- `frontchar(S, C, Rest)` - Split first char
- `upper_lower(Upper, Lower)` - Convert case

### File Predicates
- `openread(file, Name)` - Open for reading
- `openwrite(file, Name)` - Open for writing
- `closefile(file)` - Close file
- `readdevice(file)` - Set input to file
- `writedevice(file)` - Set output to file

---

**Happy Prolog Programming!** 🎯

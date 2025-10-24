# Change Log

All notable changes to the "visual-prolog-language-support" extension will be documented in this file.

## [0.1.0] - 2025-10-24

### Added
- Complete syntax highlighting for Visual Prolog 5.2
  - Directives: `domains`, `predicates`, `clauses`, `goal`, `facts`, `database`, `constants`, `global`
  - Class/OOP keywords: `class`, `object`, `interface`, `implement`, `end class`, `end object`, `end interface`
  - Control flow: `if`, `then`, `else`, `elseif`, `not`, `fail`, `true`, `and`, `or`, `repeat`, `cut`
  - Modifiers: `determ`, `nondeterm`, `multi`, `procedure`, `single`, `static`, `abstract`, `virtual`, `override`, `final`
  - Built-in types: `char`, `byte`, `short`, `ushort`, `word`, `integer`, `unsigned`, `long`, `ulong`, `dword`, `real`, `real4`, `real8`, `string`, `symbol`, `pointer`, `binary`, `file`
  - Built-in predicates: I/O, database, string, file, system, conversion, and list operations
  - Operators: arithmetic, comparison, logical, bitwise, and list operators
  
- 25+ code snippets for common Visual Prolog patterns:
  - Program structure: `program`, `domain`, `predicate`, `clause`, `goal`
  - Object-oriented: `class`, `interface`, `implement`
  - Control flow: `if`, `determ`, `nondeterm`
  - Database operations: `database`, `fact`, `assert`, `retract`, `findall`
  - I/O operations: `write`, `read`, `openread`, `openwrite`
  - List operations: `list`, `member`, `append`
  - String operations: `concat`

- Language features:
  - Auto-closing pairs for `()`, `[]`, `{}`, `""`
  - Comment toggling support (line comments `%` and block comments `/* */`)
  - Bracket matching and smart indentation
  - Support for `.pro`, `.cl`, `.pack`, `.ph` file extensions

- Naming convention support:
  - Types/Domains starting with uppercase letters
  - Predicates/Functions starting with lowercase letters
  - Proper highlighting for variables and atoms

- Comprehensive README documentation with:
  - Feature overview
  - Snippet reference with examples
  - Usage examples (factorial, list operations, classes, database)
  - Installation instructions
  - Tips and tricks

### Changed
- Updated language configuration for Visual Prolog 5.2 syntax
- Improved token scoping for better theme compatibility

### Fixed
- Comment syntax now correctly uses `%` for line comments (Prolog standard)
- Removed inappropriate auto-closing of single quotes

## [Unreleased]

- Syntax validation and error highlighting
- IntelliSense and code completion
- Integrated compiler support
- Debugger integration
- Code refactoring tools
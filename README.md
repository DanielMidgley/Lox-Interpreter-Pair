
# Lox-Interpreter-Pair

Lox is a dynamically-typed OOP language created by Robert Nystrom, featured in his book Crafting Interpreters. This repository features two implementations of Lox which I created by following the tutorials in this book. The first implementation, jlox, is a tree-walk interpreter written in Java, whilst the second implementation, clox, (work in progress) is a bytecode virtual machine written in C.

Lox supports the following features:
- Variables (Booleans, Numbers, Strings)
- Printing
- while loops
- for loops
- conditionals (if, else)
- functions (with or without parameters)
- closures
- classes (methods, fields, constructors)
- inheritance (single inheritance only)

## Project Structure

- `jLox/src/`      - Lox implementation in Java
- `jLox/README.md` - Further details on jLox
- `Lox_Examples/`  - Some Lox code which I have used to test the interpreters
- `cLox/`          - Lox implementation in C (work in progress)

## Lox Grammar

### Syntax Grammar

```
program        → declaration* EOF ;
```

#### Declarations

```
declaration    → classDecl
               | funDecl
               | varDecl
               | statement ;

classDecl      → "class" IDENTIFIER ( "<" IDENTIFIER )?
                 "{" function* "}" ;
funDecl        → "fun" function ;
varDecl        → "var" IDENTIFIER ( "=" expression )? ";" ;
```

#### Statements

```
statement      → exprStmt
               | forStmt
               | ifStmt
               | printStmt
               | returnStmt
               | whileStmt
               | block ;

exprStmt       → expression ";" ;
forStmt        → "for" "(" ( varDecl | exprStmt | ";" )
                           expression? ";"
                           expression? ")" statement ;
ifStmt         → "if" "(" expression ")" statement
                 ( "else" statement )? ;
printStmt      → "print" expression ";" ;
returnStmt     → "return" expression? ";" ;
whileStmt      → "while" "(" expression ")" statement ;
block          → "{" declaration* "}" ;
```

#### Expressions

```
expression     → assignment ;

assignment     → ( call "." )? IDENTIFIER "=" assignment
               | logic_or ;

logic_or       → logic_and ( "or" logic_and )* ;
logic_and      → equality ( "and" equality )* ;
equality       → comparison ( ( "!=" | "==" ) comparison )* ;
comparison     → term ( ( ">" | ">=" | "<" | "<=" ) term )* ;
term           → factor ( ( "-" | "+" ) factor )* ;
factor         → unary ( ( "/" | "*" ) unary )* ;

unary          → ( "!" | "-" ) unary | call ;
call           → primary ( "(" arguments? ")" | "." IDENTIFIER )* ;
primary        → "true" | "false" | "nil" | "this"
               | NUMBER | STRING | IDENTIFIER | "(" expression ")"
               | "super" "." IDENTIFIER ;
```

#### Utility Rules

```
function       → IDENTIFIER "(" parameters? ")" block ;
parameters     → IDENTIFIER ( "," IDENTIFIER )* ;
arguments      → expression ( "," expression )* ;
```

### Lexical Grammar

```
NUMBER         → DIGIT+ ( "." DIGIT+ )? ;
STRING         → "\"" <any char except "\"">* "\"" ;
IDENTIFIER     → ALPHA ( ALPHA | DIGIT )* ;
ALPHA          → "a" ... "z" | "A" ... "Z" | "_" ;
DIGIT          → "0" ... "9" ;
```

Further details: [Crafting Interpreters - Appendix I: Lox Grammar](https://craftinginterpreters.com/appendix-i.html)

## Lox Implementation in Java


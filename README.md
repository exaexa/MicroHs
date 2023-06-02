# Micro Haskell
This directory contains an implementation of a very small subset of Haskell.
It uses combinators for the runtime execution.

## Language
The language is a subset of Haskell.  There is no static type checking (yet).

It has the following features:
* variables
* application
* lambda, just variables, not pattern matching
* integer literals
* character literals
* string (list of characters) literals
* case expressions, no nested patterns, must be exhaustive
* let expressions, no mutual recursion, no pattern matching
* tuples
* list syntax
* qualified `do` notation, e.g., `IO.do`
* data type declarations
* type signatures that are ignored.
* importing of other modules, with neither import nor export lists

## Compiler
The compiler is written in Haskell (not Micro Haskell yet).
It takes a name of a module and compiles it to a file called `out.comb`.

### Compiler modules

* `Main`, the main module.  Decodes flags, compiles, and writes result.
* `Compile`, top level compiler.  Maintains a cache of already compiled modules.
* `Exp`, simple expression type, combinator abstraction and optimization
* `Desugar`, desugar full expressions to simple expressions.
* `Parse`, parse and build and abstract syntax tree.
* `ParserComb`, simple parser combinator library.

## Runtime
The runtime system is written in C and is in `eval.c`.
It uses combinators for handling variables, and has some primitive operations
for integers and for executing IO operations.
There is a also a simple mark-scan garbage collector.

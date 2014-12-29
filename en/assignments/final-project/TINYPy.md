# TINYPy

**TINYPy was the programming language used in *Compiladores I* course, [MAB 471](http://www.dcc.ufrj.br/~fabiom/comp), by professor [Fabio Mascarenhas](http://www.dcc.ufrj.br/~fabiom) from departament of Computer Science of Federal University of Rio de Janeiro.**

TINYPy is a mix of the languages TINY (from [*Compiler Construction: Principles and Practice*]() book by Kenneth C. Louden) and Python, merging the identation-based sintax of Python with the simplicity of TINY, adding primitive types (boolean and integer) and functions.

A simple example of TINYPy:

```
{ Computes the factorial of a given number in the input. }

int fat_rec(int n):
    if n < 2:
        fat_rec := 1
    else:
        fat_rec := n * fat_rec(n - 1)

int fat_loop(int n):
    fat_loop := 1
    while n > 1:
        fat_loop := fat_loop * n
        n := n - 1

void main():
    read x
    write fat_rec(x)
    write fat_loop(x)
```

## Lexical Specification

TINYPy, rather than Python and TINY, isn't case-sensitive, either for reserved words and identifiers.

* Identation: blank spaces (`[ ]`) in the beginning of a line may generate `BEGIN` or `END` tokens.
* Blank spaces ignored: `[ \n\t\r\f]`.
* Comments: start with `{` and ends with `}`, without nesting.
* Reserved words: `read`, `write`, `if`, `else`, `elif`, `while`, `int`, `bool`, `void`, `and`, `or`, `not`, `pass`, `true`, `false`.
* Identifiers: a letter, followed by zero or more letters, digits or `_`.
* Numbers: only integer numbers.
* Operators and punctuation: `(`, `)`, `,`, `=`, `<`, `:=` (`ATRIB`), `+`, `-`, `*`, `/`, `:`.

## Sintax

The sintax is given by an EBNF. EBNF meta-symbols used as  tokens are enclosed by single quotes. The precedency of operators is encoded in the grammar.

```
PROG   -> FUNC {FUNC}
FUNC   -> TIPO id '(' [PARAMS] ')' : begin CMDS end
PARAMS -> TIPO id {, TIPO id}
CMDS   -> CMD {CMD}
TIPO   -> int | bool | void
CMD    -> if EXP : begin CMDS end {elif EXP : begin CMDS end} [else : begin CMDS end]
| while EXP : begin CMDS end
| id := EXP
| id '(' [EXPS] ')'
| read id
| write EXP
| pass
EXP    -> EXP or LEXP
| LEXP
LEXP   -> LEXP and REXP
| REXP
REXP   -> REXP < AEXP
| REXP = AEXP
| AEXP
AEXP   -> AEXP + MEXP
| AEXP - MEXP
| MEXP
MEXP   -> MEXP * SEXP
| MEXP / SEXP
| SEXP
SEXP   -> not SEXP
| - SEXP
| true
| false
| num
| id
| id '(' [EXPS] ')'
| '(' EXP ')'
EXPS   -> EXP {, EXP}
```

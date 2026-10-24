<div align="center">

# λ Lambda Calculus Interpreter

**An extended, typed lambda calculus interpreter written in OCaml**

![OCaml](https://img.shields.io/badge/OCaml-EC6813?style=for-the-badge&logo=ocaml&logoColor=white)
![Course](https://img.shields.io/badge/DLP-2026%2F27-blue?style=for-the-badge)
![Status](https://img.shields.io/badge/status-in%20progress-yellow?style=for-the-badge)

*Programming Languages Design (DLP) · Computer Engineering (Q7) · Academic year 2026/27*

</div>

---

## About

This project extends the **lambda-3** interpreter (a typed lambda calculus inspired by the implementations cited in Benjamin C. Pierce's *Types and Programming Languages*) with new language features and a better user experience.

The interpreter reads expressions from an interactive prompt, type-checks them, evaluates them and prints the result together with its type.

---

## Features and progress

| #   | Feature                                             | Delivery     | Status |
|-----|-----------------------------------------------------|--------------|:------:|
| 1.1 | Multi-line expressions (terminated by `;;`)         | Intermediate | ⬜ |
| 1.2 | Full pretty-printer (minimal parentheses, indentation) | Final     | ⬜ |
| 2.1 | Internal fixed-point combinator (`letrec`)          | Intermediate | ⬜ |
| 2.2 | Global context for term and type definitions        | Intermediate | ⬜ |
| 2.3 | `String` type and concatenation                     | Intermediate | ⬜ |
| 2.4 | Tuples and positional projection                    | Intermediate | ⬜ |
| 2.5 | Records and label projection                        | Final        | ⬜ |
| 2.6 | Variants and `case` expressions                     | Final        | ⬜ |
| 2.7 | Lists (`head`, `tail`, `isempty`)                   | Final        | ⬜ |
| 2.8 | Subtyping for records and functions                 | Final        | ⬜ |
| 3.1 | Final report (user manual + technical manual, PDF)  | Final        | ⬜ |

> Legend: ⬜ pending · 🟨 in progress · ✅ done

### Deadlines

- 📅 **Intermediate delivery:** Friday, 13 November 2026 (items 1.1, 2.1, 2.2, 2.3, 2.4)
- 📅 **Final delivery:** Friday, 11 December 2026 (remaining items)
- 🎤 **Possible defense:** 15 December 2026

---

## Getting started

### Requirements

- [OCaml](https://ocaml.org/) (4.14 or later recommended)
- `make` or `dune` (depending on the build system used in the project)

### Build

```bash
git clone git@github.com:paablomiguez/INTERPRETE_LAMBDA_CALCULO_DLP_GEI_202627.git
cd INTERPRETE_LAMBDA_CALCULO_DLP_GEI_202627
make            # or: dune build
```

### Run

```bash
./top           # or: dune exec ./top.exe
```

> ⚠️ Adjust the build and run commands above to match the actual build system of the project.

---

## Usage examples

### Recursive functions with `letrec` (2.1)

```
>> letrec sum : Nat -> Nat -> Nat =
     lambda n : Nat. lambda m : Nat.
       if iszero n then m else succ (sum (pred n) m) in
   sum 21 34;;
- : Nat = 55
```

### Global definitions (2.2)

```
>> x = true;;
>> id = lambda x : Bool. x;;
>> id x;;
- : Bool = true

>> N = Nat;;
>> lambda x : N. x;;
```

### Variants (2.6)

```
>> Int = <pos:Nat, zero:Bool, neg:Nat>;;
>> p3 = <pos=3> as Int;;
>> abs = L i : Int.
     case i of
       <pos=p>  => (<pos=p> as Int)
     | <zero=z> => (<zero=true> as Int)
     | <neg=n>  => (<pos=n> as Int);;
>> abs p3;;
- : <pos : Nat, zero : Bool, neg : Nat> = <pos = 3>
```

More examples (`prod`, `fib`, `fact`, `add` on integers, `length`, `append`, `map`, subtyping) are collected in [`examples.txt`](examples.txt).

---

## Project structure

```
.
├── README.md        # This file
├── examples.txt     # Example expressions for every feature
├── lexer.mll        # Lexical analyzer
├── parser.mly       # Syntactic analyzer
├── syntax.ml        # Abstract syntax tree, pretty-printer
├── core.ml          # Typing and evaluation
├── main.ml          # Interactive loop
├── Makefile
└── report/          # Final report (PDF)
```

> ⚠️ Update this tree to match the real file layout of the project.

---

## Design notes

- **Global context:** implemented as a *functional* context (redefining a name shadows the previous binding without mutating the old one). The chosen implementation and the reasons for it are explained in the final report.
- **Language policy:** all source code, comments, examples and documentation are written in **English**.
- **Lists:** implemented from scratch, without relying on OCaml's built-in lists for the object language.

---

## Documentation

The final report (PDF) includes:

1. **User manual:** formal description and execution examples of every new feature.
2. **Technical manual:** modules modified from the original implementations and the kind of changes made to each.

---

## Author

**Pablo Míguez** · [@paablomiguez](https://github.com/paablomiguez)

---

<div align="center">

*Made with λ and a lot of parentheses.*

</div>

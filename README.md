<div align="center">

# λ Intérprete de Cálculo Lambda

**Un intérprete de cálculo lambda tipado e ampliado, escrito en OCaml**

![OCaml](https://img.shields.io/badge/OCaml-EC6813?style=for-the-badge&logo=ocaml&logoColor=white)
![Curso](https://img.shields.io/badge/DLP-2026%2F27-blue?style=for-the-badge)
![Estado](https://img.shields.io/badge/estado-en%20curso-yellow?style=for-the-badge)

*Deseño de Linguaxes de Programación (DLP) · Grao en Enxeñaría Informática (Q7)*

</div>

---

## Sobre o proxecto

Este proxecto amplía o intérprete **lambda-3** (un cálculo lambda tipado inspirado nas implementacións que Benjamin C. Pierce cita en *Types and Programming Languages*) con novas funcionalidades da linguaxe e melloras na experiencia de uso.

O intérprete le expresións desde un prompt interactivo, comproba os seus tipos, avalíaas e amosa o resultado xunto co seu tipo.

---

## Funcionalidades a alcanzar

### Melloras na introdución e escritura de expresións

- [ ] **1.1 Expresións multiliña:** poder escribir unha expresión en varias liñas, rematándoa con `;;`.
- [ ] **1.2 Pretty-printer completo:** minimizar os parénteses ao escribir unha expresión e indentar os seus elementos (mediante o módulo `Format` de OCaml).

### Ampliacións da linguaxe

- [ ] **2.1 Combinador de punto fixo interno (`letrec`):** declarar funcións recursivas directamente. Inclúe os exemplos `prod`, `fib` e `fact`.
- [ ] **2.2 Contexto de definicións globais:** asociar nomes con termos (`x = true`) e alias de tipos (`N = Nat`) para usalos en expresións posteriores. O contexto é *funcional*.
- [ ] **2.3 Tipo `String`:** cadeas de caracteres e operación de concatenación.
- [ ] **2.4 Tuplas:** produtos cartesianos de calquera número de elementos e tipos, con proxección por posición.
- [ ] **2.5 Rexistros:** campos etiquetados de calquera tipo, con proxección por etiqueta.
- [ ] **2.6 Variantes:** valores etiquetados con `case`. Inclúe o tipo `Int` e a función recursiva `add : Int -> Int -> Int`.
- [ ] **2.7 Listas:** cabeza, cola e consulta de lista baleira. Inclúe `length`, `append` e `map`, sen usar as listas de OCaml.
- [ ] **2.8 Subtipado:** para rexistros e funcións, integrado na función de tipado.

> Lenda: `[ ]` pendente · `[x]` feito

---

## Posta en marcha

### Requisitos

- [OCaml](https://ocaml.org/) (recoméndase a versión 4.14 ou posterior)
- `make` ou `dune`, segundo o sistema de compilación do proxecto

### Compilar

```bash
git clone git@github.com:paablomiguez/INTERPRETE_LAMBDA_CALCULO_DLP_GEI_202627.git
cd INTERPRETE_LAMBDA_CALCULO_DLP_GEI_202627
make            # ou: dune build
```

### Executar

```bash
./top           # ou: dune exec ./top.exe
```

> ⚠️ Axusta os comandos de compilación e execución ao sistema real do proxecto.

---

## Exemplos de uso

### Funcións recursivas con `letrec` (2.1)

```
>> letrec sum : Nat -> Nat -> Nat =
     lambda n : Nat. lambda m : Nat.
       if iszero n then m else succ (sum (pred n) m) in
   sum 21 34;;
- : Nat = 55
```

### Definicións globais (2.2)

```
>> x = true;;
>> id = lambda x : Bool. x;;
>> id x;;
- : Bool = true

>> N = Nat;;
>> lambda x : N. x;;
```

### Variantes (2.6)

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

Máis exemplos (`prod`, `fib`, `fact`, `add` sobre enteiros, `length`, `append`, `map` e subtipado) recóllense en [`examples.txt`](examples.txt).

---

<div align="center">

*Feito con λ e moitos parénteses.*

</div>

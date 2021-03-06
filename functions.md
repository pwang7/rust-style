# Function Signature Guide

## Introduction

Functions signatures are divided into several parts: the function name, the generic type list, the parameter list, the return type, and the where clause. The following paragraphs cover the formatting guidelines for each of these individual sections.

## Signatures Parts

### Naming
The Rust compiler is adamant about using snake case (i.e. `my_function_name`) function names, so this is the recommendend naming convention. Not much more to say about those.

### Generic Type List
The generic type list immediately follows the function name, and is surrounded by the `<` and `>` characters. There should be no space preceding the opening `<` and no space following the closing `>`. The generic type list contains both lifetimes and generic types. These are separated by commas. After each comma, there should be exactly one space. Generic type names should be preceded by a capital `T`, and then a descriptive name. Avoid single-letter generic type names, as are often popular in this case. Generic types are permitted to specify constraints in this list by following the generic's name with a colon, and then the constraints, separated by a `+`. There should be exactly one space on each side of the colon, and exactly one space around each of the commas.

### Parameter List
Immediately following the generic type list is the parameter list, which is surrounded by a pair of parantheses. There should be no space preceding or following the opening parenthesis. Within the parentheses, each parameter is specified with a name, followed by a colon, followed by a type. There should be exactly one space preceding and following this colon. Between each parameter is a comma. There should be no space preceding this comma, and exactly one space following this comma.

### Return Type
Following the parameter list is the return type. These are pretty cut and dry - simply include exactly one space before and after the return arrow `->`, and then write the return type.

### `where` Clauses
Some functions have where clauses. The `where` keyword should be preceded and followed by exactly one space. Within the where clause, the the same syntax is used as within the generic type list. Since style guides are boring enough as it is, I won't bother reiterating those here.

### Bracing
The opening curly brace for the function body should go on the same line as the function, not the next line. There should be exactly one space preceding it. The closing curly brace should be on its own line, aligned with the first character of the text preceding the opening curly brace.

### Examples
**TLDR: Here are what your function signatures should look like:**

Just a return type:
``` rust
fn my_function_name() -> ReturnType {
    // ...
}
```

With generic type list:
``` rust
fn my_fun<'a, 'b', TGeneric1 : Constaint1 + Constraint2>() {
    // ...
}
```

With parameters:
``` rust
fn my_fun(param1 : Type1, param2 : Type2) {
    // ...
}
```

With where clause:
``` rust
fn my_fun<TGeneric1, TGeneric2>() where TGeneric1 : Constaint1, TGeneric2 : Constraint2 {
    // ...
}
```

## Multi-line Signatures

### Basic Rules

Prefer to declare functions on one line if possible, but sometimes one line just isn't enough for a really long and complicated siggy, kind of like how one line isn't long enough for this really long run-on sentence.

Basically, for a multi-line signature, each part listed in the [Signatures Parts](functions.md#signatures-parts) should be on its own line. The following list specifies exactly which components go on which line:

1. The `fn` keyword and function name
2. The generic type list
3. The parameter list
4. The return type
5. The where clause

Each of these sections should be aligned with the starting `fn` keyword. Example:

``` rust
fn my_fun
<TGeneric1, TGeneric2>
(param1 : Type1, param2, Type2)
-> ReturnType
where TGeneric1 : Constaint1, TGeneric2 : Constaint2 {
    ...
}
```

### Splitting Lists

Often, the list sections (generic type list, parameter list, and where clause) will be very long on their own. So, there are some additional rules for aplitting them up.

* Include the first item in the list on the same line as the opening token for the list, namely the `<`, `(`, or `where` token.
* Put each additional item on its own line, preceded by two levels of indentation. Two levels are used to prevent the function signature from running into the function body.

**Do** this
``` rust
fn add_four_numbers
(number1 : u32,
        number2 : u32,
        number2 : u32,
        number2 : u32) {
    let result = number1 + number2 + number3 + number4;
}
```

**Don't** do this - hard to tell where the signature ends and function body begins
``` rust
fn add_four_numbers
(number1 : u32,
    number2 : u32,
    number2 : u32,
    number2 : u32) {
    let result = number1 + number2 + number3 + number4;
}
```
* Put the closing delimiter (`>` or `)`) on the same line as the last item in the list.

### Multi-line examples

Short parameter list:
```
fn my_function
(param1 : Type1, param2 : Type2) {
    // codez
}
```

Long parameter list:
```
fn my_function
(param1 : Type1,
        param2 : Type2,
        param3 : Type3,
        param4 : Type4) {
    // codez
}
```

Short parameter list, with return type:
```
fn my_function
(param1 : Type1, param2 : Type2)
-> ReturnType {
    // codez
}
```

Long parameter list, with return type:
```
fn my_function
(param1 : Type1,
        param2 : Type2,
        param3 : Type3,
        param4 : Type4)
-> ReturnType {
    // codez
}
```

Short template list, short parameter list:
```
fn my_function
<TGeneric1, TGeneric2, TGeneric3> {
(param1 : Type1, param2 : Type2) {
    // codez
}
```

Everything on the menu (hopefully there aren't too many any of these nasty beasties):
```
fn my_function
<'a,
        'b,
        'c,
        TGeneric1,
        TGeneric2,
        TGeneric3,
        TGeneric4>
(param1 : Type1,
        param2 : Type2,
        param3 : Type3,
        param4 : Type4)
-> ReturnType
where TGeneric1 : Constraint1,
        TGeneric2 : Constraint2,
        TGeneric3 : Constraint3,
        TGeneric4 : Constraint4 {
    // codez
}
```

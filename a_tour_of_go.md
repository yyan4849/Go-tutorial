# Basics

## Packages, variables, and functions

### Template

``` Go
filename-> multiple-results.go

import "fmt"

func swap(x, y  string)(string, string){
    return y, x
}

func main(){
    a, b := swap("Hello", "world")
    fmt.Println(a,b)
}
```

### Package

- Go program is made up of packages
- Programs start running in package `main`
- By convention, package name = the last element of the import path

### Exported names

- Exported if begins with a capital letter
- When import a package, only exported name could be refer, unexported cannot

### Functions

- Take >= 0 arguments
- type comes after the variable name
- `x int, y int` = `x, y int`

### Multiple results

- A functino can return any number of results

### Named return values

- Named return values -> variables defined at the top of the function
- Return without name without arguments -> naked return

### Variables

- `var` statement declares a list of variables

### Short variable declarations

- Inside a function, `:=` -> `var` with implicit type
- Outside a function, every statement begins with a keywords so `:=` is not available

### Basic types

``` Go
bool

string

int int8 int16 int32 int64

unit unit8 unit16 unit32 unit64 unitptr

byte // alias for unit8
    

rune // alias for int32
     // represents a Unicode code point

float32 float64

complex64 complex128

```

- Varibale declaration may be factored into blocks
- The `int`, `unit`, `unitptr` are usually 32 bits on 32-bit system, and 64bits wide on 64-bit system
- when use an integer vatiable you should declare unless you have the reason for not

``` Go
var(
    toBe    bool        =  false
    MaxInt  unit64      =  1<<64 - 1
    z       complex128  =  cmplx.Sqrt(-5 + 12i)
    )
```

### Zero values

- Variables declared without an explict initial value are given then zero values
-`0` for numeric types
-`false` for the boolen type
-`""`(the empty string) for strings

### Type conversions

- `T(v)` converts the value `v` into type `T`

### Type interface

- When declaring a variable without specitying the type, the variable's type is inferred from the value on the right hand side
- When right handside is typed, the new variable is ofo that same type
- When contains untyped numeric constant, it's depending on the precision of the constant

### Constants

- Constants are declared like variables, but with `constant` keyword
- Can be character, string, boolean, or numeric values
- Cannot be declared using `:=`
- Capital the first letter

### Numeric Constants

- ~ are high-precision *values*

## Flow control statements: for, if, else, switch anf defer

Note from the [A Tour of Go](https://go.dev/tour/welcome/1)

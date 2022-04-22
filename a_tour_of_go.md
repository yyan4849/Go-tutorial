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

### For

- Three components separated by semicolons:
-the init statement: excuted before the first iteration; only visible in the scope of `for`
-the condition expression: evaluated before every iteration
-the post statement: executed at the end of every iteration

``` Go
    sum := 0
    for i := 0; i <10; i++ {
        sum += i
    }
```

- The inital and post statements are optional

```Go
    sum := 1
    for ; sum<1000; {
        sum += sum
    }
```

### For is Go's While

```Go
    for sum < 1000{
        sum += sum
    }
```

### If

```Go
    if x < 0 {
        return sqrt(-x) + "i"
    }

```

### If with short statement

```Go
if v:= math.Pow(x,n); v <lim{
    return v
}
```

### If else

- Variable declared in if statement could also be used in else statement but not outside

### Switch

- Values invovled need not to be ints
- Switch cases cannot be constant
- Auto add break

```Go
switch os := runtime.GOOS; os {
 case "darwin":
  fmt.Println("OS X.")
 case "linux":
  fmt.Println("Linux.")
 default:
  // freebsd, openbsd,
  // plan9, windows...
  fmt.Printf("%s.\n", os)
 }
```

- Switch evaluates case from top to bottom
- Switch with no condition -> long if-then-else chains

### Defer

- A deferred statement defer execution of a funtion until the surrounding function returns
- Arguments are evaluated immediately, but the function executed after all surrounding functions return

### Stacking defers

- Defered calls are pushed onto a stack, when funtion returns, its deferred calls are executed in LIFO

## More types: structs, slices, and maps

### Pointers

- A pointers holds the memory address of a value
- `*T` is a pointer to a `T`value. Its zero value is `nil`
- `&` generates a pointer to its operand
- `*` denotes the pointer's underlying value, knowing as "dereferencing" or "indirecting"

```Go
func main() {
 i, j := 42, 2701

 p := &i         // point to i
 fmt.Println(*p) // read i through the pointer
 *p = 21         // set i through the pointer
 fmt.Println(i)  // see the new value of i

 p = &j         // point to j
 *p = *p / 37   // divide j through the pointer
 fmt.Println(j) // see the new value of j
}
```

### Structs

`struct` a collection of fields

### Stucts Fields

Struct fields are accessed using a dot

```Go
type Vertex struct {
 X int
 Y int
}

func main() {
 v := Vertex{1, 2}
 v.X = 4
 fmt.Println(v.X)
}
```

### Pointers to structes

sturct fields can be accessed by a struct pointer

```Go
type Vertex struct {
 X int
 Y int
}

func main() {
 v := Vertex{1, 2}
 p := &v
 p.X = 1e9
 fmt.Println(v)
}
```

### Struct Literals

```Go
type Vertex struct {
 X, Y int
}

var (
 v1 = Vertex{1, 2}  // has type Vertex
 v2 = Vertex{X: 1}  // Y:0 is implicit
 v3 = Vertex{}      // X:0 and Y:0
 p  = &Vertex{1, 2} // has type *Vertex
)
```

### Arrays

- `var a[10]int` declares a variable `a` as an array of ten ints

- Array's length is part of its type, so array cannot be resized

### Slice

Note from the [A Tour of Go](https://go.dev/tour/welcome/1)

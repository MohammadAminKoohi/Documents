
2025-11-22 18:41

Tags:

# Variables in Go

in Golang we can define variables using `var`

```go
var example int = 5
```

you can also define multiple variables using `var`

```go
var firstVariable, secondVariable int = 5, 6

var (
    firstVariable int = 5
    secondVariable int = 6
)
```

if you give value to the variable at instantiation time, you don't need to define the type

```go
var x = 12
```

also there is a special operator `:=` that lets you define variables without type and `var` keyword

```go
x := 12
```

	you can't use := outside functions

in golang we can define constants using `const`

```go
const x = 5
x = 6 // error
```

# Datatypes in Go

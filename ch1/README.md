# Go Fundamentals

- Run command: `go run src/hello.go`
- Build command: `go build src/hello.go`
- Build command (optimized): `go build -ldflags "-w -s" src/hello.go` 
- Run binary: `./hello`

## Data Types

### Primitive Types
- `bool`
- `string`
- `byte`
- `rune`
- `uintptr`
- `float32` and `float64`
- `complex64` and `complex128`
- `int` variations (`int`, `int8`, `int16`, `int32`, `int64`)
- `uint` variations (`uint`, `uint8`, `uint16`, `uint32`, `uint64`)

###  Instantiation
```go
var x = "Hello World"
z := int(42)
```

### Slices and Maps
```go
var s = make([]string, 0)
var m = make(map[string]string)
s = append(s, "some string")
m["some key"] = "some value"
```

### Pointers, Structs, and Interfaces

#### Pointers
```go
var count = int(42)
ptr := &count
fmt.Println(*ptr)
*ptr = 100
fmt.Println(count)
```

#### Structs
```go
type Person struct {
    Name string
    Age int
}

func (p *Person) SayHello() {
    fmt.Println("Hello, ", p.Name)
}

func main() {
    var guy = new(Person)
    guy.Name = "Dave"
    guy.SayHello()
}
```

#### Interfaces
```go
type Friend interface {
    SayHello()
}

func Greet(f Friend) {
    f.SayHello()
}

func main() {
    var guy = new(Person)
    guy.Name = "Dave"
    Greet(guy)
}
```

#### Combined
```go
type Dog struct {}

func (d *Dog) SayHello() {
    fmt.Println("Woof woof")
}

func main() {
    var guy = new(Person)
    guy.Name = "Dave"
    Greet(guy)
    var dog = new(Dog)
    Greet(dog)
}
```

## Logic Control

### `if/else`
```go
if x == 1 {
    fmt.Println("X is 1")
} else if x == 2 {
    fmt.Println("X is 2")
} else {
    fmt.Println("X is neither 1 nor 2")
}
```

### `switch`
```go
switch x {
    case "foo":
        fmt.Println("Foo")
    case "bar":
        fmt.Println("Bar")
    default:
        fmt.Println("Foobar")
}
```

### Loops

#### `for`
```go
for i := 0; i < 10; i++ {
    fmt.Println(i)
}
```

#### `range`
```go
nums := []int{2,4,6,8}
for idx, val := range nums {
    fmt.Println(idx, val)
}
```

##  Concurrency

### Goroutines
```go
func f() {
    fmt.Println("f function")
}

func main() {
    go f()
    time.Sleep(1 * time.Second)
    fmt.Println("main function")
}
```

### Channels
```go
func strlen(s string, c chan int) {
    c <- len(s)
}

func main() {
    c := make(chan int)
    go strlen("Salutations", c)
    go strlen("World", c)
    x, y := <-c, <-c
    fmt.Println(x, y, x + y)
}
```


## Error Handling

```go
type MyError string

func (e MyError) Error() string {
    return string(e)
}

func foo() error {
    return errors.New("Some error occurred")
}

func main() {
    if err := foo(); err != nil {
        // handle the error
    }
}
```

## Structured Data
```go
 type Foo struct {
    Bar string
    Baz string
 }

 func main() {
    f := Foo{" Joe Junior", "Hello Shabado"}
    b, _ := json.Marshal(f)
    fmt.Println(string(b))
    json.UnMarshal(b, &f)
 }
```
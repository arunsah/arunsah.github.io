# Go Notes
#go #may2020

---

## Table of Content

1. [Introduction](https://arunsah.github.io/gonotes#1-introduction)

1. [Data types](https://arunsah.github.io/gonotes#2-data-types)

1. [Variables](https://arunsah.github.io/gonotes#3-variables)

1. [Functions](https://arunsah.github.io/gonotes#4-functions)

1. [Control Statements](https://arunsah.github.io/gonotes#5-control-statements)

1. [Arrays, Slices, and Maps](https://arunsah.github.io/gonotes#6-arrays-slices-and-maps)

1. [Structs and Pointers](https://arunsah.github.io/gonotes#7-structs-and-pointers)

1. [Methods and Interfaces](https://arunsah.github.io/gonotes#8-methods-and-interfaces)

1. [Strings](https://arunsah.github.io/gonotes#9-strings)

1. [Handling Errors](https://arunsah.github.io/gonotes#10-handling-errors)

1. [Goroutines](https://arunsah.github.io/gonotes#11-goroutines)

1. [Introducing Channels](https://arunsah.github.io/gonotes#12-introducing-channels)

1. [Packages for Code Reuse](https://arunsah.github.io/gonotes#13-packages-for-code-reuse)

1. [Naming Conventions in Go](https://arunsah.github.io/gonotes#14-naming-conventions-in-go)

1. [Testing and Performance](https://arunsah.github.io/gonotes#15-testing-and-performance)

1. [Debugging](https://arunsah.github.io/gonotes#16-debugging)

1. [Command-Line Programs](https://arunsah.github.io/gonotes#17-command-line-programs)

1. [HTTP Servers](https://arunsah.github.io/gonotes#18-http-servers)

1. [HTTP Clients with Go](https://arunsah.github.io/gonotes#19-http-clients-with-go)

1. [JSON](https://arunsah.github.io/gonotes#20-json)

1. [Files](https://arunsah.github.io/gonotes#21-files)

1. [Introducing Regular Expressions](https://arunsah.github.io/gonotes#22-introducing-regular-expressions)

1. [Programming Time in Go](https://arunsah.github.io/gonotes#23-programming-time-in-go)

1. [Deploying Go Code](https://arunsah.github.io/gonotes#24-deploying-go-code)

1. [A RESTful JSON API](https://arunsah.github.io/gonotes#25-a-restful-json-api)

1. [A TCP Chat Server](https://arunsah.github.io/gonotes#26-a-tcp-chat-server)

1. [References](https://arunsah.github.io/gonotes#27-references)




## 1. Introduction

### Introduction

- Go is suitable for (not limited to):
	- Network Programming
	- System Programming
	- Concurrent Programming
	- Distributed Programming

- Rob Pike’s introduction to the Go programming language, 2009. It outlines many of the design goals of Golang (https://www.youtube.com/watch?v=rKnDgT73v8s).
- High level goal of go, “development speed of dynamic language like Python with performance and safety of a compiled language like C/C++”.
- Go is available for FreeBSD, Linux, Windows and MacOS.
- Go was created out of frustration of compilation time taken by C++ (among many other reasons).
- Go gopher is mascot for go.
- Go is statically/strongly typed language (data integrity).

##### Setting up Environment 

	- After installation, add go home directory to environment variable. `export GOPATH=$HOME/go`
	- Setup GitHub, Gitlab or Bitbucket account.
		- `mkdir -p $GOPATH/src/github.com/<git_username>`  //macOs and Linux
		- `mkdir %GOPATH%\src\github.com\<git_username>`
		- `go run` don’t create executables but compile and runs the code (for dev).
		- `go build` will create an executable (for distribution).
		- `go clean` will clean the executable. 
- Go binary are bulky as they are standalone.   

[↑](https://arunsah.github.io/gonotes#table-of-content)



## 2. Data types

#### Type of a Variables.

- Using `reflect` package. Useful for debugging.
- `fmt.Println( reflect.TypeOf(name) ) //string` 


#### Type Conversion

- For string to/from other type use `strong` package.

```go
var status string = "true"

is_enabled, err := strconv.ParseBool(status)

var status2 string = strconv.FormatBool(is_enabled)
```

- Gary Bernhardt’s talk titled WAT. It is a humorous look at dynamically typed languages, including JavaScript (https://www.destroyallsoftware.com/talks/wat).

[↑](https://arunsah.github.io/gonotes#table-of-content)



## 3. Variables

- All data types have default values known as zero valued.
	- Boolean: false, Integer: 0, Float: 0.0, String: “”.
	- Pointer: nil, Function: nil, Interface: nil.
	- Slice: nil, Channel: nil, Maps: nil

- `nil` cannot be assigned during initialisation.
- It is not allowed to use short variable declaration eg. `name:="Mario"`outside a function.
- `&` is similar to address of operator.

```go
package main

import "fmt"

func main() {
    fmt.Println("Go pointers!")
    a := 10
    b := 20
    fmt.Println(a, b)
    swap(&a, &b)
    fmt.Println(a, b)
}

func swap(x *int, y *int) {
    t := *x
    *x = *y
    *y = t
}
```

```shell
$ go run hello.go 
Go pointers!
10 20
20 10
```

- Constant
	- `const greeting string = "Hello world"`
- Variables/constants are block scope. There are method live;, file level, package level and universal block.

[↑](https://arunsah.github.io/gonotes#table-of-content)



## 4. Functions

- Function name are optional but required to be called at other places.
- Can returns multiple values.
- Variadic functions can accepts multiple arguments.

```go
func sum(numbers ...int) int {
    total := 0
    for _, value := range numbers {
        total += value
    }
    return total
}

fmt.Println(sum(1, 2, 3, 4, 5)) // 15

```

- Named return values allow a function to assign values to named variables before returning.  Use for short methods only (for readability).

```go
func namedReturnGreeting() (greet, name string) {
    greet = "Hello"
    name = "World"
    return // naked return statement
}

fmt.Println(namedReturnGreeting()) //Hello World
```

- Recursive function

```go
func fact(num int) int {
    if num <= 1 {
        return 1
    }
    return num * fact(num-1) // recursion
}

fmt.Println(fact(5)) // 120

```

- Passing function as argument. Go have “first-class functions” since it can be passed as arguments to other functions.

```go
func apply(num int, fn func(int) int) int {
    return fn(num)
}

func square(num int) int {
    return num * num
}

func cube(num int) int {
    return num * num * num
}


// function as parameter
greetFunc := func() string {
    return "hello world"
}

var greetFunc2 func() string = func() string {
    return "hello world"
}

fmt.Println(greetFunc())      // hello world
fmt.Println(greetFunc2())     // hello world

fmt.Println(apply(3, square)) // 9
fmt.Println(apply(3, cube))   // 27

```

[↑](https://arunsah.github.io/gonotes#table-of-content)



## 5. Control Statements

- if statements in Go can include both a condition and an initialisation statement. 

```go
if value, exists := store["apple"]; exists {
    fmt.Println("Found", "apple", value) // Found apple 150
}

```

- Loops

```go
i := 1
for i < 10 {
    i++
}

for i := 1; i < 10; i++ {
}

nums := []int{1, 2, 3, 4, 5}
for index, value := range nums {
    fmt.Println(index, value)
}

```

- Defer allows a function to be executed after a surrounding function returns. It can be trigger by return (implicit/explicit) statement. Used for cleanup task or calling coroutines or network calls. 

- Multiple defer statements are executed in reverse order. Closest to return (implicit/explicit) executes first.

```go
func testDefer() {
    defer fmt.Println(31)
    defer fmt.Println(32)
    fmt.Println(2)
}

fmt.Println("Test Defer")
fmt.Println(1)
testDefer()
fmt.Println(4)

// Output:
// Test Defer
// 1
// 2
// 32
// 31
// 4

```

[↑](https://arunsah.github.io/gonotes#table-of-content)



## 6. Arrays, Slices, and Maps

- Arrays

```go
// arrays
nums := [5]int{1, 2, 3, 4, 5}
fmt.Println(nums) // [1 2 3 4 5]
nums[0] = 10
fmt.Println(nums) // [10 2 3 4 5]
```

- Slice is a contiguous segment of an underlying array and provides access to a numbered sequence of  elements from the array. Provide operations such as add/remove/copy elements.

```go
// slice examples
var veg = make([]string, 2) // empty slice of size 2 (not hard limit)
fmt.Println(veg)            // [ ]
veg[0] = "potatos"
veg[1] = "chilli"
// appending elements will increase size of internal array
veg = append(veg, "carrot", "tomatos")
fmt.Println(veg) // [potatos chilli carrot tomatos]
// deleting element at index 2 "carrot"
veg = append(veg[:2], veg[2+1:]...)
fmt.Println(veg, len(veg)) // [potatos chilli tomatos] 3
// copy elements
var veg2 = make([]string, 2)
copy(veg2, veg)
fmt.Println(veg2, len(veg2)) // [potatos chilli]
var veg3 = make([]string, 12)
copy(veg3, veg)
fmt.Println(veg3, len(veg3)) // [potatos chilli tomatos         ] 12
var veg4 = make([]string, 2)
copy(veg4, veg[1:])
fmt.Println(veg4, len(veg4)) // [chilli tomatos] 2

```

- In map, attempts to fetch a non existing key will return zero value.

```go
// maps
attended := map[string]bool{
    "tom":   true,
    "jerry": true,
    "pluto": false,
}
fmt.Println(attended)

var store = make(map[string]float32)
store["apple"] = 150.0
store["mango"] = 200.0
store["grapes"] = 160.0
fmt.Println(store)           // map[apple:150 grapes:160 mango:200]
fmt.Println(store["apple"])  // 150
fmt.Println(store["banana"]) // 0, zerod value by default if key doesnot exists
// key exists
if value, exists := store["banana"]; exists {
    fmt.Println("Found", "banana", value)
} else {
    fmt.Println("Not Found", "banana")
}
if value, exists := store["apple"]; exists {
    fmt.Println("Found", "apple", value) // Found apple 150
} else {
    fmt.Println("Not Found", "apple")
}

fmt.Println(store) // map[apple:150 grapes:160 mango:200]
delete(store, "banana")
delete(store, "apple")
store["coconut"] = 50
fmt.Println(store) // map[grapes:160 mango:200]
// iterate map
for key, value := range store {
    fmt.Println(key, value)
}

```

```shell
$ go run hello.go 
map[jerry:true pluto:false tom:true]
map[apple:150 grapes:160 mango:200]
150
0
Not Found banana
Found apple 150
map[apple:150 grapes:160 mango:200]
map[coconut:50 grapes:160 mango:200]
grapes 160
coconut 50
mango 200

```

[↑](https://arunsah.github.io/gonotes#table-of-content)



## 7. Structs and Pointers

- Struct of different types cannot be compared (compile time error). Better to check type of struct before comparison using `reflect`  package.
- When struct is initialised, memory is allocated for the data elements with default values in struct. A pointer to the memory is returned and assigned to variable name.

```go

type Fruit struct {
    Name  string
    Price float32
}

// shortcut, without new operator
apple := Fruit{
    Name:  "apple",
    Price: 150.0,
}
fmt.Println(apple)                   // {apple 150}
fmt.Println(apple.Name, apple.Price) // apple 150

var banana Fruit = Fruit{
    Name:  "banana",
    Price: 40.0,
}
// "%+v" will show the struct
fmt.Printf("%+v  %v\n", banana, banana) // {Name:banana Price:40}  {banana 40}

// memory allocation using new operator
mango := new(Fruit)
fmt.Printf("%+v\n", mango) // &{Name: Price:0}, default zerod values are initialized
mango.Name = "mango"
mango.Price = 200.0
fmt.Printf("%+v\n", mango) // &{Name:mango Price:200}

var bananaPtr = &banana
fmt.Println(&banana, &bananaPtr, bananaPtr, *bananaPtr) // &{banana 40} 0xc00000e030 &{banana 40} {banana 40}

// field name can be removed (optional) but not recommended
grape := Fruit{"Grape", 160.0} // order is important
fmt.Printf("%+v\n", grape)     // {Name:Grape Price:160}

// nested struct
type User struct {
    Name           string
    FavouriteFruit Fruit
}

defaultUser := User{}
fmt.Printf("defaultUser = %+v\n", defaultUser) // defaultUser = {Name: FavouriteFruit:{Name: Price:0}}
tom := User{Name: "tom", FavouriteFruit: grape}
jerry := User{Name: "jerry", FavouriteFruit: Fruit{"strawberry", 300}}
fmt.Printf("%+v\n", tom)                       // {Name:tom FavouriteFruit:{Name:Grape Price:160}}
fmt.Printf("%+v\n", jerry)                     // {Name:jerry FavouriteFruit:{Name:strawberry Price:300}}
fmt.Printf("%+v\n", jerry.FavouriteFruit.Name) // strawberry

// struct comparision
// Not Equals:: {Name:tom FavouriteFruit:{Name:Grape Price:160}} and {Name:jerry FavouriteFruit:{Name:strawberry Price:300}}
fmt.Println(reflect.TypeOf(tom), reflect.TypeOf(jerry)) // main.User main.User
if tom == jerry {
    fmt.Printf("Equals:: %+v and %+v\n", tom, jerry)
} else {
    fmt.Printf("Not Equals:: %+v and %+v\n", tom, jerry)
}

copyTom := tom
fmt.Printf("copyTom = %+v\n", copyTom) // copyTom = {Name:tom FavouriteFruit:{Name:Grape Price:160}}
copyTom.Name = " Copy Tom"
// tom, copyTom :: {Name:tom FavouriteFruit:{Name:Grape Price:160}} and {Name: Copy Tom FavouriteFruit:{Name:Grape Price:160}}
fmt.Printf("tom, copyTom :: %+v and %+v\n", tom, copyTom)

refTom := &tom
refTom.Name = "Ref tom"
// tom, refTom :: {Name:Ref tom FavouriteFruit:{Name:Grape Price:160}} and &{Name:Ref tom FavouriteFruit:{Name:Grape Price:160}}
fmt.Printf("tom, refTom :: %+v and %+v\n", tom, refTom)

```

```shell
$ go run hello.go 
{apple 150}
apple 150
{Name:banana Price:40}  {banana 40}
&{Name: Price:0}
&{Name:mango Price:200}
&{banana 40} 0xc000094020 &{banana 40} {banana 40}
{Name:Grape Price:160}
defaultUser = {Name: FavouriteFruit:{Name: Price:0}}
{Name:tom FavouriteFruit:{Name:Grape Price:160}}
{Name:jerry FavouriteFruit:{Name:strawberry Price:300}}
strawberry
main.User main.User
Not Equals:: {Name:tom FavouriteFruit:{Name:Grape Price:160}} and {Name:jerry FavouriteFruit:{Name:strawberry Price:300}}
copyTom = {Name:tom FavouriteFruit:{Name:Grape Price:160}}
tom, copyTom :: {Name:tom FavouriteFruit:{Name:Grape Price:160}} and {Name: Copy Tom FavouriteFruit:{Name:Grape Price:160}}
tom, refTom :: {Name:Ref tom FavouriteFruit:{Name:Grape Price:160}} and &{Name:Ref tom FavouriteFruit:{Name:Grape Price:160}}
```

[↑](https://arunsah.github.io/gonotes#table-of-content)



## 8. Methods and Interfaces

- A method is similar to function but have parameter section immediately after `func` keyword that accepts a single argument known as receiver. A method receiver is a type.
- A method set are available to a data type promotes code reuse and modularisation.
- An interface specifies a method set and useful for modularity. These are blueprint for a method set as it described all methods in a set but does not implement them.
- Interfaces are way to create polymorphic implementations that can share methods with different concrete entity.

```go

/*
Fruit model fruit entity
*/
type Fruit struct {
    Name  string
    Price float32
}

/*
UpdatePrice new fruit entity
*/
func (fruit *Fruit) UpdatePrice(price float32) {
    fruit.Price = price
}

/*
Shape is interface for other shapes
*/
type Shape interface {
    Area() float32
}

/*
Square is 2D square
*/
type Square struct {
    Length float32
}

/*
Area calculate are of a square
*/
func (s Square) Area() float32 {
    return s.Length * s.Length
}

/*
Rect is 2D rect
*/
type Rect struct {
    Length float32
    Height float32
}

/*
Area calculate are of a rect
*/
func (s Rect) Area() float32 {
    return s.Length * s.Height
}

/*
AreaOfShape returns area of shape s
This accepts any implementation of Shape interface as args
*/
func AreaOfShape(s Shape) float32 {
    return s.Area()
}

func main() {

    fmt.Println("Methods and Interfaces")

    apple := Fruit{Name: "apple", Price: 150.0}
    fmt.Printf("%+v\n", apple) // {Name:apple Price:150}
    apple.UpdatePrice(160.0)
    fmt.Printf("%+v\n", apple) // {Name:apple Price:160}

    sq := Square{12}
    rt := Rect{12, 13}
    fmt.Printf("Area is %f of %+v\n", AreaOfShape(sq), sq) // Area is 144.000000 of {Length:12}
    fmt.Printf("Area is %f of %+v\n", AreaOfShape(rt), rt) // Area is 156.000000 of {Length:12 Height:13}

} //end of main

```

[↑](https://arunsah.github.io/gonotes#table-of-content)



## 9. Strings

- String literals can contain any character other than newline and unescaped double quote.
- Interpreted string literals uses double quotes and supports expansion of rune literals within it.
- Raw string literal uses back quotes. These are consider as pre-formatted.
- Rune literals allow an interpreted string literal to be formatted into multiple lines.
- Raw string literals are created between back quotes.
- Only strings can be concatenated, other types need to be converted explicitly before concatenation.
- String in go is a read-only slice of bytes.
- Unicode char can of multiple bytes.
- Go code is interpreted as utf-8, so identifiers can comprises any unicode characters.
- String is immutable.

```go
strconv.Itoa(num) // num to string

fmt.Println("Strng Operation")
// use byte buffer for changing string and for performance
var buffer bytes.Buffer
for i := 0; i < 100; i++ {
    buffer.WriteString("0")
}
fmt.Println(buffer.String())

greet := "hello"
// len=5, first char='h', first char(base10)=104, first char(base2)=1101000
fmt.Printf("len=%d, first char=%q, first char(base10)=%d, first char(base2)=%b\n", len(greet), greet[0], greet[0], greet[0])
fmt.Println(greet, strings.ToUpper(greet)) // hello HELLO
greetHindi := "हैलो"
// len=12, first char='à', first char(base10)=224, first char(base2)=11100000
fmt.Printf("len=%d, first char=%q, first char(base10)=%d, first char(base2)=%b\n", len(greetHindi), greetHindi[0], greetHindi[0], greetHindi[0])

// substrings
fmt.Println(strings.Index("helloworld", "world")) // index = 5
fmt.Println(strings.Index("helloworld", "moon"))  // index = -1
```

- Docs [strings - The Go Programming Language](https://golang.org/pkg/strings/)

```go
func Compare(a, b string) int
func Contains(s, substr string) bool
func ContainsAny(s, chars string) bool
func ContainsRune(s string, r rune) bool
func Count(s, substr string) int
func EqualFold(s, t string) bool
func Fields(s string) []string
func FieldsFunc(s string, f func(rune) bool) []string
func HasPrefix(s, prefix string) bool
func HasSuffix(s, suffix string) bool
func Index(s, substr string) int
func IndexAny(s, chars string) int
func IndexByte(s string, c byte) int
func IndexFunc(s string, f func(rune) bool) int
func IndexRune(s string, r rune) int
func Join(elems []string, sep string) string
func LastIndex(s, substr string) int
func LastIndexAny(s, chars string) int
func LastIndexByte(s string, c byte) int
func LastIndexFunc(s string, f func(rune) bool) int
func Map(mapping func(rune) rune, s string) string
func Repeat(s string, count int) string
func Replace(s, old, new string, n int) string
func ReplaceAll(s, old, new string) string
func Split(s, sep string) []string
func SplitAfter(s, sep string) []string
func SplitAfterN(s, sep string, n int) []string
func SplitN(s, sep string, n int) []string
func Title(s string) string
func ToLower(s string) string
func ToLowerSpecial(c unicode.SpecialCase, s string) string
func ToTitle(s string) string
func ToTitleSpecial(c unicode.SpecialCase, s string) string
func ToUpper(s string) string
func ToUpperSpecial(c unicode.SpecialCase, s string) string
func ToValidUTF8(s, replacement string) string
func Trim(s string, cutset string) string
func TrimFunc(s string, f func(rune) bool) string
func TrimLeft(s string, cutset string) string
func TrimLeftFunc(s string, f func(rune) bool) string
func TrimPrefix(s, prefix string) string
func TrimRight(s string, cutset string) string
func TrimRightFunc(s string, f func(rune) bool) string
func TrimSpace(s string) string
func TrimSuffix(s, suffix string) string
type Builder
    func (b *Builder) Cap() int
    func (b *Builder) Grow(n int)
    func (b *Builder) Len() int
    func (b *Builder) Reset()
    func (b *Builder) String() string
    func (b *Builder) Write(p []byte) (int, error)
    func (b *Builder) WriteByte(c byte) error
    func (b *Builder) WriteRune(r rune) (int, error)
    func (b *Builder) WriteString(s string) (int, error)
type Reader
    func NewReader(s string) *Reader
    func (r *Reader) Len() int
    func (r *Reader) Read(b []byte) (n int, err error)
    func (r *Reader) ReadAt(b []byte, off int64) (n int, err error)
    func (r *Reader) ReadByte() (byte, error)
    func (r *Reader) ReadRune() (ch rune, size int, err error)
    func (r *Reader) Reset(s string)
    func (r *Reader) Seek(offset int64, whence int) (int64, error)
    func (r *Reader) Size() int64
    func (r *Reader) UnreadByte() error
    func (r *Reader) UnreadRune() error
    func (r *Reader) WriteTo(w io.Writer) (n int64, err error)
type Replacer
    func NewReplacer(oldnew ...string) *Replacer
    func (r *Replacer) Replace(s string) string
    func (r *Replacer) WriteString(w io.Writer, s string) (n int, err error)
Bugs

```

[↑](https://arunsah.github.io/gonotes#table-of-content)



## 10. Handling Errors

- Return error type as its final value.
- Rob Pike’s blog post “Errors are Values” (https://blog.golang.org/errors-are-values). “Values can be programmed, and since errors are values, errors can be programmed. Errors are not like exceptions. There’s nothing special about them, whereas an unhandled exception can crash your program.”

```go
/*
error is defined in std lib
*/
type error interface {
    Error() string
}

```

- `errors` package supports creating and manipulating errors.
- error strings should not be capitalized or end with punctuation or a newline, so that they can be added with other information.
- Error message should specifies about the problem, offers a resolution and be gentle.

```go

func main() {

    file, err := ioutil.ReadFile("greeting.txt") // var file []byte; var err error;
    if err != nil {
        // Error occured while reading file: greeting.txt
        // [] open greeting.txt: no such file or directory
        fmt.Println("Error occured while reading file: greeting.txt")
        fmt.Println(file, err)
    } else { // if file exist
        fmt.Println(string(file), err) // hello world <nil>
    }

    if err := errors.New("someting bad happened"); err != nil {
        fmt.Println(err) // someting bad happened
    }

    // formatng error message
    if err := fmt.Errorf("the %v quits as %v", "tom", "cat"); err != nil {
        fmt.Println(err) // the tom quits as cat
    }

    // return error from a function
    fmt.Println(div(12, 0)) // -1 cannot divide by zero
    fmt.Println(div(12, 3)) // 4 <nil>

    //panicFunc()
} //end of main

// return error from a function
func div(numerator, denominator int) (int, error) {
    if denominator == 0 {
        return -1, fmt.Errorf("cannot divide by zero")
    }
    return numerator / denominator, nil
}

func panicFunc() {
    fmt.Println("Hello world")
    panic("This is panic situation. Execition is halted!")
    // unreachable code below
    fmt.Println("This is solution but wont execute after panic statement")
}

```

- `panic` stops flows of control and halt the execution. Avoid panic. It should last resort and used if program reaches unrecoverable state.

- Go’ idiomatic approaches to error handling says that caller is responsible for handling errors.
- More we can think of error and means to recover, better is the code.
- Errors are reported to callers rather that (exception) handling in the method itself. Design decision.

[↑](https://arunsah.github.io/gonotes#table-of-content)



## 11. Goroutines

- Rob Pike, “Concurrency is about dealing with lots of things at once. Parallelism is about doing lots of things at once.”
- “Concurrency Is Not Parallelism” by Rob Pike (https://www.youtube.com/watch?v=cN_DpYBzKso)
- Go routines returns immediately because they are non-blocking.
- Go routines does not remove latency but make the program efficient and responsive.
- For concurrency: Nodejs uses event loop to manage concurrency. Java uses threads. Apaches uses processes and threads. Nginx uses event loop.
- Go routines abstract threads and schedules them. Go routines are light weight (few KB) in comparison to threads (few MB). So go routines can be created and destroyed very efficiently.

```go

func main() {

    go slowFunc() // non blocking
    go slowFunc() // non blocking
    // NOTE: if we dnt have any blocking statements
    // go routins immediately returns and we wont see the results
    slowFunc() // blocking

    testLatency()
} //end of main

func slowFunc() {
    time.Sleep(time.Second * 2)
    fmt.Println("slowFunc completed...")
}

func testLatency() {
    // sequenctial
    urls := make([]string, 3)
    urls[0] = "https://howtodoinjava.com/"
    urls[1] = "https://www.google.com/"
    urls[2] = "https://www.wikipedia.org/"
    for _, url := range urls {
        go latency(url)
    }
    // with latency(url), order by url sequente
    // url = https://howtodoinjava.com/ took 0.182161923 seconds.
    // url = https://www.google.com/ took 0.182573379 seconds.
    // url = https://www.wikipedia.org/ took 0.191746371 seconds.

    // url = https://howtodoinjava.com/ took 0.23166841 seconds.
    // url = https://www.google.com/ took 0.192515112 seconds.
    // url = https://www.wikipedia.org/ took 0.205078934 seconds.

    // with go latency(url), order by return
    // url = https://howtodoinjava.com/ took 0.175766133 seconds.
    // url = https://www.wikipedia.org/ took 0.229217635 seconds.
    // url = https://www.google.com/ took 0.275177114 seconds.
    time.Sleep(time.Second * 2)
}
func latency(url string) {
    start := time.Now()
    res, err := http.Get(url)
    if err != nil {
        log.Fatal(err)

    } else {
        //fmt.Println(res)
    }
    defer res.Body.Close()
    elapsed := time.Since(start).Seconds()
    fmt.Printf("url = %s took %v seconds.\n", url, elapsed)
}

```


```shell
$ go run hello.go 
slowFunc completed...
slowFunc completed...
slowFunc completed...
url = https://www.wikipedia.org/ took 0.326265483 seconds.
url = https://www.google.com/ took 0.345889433 seconds.
url = https://howtodoinjava.com/ took 1.071713877 seconds.
```

[↑](https://arunsah.github.io/gonotes#table-of-content)



## 12. Introducing Channels

- Channels helps in communication between go routines.
- *Don’t communicate by sharing memory; share memory by communicating.*
- In other languages, certain memory are shared by processes or threads for communication. For synchronisation the memory are are locked (mutually exclusive-only one thread/process can access it) by a thread/processes which affects performances. (eg. joint account).
- In many situation, messaging are better way to decoupling and IPC.
- Buffered Channels, data is held until a receiver is ready.
- Channel can be readOnly, writeOnly and readWrite. Permissions on channels ensures integrity of data.
- Suppose multiple go routines and program should operates on first return, `select` statement used which are like `switch`. `select` creates a series of receivers for Channels and executes whichever receives a message first. If multiple channels returns at same time, one is selected randomly. `select` statement have timeout if in case no other messages returned within the timeout.
- To receive 5 message from channel, select statement can used inside a for loop and then exit.
- `select` statement within `for` allows message to be consumed as they are received. As this is blocking operations, these message will continue to be consumed until terminated.
- Channel can have only one data type but any.

```go

func main() {

    //queue := make(chan string)    // unbuffered channel
    queue := make(chan string, 5) //buffered channel, make initializes
    queue <- "hello"              // write to channel
    queue <- "world"
    queue <- "how are you?"
    // if channel closes before reading, for unbuffered channel
    // fatal error: all goroutines are asleep - deadlock!
    msg := <-queue
    fmt.Println(msg) // read channel
    close(queue)     // channel is closed, no more message can be sent
    for msg := range queue {
        fmt.Println(msg)
    }

    controlQueue := make(chan string)
    go ping(controlQueue)
    msg = <-controlQueue
    fmt.Println(msg)

    for i := 0; i < 1; i++ {
        msg := <-controlQueue
        fmt.Println(msg)
    }

    host1 := make(chan string)
    host2 := make(chan string)

    go func() {
        time.Sleep(2 * time.Second)
        host1 <- "result 1"
    }()
    go func() {
        time.Sleep(3 * time.Second)
        host2 <- "result 2"
    }()

    // the execution is determined by timing of the message
    // first message will determine the case executed
    // any other response will be discarded
    // once message received, select does not blocks further
    select {
    case result1 := <-host1:
        fmt.Printf("1. search result %v from host %v\n", result1, host1)
    case result2 := <-host2:
        fmt.Printf("2. search result %v from host %v\n", result2, host2)
    case <-time.After(2500 * time.Millisecond): // timeout, TODO:: retry this
        fmt.Printf("3. default or cached search result. no result returned from hosts\n")
    }

    quitChannel()

} //end of main

func quitChannel() {
    // for select to receive multiple (5) message and then stop
    dataQueue := make(chan string)
    stopQueue := make(chan bool) // quit channel
    go func(dataQueue chan string) {
        tick := time.NewTicker(1 * time.Second)
        for {
            // generate message
            dataQueue <- "Can you hear me?"
            <-tick.C
        }
    }(dataQueue)

    go func(stopQueue chan bool) {
        time.Sleep(2 * time.Second)
        fmt.Println("Timeout!")
        stopQueue <- true
    }(stopQueue)

    for {
        select {
        case <-stopQueue:
            return
        case message := <-dataQueue:
            fmt.Println(message)
        }
    }

}

func ping(queue chan string) {
    ticker := time.NewTicker(1 * time.Second)
    for {
        queue <- "ping"
        <-ticker.C
    }
}

func reacChannel(queue <-chan string) {

}
func writeChannel(queue chan<- string) {

}
func reacWriteChannel(queue chan string) {

}

```

[↑](https://arunsah.github.io/gonotes#table-of-content)



## 13. Packages for Code Reuse

- Go program starts with a package clause.
- `main` package is un-imported and must have main function with no args and returns type.
- Packages are imported with `import` statement.
- Package names are short/concise/evocative. 
- Go core std lib are small/stable.
- Sometime we just require few methods from 3rd party lib. It is better to copy the function (with keeping license terms in consideration). 
- Identifiers beginning with uppercase are exported (public)
- External packages need to be installed using `go get`.  It can download any transitive dependencies. Eg `$ go get github.com/shapeshed/golang-book-examples`will install the package at `~/go/src/github.com/shapeshed/golang-book-examples`. 
- A valid GOPATH is required to use the `go get` command. If $GOPATH is not specified, $HOME/go will be used by default: https://golang.org/doc/code.html#GOPATH - [homebrew - Where does go get install packages? - Stack Overflow](https://stackoverflow.com/a/50633093)
- `go get github.com/golang/example/stringutil` will install the package at `$GOPATH` so it is available to use within programs. Source code will be present in `$GOPATH/src/github/golang/example/stringutil` for Linux/macOS and `%GOPATH%\src\github\golang\example\stringutil` for Windows. After installation, package can be imported as `import "github.com/golang/example/stringutil"`and used as `fmt.Println(stringutil.Reverse("Hello World"))`
- Consideration required before using external package:
	- how to update package.
	- how to use specific version.
	- how to share dependency manifest.
	- how to install dependencies on a build server.
- To update all dependency of current project, from project folder run `go get -u`.
- To update specific package, `go get -u github.com/spf13/hugo`.
- To update all packages on system, `go get -u all`.
- Go get pulls source code that matches local branch. If local branch is `master`, then `master` is pulled from remote.
- Go 1.5+ introduces vendor folder that supports adding external package to vendor folder in project root and move all packages files to this folder. Rather than installing a package globally across a machine, it is installed directly into project. This is important if multiple version of an external package is used across different projects.

```shell
$ go list -deps
internal/cpu
unsafe
internal/bytealg
runtime/internal/atomic
runtime/internal/sys
runtime/internal/math
runtime
internal/reflectlite
errors
internal/race
sync/atomic
sync
io
unicode
unicode/utf8
bytes
math/bits
math
strconv
reflect
sort
internal/fmtsort
internal/oserror
syscall
time
internal/poll
internal/syscall/unix
internal/testlog
os
fmt
github.com/golang/example/stringutil
strings
path/filepath
io/ioutil
log
bufio
compress/flate
encoding/binary
hash
hash/crc32
compress/gzip
container/list
context
crypto/internal/subtle
crypto/subtle
crypto/cipher
crypto/aes
math/rand
math/big
crypto/rand
crypto
crypto/des
crypto/elliptic
crypto/internal/randutil
crypto/sha512
encoding/asn1
crypto/ecdsa
crypto/ed25519/internal/edwards25519
crypto/ed25519
crypto/hmac
crypto/md5
crypto/rc4
crypto/rsa
crypto/sha1
crypto/sha256
crypto/dsa
encoding/hex
crypto/x509/pkix
encoding/base64
encoding/pem
vendor/golang.org/x/crypto/cryptobyte/asn1
vendor/golang.org/x/crypto/cryptobyte
vendor/golang.org/x/net/dns/dnsmessage
vendor/golang.org/x/net/route
internal/nettrace
internal/singleflight
runtime/cgo
net
net/url
os/exec
crypto/x509
vendor/golang.org/x/crypto/internal/subtle
vendor/golang.org/x/crypto/internal/chacha20
vendor/golang.org/x/crypto/poly1305
vendor/golang.org/x/sys/cpu
vendor/golang.org/x/crypto/chacha20poly1305
vendor/golang.org/x/crypto/curve25519
vendor/golang.org/x/crypto/hkdf
crypto/tls
vendor/golang.org/x/text/transform
vendor/golang.org/x/text/unicode/bidi
vendor/golang.org/x/text/secure/bidirule
vendor/golang.org/x/text/unicode/norm
vendor/golang.org/x/net/idna
net/textproto
vendor/golang.org/x/net/http/httpguts
vendor/golang.org/x/net/http/httpproxy
vendor/golang.org/x/net/http2/hpack
mime
mime/quotedprintable
mime/multipart
net/http/httptrace
net/http/internal
path
net/http
_/Users/arunsah/dev/tut/golang/gonotes

```

- If vendor folder is not found. Changed the `$GOPATH` inside my shell config file. Instead of `export GOPATH=/projects/go`  changed to `export GOPATH=/Projects/go` because that’s was the actual folder name. [github - vendor folder not used with ‘go build’ - Stack Overflow](https://stackoverflow.com/questions/41319633/vendor-folder-not-used-with-go-build). GOPATH was set as $PWD. **THERE SHOULD BE a src folder under GOPATH and all your workspace should be under this src folder**. Check`go help gopath`. Check `how to move external packaged into vendor folder`. It may require to move manually.
- Vendor folder allows Go to link packages to a program rather to use globally installed version.

```shell
$ tree
.
├── currencyconv
│   ├── currencyconv.go
│   └── currencyconv_test.go
├── greeting.txt
├── hello
├── hello.go
├── vendor
│   ├── ...
```

```shell
$ go help gopath
The Go path is used to resolve import statements.
It is implemented by and documented in the go/build package.

The GOPATH environment variable lists places to look for Go code.
On Unix, the value is a colon-separated string.
On Windows, the value is a semicolon-separated string.
On Plan 9, the value is a list.

If the environment variable is unset, GOPATH defaults
to a subdirectory named "go" in the user's home directory
($HOME/go on Unix, %USERPROFILE%\go on Windows),
unless that directory holds a Go distribution.
Run "go env GOPATH" to see the current GOPATH.

See https://golang.org/wiki/SettingGOPATH to set a custom GOPATH.

Each directory listed in GOPATH must have a prescribed structure:

The src directory holds source code. The path below src
determines the import path or executable name.

The pkg directory holds installed package objects.
As in the Go tree, each target operating system and
architecture pair has its own subdirectory of pkg
(pkg/GOOS_GOARCH).

If DIR is a directory listed in the GOPATH, a package with
source in DIR/src/foo/bar can be imported as "foo/bar" and
has its compiled form installed to "DIR/pkg/GOOS_GOARCH/foo/bar.a".

The bin directory holds compiled commands.
Each command is named for its source directory, but only
the final element, not the entire path. That is, the
command with source in DIR/src/foo/quux is installed into
DIR/bin/quux, not DIR/bin/foo/quux. The "foo/" prefix is stripped
so that you can add DIR/bin to your PATH to get at the
installed commands. If the GOBIN environment variable is
set, commands are installed to the directory it names instead
of DIR/bin. GOBIN must be an absolute path.

Here's an example directory layout:

    GOPATH=/home/user/go

    /home/user/go/
        src/
            foo/
                bar/               (go code in package bar)
                    x.go
                quux/              (go code in package main)
                    y.go
        bin/
            quux                   (installed command)
        pkg/
            linux_amd64/
                foo/
                    bar.a          (installed package object)

Go searches each directory listed in GOPATH to find source code,
but new packages are always downloaded into the first directory
in the list.

See https://golang.org/doc/code.html for an example.

GOPATH and Modules

When using modules, GOPATH is no longer used for resolving imports.
However, it is still used to store downloaded source code (in GOPATH/pkg/mod)
and compiled commands (in GOPATH/bin).

Internal Directories

Code in or below a directory named "internal" is importable only
by code in the directory tree rooted at the parent of "internal".
Here's an extended version of the directory layout above:

    /home/user/go/
        src/
            crash/
                bang/              (go code in package bang)
                    b.go
            foo/                   (go code in package foo)
                f.go
                bar/               (go code in package bar)
                    x.go
                internal/
                    baz/           (go code in package baz)
                        z.go
                quux/              (go code in package main)
                    y.go


The code in z.go is imported as "foo/internal/baz", but that
import statement can only appear in source files in the subtree
rooted at foo. The source files foo/f.go, foo/bar/x.go, and
foo/quux/y.go can all import "foo/internal/baz", but the source file
crash/bang/b.go cannot.

See https://golang.org/s/go14internal for details.

Vendor Directories

Go 1.6 includes support for using local copies of external dependencies
to satisfy imports of those dependencies, often referred to as vendoring.

Code below a directory named "vendor" is importable only
by code in the directory tree rooted at the parent of "vendor",
and only using an import path that omits the prefix up to and
including the vendor element.

Here's the example from the previous section,
but with the "internal" directory renamed to "vendor"
and a new foo/vendor/crash/bang directory added:

    /home/user/go/
        src/
            crash/
                bang/              (go code in package bang)
                    b.go
            foo/                   (go code in package foo)
                f.go
                bar/               (go code in package bar)
                    x.go
                vendor/
                    crash/
                        bang/      (go code in package bang)
                            b.go
                    baz/           (go code in package baz)
                        z.go
                quux/              (go code in package main)
                    y.go

The same visibility rules apply as for internal, but the code
in z.go is imported as "baz", not as "foo/vendor/baz".

Code in vendor directories deeper in the source tree shadows
code in higher directories. Within the subtree rooted at foo, an import
of "crash/bang" resolves to "foo/vendor/crash/bang", not the
top-level "crash/bang".

Code in vendor directories is not subject to import path
checking (see 'go help importpath').

When 'go get' checks out or updates a git repository, it now also
updates submodules.

Vendor directories do not affect the placement of new repositories
being checked out for the first time by 'go get': those are always
placed in the main GOPATH, never in a vendor subtree.

See https://golang.org/s/go15vendor for details.

```


- Creating a package currency convertor and unit test

```go
// file: currencyconv/currencyconv.go
package currencyconv


const USDValue float64 = 75.98
const EUROValue float64 = 82.85

func INR2USD(value float64) float64 {
    return value / USDValue
}

func USD2INR(value float64) float64 {
    return value * USDValue
}

func INR2Euro(value float64) float64 {
    return value / EUROValue
}

func Euro2INR(value float64) float64 {
    return value * EUROValue
}
```

```go
// file: currencyconv/currencyconv_test.go
package currencyconv

import "testing"

type currency struct {
    value    float64
    expected float64
}

var currencyINR2USD = []currency{
    {1, 1 / USDValue},
    {1000, 1000 / USDValue},
    {2500, 2500 / USDValue},
}

func TestINR2USD(test *testing.T) {
    for _, money := range currencyINR2USD {
        actual := INR2USD(money.value)
        if actual != money.expected {
            test.Errorf("expected %v, actual %v", money.expected, actual)
        }
    }
}

```

- Run test

```shell
$ pwd
/Users/arunsah/dev/tut/golang/gonotes/currencyconv

# when fails (intentionally)
$ go test .
--- FAIL: TestINR2USD (0.00s)
    currencyconv_test.go:20: expected 0.013161358252171624, actual 1.0131613582521717
    currencyconv_test.go:20: expected 13.161358252171624, actual 14.161358252171624
    currencyconv_test.go:20: expected 32.90339563042906, actual 33.90339563042906
FAIL
FAIL    _/Users/arunsah/dev/tut/golang/gonotes/currencyconv     0.006s
FAIL

# when pass
$ go test .
ok      _/Users/arunsah/dev/tut/golang/gonotes/currencyconv     0.005s
mario:currencyconv arunsah$ 

# from project root use
$ pwd
/Users/arunsah/dev/tut/golang/gonotes
$ go test ./..
can't load package: package ./..: non-canonical import path: "./.." should be ".."
mario:gonotes arunsah$ go test ./currencyconv/
ok      _/Users/arunsah/dev/tut/golang/gonotes/currencyconv     0.005s

```

- Using in main

```go
package main

import (
    "fmt"

    "./currencyconv"
)

func main() {
    fmt.Println(currencyconv.INR2USD(800)) // 10.5290866017373
} //end of main

```

```shell
$ go run hello.go 
10.5290866017373
mario:gonotes arunsah$ tree
.
├── currencyconv
│   ├── currencyconv.go
│   └── currencyconv_test.go
├── greeting.txt
└── hello.go


```

- For public package it is good to create LICENSE/README/Changelog file. 
	- LICENSE: List of Open Source Licenses [Licenses & Standards | Open Source Initiative](https://opensource.org/licenses)
	- README: it contains information about package, how to install/build/use/demo sample codes. How other can contribute.
	- Changelog: list changes to packages. Addition/removal of features. Git tags to denote releases

[↑](https://arunsah.github.io/gonotes#table-of-content)



## 14. Naming Conventions in Go

- Idiomatic go, using of standard conversions.
- Go compiler does not enforce code formatting but `gofmt` formatted code which is expected by go community. Eg, `gofmt hello.go`. To check difference use `diff hello.go gofmt/hello.go`. `gofmt` does not write to disk, to write use `gofmt -w hello.go`
- In cs two hardest things are caching and naming things.
- Use camelCase for identifiers (private) and PascalCase (public).
- Interfaces are named with verbs and “er” suffix to make it noun which signifies an action (eg. Reader). This also allow some not English words such as “Tower”. Eg. Parser, Authorizer are interfaces.
- For exported functions use meaningful names such as `Sqrt` rather than `MathSqrt`to be part of `math` package.
- `golint` (official tooling) checkstyles for conventions. Not installed b default, `go get -u github.com/golang/lint/golint`. Verify installation by `golint --help`.
- `godoc` (official) parse Go source code and produce documentation from code and comments. Install by `go get golang.org/x/tools/cmd/godoc`and verify installation by `godoc --help`. `godoc ./helloworld`
- To add comments for section of code, begin line with name of element that need comments. 

```shell
mario:gonotes arunsah$ godocs
bash: godocs: command not found
mario:gonotes arunsah$ go get golang.org/x/tools/cmd/godoc
mario:gonotes arunsah$ godoc hello.go 
bash: godoc: command not found
mario:gonotes arunsah$ which godoc
mario:gonotes arunsah$ go get -v golang.org/x/tools/cmd/godocmario:gonotes arunsah$ godoc hello.go                        bash: godoc: command not found
mario:gonotes arunsah$ go get -v golang.org/x/tools/cmd/godocmario:gonotes arunsah$ godoc -http=:6060
bash: godoc: command not found
mario:gonotes arunsah$ go get golang.org/x/tools/cmd/godoc
mario:gonotes arunsah$ godoc --help
bash: godoc: command not found
mario:gonotes arunsah$ godoc string
bash: godoc: command not found
mario:gonotes arunsah$ godoc --help 
bash: godoc: command not found
mario:gonotes arunsah$ go get golang.org/x/tools/cmd/godoc
mario:gonotes arunsah$ godoc --help 
bash: godoc: command not found
mario:gonotes arunsah$ 
mario:gonotes arunsah$ 
mario:gonotes arunsah$ go get golang.org/x/tools/cmd/godoc
package golang.org/x/tools/cmd/godoc: cannot find package "golang.org/x/tools/cmd/godoc" in any of:
        /usr/local/go/src/golang.org/x/tools/cmd/godoc (from $GOROOT)
        /Users/arunsah/go/src/golang.org/x/tools/cmd/godoc (from $GOPATH)
mario:gonotes arunsah$ 
mario:gonotes arunsah$ 
mario:gonotes arunsah$ go get golang.org/x/tools/cmd/godoc
package golang.org/x/tools/cmd/godoc: cannot find package "golang.org/x/tools/cmd/godoc" in any of:
        /usr/local/go/src/golang.org/x/tools/cmd/godoc (from $GOROOT)
        /Users/arunsah/go/src/golang.org/x/tools/cmd/godoc (from $GOPATH)
mario:gonotes arunsah$ 
mario:gonotes arunsah$ 
mario:gonotes arunsah$ go get golang.org/x/tools/cmd/godoc
mario:gonotes arunsah$ godoc --help 
bash: godoc: command not found
mario:gonotes arunsah$ go clean -i importpath...
go: warning: "importpath..." matched no packages
mario:gonotes arunsah$ go clean -i 
mario:gonotes arunsah$ which godoc
mario:gonotes arunsah$ go get golang.org/x/tools/cmd/godoc
mario:gonotes arunsah$ which godoc
mario:gonotes arunsah$ go clean -i -n golang.org/x/tools/cmd/godoc...
cd /Users/arunsah/go/src/golang.org/x/tools/cmd/godoc
rm -f godoc godoc.exe godoc.test godoc.test.exe doc doc.exe godoc_test godoc_test.exe goroot goroot.exe handlers handlers.exe main main.exe
rm -f /Users/arunsah/go/bin/godoc
mario:gonotes arunsah$ go get golang.org/x/tools/cmd/godoc   mario:gonotes arunsah$ which godoc                           mario:gonotes arunsah$ echo $PATH
/Applications/vscode.app/Contents/Resources/app/bin:/Users/arunsah/bin/istio/istio-1.5.2/bin:/Users/arunsah/bin/Postman.app:/Users/arunsah/bin/kafka_2.13-2.4.0/bin:/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin:/opt/apache-maven/bin:/usr/local/mysql/bin:/usr/local/go/bin:/Users/arunsah/bin/istio/istio-1.5.2:/Users/arunsah/bin/istio/istio-1.5.2/bin:/Users/arunsah/bin/Postman.app:/Users/arunsah/bin/kafka_2.13-2.4.0/bin
mario:gonotes arunsah$ nano ~/.bash_profile 
mario:gonotes arunsah$ 
mario:gonotes arunsah$ 
mario:gonotes arunsah$ which go
/usr/local/go/bin/go
mario:gonotes arunsah$ which godoc
mario:gonotes arunsah$ find godoc
find: godoc: No such file or directory
mario:gonotes arunsah$ which godoc
mario:gonotes arunsah$ /Users/arunsah/go/bin/go
go-outline            gocode                godef                 godoctor              golint                gopkgs                gorename              gotests
go-symbols            gocode-gomod          godoc                 golang-book-examples  gomodifytags          goplay                goreturns             
mario:gonotes arunsah$ /Users/arunsah/go/bin/go
go-outline            gocode                godef                 godoctor              golint                gopkgs                gorename              gotests
go-symbols            gocode-gomod          godoc                 golang-book-examples  gomodifytags          goplay                goreturns             
mario:gonotes arunsah$ /Users/arunsah/go/bin/godoc
using GOPATH mode
^C
mario:gonotes arunsah$ 
mario:gonotes arunsah$ 
mario:gonotes arunsah$ nano ~/.bash_profile 
mario:gonotes arunsah$ godoc
bash: godoc: command not found
mario:gonotes arunsah$ 

```

- [Removing packages installed with go get - Stack Overflow](https://stackoverflow.com/questions/13792254/removing-packages-installed-with-go-get)
- [Removing packages installed with go get - Stack Overflow](https://stackoverflow.com/a/33372718)

```shell
$ go get -u github.com/motemen/gore

$ which gore
/Users/ches/src/go/bin/gore

$ go clean -i -n github.com/motemen/gore...
cd /Users/ches/src/go/src/github.com/motemen/gore
rm -f gore gore.exe gore.test gore.test.exe commands commands.exe commands_test commands_test.exe complete complete.exe complete_test complete_test.exe debug debug.exe helpers_test helpers_test.exe liner liner.exe log log.exe main main.exe node node.exe node_test node_test.exe quickfix quickfix.exe session_test session_test.exe terminal_unix terminal_unix.exe terminal_windows terminal_windows.exe utils utils.exe
rm -f /Users/ches/src/go/bin/gore
cd /Users/ches/src/go/src/github.com/motemen/gore/gocode
rm -f gocode.test gocode.test.exe
rm -f /Users/ches/src/go/pkg/darwin_amd64/github.com/motemen/gore/gocode.a

$ go clean -i github.com/motemen/gore...

$ which gore

$ tree $GOPATH/pkg/darwin_amd64/github.com/motemen/gore
/Users/ches/src/go/pkg/darwin_amd64/github.com/motemen/gore

0 directories, 0 files

# If that empty directory really bugs you...
$ rmdir $GOPATH/pkg/darwin_amd64/github.com/motemen/gore

$ rm -rf $GOPATH/src/github.com/motemen/gore

```

```shell
#!/bin/bash
# [Removing packages installed with go get - Stack Overflow](https://stackoverflow.com/a/50069549)
goclean() {
 local pkg=$1; shift || return 1
 local ost
 local cnt
 local scr

 # Clean removes object files from package source directories (ignore error)
 go clean -i $pkg &>/dev/null

 # Set local variables
 [[ "$(uname -m)" == "x86_64" ]] \
 && ost="$(uname)";ost="${ost,,}_amd64" \
 && cnt="${pkg//[^\/]}"

 # Delete the source directory and compiled package directory(ies)
 if (("${#cnt}" == "2")); then
  rm -rf "${GOPATH%%:*}/src/${pkg%/*}"
  rm -rf "${GOPATH%%:*}/pkg/${ost}/${pkg%/*}"
 elif (("${#cnt}" > "2")); then
  rm -rf "${GOPATH%%:*}/src/${pkg%/*/*}"
  rm -rf "${GOPATH%%:*}/pkg/${ost}/${pkg%/*/*}"
 fi

 # Reload the current shell
 source ~/.bashrc
}

# Either launch a new terminal and copy `goclean` into the current shell process, 
# or create a shell script and add it to the PATH to enable command invocation with bash.

#goclean github.com/your-username/your-repository

```

- `Makefile` helps to automate the flow to run tests, lint code, compile code and can be used in continuous integration.
- Run from root of project using `make` command.

```shell
all: check-gofmt

check-gofmt:
# if any files are incorrectly formated,
# they will be printed to terminal.
@if [ -n "$(shell gofmt -l .)" ]; then \

    echo 1>&2 'The following files need to be formatted:'; \

    gofmt -l .; \

    exit 1; \

fi

```

[↑](https://arunsah.github.io/gonotes#table-of-content)



## 15. Testing and Performance

- Test works as documents for developer. Caught bugs. 
- Unit Test:
	- cover small part of code and test in isolation.
	- often test single function.
	- as program changes/grows unit test are excellent way to caught any regressions (bug/fault that has been introduced as a result of a change).
- Integration Test:
	- test how various parts of application works together.
	- test network calls, db connection, system as a whole.
- Functional Test:
	- end-to-end test and outside-in test.
	- test from enduser perspective.
	- Eg: running automated tests on a web page, testing api to check response code and headers, command line tool response to specific inputs.
- Test-Driven Development (TDD): 
	- thinking about a new features in terms of a test.
	- test is written that describes the expected functionality of a piece of code before writing implementation.
	- communicate code design; thinking how piece of code works helps improves design.
	- provide definition about how a feature should work.
	- there will be test that can caught regression.
	- test can verify once the implementation is completed.
	- Using TDD, code design improves, code functionality are ensures.
- Go provide `testing` package and `go test`.
- Conventions: 
	- Test code (`feature_test.go`) are placed in same directory of the implementation code (`feature.go`).
	- Tests function begin with `Test*`.
	- Two variables `got/actual` and `want/expected` represents the value to be tested and expected value.

```go
func TestNumber(test *testing.T) {
    got := 1
    want := 1
    if got != want {
        test.Errorf("Expected %v, got %v", want, got)
    }
}
```

- Table Tests:
	- Create struct with got, want and other parameters and create arrays/table with values. This will reduce code duplication based on parameters.

```go
package currencyconv

import "testing"

type currency struct {
    value    float64
    expected float64
}

var currencyINR2USD = []currency{
    {1, 1 / USDValue},
    {1000, 1000 / USDValue},
    {2500, 2500 / USDValue},
}

func TestINR2USD(test *testing.T) {
    for _, money := range currencyINR2USD {
        actual := INR2USD(money.value)
        if actual != money.expected {
            test.Errorf("expected %v, actual %v", money.expected, actual)
        }
    }
}

```

- Testing package include benchmarking framework that allows a function to be run repeatedly and a benchmark to be applied. Count of execution of function is not manually set but decided by framework to have reliable data set. A report is give on number of operations that were complete per nanosecond. Benchmark method starts with `Benchmark*`and takes `b *testing.B` as method arguments.

```go
func BenchmarkINR2USD(benchmark *testing.B) {
    for i := 0; i < benchmark.N; i++ {
        INR2USD(100)
    }
}

```

- `-bench` flag is passed to `go test` command. Eg. `go test -bench=.`

```shell
Running tool: /usr/local/go/bin/go test -benchmem -run=^$ -bench ^(BenchmarkINR2USD)$

goos: darwin
goarch: amd64
BenchmarkINR2USD-8      1000000000           0.501 ns/op           0 B/op          0 allocs/op
PASS
ok      _/Users/arunsah/dev/tut/golang/gonotes/currencyconv    0.558s

```

- Test coverage provide percentages of values of code have that have test.
- `-cover` flag is used with `go test`. Eg. `go test –cover hello.go`

```shell
$ go test -cover ./currencyconv/*
ok      command-line-arguments  0.005s  coverage: 25.0% of statements
mario:gonotes arunsah$ 
mario:gonotes arunsah$ go test -cover .
?       _/Users/arunsah/dev/tut/golang/gonotes     [no test files]
mario:gonotes arunsah$ 
```

- Test should be run each time before committing.

[↑](https://arunsah.github.io/gonotes#table-of-content)



## 16. Debugging

- Logging:
	- log are useful for monitoring, track down issue and identify problems.
	- logging is proactive approach to debugging when an unexpected/abnormal event occurs.
	- `log` package provide logging features to terminal/file. 

```go
// 2020/05/25 00:58:55 This is a log message
log.Printf("This is a log message")

// 2020/05/25 01:01:21 This is fatal error: fatal error ocurred
// exit status 1
log.Fatalf("This is fatal error: %v", errors.New("fatal error ocurred"))

//  logging to file
logfile, err := os.OpenFile("logfile.txt", os.O_APPEND|os.O_CREATE|os.O_RDWR, 0666)
if err != nil {
    log.Fatalf("This is fatal error: %v", errors.New("fatal error ocurred"))
}
defer logfile.Close()
log.SetOutput(logfile) // os redirect to file

log.Printf("This is a log message")

```

```shell
# shell recirection
go run hello.go > logfile.txt

```

- In `fmt.Printf` `%v` verb is default format of a type. `%+v` prints the files names within struct.

- Debugger:
	- No official debugger (verify??).
	- `go get github.com/derekparker/delve/cmd/dlv`
	- `dlv --help`
	- Delve allows to interact with program while it is executing, attach to a running process, examine core dumps and stack traces.
	- `dlv debug hello.go`. It will start `dlv` consoles.
		- Suppose we want to apply breakpoint at function call `greeting(name)`, type ` (dlv) break greeting`
		- Once all breakpoints are created, program can be executed by `continue` command.
		- `(dlv) print message`
	- Unix, `gdb`operated on binary files.
		- `go build hello.go`
		- `gdb hello`
		- `list` commands helps to inspect parts of code. Eg, `list main.greeting` shows context of greeting function.
		- `break main.greeting` set breakpoints, a line number or a function name can be provided.
		- `run` to execute the program until files breakpoint is hit.
		- `(dlv) print message` will show value of message.
		- `continue` to continue execution.

[↑](https://arunsah.github.io/gonotes#table-of-content)



## 17. Command-Line Programs

```go

func main() {
    for i, arg := range os.Args {
        fmt.Printf("%d:%v, ", i, arg)
    }

    msg := flag.String("m", "[value]hello world", "[help]default greeting message")
    flag.Parse()
    fmt.Println("value of msg: ", *msg)

} //end of main

```

```shell
$ go run hello.go -m hi 1 2 3 4 5 6
0:/var/folders/5t/kf28839s1tlgfv7bkwm_04z40000gn/T/go-build119574370/b001/exe/hello, 1:-m, 2:hi, 3:1, 4:2, 5:3, 6:4, 7:5, 8:6, value of msg:  hi

$ go run hello.go -h
0:/var/folders/5t/kf28839s1tlgfv7bkwm_04z40000gn/T/go-build435649009/b001/exe/hello, 1:-h, Usage of /var/folders/5t/kf28839s1tlgfv7bkwm_04z40000gn/T/go-build435649009/b001/exe/hello:
  -m string
        [help]default greeting message (default "[value]hello world")
exit status 2
```

- Flag types: If incorrect value is pass to flag then error is shown and will print help text.

```go
s := flag.String("s", "Hello World", "any string value")
i := flag.Int("i", 1, "any integer value")
b := flag.Bool("b", false, "any boolean value")

flag.Parse()
fmt.Println("value of s: ", *s)
fmt.Println("value of i: ", *i)
fmt.Println("value of b: ", *b)

```

- Help context is available by using any of the following: `-h` or `--h` or `-help` or `--help`.
- Customising help text by overriding `flag.Usage = func(){}`. Raw string literals will preserve formatting (backtick).

```go
    flag.Usage = func() {
        helpText := `Usage calculator [OPTION]
An example of customizing usage output
-s, --s         example string argument, default: String help text
-i, --i         example integer argument, default: Int help text
-b, --b         example boolean argument, default: Bool help text`

        fmt.Fprintln(os.Stderr, helpText)
    }

    flag.Parse()

```

```shell
$ go run hello.go -h
Usage calculator [OPTION]
An example of customizing usage output
-s, --s         example string argument, default: String help text
-i, --i         example integer argument, default: Int help text
-b, --b         example boolean argument, default: Bool help text
exit status 2
```

- Subcommands can have their own set of options. Eg `git` is top level command and have subcommands such as `branch`, `clone`, `push`, `pull`, etc.
- `FlagSets` is provided by `flag` which created independent sets of flags for subcommands.
- `gitCloneCommand := flag.NewFlagSet("clone", flag.ExitOnError)`
	- 1st arg is name of command
	- 2nd arg is error handling behaviour for parsing error
		- `flag.ContinueOnError` continue execution.
		- `flag.ExitOnError` exit with status code 2.
		- `flag.PanicOnError` panic.
- The POSIX recommendation and GNU extensions: https://www.gnu.org/software/libc/manual/html_node/Argument-Syntax.html.

```go
package main

import (
    "flag"
    "fmt"
    "os"
)

func programUsage() {
    text := `calc is an cli tool which provide basic calculator functionality.

    Usage:
    
    calc command [arguments]
    
    The commands are:
    
    add  addition operation
    
    sub  subtraction operation
    
    mul  multiplication operation
    
    div  division operation
    
    Use "calc [command] --help" for more information about a command.`

    fmt.Fprintf(os.Stderr, "%s\n\n", text)

}

func main() {

    flag.Usage = programUsage
    addCmd := flag.NewFlagSet("add", flag.ExitOnError)
    addCmd.Usage = func() {
        text := `Usage of add:
    - a (Int)   first integer value
    - b (Int)   second integer value
        
Use "calc add -a 10 -b 20" to get result of addition of a and b. ie, 10 + 20 = 30
Use "calc add --help" for more information about a command.`

        fmt.Fprintf(os.Stderr, "%s\n\n", text)
    }
    subCmd := flag.NewFlagSet("sub", flag.ExitOnError)
    mulCmd := flag.NewFlagSet("mul", flag.ExitOnError)
    divCmd := flag.NewFlagSet("div", flag.ExitOnError)

    if len(os.Args) == 1 {
        flag.Usage()
        return
    }

    switch os.Args[1] {
    case "add":
        a := addCmd.Int("a", 1, "first integer value")
        b := addCmd.Int("b", 1, "sencond integer value")
        addCmd.Parse(os.Args[2:])
        // call external function
        fmt.Printf("%d + %d = %d\n", *a, *b, (*a + *b))

    case "sub":
        a := subCmd.Int("a", 1, "first integer value")
        b := subCmd.Int("b", 1, "sencond integer value")
        subCmd.Parse(os.Args[2:])
        // call external function
        fmt.Printf("%d - %d = %d\n", *a, *b, (*a - *b))

    case "mul":
        a := mulCmd.Int("a", 1, "first integer value")
        b := mulCmd.Int("b", 1, "sencond integer value")
        mulCmd.Parse(os.Args[2:])
        // call external function
        fmt.Printf("%d * %d = %d\n", *a, *b, (*a * *b))

    case "div":
        a := divCmd.Int("a", 1, "first integer value")
        b := divCmd.Int("b", 1, "sencond integer value")
        divCmd.Parse(os.Args[2:])
        // call external function
        fmt.Printf("%d / %d = %d\n", *a, *b, (*a / *b))

    default:
        flag.Usage()
    }

} //end of main

```

```shell
$ go run calc.go add -ap
flag provided but not defined: -ap
Usage of add:
        - a     (Int)   first integer value
        - b     (Int)   second integer value

Use "calc add -a 10 -b 20" to get result of addition of a and b. ie, 10 + 20 = 30
Use "calc add --help" for more information about a command.

exit status 2
mario:gonotes arunsah$ go run calc.go add -help
Usage of add:
        - a     (Int)   first integer value
        - b     (Int)   second integer value

Use "calc add -a 10 -b 20" to get result of addition of a and b. ie, 10 + 20 = 30
Use "calc add --help" for more information about a command.

exit status 2
mario:gonotes arunsah$ go run calc.go add -a 12 -b 21
12 + 21 = 33

```

- Sharing command line applications. Set `$GOPATH` correctly and develop using standard directory layout. `$GOPATH/src/github.com/arunsah/calc` Create `calc.go` inside the folder and install the program using `go install <path>`. `<path>` should be relative to `$GOPATH` eg. `go install github.com/arunsah/calc`. You can push your project on GitHub. Other can use you program as `go get github.com/arunsah/calc`
- Exit status of command can be seen using `echo %errorlevel%` on Windows and `echo $?` on unix system.

```shell
$ go run calc.go add -a 12 -b 21
12 + 21 = 33
mario:gonotes arunsah$ echo $?
0
mario:gonotes arunsah$ go run calc.go add -help
Usage of add:
        - a     (Int)   first integer value
        - b     (Int)   second integer value

Use "calc add -a 10 -b 20" to get result of addition of a and b. ie, 10 + 20 = 30
Use "calc add --help" for more information about a command.

exit status 2
mario:gonotes arunsah$ echo $?
1

```

- `go install` is used to install local packages (my be from remote). `go get` downloads files and install.

[↑](https://arunsah.github.io/gonotes#table-of-content)



## 18. HTTP Servers

```go
package main

import (
    "fmt"
    "net/http"
)

func rootHandler(res http.ResponseWriter, req *http.Request) {
    fmt.Printf("%+v\n", res)
    fmt.Printf("%+v\n", req)

    var message []byte = []byte("greeting from host\n")
    res.Write(message)
}

func main() {

    const host string = ":8000"
    fmt.Printf("Server is running at %s...\n", host)
    http.HandleFunc("/", rootHandler)
    http.ListenAndServe(host, nil)
}

```

```shell
# server console
$ go run server-hello.go 
Server is running at :8000...
&{conn:0xc00009eaa0 req:0xc0000e8000 reqBody:{} cancelCtx:0x112a5f0 wroteHeader:false wroteContinue:false wants10KeepAlive:false wantsClose:false w:0xc0000224c0 cw:{res:0xc0000d40e0 header:map[] wroteHeader:false chunking:false} handlerHeader:map[] calledHeader:false written:0 contentLength:-1 status:0 closeAfterReply:false requestBodyLimitHit:false trailers:[] handlerDone:0 dateBuf:[0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0] clenBuf:[0 0 0 0 0 0 0 0 0 0] statusBuf:[0 0 0] closeNotifyCh:0xc00006a070 didCloseNotify:0}
&{Method:GET URL:/ Proto:HTTP/1.1 ProtoMajor:1 ProtoMinor:1 Header:map[Accept:[*/*] User-Agent:[curl/7.54.0]] Body:{} GetBody:<nil> ContentLength:0 TransferEncoding:[] Close:false Host:localhost:8000 Form:map[] PostForm:map[] MultipartForm:<nil> Trailer:map[] RemoteAddr:[::1]:53129 RequestURI:/ TLS:<nil> Cancel:<nil> Response:<nil> ctx:0xc000022440}

# client terminal
$ curl -v localhost:8000
* Rebuilt URL to: localhost:8000/
*   Trying ::1...
* TCP_NODELAY set
* Connected to localhost (::1) port 8000 (#0)
> GET / HTTP/1.1
> Host: localhost:8000
> User-Agent: curl/7.54.0
> Accept: */*
> 
< HTTP/1.1 200 OK
< Date: Mon, 25 May 2020 10:22:02 GMT
< Content-Length: 19
< Content-Type: text/plain; charset=utf-8
< 
greeting from host
* Connection #0 to host localhost left intact
```

- `rootHandler` takes `res http.ResponseWriter, req *http.Request` as input this the `req` can be manipulated before returning a response.

- `http.HandleFunc` set up routing table. Default router directs request to `/` is no handler is defined for any path.
- `http.HandleFunc("/guest/", guestHandler)` will route all request `"/guest/"`  to  `guestHandler` while `"/guest"`(missing trailing slash) will route to `/` handler so route must match exactly.
- Route does not concern about the type of request.
- handler function are responsive for:
	- read/write header
	- check type of request (GET/POST/PUT/DELETE/etc).
	- execute business logic if any (persistence, other api call, etc).
	- parsing request data.
	- authentication.
	- once response is written, no further processing on response can take place so complete all task before writing.
- If non existing handler and route are handle by `rootHandler` with `200 OK` response status.
- Common content types are `text/plain`, `text/html`, `application/json` and `application/xml`. If a server supports multiple content types, client may request a content type using `Accept` header. Ie., same url can serve `text/html` or `application/json`.

```go
package main

import (
    "fmt"
    "net/http"
)

func rootHandler(res http.ResponseWriter, req *http.Request) {
    fmt.Printf("%+v\n", res)
    fmt.Printf("%+v\n", req)

    // hadling non existing pages
    if req.URL.Path != "/" {
        http.NotFound(res, req)
        return
    }

    // handle "Accept" header from client
    switch req.Header.Get("Accept") {
    case "application/json":
        res.Header().Set("Content-Type", "application/json; charset=utf-8")
        res.Write([]byte(`{"message": "Hello World"}`))

    case "application/xml":
        res.Header().Set("Content-Type", "application/xml; charset=utf-8")
        res.Write([]byte(`<?xml version="1.0" encoding="utf-8"?><message>Hello World</message>`))

    case "text/plain":
        res.Header().Set("Content-Type", "text/plain; charset=utf-8")
        res.Write([]byte("Hello World\n"))

    default:
        res.Header().Set("X-User", "tom")
        res.Header().Set("Content-Type", "application/json; charset=utf-8")
        var message []byte = []byte("{\"message\":\"greeting from host\"}\n")
        res.Write(message)
    }

}

func main() {

    const host string = ":8000"
    fmt.Printf("Server is running at %s...\n", host)
    http.HandleFunc("/", rootHandler)
    http.ListenAndServe(host, nil)
}

```

```shell
# client request

mario:bin arunsah$ curl -v localhost:8000 -H 'Accept: application/json'
* Rebuilt URL to: localhost:8000/
*   Trying ::1...
* TCP_NODELAY set
* Connected to localhost (::1) port 8000 (#0)
> GET / HTTP/1.1
> Host: localhost:8000
> User-Agent: curl/7.54.0
> Accept: application/json
> 
< HTTP/1.1 200 OK
< Content-Type: application/json; charset=utf-8
< Date: Mon, 25 May 2020 10:49:55 GMT
< Content-Length: 26
< 
* Connection #0 to host localhost left intact
{"message": "Hello World"}

mario:bin arunsah$ 
mario:bin arunsah$ 
mario:bin arunsah$ curl -v localhost:8000 -H 'Accept: application/xml'
* Rebuilt URL to: localhost:8000/
*   Trying ::1...
* TCP_NODELAY set
* Connected to localhost (::1) port 8000 (#0)
> GET / HTTP/1.1
> Host: localhost:8000
> User-Agent: curl/7.54.0
> Accept: application/xml
> 
< HTTP/1.1 200 OK
< Content-Type: application/xml; charset=utf-8
< Date: Mon, 25 May 2020 10:50:02 GMT
< Content-Length: 68
< 
* Connection #0 to host localhost left intact
<?xml version="1.0" encoding="utf-8"?><message>Hello World</message>

mario:bin arunsah$ 
mario:bin arunsah$ 
mario:bin arunsah$ curl -v localhost:8000
* Rebuilt URL to: localhost:8000/
*   Trying ::1...
* TCP_NODELAY set
* Connected to localhost (::1) port 8000 (#0)
> GET / HTTP/1.1
> Host: localhost:8000
> User-Agent: curl/7.54.0
> Accept: */*
> 
< HTTP/1.1 200 OK
< Content-Type: application/json; charset=utf-8
< X-User: tom
< Date: Mon, 25 May 2020 10:50:09 GMT
< Content-Length: 33
< 
{"message":"greeting from host"}
* Connection #0 to host localhost left intact
mario:bin arunsah$ 

```

- Response to different method type.

```go
func rootHandler(res http.ResponseWriter, req *http.Request) {
    fmt.Printf("%+v\n", res)
    fmt.Printf("%+v\n", req)

    // hadling non existing pages
    if req.URL.Path != "/" {
        http.NotFound(res, req)
        return
    }

    // handle method types
    switch req.Method {
    case "GET":
        res.Write([]byte("Received a GET request\n"))

    case "POST":
        res.Write([]byte("Received a POST request\n"))

    default:
        res.WriteHeader(http.StatusNotImplemented)
        res.Write([]byte(http.StatusText(http.StatusNotImplemented)))

    }

    // handle "Accept" header from client
    switch req.Header.Get("Accept") {
    case "application/json":
        res.Header().Set("Content-Type", "application/json; charset=utf-8")
        res.Write([]byte(`{"message": "Hello World"}`))

    case "application/xml":
        res.Header().Set("Content-Type", "application/xml; charset=utf-8")
        res.Write([]byte(`<?xml version="1.0" encoding="utf-8"?><message>Hello World</message>`))

    case "text/plain":
        res.Header().Set("Content-Type", "text/plain; charset=utf-8")
        res.Write([]byte("Hello World\n"))

    default:
        res.Header().Set("X-User", "tom")
        res.Header().Set("Content-Type", "application/json; charset=utf-8")
        var message []byte = []byte("{\"message\":\"greeting from host\"}\n")
        res.Write(message)
    }

}
```

```shell
$ curl -v  -X GET localhost:8000 
Note: Unnecessary use of -X or --request, GET is already inferred.
* Rebuilt URL to: localhost:8000/
*   Trying ::1...
* TCP_NODELAY set
* Connected to localhost (::1) port 8000 (#0)
> GET / HTTP/1.1
> Host: localhost:8000
> User-Agent: curl/7.54.0
> Accept: */*
> 
< HTTP/1.1 200 OK
< Date: Mon, 25 May 2020 11:18:09 GMT
< Content-Length: 56
< Content-Type: text/plain; charset=utf-8
< 
Received a GET request
{"message":"greeting from host"}
* Connection #0 to host localhost left intact
mario:bin arunsah$ 
mario:bin arunsah$ 
mario:bin arunsah$ curl -v  -X POST localhost:8000 
* Rebuilt URL to: localhost:8000/
*   Trying ::1...
* TCP_NODELAY set
* Connected to localhost (::1) port 8000 (#0)
> POST / HTTP/1.1
> Host: localhost:8000
> User-Agent: curl/7.54.0
> Accept: */*
> 
< HTTP/1.1 200 OK
< Date: Mon, 25 May 2020 11:18:28 GMT
< Content-Length: 57
< Content-Type: text/plain; charset=utf-8
< 
Received a POST request
{"message":"greeting from host"}
* Connection #0 to host localhost left intact
mario:bin arunsah$ 
```

- For`GET` request, data re sent though `query string`. **Always quote the url while sending multiple query stings with curl else only first query string is sent others are ignored**. Eg, `curl -v -X GET "localhost:8000/api/fruit?name=apple&price=150"`, `curl -si "http://localhost:8000/api/fruit?foo=1&bar=2"`

```go
for k, v := range req.URL.Query() {
    fmt.Printf("%s: %s\n", k, v)
}
```

- For `POST` request, data is sent through request body. `curl -si -X POST -d "some data to send" http://localhost:8000/api/fruit`

```go
reqBody, err := ioutil.ReadAll(req.Body)
if err != nil {
    log.Fatal(err)
}
fmt.Printf("%s", reqBody)
```

```go

func main() {

    const host string = ":8000"
    fmt.Printf("Server is running at %s...\n", host)
    http.HandleFunc("/", rootHandler)
    http.HandleFunc("/api/fruit", apiHandler)
    http.ListenAndServe(host, nil)
}

func apiHandler(res http.ResponseWriter, req *http.Request) {
    fmt.Printf("%+v\n", res)
    fmt.Printf("%+v\n", req)

    // query string are availabe as map of strings
    fmt.Printf("%+v\n", req.URL.Query())

    // request method type
    fmt.Printf("%+v\n", req.Method)

    // header info
    fmt.Printf("%+v\n", req.Header)

    switch req.Method {
    case "GET":
        for k, v := range req.URL.Query() {
            fmt.Printf("%s: %s\n", k, v)
        }

        message, err := json.Marshal(req.URL.Query())
        if err != nil {
            fmt.Println(err)
        }
        var buffer []byte = []byte(message)
        res.Write(buffer)
    case "POST":
        reqBody, err := ioutil.ReadAll(req.Body)
        if err != nil {
            log.Fatal(err)
        }

        fmt.Printf("%s\n", reqBody)
        res.Write([]byte("Received a POST request! " + string(reqBody) + " \n"))
    default:
        res.WriteHeader(http.StatusNotImplemented)
        res.Write([]byte(http.StatusText(http.StatusNotImplemented)))
    }

}

```

```shell
# client request

$ curl -v -X GET "localhost:8000/api/fruit?name=apple&price=150"
Note: Unnecessary use of -X or --request, GET is already inferred.
*   Trying ::1...
* TCP_NODELAY set
* Connected to localhost (::1) port 8000 (#0)
> GET /api/fruit?name=apple&price=150 HTTP/1.1
> Host: localhost:8000
> User-Agent: curl/7.54.0
> Accept: */*
> 
< HTTP/1.1 200 OK
< Date: Mon, 25 May 2020 11:56:15 GMT
< Content-Length: 34
< Content-Type: text/plain; charset=utf-8
< 
* Connection #0 to host localhost left intact
{"name":["apple"],"price":["150"]}

$ curl -v -X POST localhost:8000/api/fruit -d "{\"message\":\"hello world\"}"
Note: Unnecessary use of -X or --request, POST is already inferred.
*   Trying ::1...
* TCP_NODELAY set
* Connected to localhost (::1) port 8000 (#0)
> POST /api/fruit HTTP/1.1
> Host: localhost:8000
> User-Agent: curl/7.54.0
> Accept: */*
> Content-Length: 25
> Content-Type: application/x-www-form-urlencoded
> 
* upload completely sent off: 25 out of 25 bytes
< HTTP/1.1 200 OK
< Date: Mon, 25 May 2020 11:57:04 GMT
< Content-Length: 52
< Content-Type: text/plain; charset=utf-8
< 
Received a POST request! {"message":"hello world"} 
* Connection #0 to host localhost left intact

```

- Always sanitize user inputs.
- `http` package uses `ServeMux` to handle routing and does not support regular expression and variables in url eg `/api/fruits/:id` where `:id` is variable.
- ⭐️ **TODO**: create routers that supports variables, request method type, content type integrated with `http`.
- ⭐️ **TODO**: `ListenAndServeTLS` supports HTTPS and requires certificate and key files as parameters.
- ⭐️ **TODO**: `POST` file and handle multipart data.

[↑](https://arunsah.github.io/gonotes#table-of-content)



## 19. HTTP Clients with Go

```shell
$ curl -s -o /dev/null -v http://google.com
* Rebuilt URL to: http://google.com/
*   Trying 172.217.166.78...
* TCP_NODELAY set
* Connected to google.com (172.217.166.78) port 80 (#0)
> GET / HTTP/1.1
> Host: google.com
> User-Agent: curl/7.54.0
> Accept: */*
> 
< HTTP/1.1 301 Moved Permanently
< Location: http://www.google.com/
< Content-Type: text/html; charset=UTF-8
< Date: Mon, 25 May 2020 12:12:38 GMT
< Expires: Wed, 24 Jun 2020 12:12:38 GMT
< Cache-Control: public, max-age=2592000
< Server: gws
< Content-Length: 219
< X-XSS-Protection: 0
< X-Frame-Options: SAMEORIGIN
< 
{ [219 bytes data]
* Connection #0 to host google.com left intact
mario:bin arunsah$ 


$ curl -v http://google.com
* Rebuilt URL to: http://google.com/
*   Trying 172.217.166.78...
* TCP_NODELAY set
* Connected to google.com (172.217.166.78) port 80 (#0)
> GET / HTTP/1.1
> Host: google.com
> User-Agent: curl/7.54.0
> Accept: */*
> 
< HTTP/1.1 301 Moved Permanently
< Location: http://www.google.com/
< Content-Type: text/html; charset=UTF-8
< Date: Mon, 25 May 2020 12:15:12 GMT
< Expires: Wed, 24 Jun 2020 12:15:12 GMT
< Cache-Control: public, max-age=2592000
< Server: gws
< Content-Length: 219
< X-XSS-Protection: 0
< X-Frame-Options: SAMEORIGIN
< 
<HTML><HEAD><meta http-equiv="content-type" content="text/html;charset=utf-8">
<TITLE>301 Moved</TITLE></HEAD><BODY>
<H1>301 Moved</H1>
The document has moved
<A HREF="http://www.google.com/">here</A>.
</BODY></HTML>
* Connection #0 to host google.com left intact
```

- Chrome DevTools is available at https://developer.chrome.com/devtools can be used in alternative to `curl`.
- `DumpRequestOut` and `DumpResponse` methods from `net/http/httputil` are useful for debugging http request.

```go
func main() {

    func() { // GET client
        res, err := http.Get("https://ifconfig.co/")
        if err != nil {
            log.Fatal(err)
        }
        defer res.Body.Close()

        body, err := ioutil.ReadAll(res.Body)
        if err != nil {
            log.Fatal(err)
        }
        fmt.Printf("%s", string(body)) // 103.141.116.250

    }()

    func() { // POST client
        data := strings.NewReader(`{"message":"hello world"}`)
        // httpbin is client test tool
        res, err := http.Post("https://httpbin.org/post", "application/json", data)
        if err != nil {
            log.Fatal(err)
        }
        defer res.Body.Close()
        body, err := ioutil.ReadAll(res.Body)
        if err != nil {
            log.Fatal(err)
        }
        fmt.Printf("%s", string(body))
        /*
            {
                "args": {},
                "data": "{\"message\":\"hello world\"}",
                "files": {},
                "form": {},
                "headers": {
                  "Accept-Encoding": "gzip",
                  "Content-Length": "25",
                  "Content-Type": "application/json",
                  "Host": "httpbin.org",
                  "User-Agent": "Go-http-client/2.0",
                  "X-Amzn-Trace-Id": "Root=1-5ecbba08-5009e3a08e6d1da89d88dd78"
                },
                "json": {
                  "message": "hello world"
                },
                "origin": "103.141.116.250",
                "url": "https://httpbin.org/post"
              }
        */
    }()

    func() { // custom client (recommended to use custom client)
        client := &http.Client{} // new client created
        fmt.Println("Custom HTTP Client:")
        /*
            $ DEBUG=1 go run httpClient.go  # for linux
            $ set DEBUG=1 # for windows
            $ go run httpClient.go
        */

        debug := os.Getenv("DEBUG")

        req, err := http.NewRequest("GET", "https://ifconfig.co/", nil)
        if err != nil {
            log.Fatal(err)
        }

        if debug == "1" {
            debugReq, err := httputil.DumpRequestOut(req, true)
            if err != nil {
                log.Fatal(err)
            }
            fmt.Printf("%s", string(debugReq))
        }

        res, err := client.Do(req) // send req and handle res
        if err != nil {
            log.Fatal(err)
        }
        defer res.Body.Close()

        if debug == "1" {
            debugRes, err := httputil.DumpResponse(res, true)
            if err != nil {
                log.Fatal(err)
            }
            fmt.Printf("%s", string(debugRes))
        }
        body, err := ioutil.ReadAll(res.Body)
        fmt.Printf("%s", string(body)) // 103.141.116.250

    }()
} //end of main


```

```shell
$ go run httpClient.go 
103.141.116.250
{
  "args": {}, 
  "data": "{\"message\":\"hello world\"}", 
  "files": {}, 
  "form": {}, 
  "headers": {
    "Accept-Encoding": "gzip", 
    "Content-Length": "25", 
    "Content-Type": "application/json", 
    "Host": "httpbin.org", 
    "User-Agent": "Go-http-client/2.0", 
    "X-Amzn-Trace-Id": "Root=1-5ecbbf77-e190853c3e155f6088595828"
  }, 
  "json": {
    "message": "hello world"
  }, 
  "origin": "103.141.116.250", 
  "url": "https://httpbin.org/post"
}
Custom HTTP Client:
103.141.116.250
mario:gonotes arunsah$ echo $DEBUG

mario:gonotes arunsah$ DEBUG=1 go run httpClient.go
<!DOCTYPE html>
<html>
<head>
<meta name="viewport" content="width=device-width, initial-scale=1">
<meta charset="utf-8">
<title>Application Error</title>
<style media="screen">
                  html,body,iframe {
                        margin: 0;
                        padding: 0;
                  }
                  html,body {
                        height: 100%;
                        overflow: hidden;
                  }
                  iframe {
                        width: 100%;
                        height: 100%;
                        border: 0;
                  }
                </style>
<script async src='/cdn-cgi/bm/cv/1284585713/api.js'></script></head>
<body>
<iframe src="//www.herokucdn.com/error-pages/application-error.html"></iframe>
<script type="text/javascript">(function(){window['__CF$cv$params']={r:'598f6526eba8ce1f',m:'19516d0da73ba4d116a4651e966caf7fd3b6aba9-1590411162-1800-ASxy4XIrcwvDIIjf1ooXsjWNgt/Sq4wII13LfC7A9D/iZe3SC+L1g8lKxq2mAgwh2pvpms8ki2Vx2xy7y0shUZbFPx4RlIj/htmlQM5s+Z83+PItPNy/gKCv/G+dSo6Owg==',s:[0xde2e8d91fa,0x50360c8fda],}})();</script></body>
</html>{
  "args": {}, 
  "data": "{\"message\":\"hello world\"}", 
  "files": {}, 
  "form": {}, 
  "headers": {
    "Accept-Encoding": "gzip", 
    "Content-Length": "25", 
    "Content-Type": "application/json", 
    "Host": "httpbin.org", 
    "User-Agent": "Go-http-client/2.0", 
    "X-Amzn-Trace-Id": "Root=1-5ecbbf9b-1bf187a89a099f4c181aef8e"
  }, 
  "json": {
    "message": "hello world"
  }, 
  "origin": "103.141.116.250", 
  "url": "https://httpbin.org/post"
}
Custom HTTP Client:
GET / HTTP/1.1
Host: ifconfig.co
User-Agent: Go-http-client/1.1
Accept-Encoding: gzip

HTTP/2.0 200 OK
Content-Length: 16
Cf-Cache-Status: DYNAMIC
Cf-Ray: 598f652cfeeece1f-LHR
Cf-Request-Id: 02ed7d90190000ce1fee34b200000001
Content-Type: text/plain; charset=utf-8
Date: Mon, 25 May 2020 12:52:45 GMT
Expect-Ct: max-age=604800, report-uri="https://report-uri.cloudflare.com/cdn-cgi/beacon/expect-ct"
Server: cloudflare
Set-Cookie: __cfduid=d1398c5ecb81b079073888820025099ef1590411163; expires=Wed, 24-Jun-20 12:52:43 GMT; path=/; domain=.ifconfig.co; HttpOnly; SameSite=Lax
Set-Cookie: __cf_bm=4ffc17a78485c5626caf8b090885c40bbfe4224f-1590411165-1800-AcpsUtGvuRcYeQmmdGaBi9KHEL8FnUfYbiYZteIBBcpRrQYTCWGJDhpGsRzdTBSdi03MpVzNoLTcPE1Zl10NjRA=; path=/; expires=Mon, 25-May-20 13:22:45 GMT; domain=.ifconfig.co; HttpOnly; Secure; SameSite=None
Via: 1.1 vegur

103.141.116.250
103.141.116.250
mario:gonotes arunsah$ 
mario:gonotes arunsah$ 
mario:gonotes arunsah$ echo $DEBUG

mario:gonotes arunsah$ 
```

- To request json data `req.Header.Add("Accept", "application/json")`

```go
func() { // custom client (recommended to use custom client)
    client := &http.Client{} // new client created
    fmt.Println("Custom HTTP Client:")
    /*
        $ DEBUG=1 go run httpClient.go  # for linux
        $ set DEBUG=1 # for windows
        $ go run httpClient.go
    */

    debug := os.Getenv("DEBUG")

    req, err := http.NewRequest("GET", "https://ifconfig.co/", nil)
    if err != nil {
        log.Fatal(err)
    }
    req.Header.Add("Accept", "application/json")

    if debug == "1" {
        debugReq, err := httputil.DumpRequestOut(req, true)
        if err != nil {
            log.Fatal(err)
        }
        fmt.Printf("%s", string(debugReq))
    }

    res, err := client.Do(req) // send req and handle res
    if err != nil {
        log.Fatal(err)
    }
    defer res.Body.Close()

    if debug == "1" {
        debugRes, err := httputil.DumpResponse(res, true)
        if err != nil {
            log.Fatal(err)
        }
        fmt.Printf("%s", string(debugRes))
    }
    body, err := ioutil.ReadAll(res.Body)
    fmt.Printf("%s", string(body)) // 103.141.116.250

}()

```

```shell
Custom HTTP Client:
GET / HTTP/1.1
Host: ifconfig.co
User-Agent: Go-http-client/1.1
Accept: application/json
Accept-Encoding: gzip

HTTP/2.0 200 OK
Cf-Cache-Status: DYNAMIC
Cf-Ray: 598f6ceb585e0652-LHR
Cf-Request-Id: 02ed826717000006527f02e200000001
Content-Type: application/json
Date: Mon, 25 May 2020 12:58:01 GMT
Expect-Ct: max-age=604800, report-uri="https://report-uri.cloudflare.com/cdn-cgi/beacon/expect-ct"
Server: cloudflare
Set-Cookie: __cfduid=d74f118ee7dded9977cce090362a454221590411480; expires=Wed, 24-Jun-20 12:58:00 GMT; path=/; domain=.ifconfig.co; HttpOnly; SameSite=Lax
Set-Cookie: __cf_bm=39ac53bbaf02fa7f7ce357872c958163e256028c-1590411481-1800-Ac82tC1HwuFOw1zVggh04pl+lWh1pkkyN1tibX5RMP1SvxagFu1GEALEsROk59A6TpwGInMppGeycm6Xtg9suw4=; path=/; expires=Mon, 25-May-20 13:28:01 GMT; domain=.ifconfig.co; HttpOnly; Secure; SameSite=None
Via: 1.1 vegur

{"ip":"103.141.116.250","ip_decimal":1737323770,"country":"India","country_iso":"IN","country_eu":false,"region_name":"Maharashtra","region_code":"MH","zip_code":"411005","city":"Pune","latitude":18.5213,"longitude":73.8523,"time_zone":"Asia/Kolkata","asn":"AS138798","asn_org":"Mutiny Systems Private Limited","user_agent":{"product":"Go-http-client","version":"2.0","raw_value":"Go-http-client/2.0"}}{"ip":"103.141.116.250","ip_decimal":1737323770,"country":"India","country_iso":"IN","country_eu":false,"region_name":"Maharashtra","region_code":"MH","zip_code":"411005","city":"Pune","latitude":18.5213,"longitude":73.8523,"time_zone":"Asia/Kolkata","asn":"AS138798","asn_org":"Mutiny Systems Private Limited","user_agent":{"product":"Go-http-client","version":"2.0","raw_value":"Go-http-client/2.0"}}mario:gonotes arunsah$ 
```

- Response time depends on number of a factory and are variables. It may depends on speed of:
	- dns lookup
	- opening tcp socket to server IP.
	- establishing a tcp connection
	- tls handshake 
	- sending data to server.
	- any redirects.
	- server returning response
	- data returned to client
- Default http client does not timeout. Add timeout as `client := &http.Client{Timeout: 2000 * time.Millisecond}`

```shell
# timeout set for 50ms
$ DEBUG=1 go run httpClient.go
103.141.116.250
{
  "args": {}, 
  "data": "{\"message\":\"hello world\"}", 
  "files": {}, 
  "form": {}, 
  "headers": {
    "Accept-Encoding": "gzip", 
    "Content-Length": "25", 
    "Content-Type": "application/json", 
    "Host": "httpbin.org", 
    "User-Agent": "Go-http-client/2.0", 
    "X-Amzn-Trace-Id": "Root=1-5ecbc28c-c7946e1c77d1b6746f2b8730"
  }, 
  "json": {
    "message": "hello world"
  }, 
  "origin": "103.141.116.250", 
  "url": "https://httpbin.org/post"
}
Custom HTTP Client:
GET / HTTP/1.1
Host: ifconfig.co
User-Agent: Go-http-client/1.1
Accept: application/json
Accept-Encoding: gzip

2020/05/25 18:32:43 Get https://ifconfig.co/: net/http: request canceled (Client.Timeout exceeded while awaiting headers)
exit status 1
mario:gonotes arunsah$ 

```

- For fine grain controls.

```go
tr := &http.Transport{
    DialContext: (&net.Dialer{
        Timeout:   30 * time.Second,
        KeepAlive: 30 * time.Second,
    }).DialContext,
    TLSHandshakeTimeout:   10 * time.Second,
    IdleConnTimeout:       90 * time.Second,
    ResponseHeaderTimeout: 10 * time.Second,
    ExpectContinueTimeout: 1 * time.Second,
}

client := &http.Client{
    Transport: tr,
}

```

```go
func() { // custom client (recommended to use custom client)
    //client := &http.Client{Timeout: 50 * time.Millisecond} // new client created

    // for fine grain controls
    tr := &http.Transport{
        DialContext: (&net.Dialer{
            Timeout:   30 * time.Second,
            KeepAlive: 30 * time.Second,
        }).DialContext,
        TLSHandshakeTimeout:   10 * time.Second,
        IdleConnTimeout:       90 * time.Second,
        ResponseHeaderTimeout: 10 * time.Second,
        ExpectContinueTimeout: 1 * time.Second,
    }

    client := &http.Client{
        Transport: tr,
    }

    fmt.Println("Custom HTTP Client:")
    /*
        $ DEBUG=1 go run httpClient.go  # for linux
        $ set DEBUG=1 # for windows
        $ go run httpClient.go
    */

    debug := os.Getenv("DEBUG")

    req, err := http.NewRequest("GET", "https://ifconfig.co/", nil)
    if err != nil {
        log.Fatal(err)
    }
    req.Header.Add("Accept", "application/json")

    if debug == "1" {
        debugReq, err := httputil.DumpRequestOut(req, true)
        if err != nil {
            log.Fatal(err)
        }
        fmt.Printf("%s", string(debugReq))
    }

    res, err := client.Do(req) // send req and handle res
    if err != nil {
        log.Fatal(err)
    }
    defer res.Body.Close()

    if debug == "1" {
        debugRes, err := httputil.DumpResponse(res, true)
        if err != nil {
            log.Fatal(err)
        }
        fmt.Printf("%s", string(debugRes))
    }
    body, err := ioutil.ReadAll(res.Body)
    fmt.Printf("%s", string(body)) // 103.141.116.250

}()

```

- `res.StatusCode` can be used to alter the logic based on status code.
- `NewRequest` should be used to have more controls over request headers.
- `http://google.com/404` is seems to be static page.

[↑](https://arunsah.github.io/gonotes#table-of-content)



## 20. JSON

- struct tags helps to fine control json.
- **Protobuf Performance Comparison and Points to Consider When Deciding If It’s Right For You**
 https://dzone.com/articles/protobuf-performance-comparison-and-points-to-make
Struct tag can be use to profile comparable camelCase name for fields and to omit empty fields in struct from being encoded to JSON. 

```go
// Person signifies person entity
type Person struct {
    Name  string   `json:"name,omitempty"`
    Age   int      `json:"age,omitempty"`
    Likes []string `json:"likes,omitempty"`
}

```

- Datatype mapping in JSON vs Go: `Boolean: bool, Number: float64, String: string, Array: []interface{}, Object: map[string]interface{}, Null:nil`
- Error is thrown if data type does not matches.

```go
package main

import (
    json "encoding/json"
    "fmt"
    "log"
)

// Person signifies person entity
type Person struct {
    Name  string   `json:"name,omitempty"`
    Age   int      `json:"age,omitempty"`
    Likes []string `json:"likes,omitempty"`
}

func main() {
    tom := Person{
        Name:  "tom",
        Age:   8,
        Likes: []string{"painting", "chocolates", "treking"},
    }
    // NOTE: Go struct are having PascalCase properties
    // while JSON have camelCase properties.
    // Use go struct tags eg. `json:"name"`
    // {Name:tom Age:8 Likes:[painting chocolates treking]}
    fmt.Printf("tom = %+v\n", tom)

    tomByteJSON, err := json.Marshal(tom)
    if err != nil {
        log.Fatal(err)
    }
    tomJSON := string(tomByteJSON)
    // {"Name":"tom","Age":8,"Likes":["painting","chocolates","treking"]}
    // after go struct tags
    // {"name":"tom","age":8,"likes":["painting","chocolates","treking"]}
    fmt.Printf("tomJSON = %+v\n", tomJSON)

    tomDecoded := Person{}
    errTomDecoded := json.Unmarshal([]byte(tomJSON), &tomDecoded)
    if errTomDecoded != nil {
        log.Fatal(err)
    }
    // tomDecoded = {Name:tom Age:8 Likes:[painting chocolates treking]}
    fmt.Printf("tomDecoded = %+v\n", tomDecoded)

    emptyPerson := &Person{}
    fmt.Printf("%+v\n", emptyPerson) // &{Name: Age:0 Likes:[]}
    emptyByteJSON, err := json.Marshal(emptyPerson)
    if err != nil {
        log.Fatal(err)
    }
    emptyJSON := string(emptyByteJSON)
    fmt.Printf("emptyJSON = %+v\n", emptyJSON) // {}


} //end of main

```


- For stream data `NewDecoder` from `encoding/json` is used, it expects `io.Reader` (returned by `http.Get` and returns a Decoder type. It decodes data into (expects) struct.


- Use online tool eg [JSON-to-Go: Convert JSON to Go instantly](https://mholt.github.io/json-to-go/) 

```json
{
  "login": "arunsah",
  "id": 25679050,
  "node_id": "MDQ6VXNlcjI1Njc5MDUw",
  "avatar_url": "https://avatars3.githubusercontent.com/u/25679050?v=4",
  "gravatar_id": "",
  "url": "https://api.github.com/users/arunsah",
  "html_url": "https://github.com/arunsah",
  "followers_url": "https://api.github.com/users/arunsah/followers",
  "following_url": "https://api.github.com/users/arunsah/following{/other_user}",
  "gists_url": "https://api.github.com/users/arunsah/gists{/gist_id}",
  "starred_url": "https://api.github.com/users/arunsah/starred{/owner}{/repo}",
  "subscriptions_url": "https://api.github.com/users/arunsah/subscriptions",
  "organizations_url": "https://api.github.com/users/arunsah/orgs",
  "repos_url": "https://api.github.com/users/arunsah/repos",
  "events_url": "https://api.github.com/users/arunsah/events{/privacy}",
  "received_events_url": "https://api.github.com/users/arunsah/received_events",
  "type": "User",
  "site_admin": false,
  "name": "Arun",
  "company": null,
  "blog": "",
  "location": "Pune, India",
  "email": null,
  "hireable": null,
  "bio": "Hi, I am Arun. This profile hosts my personal projects. Primary languages: Java, C++, Go, Javascript. Interested: backend developer;",
  "public_repos": 16,
  "public_gists": 3,
  "followers": 2,
  "following": 27,
  "created_at": "2017-02-10T04:54:36Z",
  "updated_at": "2020-05-09T18:05:05Z"
}
```

```go
type AutoGenerated struct {
	Login             string      `json:"login"`
	ID                int         `json:"id"`
	NodeID            string      `json:"node_id"`
	AvatarURL         string      `json:"avatar_url"`
	GravatarID        string      `json:"gravatar_id"`
	URL               string      `json:"url"`
	HTMLURL           string      `json:"html_url"`
	FollowersURL      string      `json:"followers_url"`
	FollowingURL      string      `json:"following_url"`
	GistsURL          string      `json:"gists_url"`
	StarredURL        string      `json:"starred_url"`
	SubscriptionsURL  string      `json:"subscriptions_url"`
	OrganizationsURL  string      `json:"organizations_url"`
	ReposURL          string      `json:"repos_url"`
	EventsURL         string      `json:"events_url"`
	ReceivedEventsURL string      `json:"received_events_url"`
	Type              string      `json:"type"`
	SiteAdmin         bool        `json:"site_admin"`
	Name              string      `json:"name"`
	Company           interface{} `json:"company"`
	Blog              string      `json:"blog"`
	Location          string      `json:"location"`
	Email             interface{} `json:"email"`
	Hireable          interface{} `json:"hireable"`
	Bio               string      `json:"bio"`
	PublicRepos       int         `json:"public_repos"`
	PublicGists       int         `json:"public_gists"`
	Followers         int         `json:"followers"`
	Following         int         `json:"following"`
	CreatedAt         time.Time   `json:"created_at"`
	UpdatedAt         time.Time   `json:"updated_at"`
}
```

- It is not required to mapped all json fields to go, only required fields can be mapped.

```go


func main() {
    tom := Person{
        Name:  "tom",
        Age:   8,
        Likes: []string{"painting", "chocolates", "treking"},
    }
    // NOTE: Go struct are having PascalCase properties
    // while JSON have camelCase properties.
    // Use go struct tags eg. `json:"name"`
    // {Name:tom Age:8 Likes:[painting chocolates treking]}
    fmt.Printf("tom = %+v\n", tom)

    tomByteJSON, err := json.Marshal(tom)
    if err != nil {
        log.Fatal(err)
    }
    tomJSON := string(tomByteJSON)
    // {"Name":"tom","Age":8,"Likes":["painting","chocolates","treking"]}
    // after go struct tags
    // {"name":"tom","age":8,"likes":["painting","chocolates","treking"]}
    fmt.Printf("tomJSON = %+v\n", tomJSON)

    tomDecoded := Person{}
    errTomDecoded := json.Unmarshal([]byte(tomJSON), &tomDecoded)
    if errTomDecoded != nil {
        log.Fatal(err)
    }
    // tomDecoded = {Name:tom Age:8 Likes:[painting chocolates treking]}
    fmt.Printf("tomDecoded = %+v\n", tomDecoded)

    emptyPerson := &Person{}
    fmt.Printf("%+v\n", emptyPerson) // &{Name: Age:0 Likes:[]}
    emptyByteJSON, err := json.Marshal(emptyPerson)
    if err != nil {
        log.Fatal(err)
    }
    emptyJSON := string(emptyByteJSON)
    fmt.Printf("emptyJSON = %+v\n", emptyJSON) // {}

    func() { // working with json from api

        type User struct {
            Name     string `json:"name"`
            Location string `json:"location"`
        }

        res, err := http.Get("https://api.github.com/users/arunsah")
        if err != nil {
            log.Fatal(err)
        }
        defer res.Body.Close()

        u := User{}
        err = json.NewDecoder(res.Body).Decode(&u)
        if err != nil {
            log.Fatal(err)
        }

        fmt.Printf("%+v\n", u) // {Name:Arun Location:Pune, India}
    }()

} //end of main

```

[↑](https://arunsah.github.io/gonotes#table-of-content)



## 21. Files

- Unix system, everything is treated as file. Process information are virtual fs.

```shell
# shows realtime load on the system
$ cat /proc/loadavg

# watch command can be use to create a real time view of the system load
$ watch cat /proc/loadavg

```

- `ioutil` is wrapper for `os` module.

#### File Permissions

- Unix file permission is for 3 level: owner permission, same group permission and everyone else. File permission are often assigned with Octal Notation. There are 10 character in symbolic notation. Left most value represent it is a regular file, a directory or something else.
 	- `-rwxrwxrwx` = `0777`: owner (`rwx`), group (`rwx`) and others (`rwx`). [All Permission]
	- `-rwx------` = `0700`: owner (`rwx`), group (`---`) and others (`---`).
	-  `-r--r--r--` = `0444`: owner (`r--`), group (`r--`) and others (`r--`).[All Read Permission]
	- `----------` = `0000`: owner (`---`), group (`---`) and others (`---`). [No permission]

```
| Octal | Bin | Mode |
|-------|-----|------|
| 0     | 000 | ---  |
| 1     | 001 | --x  |
| 2     | 010 | -w-  |
| 3     | 011 | -wx  |
| 4     | 100 | r--  |
| 5     | 101 | r-x  |
| 6     | 110 | rw-  |
| 7     | 111 | rwx  |

```

- Item type:
	- (-) file
	- (d) directory
	- (l) symbolic link
	- (b) block special file
	- (c) character special file
	- (p) named pipe special file
	- (s) local socket special file

- Changing file permission:
	- `chmod g+w file` provide write access to group
	- `chmod o-x file` remove execute access from others
	- `chmod 444 file` absolute access, provide read only access to all.
	- `chmod g+r dir -R` recursively provide read only access to group.
	- `0644` commonly used file permission
	- [Unix Permissions](https://networking.ringofsaturn.com/Unix/unixpermissions.php)

- `WriteFile` will Crete file id it does not exists.

- BurntSushi https://github.com/BurntSushi/toml makes uses of TOML configuration file easy. `go get github.com/BurntSushi/toml`

```go
package main

import (
    json "encoding/json"
    "fmt"
    "io"
    "io/ioutil"
    "log"
    "os"

    "github.com/BurntSushi/toml"
)

func main() {

    func(execute bool) { // read file
        if !execute {
            return
        }
        fmt.Println("Reading the file")
        fileBytes, err := ioutil.ReadFile("hello.txt")
        if err != nil {
            //log.Fatal(err)
            fmt.Println(err)
        }

        fmt.Println(fileBytes)
        fmt.Println(string(fileBytes))
    }(true)

    func(execute bool) { // create file using WriteFile
        if !execute {
            return
        }
        fmt.Println("Creating empty file: hello-empty-file.txt")
        emptyBuffer := make([]byte, 0) // to create empty file
        // will create empty file if file does not exist
        err := ioutil.WriteFile("hello-empty-file.txt", emptyBuffer, 0644)
        if err != nil {
            log.Fatal(err)
        }

        fmt.Println("Creating data file: hello-world-in-file.txt")
        dataBuffer := []byte("hello world written in file")
        err = ioutil.WriteFile("hello-world-in-file.txt", dataBuffer, 0644)
        if err != nil {
            log.Fatal(err)
        }

    }(true)

    func(execute bool) { // listing directory
        if !execute {
            return
        }
        fmt.Println("Listing directory")

        // list of dir sorted by filename
        files, err := ioutil.ReadDir(".")
        if err != nil {
            log.Fatal(err)
        }

        /*
            hellofiles.go 2881 -rw-r--r-- 2020-05-27 15:41:20.939901423 +0530 IST false &{16777220 33188 1 8529145 501 20 0 [0 0 0 0] {1590574284 394716429} {1590574280 939901423} {1590574280 939901423} {1590500478 595160714} 2881 8 4096 0 0 0 [0 0]}

            &{name:hello size:2132976 mode:493 modTime:{wall:674189210 ext:63725947358 loc:0x11879c0} sys:{Dev:16777220 Mode:33261 Nlink:1 Ino:8419306 Uid:501 Gid:20 Rdev:0 Pad_cgo_0:[0 0 0 0] Atimespec:{Sec:1590414877 Nsec:982075861} Mtimespec:{Sec:1590350558 Nsec:674189210} Ctimespec:{Sec:1590350558 Nsec:674536163} Birthtimespec:{Sec:1590350558 Nsec:525200783} Size:2132976 Blocks:4168 Blksize:4096 Flags:0 Gen:0 Lspare:0 Qspare:[0 0]}}
            &{name:hellofiles.go size:1484 mode:420 modTime:{wall:280571092 ext:63726170764 loc:0x11879c0} sys:{Dev:16777220 Mode:33188 Nlink:1 Ino:8529145 Uid:501 Gid:20 Rdev:0 Pad_cgo_0:[0 0 0 0] Atimespec:{Sec:1590573967 Nsec:562322309} Mtimespec:{Sec:1590573964 Nsec:280571092} Ctimespec:{Sec:1590573964 Nsec:280571092} Birthtimespec:{Sec:1590500478 Nsec:595160714} Size:1484 Blocks:8 Blksize:4096 Flags:0 Gen:0 Lspare:0 Qspare:[0 0]}}
            &{name:vendor size:64 mode:2147484141 modTime:{wall:346929931 ext:63725908975 loc:0x11879c0} sys:{Dev:16777220 Mode:16877 Nlink:2 Ino:8392760 Uid:501 Gid:20 Rdev:0 Pad_cgo_0:[0 0 0 0] Atimespec:{Sec:1590563660 Nsec:236236876} Mtimespec:{Sec:1590312175 Nsec:346929931} Ctimespec:{Sec:1590312175 Nsec:346929931} Birthtimespec:{Sec:1590312175 Nsec:346929931} Size:64 Blocks:0 Blksize:4096 Flags:0 Gen:0 Lspare:0 Qspare:[0 0]}}
        */

        for _, file := range files {
            fmt.Printf("%+v\n", file)
            fmt.Println(file.Name(), file.Size(), file.Mode(), file.ModTime(), file.IsDir(), file.Sys()) // Sys: underlying data source
        }

    }(true)

    func(execute bool) { // copy file
        if !execute {
            return
        }
        fmt.Println("Copy file")
        // for complex operatin use `os` package
        src := "hello-world-in-file.txt"
        dest := "hello-world-in-file-copy.txt"
        srcFile, err := os.Open(src)
        if err != nil {
            log.Fatal(err)
        }
        defer srcFile.Close()

        destFile, err := os.OpenFile(dest, os.O_RDWR|os.O_CREATE, 0666)
        if err != nil {
            log.Fatal(err)
        }
        defer destFile.Close()

        _, err = io.Copy(destFile, srcFile)
        if err != nil {
            log.Fatal(err)
        }

    }(true)

    func(execute bool) { // delete file
        if !execute {
            return
        }
        fmt.Println("Delete file : hello-world-in-file-copy.txt")
        err := os.Remove("hello-world-in-file-copy.txt")
        if err != nil {
            log.Fatal(err)
        }

    }(true)

    func(execute bool) { // manage configuration using json file
        if !execute {
            return
        }
        fmt.Println("manage configuration using json file")
        // using menu.json

        type MenuItem struct {
            Value   string `json:"value"`
            OnClick string `json:"onclick"`
        }

        type Menu struct {
            MenuItem []MenuItem `json:"menuitem"`
        }

        file, err := ioutil.ReadFile("menu.json")
        if err != nil {
            log.Fatal(err)
        }
        menu := Menu{}
        err = json.Unmarshal(file, &menu)
        if err != nil {
            log.Fatal(err)
        }
        // {MenuItem:[{Value:New OnClick:CreateNewDoc()} {Value:Open OnClick:OpenDoc()} {Value:Close OnClick:CloseDoc()}]}
        fmt.Printf("%+v\n", menu)
    }(true)

    func(execute bool) { // manage configuration using TOML file
        if !execute {
            return
        }
        fmt.Println("manage configuration using TOML file")
        // TOML: Tom Obvious Minimal Language https://github.com/toml-lang/toml
        // is popular in go cummunity as it maps more closely to go types.
        // JSON is designed for serializing data files
        // TOML is designed for configuration files

        type MenuItem struct {
            Value   string
            OnClick string
        }

        menuItem := MenuItem{}
        _, err := toml.DecodeFile("menu.toml", &menuItem)
        if err != nil {
            log.Fatal(err)
        }
        // {Value:New OnClick:CreateNewDoc()}
        fmt.Printf("%+v\n", menuItem)

    }(true)
} //end of main

```

- `menu.toml`

```toml
Value = "New"
OnClick = "CreateNewDoc()"

```

- `menu.json`

```json
{
    "menuitem": [
      {"value": "New", "onclick": "CreateNewDoc()"},
      {"value": "Open", "onclick": "OpenDoc()"},
      {"value": "Close", "onclick": "CloseDoc()"}
    ]
  }

```

```go
t := time.Now()
fmt.Println(t.String())
fmt.Println(t.Format("2006-01-02 15:04:05"))

// 2009-11-10 23:00:00 +0000 UTC
// 2009-11-10 23:00:00


```

```go
// [Convert time.Time to string - Stack Overflow](https://stackoverflow.com/a/39287194)
package main                                                                                                                                                           

import (
    "fmt"
    "time"
)

// @link https://golang.org/pkg/time/

func main() {

    //caution : format string is `2006-01-02 15:04:05.000000000`
    current := time.Now()

    fmt.Println("origin : ", current.String())
    // origin :  2016-09-02 15:53:07.159994437 +0800 CST

    fmt.Println("mm-dd-yyyy : ", current.Format("01-02-2006"))
    // mm-dd-yyyy :  09-02-2016

    fmt.Println("yyyy-mm-dd : ", current.Format("2006-01-02"))
    // yyyy-mm-dd :  2016-09-02

    // separated by .
    fmt.Println("yyyy.mm.dd : ", current.Format("2006.01.02"))
    // yyyy.mm.dd :  2016.09.02

    fmt.Println("yyyy-mm-dd HH:mm:ss : ", current.Format("2006-01-02 15:04:05"))
    // yyyy-mm-dd HH:mm:ss :  2016-09-02 15:53:07

    // StampMicro
    fmt.Println("yyyy-mm-dd HH:mm:ss: ", current.Format("2006-01-02 15:04:05.000000"))
    // yyyy-mm-dd HH:mm:ss:  2016-09-02 15:53:07.159994

    //StampNano
    fmt.Println("yyyy-mm-dd HH:mm:ss: ", current.Format("2006-01-02 15:04:05.000000000"))
    // yyyy-mm-dd HH:mm:ss:  2016-09-02 15:53:07.159994437
}    

```

[↑](https://arunsah.github.io/gonotes#table-of-content)



## 22. Introducing Regular Expressions

- `regexp` package implements `RE2` syntax (same is for Perl/Python). It can operated on strings or bytes.
- `regexp.MatchString(pattern, text)` are case sensitive and returns bool.
- Common regex characters:
	- `.` any char except a line
	- `*` matches prev char zero or more times
	- `+` matches prev char one or more times
	- `?` matches prev char zero or one times
	- `[]` matches any char within brackets
	- `{n}` matches n times
	- `{n,}` matches n or more times
	- `{m,n}` matches at least m times and at most n times
	- `^` start of a line
	- `$` end of a line
- `^[a-zA-Z0-9]{5-10}` will match alphanumeric character of length 5-10. 
- Data validation:
	- `Compile` returns error if regex fails to compile.
	- `MustCompile` panics if it cannot compile regex.

- Transform Data:
	- clean invalid char to valid char in invalid input and transform it into valid input.

- Parsing Data:
	- `regexp.MustCompile("\\<h3\\>.*\\</h3\\>")` matches any character within h3 tag.
	- `regexp.MustCompile("<[>]*>")` matches open angle bracket and zero or more close angle bracket char.
	- `regexp.MustCompile("<[^>]*>")` matches open angle bracket and zero or more NOT close angle bracket char.

```go
package main

import (
    "fmt"
    "io/ioutil"
    "log"
    "net/http"
    "regexp"
)

func main() {

    func(execute bool) { // MatchString are case sensitive
        if !execute {
            return
        }
        fmt.Println("MatchString")
        isMatch, err := regexp.MatchString("golang", "hello world from golang")
        if err != nil {
            log.Fatal(err)
        }
        fmt.Println(isMatch) // true
        // case sensitive: f    alse <nil>
        fmt.Println(regexp.MatchString("Golang", "hello world from golang"))

        // case insensitive:    true <nil>
        fmt.Println(regexp.MatchString("(?i)Golang", "hello world from golang"))

        // case insensitive:    true <nil>
        fmt.Println(regexp.MatchString("(?i)GoLANG", "hello world from golang"))

    }(true)

    func(execute bool) { // Validate input
        if !execute {
            return
        }
        fmt.Println("Validate input")

        pattern := regexp.MustCompile("^[a-zA-Z0-9]{5,10}")
        fmt.Println(pattern.MatchString("world"))          // true
        fmt.Println(pattern.MatchString("world123"))       // true
        fmt.Println(pattern.MatchString("world123456789")) // true
        fmt.Println(pattern.MatchString("123world"))       // true
        fmt.Println(pattern.MatchString("hi"))             // false

    }(true)

    func(execute bool) { // Transform input after cleaning invalid input
        if !execute {
            return
        }
        fmt.Println("Transform input after cleaning invalid input")

        words := []string{"world", "world123", "world123456789", "hi", "!!hi123!!!", "happy#£2£3£4"}
        pattern := regexp.MustCompile("^[a-zA-Z0-9]{5,10}")
        validPttern := regexp.MustCompile(":^alnum:")

        for _, word := range words {
            fmt.Println("Original word: ", word)
            if len(word) > 10 {
                word = word[:10] // trimmed
                fmt.Println("Trimmed word: ", word)
            }

            if !pattern.MatchString(word) { // if invalid pattern
                validPttern.ReplaceAllString(word, "x")
                fmt.Println("Cleaned word: ", word)
            }

        }

    }(true)

    func(execute bool) { // Parsing data : web scrapping
        if !execute {
            return
        }
        fmt.Println("Parsing data")
        url := "https://petition.parliament.uk/petitions"

        // matched any text in h3 tag
        pattern := regexp.MustCompile("\\<h3\\>.*\\</h3\\>")

        res, err := http.Get(url)
        if err != nil {
            log.Fatal(err)
        }
        defer res.Body.Close()

        body, err := ioutil.ReadAll(res.Body)
        if err != nil {
            log.Fatal(err)
        }

        text := string(body)

        titles := pattern.FindAllString(text, -1)
        for index, title := range titles {
            fmt.Println(index, title)
        }

        fmt.Println("Clean html tags")
        cleanPattern := regexp.MustCompile("<[^>]*>")
        for index, title := range titles {
            cleanTitle := cleanPattern.ReplaceAllString(title, "")
            fmt.Println(index, cleanTitle)
        }

        // these kind of data can be feed into sentement analysis engin.

    }(true)

} //end of main

```

```
$ go run helloregs.go 
MatchString
true
false <nil>
true <nil>
true <nil>
Validate input
true
true
true
true
false
Transform input after cleaning invalid input
Original word:  world
Original word:  world123
Original word:  world123456789
Trimmed word:  world12345
Original word:  hi
Cleaned word:  hi
Original word:  !!hi123!!!
Cleaned word:  !!hi123!!!
Original word:  happy#£2£3£4
Trimmed word:  happy#£2�



Parsing data
0 <h3><a href="/petitions/300336">Include self-employed in statutory sick pay during Coronavirus</a></h3>
1 <h3><a href="/petitions/300403">Close Schools/Colleges down for an appropriate amount of time amidst COVID19.</a></h3>
2 <h3><a href="/petitions/301397">Implement UK lockdown for preventing spread of COVID19</a></h3>
3 <h3><a href="/petitions/302855">Reimburse all students of this year’s fees due to strikes and COVID-19</a></h3>
4 <h3><a href="/petitions/306691">Extend maternity leave by 3 months with pay in light of COVID-19</a></h3>
5 <h3><a href="/petitions/300073">Increase pay for NHS healthcare workers and recognise their work</a></h3>
6 <h3><a href="/petitions/301186">Government to offer economic assistance to the events industry during COVID-19</a></h3>
7 <h3><a href="/petitions/306845">Give all key workers a 100% tax and Nat. Ins. holiday through COVID-19 crisis</a></h3>
8 <h3><a href="/petitions/300528">Require universities to reimburse students&#39; tuition fees during strike action</a></h3>
9 <h3><a href="/petitions/300239">Release the Home Office&#39;s Grooming Gang Review in full</a></h3>
10 <h3><a href="/petitions/302256">Encourage lenders, landlords and utilities to freeze payments during lockdown</a></h3>
11 <h3><a href="/petitions/300628">Close all universities down for an appropriate amount of time amidst COVID-19</a></h3>
12 <h3><a href="/petitions/302284">Implement Universal Basic Income to give home &amp; food security through Covid-19</a></h3>
13 <h3><a href="/petitions/306494">Refund university students for 3rd Semester Tuition 2020</a></h3>
14 <h3><a href="/petitions/301836">Give UK nurseries emergency funding if they have to close down amid COVID-19</a></h3>
15 <h3><a href="/petitions/303274">Require councils to suspend council tax payments during the coronavirus outbreak</a></h3>
16 <h3><a href="/petitions/303081">Support the British aviation industry during the COVID-19 outbreak</a></h3>
17 <h3><a href="/petitions/300399">No prosecution for parents that remove child from school during a pandemic.</a></h3>
18 <h3><a href="/petitions/300976">Make LGBT conversion therapy illegal in the UK</a></h3>
19 <h3><a href="/petitions/300561">Replace Breed Specific Legislation with a new statutory framework</a></h3>
20 <h3><a href="/petitions/300412">Extend the transition; delay negotiations until after the coronavirus outbreak</a></h3>
21 <h3><a href="/petitions/310515">Coronavirus Support Package for Directors / Shareholders of small Limited Co&#39;s.</a></h3>
22 <h3><a href="/petitions/305129">Give non-British citizens who are NHS workers automatic citizenship</a></h3>
23 <h3><a href="/petitions/300059">Publish the Russia report</a></h3>
24 <h3><a href="/petitions/305604">Release HMP Prisoners due to COVID-19 - temporary release, licence, tag, curfew</a></h3>
25 <h3><a href="/petitions/312997">Delay 5G in the UK until there’s been an independent investigation</a></h3>
26 <h3><a href="/petitions/301033">Explore options for making NurOwn available to treat Motor Neurone Disease (MND)</a></h3>
27 <h3><a href="/petitions/300100">Make Hedgehogs a Protected Species</a></h3>
28 <h3><a href="/petitions/303345">Pay self employed workers a wage due to lack of earnings caused by COVID-19.</a></h3>
29 <h3><a href="/petitions/302897">We would like the government to consider social care as equally important to NHS</a></h3>
30 <h3><a href="/petitions/305423">Make COVID19 testing available to teaching staff caring for pupils.</a></h3>
31 <h3><a href="/petitions/311642">Cancel HS2 and use the money for the NHS and local economies, post Covid-19.</a></h3>
32 <h3><a href="/petitions/318206">Delay the reopening of schools to September</a></h3>
33 <h3><a href="/petitions/307146">Allow gyms and leisure centres to reopen</a></h3>
34 <h3><a href="/petitions/300010">Fern’s Law: Compulsory to scan &amp; check microchips to reunite stolen dogs, cats.</a></h3>
35 <h3><a href="/petitions/300025">Vets to scan prior to euthanasia for Rescue Back up and confirm keeper details</a></h3>
36 <h3><a href="/petitions/306054">Cut beer duty for at least 12 months, so pubs can survive after the covid virus.</a></h3>
37 <h3><a href="/petitions/300122">Highway Code Rules 163 and 215 to be made law. Pass horses wide and slow. </a></h3>
38 <h3><a href="/petitions/300019">Revoke the Health and Social Care Act 2012 and renationalise the NHS</a></h3>
39 <h3><a href="/petitions/305024">Extend grants immediately to small businesses outside of SBRR</a></h3>
40 <h3><a href="/petitions/300027">Fund research for childhood cancers with the worst survival rates</a></h3>
41 <h3><a href="/petitions/300170">Repeal the 2013 and 2017 HS2 Hybrid Bills halting all HS2 works immediately.</a></h3>
42 <h3><a href="/petitions/301696">Create an earned amnesty route for migrants without leave to remain</a></h3>
43 <h3><a href="/petitions/300270">Change the Sexual Offences Act so women can be charged with rape against males</a></h3>
44 <h3><a href="/petitions/301328">Give financial help to agency and zero hour workers during COVID-19 outbreak.</a></h3>
45 <h3><a href="/petitions/301461">Require British Sign Language Interpreters for emergency announcements on TV.</a></h3>
46 <h3><a href="/petitions/300139">Don’t criminalise trespass</a></h3>
47 <h3><a href="/petitions/300034">Fund Kuvan (sapropterin) on the NHS for people with PKU</a></h3>
48 <h3><a href="/petitions/300297">Rejoin the EU under Article 49 TEU</a></h3>
49 <h3><a href="/petitions/300071">Make pet theft crime a specific offence with custodial sentences.</a></h3>



Clean html tags
0 Include self-employed in statutory sick pay during Coronavirus
1 Close Schools/Colleges down for an appropriate amount of time amidst COVID19.
2 Implement UK lockdown for preventing spread of COVID19
3 Reimburse all students of this year’s fees due to strikes and COVID-19
4 Extend maternity leave by 3 months with pay in light of COVID-19
5 Increase pay for NHS healthcare workers and recognise their work
6 Government to offer economic assistance to the events industry during COVID-19
7 Give all key workers a 100% tax and Nat. Ins. holiday through COVID-19 crisis
8 Require universities to reimburse students&#39; tuition fees during strike action
9 Release the Home Office&#39;s Grooming Gang Review in full
10 Encourage lenders, landlords and utilities to freeze payments during lockdown
11 Close all universities down for an appropriate amount of time amidst COVID-19
12 Implement Universal Basic Income to give home &amp; food security through Covid-19
13 Refund university students for 3rd Semester Tuition 2020
14 Give UK nurseries emergency funding if they have to close down amid COVID-19
15 Require councils to suspend council tax payments during the coronavirus outbreak
16 Support the British aviation industry during the COVID-19 outbreak
17 No prosecution for parents that remove child from school during a pandemic.
18 Make LGBT conversion therapy illegal in the UK
19 Replace Breed Specific Legislation with a new statutory framework
20 Extend the transition; delay negotiations until after the coronavirus outbreak
21 Coronavirus Support Package for Directors / Shareholders of small Limited Co&#39;s.
22 Give non-British citizens who are NHS workers automatic citizenship
23 Publish the Russia report
24 Release HMP Prisoners due to COVID-19 - temporary release, licence, tag, curfew
25 Delay 5G in the UK until there’s been an independent investigation
26 Explore options for making NurOwn available to treat Motor Neurone Disease (MND)
27 Make Hedgehogs a Protected Species
28 Pay self employed workers a wage due to lack of earnings caused by COVID-19.
29 We would like the government to consider social care as equally important to NHS
30 Make COVID19 testing available to teaching staff caring for pupils.
31 Cancel HS2 and use the money for the NHS and local economies, post Covid-19.
32 Delay the reopening of schools to September
33 Allow gyms and leisure centres to reopen
34 Fern’s Law: Compulsory to scan &amp; check microchips to reunite stolen dogs, cats.
35 Vets to scan prior to euthanasia for Rescue Back up and confirm keeper details
36 Cut beer duty for at least 12 months, so pubs can survive after the covid virus.
37 Highway Code Rules 163 and 215 to be made law. Pass horses wide and slow. 
38 Revoke the Health and Social Care Act 2012 and renationalise the NHS
39 Extend grants immediately to small businesses outside of SBRR
40 Fund research for childhood cancers with the worst survival rates
41 Repeal the 2013 and 2017 HS2 Hybrid Bills halting all HS2 works immediately.
42 Create an earned amnesty route for migrants without leave to remain
43 Change the Sexual Offences Act so women can be charged with rape against males
44 Give financial help to agency and zero hour workers during COVID-19 outbreak.
45 Require British Sign Language Interpreters for emergency announcements on TV.
46 Don’t criminalise trespass
47 Fund Kuvan (sapropterin) on the NHS for people with PKU
48 Rejoin the EU under Article 49 TEU
49 Make pet theft crime a specific offence with custodial sentences.
mario:gonotes arunsah$ 
```

[↑](https://arunsah.github.io/gonotes#table-of-content)



## 23. Programming Time in Go

- Time is also referred as `real time`, `elapsed real time`, `wall clock` are subjected to timezone.
- `monotonic clock` measures time in with any variance are are reliable for programming.
- `sudo date +%Y%m%d -s "20500101"` set unix time to 2050. So system time are not accurate and varies precisions.
- Network Time Protocol (NTP) can be used to synchronising time across network.
- Coordinated Universal Time (UTC) is a time standard not time zone.
- UTC/NTP are important for coordinating services running globally.
- `ticker` can be use for repeated execution.
- Use `ISO 8601` or extended version `RFC3339` for time format.

```go
package main

import (
    "fmt"
    "log"
    "time"
)

func main() {

    func(execute bool) { // Basic Time
        if !execute {
            return
        }
        fmt.Println("Basic Time")

        // 2020-05-29 00:02:43.080643 +0530 IST m=+0.000096694
        fmt.Println(time.Now())

    }(true)

    func(execute bool) { // Sleeping/pausing program/execution
        if !execute {
            return
        }
        fmt.Println("Sleeping program")

        fmt.Println("I am sleeping at\t", time.Now())
        time.Sleep(2 * time.Second)
        fmt.Println("I am awake at\t", time.Now())

    }(true)

    func(execute bool) { // Setting timeout
        if !execute {
            return
        }
        fmt.Println("Setting timeout")

        fmt.Println("Waiting for 2 sencods: \t", time.Now())
        for {
            select {
            case <-time.After(2 * time.Second):
                fmt.Println("Timeout at\t", time.Now())
                return
            }
        }
        // unreachable code
        //fmt.Println("After timeout: \t", time.Now())

    }(true)

    func(execute bool) { // Ticker: execute are regular interval
        if !execute {
            return
        }
        fmt.Println("Ticker")
        c := time.Tick(1 * time.Second)
        for t := range c {
            fmt.Println("Hello ", t)
        }

        /*
            Ticker
            Hello  2020-05-29 00:18:30.31107 +0530 IST m=+5.009741451
            Hello  2020-05-29 00:18:31.3107 +0530 IST m=+6.009371735
            Hello  2020-05-29 00:18:32.313463 +0530 IST m=+7.012134720
            Hello  2020-05-29 00:18:33.313644 +0530 IST m=+8.012315690
            Hello  2020-05-29 00:18:34.31435 +0530 IST m=+9.013021269
            Hello  2020-05-29 00:18:35.310365 +0530 IST m=+10.009036297
        */

    }(false)

    func(execute bool) { // Parsing string time
        if !execute {
            return
        }
        fmt.Println("Parsing string time")

        t := "2020-05-29T23:04:05+05:30" // RFC3339
        tt, err := time.Parse(time.RFC3339, t)
        if err != nil {
            log.Fatal(err)
        }
        // 2020-05-29T23:04:05+05:30 2020-05-29 23:04:05 +0530 IST
        fmt.Println(t, tt)

        fmt.Println("component of time:")
        fmt.Println(tt.Date())    // 2020 May 29
        fmt.Println(tt.Unix())    // 1590773645
        fmt.Println(tt.Weekday()) // Friday
        fmt.Println(tt.Month())   // May

        // adding/subtracting time
        fmt.Println("adding/subtracting time:")
        fmt.Println(tt)                       // 2020-05-29 23:04:05 +0530 IST
        fmt.Println(tt.Add(5 * time.Second))  // 2020-05-29 23:04:10 +0530 IST
        fmt.Println(tt.Add(-5 * time.Second)) // 2020-05-29 23:04:00 +0530 IST
        fmt.Println(tt.Sub(tt))               // 0s

        // comparing time: Before/After/Equal
        fmt.Println("comparing time:")
        // 2020-05-29 23:04:05 +0530 IST 2020-05-29 00:34:34.266783 +0530 IST m=+4.004717908
        fmt.Println(tt, time.Now())
        fmt.Println(tt.After(time.Now()))  // true
        fmt.Println(tt.Before(time.Now())) // false
        fmt.Println(tt.Equal(time.Now()))  // false

    }(true)

} //end of main

```


```shell
$ go run hellotime.go 
Basic Time
2020-05-29 00:34:30.262158 +0530 IST m=+0.000093379
Sleeping program
I am sleeping at         2020-05-29 00:34:30.262354 +0530 IST m=+0.000289518
I am awake at    2020-05-29 00:34:32.262534 +0530 IST m=+2.000468949
Setting timeout
Waiting for 2 sencods:   2020-05-29 00:34:32.26261 +0530 IST m=+2.000544798
Timeout at       2020-05-29 00:34:34.266664 +0530 IST m=+4.004599044
Parsing string time
2020-05-29T23:04:05+05:30 2020-05-29 23:04:05 +0530 IST
component of time:
2020 May 29
1590773645
Friday
May
adding/subtracting time:
2020-05-29 23:04:05 +0530 IST
2020-05-29 23:04:10 +0530 IST
2020-05-29 23:04:00 +0530 IST
0s
comparing time:
2020-05-29 23:04:05 +0530 IST 2020-05-29 00:34:34.266783 +0530 IST m=+4.004717908
true
false
false
mario:gonotes arunsah$ 
```

[↑](https://arunsah.github.io/gonotes#table-of-content)



## 24. Deploying Go Code

- Go can run on many OS platform and CPU architecture.

```shell
$ go env
GO111MODULE=""
GOARCH="amd64"
GOBIN=""
GOCACHE="/Users/arunsah/Library/Caches/go-build"
GOENV="/Users/arunsah/Library/Application Support/go/env"
GOEXE=""
GOFLAGS=""
GOHOSTARCH="amd64"
GOHOSTOS="darwin"
GONOPROXY=""
GONOSUMDB=""
GOOS="darwin"
GOPATH="/Users/arunsah/go"
GOPRIVATE=""
GOPROXY="https://proxy.golang.org,direct"
GOROOT="/usr/local/go"
GOSUMDB="sum.golang.org"
GOTMPDIR=""
GOTOOLDIR="/usr/local/go/pkg/tool/darwin_amd64"
GCCGO="gccgo"
AR="ar"
CC="clang"
CXX="clang++"
CGO_ENABLED="1"
GOMOD=""
CGO_CFLAGS="-g -O2"
CGO_CPPFLAGS=""
CGO_CXXFLAGS="-g -O2"
CGO_FFLAGS="-g -O2"
CGO_LDFLAGS="-g -O2"
PKG_CONFIG="pkg-config"
GOGCCFLAGS="-fPIC -m64 -pthread -fno-caret-diagnostics -Qunused-arguments -fmessage-length=0 -fdebug-prefix-map=/var/folders/5t/kf28839s1tlgfv7bkwm_04z40000gn/T/go-build837554669=/tmp/go-build -gno-record-gcc-switches -fno-common"
mario:gonotes arunsah$ 
```

- Go allows cross compilation:
	- To build for specific env, `GOOS=linux GOARCH=386 go build hello.go`.
	- For win64, `GOOS=windows GOARCH-amd64 go build hello.go`.

```shell
$ GOOS=windows GOARCH=amd64 go build hellotime.go 
mario:gonotes arunsah$ go build hellotime.go 
mario:gonotes arunsah$ ls | grep "time"
hellotime
hellotime.exe
hellotime.go
mario:gonotes arunsah$ 
```

- Platform and Architecture Supported:
	- `android{arm}, darwin{386, amd64, arm, arm64}, dragonfly{amd64}, freebsd{386, amd64, arm}, linux{386, amd64, arm, arm64, ppc64, pcc64le, mips, mipsle, mips64, mips64le}, netbsd{386, amd64, arm}, openbsd{386, amd64, arm}, plan9{386, amd64}, solaris{and64}, windows{386, amd64}`


- Go binary are bigger in size as they contains all the dependencies (including Go runtime) and this make deployment easy. Go uses `statically linked` binary.
- Some compile flags can reduce size by removing symbol tables, debug information and DWARF symbol table.
	- `GOOS=linux go build -ldflags="-s -w" hello.go`, it may reduce size by 500 KB.
	- Fo IOT devices, tools like  upx (https://upx.github.io/)(linux) can be used to compress binary and require decompression while execution. It can further reduce file size by 60-70%.

- Docker provide sandbox environment within an OS.
- It may be argued that deploying Go with docker is overkilled as Go binary contains all dependency. 

```go
package main

import (
    "fmt"
    "net/http"
    "os"
    "time"
)

func rootHandler(res http.ResponseWriter, req *http.Request) {
    host, err := os.Hostname()
    if err != nil {
        fmt.Println("Error occured while getting host.", err)
        host = "default_host"
    }
    message := time.Now().Format("2006-01-02 15:04:05") + ": greeting form " + host + "\n\n"
    buffer := []byte(message)
    // 2020-05-30 15:25:31: greeting form mario
    res.Write(buffer)
}

func main() {
    const PORT string = ":18080"
    fmt.Println("Started server on", PORT)
    http.HandleFunc("/", rootHandler)
    http.ListenAndServe(PORT, nil)
} //end of main


```

```dockerfile
FROM golang:1.13.8
COPY hellodocker.go /
RUN go build -o /hellodocker /hellodocker.go
EXPOSE 18080
ENTRYPOINT [ "/hellodocker" ]
#   docker build -t hellodocker:1 .
#   docker run -p 18081:18080 hellodocker:1

```

```shell
$ go version
go version go1.13.8 darwin/amd64

$ docker build -t hellodocker:1 .
Sending build context to Docker daemon  8.982MB
Step 1/5 : FROM golang:1.13.8
1.13.8: Pulling from library/golang
50e431f79093: Pull complete 
dd8c6d374ea5: Pull complete 
c85513200d84: Pull complete 
55769680e827: Pull complete 
15357f5e50c4: Pull complete 
e2d9b328fba5: Pull complete 
f8e0159fc852: Pull complete 
Digest: sha256:d7e0b99badf7f34b5096089484a733897c9b89aa12ffb9f67f81da054f8a403e
Status: Downloaded newer image for golang:1.13.8
 ---> 3a7408f53f79
Step 2/5 : COPY hellodocker.go /
 ---> 87a9ec57da11
Step 3/5 : RUN go build -o /hellodocker /hellodocker.go
 ---> Running in 00439540ec47
Removing intermediate container 00439540ec47
 ---> 9a88b04cd285
Step 4/5 : EXPOSE 18080
 ---> Running in 75fbefb51a38
Removing intermediate container 75fbefb51a38
 ---> 43fe6cd1989f
Step 5/5 : ENTRYPOINT [ "/hellodocker" ]
 ---> Running in da697b4943fe
Removing intermediate container da697b4943fe
 ---> 3dc3e3a8a991
Successfully built 3dc3e3a8a991
Successfully tagged hellodocker:1
mario:gonotes arunsah$ 
$ docker run -p 18081:18080 hellodocker:1
Started server on :18080

# in another shell
$ docker container ls
CONTAINER ID        IMAGE                                COMMAND                  CREATED             STATUS              PORTS                      NAMES
cd5a51f7dafd        hellodocker:1                        "/hellodocker"           2 minutes ago       Up 2 minutes        0.0.0.0:18081->18080/tcp   romantic_sammet


$ docker images
REPOSITORY                           TAG                                              IMAGE ID            CREATED             SIZE
hellodocker                          1                                                3dc3e3a8a991        7 minutes ago       810MB

$ docker stop cd5a51f7dafd

```


```shell
# client
$ curl localhost:18081
2020-05-30 10:15:51: greeting form cd5a51f7dafd
```

- Downloading the Go binary files:
	- host file on `https`.
	- provide checksum of the file.

```shell
# calculating SHA51

$ ls -all | grep "hellodocker"
-rwxr-xr-x   1 arunsah  staff  7336844 30 May 15:56 hellodocker
-rw-r--r--   1 arunsah  staff      605 30 May 15:43 hellodocker.go
mario:gonotes arunsah$ 

$ which shasum
/usr/bin/shasum
mario:gonotes arunsah$ shasum -a 512 hellodocker
3b594ef9c33c9f99264ed8109d09d384402e8ca3238af2ec500960193bf09d9d6e778278d561680fe07b56b44a0d6ce38de945cdbe0791ffd680f7c866a66cdf  hellodocker

$ openssl sha512 hellodocker
SHA512(hellodocker)= 3b594ef9c33c9f99264ed8109d09d384402e8ca3238af2ec500960193bf09d9d6e778278d561680fe07b56b44a0d6ce38de945cdbe0791ffd680f7c866a66cdf

$ openssl sha256 hellodocker
SHA256(hellodocker)= 80738ac99298a05e1b25555545fd0763a52122121d3cb6134a06ba7f3c4015da

$ openssl sha1 hellodocker
SHA1(hellodocker)= 95e8b5e6231a286bb48248396456ca91b60e73d1

$ openssl md5 hellodocker
MD5(hellodocker)= 4f1c2dc7c60030e000d00f31aa50e6e1
```

- Host code over GitHub.

```shell
go get -u github.com/golang/dep/cmd/dep
dep –help
dep is a tool for managing dependencies for Go projects
```

- Use package manager:
	- Homebrew (https://brew.sh/) - macOS
	- Image Chocolatey (https://chocolatey.org/) - Windows
	- Image Apt (https://wiki.debian.org/Apt) - Debian, Ubuntu
	- Image Yum (http://yum.baseurl.org/) - Fedora, Red Hat, Centos
	- Image Pacman (https://www.archlinux.org/pacman/) - Arch Linux

[↑](https://arunsah.github.io/gonotes#table-of-content)



## 25. A RESTful JSON API

- Using `dep` for manage dependencies.
	- `go get -u github.com/golang/dep/cmd/dep`

```shell
# make sure that `/Users/arunsah/go/bin` is in PATH
$ which dep
/Users/arunsah/go/bin/dep

$ dep --help
Dep is a tool for managing dependencies for Go projects

Usage: "dep [command]"

Commands:

  init     Set up a new Go project, or migrate an existing one
  status   Report the status of the project's dependencies
  ensure   Ensure a dependency is safely vendored in the project
  version  Show the dep version information
  check    Check if imports, Gopkg.toml, and Gopkg.lock are in sync

Examples:
  dep init                               set up a new project
  dep ensure                             install the project's dependencies
  dep ensure -update                     update the locked versions of all dependencies
  dep ensure -add github.com/pkg/errors  add a dependency to the project

Use "dep help [command]" for more information about a command.
```

- `dep` tools only works with go project within `$GOPATH`. It uses `vendor` folder
- Using `boltdb` an embedded go database.


- Setting up gaoling in macOS ([Setup Golang on Mac OS X](http://todsul.com/tech/setup-golang-on-mac-os-x/))

```shell
$ cat ~/.bash_profile
$ nano ~/.bash_profile 
export PATH="/Users/arunsah/go/bin:/Users/arunsah/go/bin/godoc:/User/arunsah/go:$PATH"
export GOPATH=$HOME/go

$ echo $GOPATH
/Users/arunsah/go

mario:~ arunsah$ mkdir $GOPATH/src/github.com/arunsah/
mario:~ arunsah$ mkdir $GOPATH/src/github.com/arunsah/restful-api-golang/
mario:~ arunsah$ touch $GOPATH/src/github.com/arunsah/restful-api-golang/helloapi.go

$ touch $GOPATH/src/github.com/arunsah/restful-api-golang/helloapi.go

mario:~ arunsah$ cd $GOPATH/src/github.com/arunsah/restful-api-golang/
mario:restful-api-golang arunsah$ pwd
/Users/arunsah/go/src/github.com/arunsah/restful-api-golang
mario:restful-api-golang arunsah$ which dep
/Users/arunsah/go/bin/dep
mario:restful-api-golang arunsah$ dep init
mario:restful-api-golang arunsah$ tree .
.
├── Gopkg.lock
├── Gopkg.toml
├── helloapi.go
└── vendor

1 directory, 3 files
mario:restful-api-golang arunsah$ 
```

	- `lock` file will lock dependencies to a specific version.
	- `toml` file will declare dependencies.
	- `vendor` folder will holds the packages

- After using various dependencies in `import`. Run `$ dep ensure` to initialise and install those dependencies.

```go
package main

import (
    "fmt"
    "log"
    "net/http"

    "github.com/julienschmidt/httprouter"
)

func main() {
    const HOST string = ":18080"
    fmt.Println("Running server at ", HOST)

    router := httprouter.New()
    router.GET("/", rootHandler)
    router.GET("/greeting/:username", greetineHandler)
    log.Fatal(http.ListenAndServe(HOST, router))
}

func rootHandler(res http.ResponseWriter, req *http.Request, param httprouter.Params) {
    fmt.Fprint(res, "Welcome to greeting api!\n")
}
func greetineHandler(res http.ResponseWriter, req *http.Request, param httprouter.Params) {
    fmt.Fprintf(res, "Hello, %s!\n", param.ByName("username"))
}

```

```shell
# server
$ dep ensure
mario:restful-api-golang arunsah$ go run helloapi.go 
Running server at  :18080

# client
$ curl localhost:18080
Welcome to greeting api!
mario:restful-api-golang arunsah$ curl localhost:18080/greeting/tom
Hello, tom!

```

- It is possible to extend `net/http` to accept regex to serve dynamic routes while `httprouter` provide this features through placeholders.

- Writing test

```go
package main

import (
    "fmt"
    "log"
    "net/http"

    "github.com/julienschmidt/httprouter"
)

// Server is server
type Server struct {
    route *httprouter.Router
}

// ServeHTTP will apply common header in all route
func (server *Server) ServeHTTP(res http.ResponseWriter, req *http.Request) {
    res.Header().Set("Content-Type", "application/json; charset=utf-8")
    server.route.ServeHTTP(res, req)
}

func main() {
    const HOST string = ":18080"
    fmt.Println("Running server at ", HOST)

    router := httprouter.New()
    router.GET("/", RootHandler)

    router.GET("/task", ListTask)
    router.POST("/task", CreateTask)

    router.GET("/task/:id", ReadTask)
    router.PUT("/task/:id", UpdateTask)
    router.DELETE("/task/:id", DeleteTask)

    // log.Fatal(http.ListenAndServe(HOST, router))
    log.Fatal(http.ListenAndServe(HOST, &Server{router}))
}

// RootHandler is root handler
func RootHandler(res http.ResponseWriter, req *http.Request, param httprouter.Params) {
    fmt.Fprint(res, "Welcome to todo api!\n")
}

// ListTask list all task
func ListTask(res http.ResponseWriter, req *http.Request, param httprouter.Params) {

    //res.Header().Set("Content-Type", "application/json; charset=utf-8")
    fmt.Fprintf(res, "todo")
}

// CreateTask create task
func CreateTask(res http.ResponseWriter, req *http.Request, param httprouter.Params) {
    fmt.Fprintf(res, "todo")
}

// ReadTask task with particular id
func ReadTask(res http.ResponseWriter, req *http.Request, param httprouter.Params) {
    fmt.Fprintf(res, "todo")
}

// UpdateTask task with particular id
func UpdateTask(res http.ResponseWriter, req *http.Request, param httprouter.Params) {
    fmt.Fprintf(res, "todo")
}

// DeleteTask task with particular id
func DeleteTask(res http.ResponseWriter, req *http.Request, param httprouter.Params) {
    fmt.Fprintf(res, "todo")
}
```


```go
package main

import (
    "net/http"
    "net/http/httptest"
    "testing"

    "github.com/julienschmidt/httprouter"
)

// ListTask list all task
func TestListTask(test *testing.T) {
    router := httprouter.New()
    router.GET("/", ListTask)

    req, _ := http.NewRequest("GET", "/", nil)
    res := httptest.NewRecorder()
    //router.ServeHTTP(res, req)
    server := Server{router}
    server.ServeHTTP(res, req)

    expectedContentTypeHeader := "application/json; charset=utf-8"
    actualContentTypeHeader := res.Header().Get("Content-Type")
    if actualContentTypeHeader != expectedContentTypeHeader {
        test.Errorf("handler returned Content-Type as " + actualContentTypeHeader + " but required " + expectedContentTypeHeader)
    }

    expectedStatusCode := http.StatusOK
    actualStatusCode := res.Code
    if actualStatusCode != expectedStatusCode {
        test.Errorf("handler returned StatusCode as " + string(actualStatusCode) + " but required " + string(expectedStatusCode))
    }

    /*
        Running tool: /usr/local/go/bin/go test -timeout 30s github.com/arunsah/restful-api-golang -run ^(TestListTask)$

        --- FAIL: TestListTask (0.00s)
            /Users/arunsah/go/src/github.com/arunsah/restful-api-golang/hellotodo_test.go:28: handler returned Content-Type as text/plain; charset=utf-8 but required application/json; charset=utf-8
        FAIL
        FAIL    github.com/arunsah/restful-api-golang   0.012s
        FAIL

        /////////// After fixing the Content-Type
        Running tool: /usr/local/go/bin/go test -timeout 30s github.com/arunsah/restful-api-golang -run ^(TestListTask)$

        ok      github.com/arunsah/restful-api-golang   0.013s
    */
}

```


- Persistence using `BoltDB`
	- Its a key value db
	- Debug configuration in `vscode`.

```json
{
    // Use IntelliSense to learn about possible attributes.
    // Hover to view descriptions of existing attributes.
    // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Launch",
            "type": "go",
            "request": "launch",
            "mode": "auto",
            "program": "${fileDirname}",
            "env": {},
            "args": []
        }
    ]
}


```

- [Fielding Dissertation: CHAPTER 5: Representational State Transfer (REST)](https://www.ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm)

[↑](https://arunsah.github.io/gonotes#table-of-content)



## 26. A TCP Chat Server

- TODO

[↑](https://arunsah.github.io/gonotes#table-of-content)



## 27. References

- Go in 24 Hours, Sams Teach Yourself: Next Generation Systems Programming with Golang, First Edition (https://learning.oreilly.com/library/view/go-in-24/9780134771922/)

[↑](https://arunsah.github.io/gonotes#table-of-content)

[arunsah.github.io](https://arunsah.github.io)

# Golang
#go #may2020

---

### Getting started

```
$ go
Go is a tool for managing Go source code.

Usage:

        go <command> [arguments]

The commands are:

        bug         start a bug report
        build       compile packages and dependencies
        clean       remove object files and cached files
        doc         show documentation for package or symbol
        env         print Go environment information
        fix         update packages to use new APIs
        fmt         gofmt (reformat) package sources
        generate    generate Go files by processing source
        get         add dependencies to current module and install them
        install     compile and install packages and dependencies
        list        list packages or modules
        mod         module maintenance
        run         compile and run Go program
        test        test packages
        tool        run specified go tool
        version     print Go version
        vet         report likely mistakes in packages

Use "go help <command>" for more information about a command.

Additional help topics:

        buildmode   build modes
        c           calling between Go and C
        cache       build and test caching
        environment environment variables
        filetype    file types
        go.mod      the go.mod file
        gopath      GOPATH environment variable
        gopath-get  legacy GOPATH go get
        goproxy     module proxy protocol
        importpath  import path syntax
        modules     modules, module versions, and more
        module-get  module-aware go get
        module-auth module authentication using go.sum
        module-private module configuration for non-public modules
        packages    package lists and patterns
        testflag    testing flags
        testfunc    testing functions

Use "go help <topic>" for more information about that topic.


$ go version
go version go1.13.8 darwin/amd64

$ cat hello_world.go 
package helloworld

import "fmt"

func main() {
        fmt.Println("hello world")
}

$ go build hello_world.go 

$ ls
hello_world.go

$ ls -all
total 8
drwxr-xr-x  3 arunsah  staff  96  9 May 21:44 .
drwxr-xr-x  3 arunsah  staff  96  9 May 21:44 ..
-rw-r--r--  1 arunsah  staff  78  9 May 21:45 hello_world.go

$ go run hello_world.go 
go run: cannot run non-main package

$ cat hello_world.go 
package main

import "fmt"

func main() {
        fmt.Println("hello world")
}

$ go build hello_world.go 

$ ls -all
total 4152
drwxr-xr-x  4 arunsah  staff      128  9 May 21:48 .
drwxr-xr-x  3 arunsah  staff       96  9 May 21:44 ..
-rwxr-xr-x  1 arunsah  staff  2120320  9 May 21:48 hello_world
-rw-r--r--  1 arunsah  staff       72  9 May 21:48 hello_world.go

$ ./hello_world 
hello world

$ go run hello_world.go 
hello world

$ go build hello_world.go  && ./hello_world 
hello world

```



### Cheatsheet
#### Variables

```go
// variable declaration
var msg string
msg = "hello world"

// variable declaration and initiaization
msg:= "hello world"

```

#### Constants
```go
const Pi = 3.141
```

#### Basic Type
```go
// string
msg:= "hello world"
// multi-line string
msg:= `Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. 
Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.`

// numbers
num:= 42					// int
num:= 42.					// float64
num:= 42 + 3i				// complex128
num:= byte('A')			// byte, alias for uint8

var age uint = 26			// uint
var pi float32 = 3.141	// float32

// arrays have fixed size
nums := [...]int{1,2,3,4,5}
nums := [5]int{1,2,3,4,5}

// slices have dynamic size
nums := []int{1,2,3,4,5}
data := []byte("hello world")


```


##### Pointers
``` go
// pointers point to a memor location of a variable.
// go is garbage-collected language 
func main(){
	b := *getValueByReference()
	...
}

func getValueByReference() (x *int){
	value:= 42
	return &value
}
```

##### Type Conversions
```go
iNum := 42
fNum := float64(iNum)
uNum := uint(iNum)

```


#### Control Flow and Loop Example

##### FizzBuzz example
- if else
- for loop
- conversion from int to string
- printing message
```go
// FizzBuzz program: for i= 1 to 20, 
// if i is multiple of 3 and 5 then print 'Fizz buzz', 
// if i is numtiple of 3 then print 'fizz', 
// if i is numtiple of 5 then print 'buzz' 
// else print the number
package main

import (
    "fmt"
    "strconv"
)

func main() {
    fmt.Println("hello world")

    var msg string
    for num := 0; num <= 20; num++ {
        if num%3 == 0 && num%5 == 0 {
            msg = "fizz buzz"
        } else if num%3 == 0 {
            msg = "fizz"
        } else if num%5 == 0 {
            msg = "buzz"
        } else {
            // conveting number to string
            msg = strconv.Itoa(num)
            //msg = strconv.FormatInt(int64(num), 10)
        }
        fmt.Println(msg)
        //fmt.Printf("%v\n", msg)
    }
}

```

```go
// statements in if: condition in if can be preceded with a statement before ;
if _, err := getResult(); err != nil{
	// handle error
}


// switch
day := "sunday"
switch day {
case "saturday":
    fallthrough // cases doesnot fall by default
case "sunday":
    msg = "weekend"
default:
    msg = "workday"
}


// for loop
for i:= 0; i<10; i++}
	//...
}

// for range loop
names := []string{"tom", "jerry", "nibbles", "droopy"}
for index, name := range names {
    fmt.Printf("%d, %s\n", index, name)
}

```

#### Functions

##### Lambda
```go
// legal voting age is 18 in India
canVote := func(age int) bool { return age >= 18 }
age := 17
fmt.Printf("Age: %v, can vote: %v\n", age, canVote(age))

```

##### Multiple return types
```go
fmt.Println(getName()) // Michael Jackson
a, b := getName()
fmt.Printf("First name: %v, Last name: %v\n", a, b) // First name: Michael, Last name: Jackson

func getName() (firstName, lastName string) {
    return "Michael", "Jackson"
}

// by defining return value identifier in signatiure,
// return statement with no args will return variables with those identifier name
func getSize() (width, height float64) {
    width = 32
    height = 30
    return
}
fmt.Println(getSize())	// 32 30

```


#### Packages
```go
// import statement per package
import "fmt"
import "math/rand"

// import statement grouped together
import (
	"fmt"		//fmt.Println
	"math/rand"	//rand.Intn
)

// import with alias
import randomNumber "math/rand" 	// randomNumber.Intn


// every package file starts with package name
package main

// Function with Capital names are exposes in the package

```

##### Exposing Methods
```go

//---------- directory structure ----------------
arsah-Mac:hello_world arsah$ tree
.
├── hello
│   └── Hello.go		//package hello
├── hello_world
└── hello_world.go	//package main

//---------- ./hello/Hello.go ----------------
package hello

/*
Hello return string "hello"
*/
func Hello() string { // method name must start with upper case
						// to expose the method outside package
						// Documentation is compulsory
    return "hello"
}

//---------- ./hello_world.go ----------------
package main

import (
    hello "./hello"				//exposing via alias
)

func main() {
    fmt.Println(hello.Hello())
}

```

#### Concurrency
##### Go routines
- channels are concurrency safe communication objects
- buffered channels limit size of channel (cannot be over-filled. `messageQueue := make(chan string, 10)`
- over-reading or reading closed channel gives: `// fatal error: all goroutines are asleep - deadlock!`

```go
func publish(message string, messageQueue chan string) {
    messageQueue <- "Hello, " + message + "! "
}

// create channel
messageQueue := make(chan string)

// start concurrent go routines
// publish to channel
// order of execution is not guranted
go publish("tom", messageQueue)
go publish("jerry", messageQueue)
go publish("droopy", messageQueue)
go publish("nibbles", messageQueue)

// read from channel/messageQueue
fmt.Println(<-messageQueue,
    <-messageQueue,
    <-messageQueue,
    <-messageQueue)
// Hello, nibbles!  Hello, tom!  Hello, jerry!  Hello, droopy!
// Hello, nibbles!  Hello, jerry!  Hello, droopy!  Hello, tom!


// iterates across a channel until its closed
for msg := range messageQueue { // iterated until closed
    fmt.Println(msg)
}

// read with repetation
for true {
    if greetingMsg, isClosed := <-messageQueue; isClosed != false {
        fmt.Println(greetingMsg)
        // close(messageQueue) // shutdown channel
        if isClosed == true {
            break //break loop
        }
    }
}

```

#### References
- [Go cheatsheet](https://devhints.io/go)
- [A Tour of Go](https://tour.golang.org/basics/1)
- https://www.lipsum.com/


### The Go Programming Language Specification
**Version of Jan 14, 2020** [https://golang.org/ref/spec](https://golang.org/ref/spec)

[Introduction](https://golang.org/ref/spec#Introduction), [Notation](https://golang.org/ref/spec#Notation), [Source code representation](https://golang.org/ref/spec#Source_code_representation), [Characters](https://golang.org/ref/spec#Characters), [Letters and digits](https://golang.org/ref/spec#Letters_and_digits), [Lexical elements](https://golang.org/ref/spec#Lexical_elements), [Comments](https://golang.org/ref/spec#Comments), [Tokens](https://golang.org/ref/spec#Tokens), [Semicolons](https://golang.org/ref/spec#Semicolons), [Identifiers](https://golang.org/ref/spec#Identifiers), [Keywords](https://golang.org/ref/spec#Keywords), [Operators and punctuation](https://golang.org/ref/spec#Operators_and_punctuation), [Integer literals](https://golang.org/ref/spec#Integer_literals), [Floating-point literals](https://golang.org/ref/spec#Floating-point_literals), [Imaginary literals](https://golang.org/ref/spec#Imaginary_literals), [Rune literals](https://golang.org/ref/spec#Rune_literals), [String literals](https://golang.org/ref/spec#String_literals), [Constants](https://golang.org/ref/spec#Constants), [Variables](https://golang.org/ref/spec#Variables), [Types](https://golang.org/ref/spec#Types), [Method sets](https://golang.org/ref/spec#Method_sets), [Boolean types](https://golang.org/ref/spec#Boolean_types), [Numeric types](https://golang.org/ref/spec#Numeric_types), [String types](https://golang.org/ref/spec#String_types), [Array types](https://golang.org/ref/spec#Array_types), [Slice types](https://golang.org/ref/spec#Slice_types), [Struct types](https://golang.org/ref/spec#Struct_types), [Pointer types](https://golang.org/ref/spec#Pointer_types) [Function types](https://golang.org/ref/spec#Function_types), [Interface types](https://golang.org/ref/spec#Interface_types), [Map types](https://golang.org/ref/spec#Map_types), [Channel types](https://golang.org/ref/spec#Channel_types), [Properties of types and values](https://golang.org/ref/spec#Properties_of_types_and_values), [Type identity](https://golang.org/ref/spec#Type_identity), [Assignability](https://golang.org/ref/spec#Assignability), [Representability](https://golang.org/ref/spec#Representability), [Blocks](https://golang.org/ref/spec#Blocks), [Declarations and scope](https://golang.org/ref/spec#Declarations_and_scope), [Label scopes](https://golang.org/ref/spec#Label_scopes), [Blank identifier](https://golang.org/ref/spec#Blank_identifier), [Predeclared identifiers](https://golang.org/ref/spec#Predeclared_identifiers), [Exported identifiers](https://golang.org/ref/spec#Exported_identifiers), [Uniqueness of identifiers](https://golang.org/ref/spec#Uniqueness_of_identifiers), [Constant declarations](https://golang.org/ref/spec#Constant_declarations), [Iota](https://golang.org/ref/spec#Iota), [Type declarations](https://golang.org/ref/spec#Type_declarations), [Variable declarations](https://golang.org/ref/spec#Variable_declarations), [Short variable declarations](https://golang.org/ref/spec#Short_variable_declarations), [Function declarations](https://golang.org/ref/spec#Function_declarations), [Method declarations](https://golang.org/ref/spec#Method_declarations), [Expressions](https://golang.org/ref/spec#Expressions), [Operands](https://golang.org/ref/spec#Operands), [Qualified identifiers](https://golang.org/ref/spec#Qualified_identifiers), [Composite literals](https://golang.org/ref/spec#Composite_literals), [Function literals](https://golang.org/ref/spec#Function_literals), [Primary expressions](https://golang.org/ref/spec#Primary_expressions), [Selectors](https://golang.org/ref/spec#Selectors), [Method expressions](https://golang.org/ref/spec#Method_expressions), [Method values](https://golang.org/ref/spec#Method_values), [Index expressions](https://golang.org/ref/spec#Index_expressions), [Slice expressions](https://golang.org/ref/spec#Slice_expressions), [Type assertions](https://golang.org/ref/spec#Type_assertions), [Calls](https://golang.org/ref/spec#Calls), [Passing arguments to … parameters](https://golang.org/ref/spec#Passing_arguments_to_..._parameters), [Operators](https://golang.org/ref/spec#Operators), [Arithmetic operators](https://golang.org/ref/spec#Arithmetic_operators), [Comparison operators](https://golang.org/ref/spec#Comparison_operators), [Logical operators](https://golang.org/ref/spec#Logical_operators), [Address operators](https://golang.org/ref/spec#Address_operators), [Receive operator](https://golang.org/ref/spec#Receive_operator), [Conversions](https://golang.org/ref/spec#Conversions), [Constant expressions](https://golang.org/ref/spec#Constant_expressions), [Order of evaluation](https://golang.org/ref/spec#Order_of_evaluation), [Statements](https://golang.org/ref/spec#Statements), [Terminating statements](https://golang.org/ref/spec#Terminating_statements), [Empty statements](https://golang.org/ref/spec#Empty_statements), [Labeled statements](https://golang.org/ref/spec#Labeled_statements), [Expression statements](https://golang.org/ref/spec#Expression_statements), [Send statements](https://golang.org/ref/spec#Send_statements), [IncDec statements](https://golang.org/ref/spec#IncDec_statements), [Assignments](https://golang.org/ref/spec#Assignments), [If statements](https://golang.org/ref/spec#If_statements), [Switch statements](https://golang.org/ref/spec#Switch_statements), [For statements](https://golang.org/ref/spec#For_statements), [Go statements](https://golang.org/ref/spec#Go_statements), [Select statements](https://golang.org/ref/spec#Select_statements), [Return statements](https://golang.org/ref/spec#Return_statements), [Break statements](https://golang.org/ref/spec#Break_statements), [Continue statements](https://golang.org/ref/spec#Continue_statements), [Goto statements](https://golang.org/ref/spec#Goto_statements), [Fallthrough statements](https://golang.org/ref/spec#Fallthrough_statements), [Defer statements](https://golang.org/ref/spec#Defer_statements), [Built-in functions](https://golang.org/ref/spec#Built-in_functions), [Close](https://golang.org/ref/spec#Close), [Length and capacity](https://golang.org/ref/spec#Length_and_capacity), [Allocation](https://golang.org/ref/spec#Allocation), [Making slices, maps and channels](https://golang.org/ref/spec#Making_slices_maps_and_channels), [Appending to and copying slices](https://golang.org/ref/spec#Appending_and_copying_slices), [Deletion of map elements](https://golang.org/ref/spec#Deletion_of_map_elements), [Manipulating complex numbers](https://golang.org/ref/spec#Complex_numbers), [Handling panics](https://golang.org/ref/spec#Handling_panics), [Bootstrapping](https://golang.org/ref/spec#Bootstrapping), [Packages](https://golang.org/ref/spec#Packages), [Source file organization](https://golang.org/ref/spec#Source_file_organization), [Package clause](https://golang.org/ref/spec#Package_clause), [Import declarations](https://golang.org/ref/spec#Import_declarations), [An example package](https://golang.org/ref/spec#An_example_package), [Program initialization and execution](https://golang.org/ref/spec#Program_initialization_and_execution), [The zero value](https://golang.org/ref/spec#The_zero_value), [Package initialization](https://golang.org/ref/spec#Package_initialization), [Program execution](https://golang.org/ref/spec#Program_execution), [Errors](https://golang.org/ref/spec#Errors), [Run-time panics](https://golang.org/ref/spec#Run_time_panics), [System considerations](https://golang.org/ref/spec#System_considerations), [Package unsafe](https://golang.org/ref/spec#Package_unsafe), [Size and alignment guarantees](https://golang.org/ref/spec#Size_and_alignment_guarantees) 

### Go Standard library
[Packages - The Go Programming Language](https://golang.org/pkg/)


- [archive](https://golang.org/pkg/archive/)
	- [tar](https://golang.org/pkg/archive/tar/): Package tar implements access to tar archives.
	- [zip](https://golang.org/pkg/archive/zip/): Package zip provides support for reading and writing ZIP archives.
- [bufio](https://golang.org/pkg/bufio/): Package bufio implements buffered I/O. It wraps an io.Reader or io.Writer object, creating another object (Reader or Writer) that also implements the interface but provides buffering and some help for textual I/O.
- [builtin](https://golang.org/pkg/builtin/): Package builtin provides documentation for Go’s predeclared identifiers.
- [bytes](https://golang.org/pkg/bytes/): Package bytes implements functions for the manipulation of byte slices.
- [compress](https://golang.org/pkg/compress/)
	- [bzip2](https://golang.org/pkg/compress/bzip2/): Package bzip2 implements bzip2 decompression.
	- [flate](https://golang.org/pkg/compress/flate/): Package flate implements the DEFLATE compressed data format, described in RFC 1951.
	- [gzip](https://golang.org/pkg/compress/gzip/): Package gzip implements reading and writing of gzip format compressed files, as specified in RFC 1952.
	- [lzw](https://golang.org/pkg/compress/lzw/): Package lzw implements the Lempel-Ziv-Welch compressed data format, described in T. A. Welch, “A Technique for High-Performance Data Compression”, Computer, 17(6) (June 1984), pp 8-19.
	- [zlib](https://golang.org/pkg/compress/zlib/): Package zlib implements reading and writing of zlib format compressed data, as specified in RFC 1950.
- [container](https://golang.org/pkg/container/)
	- [heap](https://golang.org/pkg/container/heap/): Package heap provides heap operations for any type that implements heap.Interface.
	- [list](https://golang.org/pkg/container/list/): Package list implements a doubly linked list.
	- [ring](https://golang.org/pkg/container/ring/): Package ring implements operations on circular lists.
- [context](https://golang.org/pkg/context/): Package context defines the Context type, which carries deadlines, cancellation signals, and other request-scoped values across API boundaries and between processes.
- [crypto](https://golang.org/pkg/crypto/): Package crypto collects common cryptographic constants.
	- [aes](https://golang.org/pkg/crypto/aes/): Package aes implements AES encryption (formerly Rijndael), as defined in U.S. Federal Information Processing Standards Publication 197.
	- [cipher](https://golang.org/pkg/crypto/cipher/): Package cipher implements standard block cipher modes that can be wrapped around low-level block cipher implementations.
	- [des](https://golang.org/pkg/crypto/des/): Package des implements the Data Encryption Standard (DES) and the Triple Data Encryption Algorithm (TDEA) as defined in U.S. Federal Information Processing Standards Publication 46-3.
	- [dsa](https://golang.org/pkg/crypto/dsa/): Package dsa implements the Digital Signature Algorithm, as defined in FIPS 186-3.
	- [ecdsa](https://golang.org/pkg/crypto/ecdsa/): Package ecdsa implements the Elliptic Curve Digital Signature Algorithm, as defined in FIPS 186-3.
	- [ed25519](https://golang.org/pkg/crypto/ed25519/): Package ed25519 implements the Ed25519 signature algorithm.
	- [elliptic](https://golang.org/pkg/crypto/elliptic/): Package elliptic implements several standard elliptic curves over prime fields.
	- [hmac](https://golang.org/pkg/crypto/hmac/): Package hmac implements the Keyed-Hash Message Authentication Code (HMAC) as defined in U.S. Federal Information Processing Standards Publication 198.
	- [md5](https://golang.org/pkg/crypto/md5/): Package md5 implements the MD5 hash algorithm as defined in RFC 1321.
	- [rand](https://golang.org/pkg/crypto/rand/): Package rand implements a cryptographically secure random number generator.
	- [rc4](https://golang.org/pkg/crypto/rc4/): Package rc4 implements RC4 encryption, as defined in Bruce Schneier’s Applied Cryptography.
	- [rsa](https://golang.org/pkg/crypto/rsa/): Package rsa implements RSA encryption as specified in PKCS#1.
	- [sha1](https://golang.org/pkg/crypto/sha1/): Package sha1 implements the SHA-1 hash algorithm as defined in RFC 3174.
	- [sha256](https://golang.org/pkg/crypto/sha256/): Package sha256 implements the SHA224 and SHA256 hash algorithms as defined in FIPS 180-4.
	- [sha512](https://golang.org/pkg/crypto/sha512/): Package sha512 implements the SHA-384, SHA-512, SHA-512/224, and SHA-512/256 hash algorithms as defined in FIPS 180-4.
	- [subtle](https://golang.org/pkg/crypto/subtle/): Package subtle implements functions that are often useful in cryptographic code but require careful thought to use correctly.
	- [tls](https://golang.org/pkg/crypto/tls/): Package tls partially implements TLS 1.2, as specified in RFC 5246, and TLS 1.3, as specified in RFC 8446.
	- [x509](https://golang.org/pkg/crypto/x509/): Package x509 parses X.509-encoded keys and certificates.
		- [pkix](https://golang.org/pkg/crypto/x509/pkix/): Package pkix contains shared, low level structures used for ASN.1 parsing and serialization of X.509 certificates, CRL and OCSP.
- [database](https://golang.org/pkg/database/):
	- [sql](https://golang.org/pkg/database/sql/): Package sql provides a generic interface around SQL (or SQL-like) databases.
		- [driver](https://golang.org/pkg/database/sql/driver/): Package driver defines interfaces to be implemented by database drivers as used by package sql.
- [debug](https://golang.org/pkg/debug/)
	- [dwarf](https://golang.org/pkg/debug/dwarf/): Package dwarf provides access to DWARF debugging information loaded from executable files, as defined in the DWARF 2.0 Standard at http://dwarfstd.org/doc/dwarf-2.0.0.pdf
	- [elf](https://golang.org/pkg/debug/elf/): Package elf implements access to ELF object files.
	- [gosym](https://golang.org/pkg/debug/gosym/): Package gosym implements access to the Go symbol and line number tables embedded in Go binaries generated by the gc compilers.
	- [macho](https://golang.org/pkg/debug/macho/): Package macho implements access to Mach-O object files.
	- [pe](https://golang.org/pkg/debug/pe/): Package pe implements access to PE (Microsoft Windows Portable Executable) files.
	- [plan9obj](https://golang.org/pkg/debug/plan9obj/): Package plan9obj implements access to Plan 9 a.out object files.
- [encoding](https://golang.org/pkg/encoding/): Package encoding defines interfaces shared by other packages that convert data to and from byte-level and textual representations.
	- [ascii85](https://golang.org/pkg/encoding/ascii85/): Package ascii85 implements the ascii85 data encoding as used in the btoa tool and Adobe’s PostScript and PDF document formats.
	- [asn1](https://golang.org/pkg/encoding/asn1/): Package asn1 implements parsing of DER-encoded ASN.1 data structures, as defined in ITU-T Rec X.690.
	- [base32](https://golang.org/pkg/encoding/base32/): Package base32 implements base32 encoding as specified by RFC 4648.
	- [base64](https://golang.org/pkg/encoding/base64/): Package base64 implements base64 encoding as specified by RFC 4648.
	- [binary](https://golang.org/pkg/encoding/binary/): Package binary implements simple translation between numbers and byte sequences and encoding and decoding of varints.
	- [csv](https://golang.org/pkg/encoding/csv/): Package csv reads and writes comma-separated values (CSV) files.
	- [gob](https://golang.org/pkg/encoding/gob/): Package gob manages streams of gobs - binary values exchanged between an Encoder (transmitter) and a Decoder (receiver).
	- [hex](https://golang.org/pkg/encoding/hex/): Package hex implements hexadecimal encoding and decoding.
	- [json](https://golang.org/pkg/encoding/json/): Package json implements encoding and decoding of JSON as defined in RFC 7159.
	- [pem](https://golang.org/pkg/encoding/pem/): Package pem implements the PEM data encoding, which originated in Privacy Enhanced Mail.
	- [xml](https://golang.org/pkg/encoding/xml/): Package xml implements a simple XML 1.0 parser that understands XML name spaces.
- [errors](https://golang.org/pkg/errors/): Package errors implements functions to manipulate errors.
- [expvar](https://golang.org/pkg/expvar/): Package expvar provides a standardized interface to public variables, such as operation counters in servers.
- [flag](https://golang.org/pkg/flag/): Package flag implements command-line flag parsing.
- [fmt](https://golang.org/pkg/fmt/): Package fmt implements formatted I/O with functions analogous to C’s printf and scanf.
- [go](https://golang.org/pkg/go/):
	- [ast](https://golang.org/pkg/go/ast/): Package ast declares the types used to represent syntax trees for Go packages.
	- [build](https://golang.org/pkg/go/build/): Package build gathers information about Go packages.
	- [constant](https://golang.org/pkg/go/constant/): Package constant implements Values representing untyped Go constants and their corresponding operations.
	- [doc](https://golang.org/pkg/go/doc/): Package doc extracts source code documentation from a Go AST.
	- [format](https://golang.org/pkg/go/format/): Package format implements standard formatting of Go source.
	- [importer](https://golang.org/pkg/go/importer/): Package importer provides access to export data importers.
	- [parser](https://golang.org/pkg/go/parser/): Package parser implements a parser for Go source files.
	- [printer](https://golang.org/pkg/go/printer/): Package printer implements printing of AST nodes.
	- [scanner](https://golang.org/pkg/go/scanner/): Package scanner implements a scanner for Go source text.
	- [token](https://golang.org/pkg/go/token/): Package token defines constants representing the lexical tokens of the Go programming language and basic operations on tokens (printing, predicates).
	- [types](https://golang.org/pkg/go/types/): Package types declares the data types and implements the algorithms for type-checking of Go packages.
- [hash](https://golang.org/pkg/hash/): Package hash provides interfaces for hash functions.
	- [adler32](https://golang.org/pkg/hash/adler32/): Package adler32 implements the Adler-32 checksum.
	- [crc32](https://golang.org/pkg/hash/crc32/): Package crc32 implements the 32-bit cyclic redundancy check, or CRC-32, checksum.
	- [crc64](https://golang.org/pkg/hash/crc64/): Package crc64 implements the 64-bit cyclic redundancy check, or CRC-64, checksum.
	- [fnv](https://golang.org/pkg/hash/fnv/): Package fnv implements FNV-1 and FNV-1a, non-cryptographic hash functions created by Glenn Fowler, Landon Curt Noll, and Phong Vo.
	- [maphash](https://golang.org/pkg/hash/maphash/): Package maphash provides hash functions on byte sequences.
- [html](https://golang.org/pkg/html/): Package html provides functions for escaping and unescaping HTML text.
	- [template](https://golang.org/pkg/html/template/): Package template (html/template) implements data-driven templates for generating HTML output safe against code injection.
- [image](https://golang.org/pkg/image/): Package image implements a basic 2-D image library.
	- [color](https://golang.org/pkg/image/color/): Package color implements a basic color library.
		- [palette](https://golang.org/pkg/image/color/palette/): Package palette provides standard color palettes.
	- [draw](https://golang.org/pkg/image/draw/): Package draw provides image composition functions.
	- [gif](https://golang.org/pkg/image/gif/): Package gif implements a GIF image decoder and encoder.
	- [jpeg](https://golang.org/pkg/image/jpeg/): Package jpeg implements a JPEG image decoder and encoder.
	- [png](https://golang.org/pkg/image/png/): Package png implements a PNG image decoder and encoder.
- [index](https://golang.org/pkg/index/):
	- [suffixarray](https://golang.org/pkg/index/suffixarray/): Package suffixarray implements substring search in logarithmic time using an in-memory suffix array.
- [io](https://golang.org/pkg/io/): Package io provides basic interfaces to I/O primitives.
	- [ioutil](https://golang.org/pkg/io/ioutil/): Package ioutil implements some I/O utility functions.
- [log](https://golang.org/pkg/log/): Package log implements a simple logging package.
	- [syslog](https://golang.org/pkg/log/syslog/): Package syslog provides a simple interface to the system log service.
- [math](https://golang.org/pkg/math/): Package math provides basic constants and mathematical functions.
	- [big](https://golang.org/pkg/math/big/): Package big implements arbitrary-precision arithmetic (big numbers).
	- [bits](https://golang.org/pkg/math/bits/): Package bits implements bit counting and manipulation functions for the predeclared unsigned integer types.
	- [cmplx](https://golang.org/pkg/math/cmplx/): Package cmplx provides basic constants and mathematical functions for complex numbers.
	- [rand](https://golang.org/pkg/math/rand/): Package rand implements pseudo-random number generators.
- [mime](https://golang.org/pkg/mime/): Package mime implements parts of the MIME spec.
	- [multipart](https://golang.org/pkg/mime/multipart/): Package multipart implements MIME multipart parsing, as defined in RFC 2046.
	- [quotedprintable](https://golang.org/pkg/mime/quotedprintable/): Package quotedprintable implements quoted-printable encoding as specified by RFC 2045.
- [net](https://golang.org/pkg/net/): Package net provides a portable interface for network I/O, including TCP/IP, UDP, domain name resolution, and Unix domain sockets.
	- [http](https://golang.org/pkg/net/http/): Package http provides HTTP client and server implementations.
		- [cgi](https://golang.org/pkg/net/http/cgi/): Package cgi implements CGI (Common Gateway Interface) as specified in RFC 3875.
		- [cookiejar](https://golang.org/pkg/net/http/cookiejar/): Package cookiejar implements an in-memory RFC 6265-compliant http.CookieJar.
		- [fcgi](https://golang.org/pkg/net/http/fcgi/): Package fcgi implements the FastCGI protocol.
		- [httptest](https://golang.org/pkg/net/http/httptest/): Package httptest provides utilities for HTTP testing.
		- [httptrace](https://golang.org/pkg/net/http/httptrace/): Package httptrace provides mechanisms to trace the events within HTTP client requests.
		- [httputil](https://golang.org/pkg/net/http/httputil/): Package httputil provides HTTP utility functions, complementing the more common ones in the net/http package.
		- [pprof](https://golang.org/pkg/net/http/pprof/): Package pprof serves via its HTTP server runtime profiling data in the format expected by the pprof visualization tool.
	- [mail](https://golang.org/pkg/net/mail/): Package mail implements parsing of mail messages.
	- [rpc](https://golang.org/pkg/net/rpc/): Package rpc provides access to the exported methods of an object across a network or other I/O connection.
		- [jsonrpc](https://golang.org/pkg/net/rpc/jsonrpc/): Package jsonrpc implements a JSON-RPC 1.0 ClientCodec and ServerCodec for the rpc package.
	- [smtp](https://golang.org/pkg/net/smtp/): Package smtp implements the Simple Mail Transfer Protocol as defined in RFC 5321.
	- [textproto](https://golang.org/pkg/net/textproto/): Package textproto implements generic support for text-based request/response protocols in the style of HTTP, NNTP, and SMTP.
	- [url](https://golang.org/pkg/net/url/): Package url parses URLs and implements query escaping.
- [os](https://golang.org/pkg/os/): Package os provides a platform-independent interface to operating system functionality.
	- [exec](https://golang.org/pkg/os/exec/): Package exec runs external commands.
	- [signal](https://golang.org/pkg/os/signal/): Package signal implements access to incoming signals.
	- [user](https://golang.org/pkg/os/user/): Package user allows user account lookups by name or id.
- [path](https://golang.org/pkg/path/): Package path implements utility routines for manipulating slash-separated paths.
	- [filepath](https://golang.org/pkg/path/filepath/): Package filepath implements utility routines for manipulating filename paths in a way compatible with the target operating system-defined file paths.
- [plugin](https://golang.org/pkg/plugin/): Package plugin implements loading and symbol resolution of Go plugins.
- [reflect](https://golang.org/pkg/reflect/): Package reflect implements run-time reflection, allowing a program to manipulate objects with arbitrary types.
- [regexp](https://golang.org/pkg/regexp/): Package regexp implements regular expression search.
	- [syntax](https://golang.org/pkg/regexp/syntax/): Package syntax parses regular expressions into parse trees and compiles parse trees into programs.
- [runtime](https://golang.org/pkg/runtime/): Package runtime contains operations that interact with Go’s runtime system, such as functions to control goroutines.
	- [cgo](https://golang.org/pkg/runtime/cgo/): Package cgo contains runtime support for code generated by the cgo tool.
	- [debug](https://golang.org/pkg/runtime/debug/): Package debug contains facilities for programs to debug themselves while they are running.
	- [msan](https://golang.org/pkg/runtime/msan/):  [pprof](https://golang.org/pkg/runtime/pprof/): Package pprof writes runtime profiling data in the format expected by the pprof visualization tool.
	- [race](https://golang.org/pkg/runtime/race/): Package race implements data race detection logic.
	- [trace](https://golang.org/pkg/runtime/trace/): Package trace contains facilities for programs to generate traces for the Go execution tracer.
- [sort](https://golang.org/pkg/sort/): Package sort provides primitives for sorting slices and user-defined collections.
- [strconv](https://golang.org/pkg/strconv/): Package strconv implements conversions to and from string representations of basic data types.
- [strings](https://golang.org/pkg/strings/): Package strings implements simple functions to manipulate UTF-8 encoded strings.
- [sync](https://golang.org/pkg/sync/): Package sync provides basic synchronization primitives such as mutual exclusion locks.
	- [atomic](https://golang.org/pkg/sync/atomic/): Package atomic provides low-level atomic memory primitives useful for implementing synchronization algorithms.
- [syscall](https://golang.org/pkg/syscall/): Package syscall contains an interface to the low-level operating system primitives.
	- [js](https://golang.org/pkg/syscall/js/): Package js gives access to the WebAssembly host environment when using the js/wasm architecture.
- [testing](https://golang.org/pkg/testing/): Package testing provides support for automated testing of Go packages.
	- [iotest](https://golang.org/pkg/testing/iotest/): Package iotest implements Readers and Writers useful mainly for testing.
	- [quick](https://golang.org/pkg/testing/quick/): Package quick implements utility functions to help with black box testing.
- [text](https://golang.org/pkg/text/)
	- [scanner](https://golang.org/pkg/text/scanner/): Package scanner provides a scanner and tokenizer for UTF-8-encoded text.
	- [tabwriter](https://golang.org/pkg/text/tabwriter/): Package tabwriter implements a write filter (tabwriter.Writer) that translates tabbed columns in input into properly aligned text.
	- [template](https://golang.org/pkg/text/template/): Package template implements data-driven templates for generating textual output.
		- [parse](https://golang.org/pkg/text/template/parse/): Package parse builds parse trees for templates as defined by text/template and html/template.
- [time](https://golang.org/pkg/time/): Package time provides functionality for measuring and displaying time.
- [unicode](https://golang.org/pkg/unicode/): Package unicode provides data and functions to test some properties of Unicode code points.
	- [utf16](https://golang.org/pkg/unicode/utf16/): Package utf16 implements encoding and decoding of UTF-16 sequences.
	- [utf8](https://golang.org/pkg/unicode/utf8/): Package utf8 implements functions and constants to support text encoded in UTF-8.
- [unsafe](https://golang.org/pkg/unsafe/): Package unsafe contains operations that step around the type safety of Go programs.


### Sub-repositories
These packages are part of the Go Project but outside the main Go tree. They are developed under looser  [compatibility requirements](https://golang.org/doc/go1compat)  than the Go core. Install them with “ [go get](https://golang.org/cmd/go/#hdr-Download_and_install_packages_and_dependencies) “.
*  [benchmarks](https://godoc.org/golang.org/x/benchmarks)  — benchmarks to measure Go as it is developed.
*  [blog](https://godoc.org/golang.org/x/blog)  —  [blog.golang.org](https://blog.golang.org/) ’s implementation.
*  [build](https://godoc.org/golang.org/x/build)  —  [build.golang.org](https://build.golang.org/) ’s implementation.
*  [crypto](https://godoc.org/golang.org/x/crypto)  — additional cryptography packages.
*  [debug](https://godoc.org/golang.org/x/debug)  — an experimental debugger for Go.
*  [image](https://godoc.org/golang.org/x/image)  — additional imaging packages.
*  [mobile](https://godoc.org/golang.org/x/mobile)  — experimental support for Go on mobile platforms.
*  [net](https://godoc.org/golang.org/x/net)  — additional networking packages.
*  [perf](https://godoc.org/golang.org/x/perf)  — packages and tools for performance measurement, storage, and analysis.
*  [review](https://godoc.org/golang.org/x/review)  — a tool for working with Gerrit code reviews.
*  [sync](https://godoc.org/golang.org/x/sync)  — additional concurrency primitives.
*  [sys](https://godoc.org/golang.org/x/sys)  — packages for making system calls.
*  [text](https://godoc.org/golang.org/x/text)  — packages for working with text.
*  [time](https://godoc.org/golang.org/x/time)  — additional time packages.
*  [tools](https://godoc.org/golang.org/x/tools)  — godoc, goimports, gorename, and other tools.
*  [tour](https://godoc.org/golang.org/x/tour)  —  [tour.golang.org](https://tour.golang.org/) ’s implementation.
*  [exp](https://godoc.org/golang.org/x/exp)  — experimental and deprecated packages (handle with care; may change without warning).



### References
- [Go by Example](https://gobyexample.com/)
- [Documentation - The Go Programming Language](https://golang.org/doc/)
	- [Package Documentation](https://golang.org/pkg/): The documentation for the Go standard library.
	- [Command Documentation](https://golang.org/doc/cmd): The documentation for the Go tools.
	- [Language Specification](https://golang.org/ref/spec): The official Go Language specification.
	- [The Go Memory Model](https://golang.org/ref/mem): A document that specifies the conditions under which reads of a variable in one goroutine can be guaranteed to observe values produced by writes to the same variable in a different goroutine.
	- [Release History](https://golang.org/doc/devel/release.html): A summary of the changes between Go releases.
- [API Resources for Go Developers - API Guide](https://www.moesif.com/blog/api-guide/development/api-resources-for-go-developers/)
- https://flaviocopes.com/golang-tutorial-rest-api/
- [Making a RESTful JSON API in Go – The New Stack](https://thenewstack.io/make-a-restful-json-api-go/)


# Golang Notes

### <u>Basic Syntax</u>

A Go program consists of various tokens. <u>*A token is either a keyword, an identifier, a constant, a string literal, or a symbol.*</u> 

For example, the following Go statement consists of 6 tokens: 

```go
fmt.Println("Hello, World!")
```

The individual tokens are :

```go
fmt
.
Println
(
	"Hello, World!"
)
```

Comments are like helping texts in your Go program. They start with /* and ends with */ as shown below:

```go
/* comment */
```



### <u>Data Types</u>

1. Boolean types: They consist of 2 predefined constants, (a) true and (b) false, hence only comparison and logical operation can be performed. 

   Examples of comparison operation for Boolean types: 

   - Equality operator (==)
   - Inequality operator (!=)
   - Less than operator (<)
   - Greater than operator (>)
   - Less than equal to (<=)
   - Greater than equal to (>=)

   Examples of logical operation for Boolean types: 

   - Logical AND (&&)
   - Logical OR (||)
   - Logical NOT (!)
   - Logical EXCLUSIVE OR (^)
   - Logical AND NOT (&^)

   ```go
   package main
   
   import "fmt"
   
   // comparison operations
   func main() {
       var num1 = 10 
       var num2 = 12
       var res1 = num1 == num2 //false
       var res2 = num1 != num2 //true
       var res3 = num1 > num2 //false
       var res4 = num1 < num2 //true
       var res5 = num1 <= num2 //true
       var res6 = num1 >= num2 //false
   }
   
   //logical operations
   func main() {
       var enum1 = 12<5 && 12==12 //false
       var enum2 = 5*2==10 || 23%2==10 //true
   }
   ```

   ```go
   package main
   
   import (
   	"fmt"
   )
   
   func main() {
       a := 10             //1010 
       b := 3              //0011 
       fmt.Println(a & b)  //0010 (2)
       fmt.Println(a | b)  //1011 (11)
       fmt.Println(a ^ b)  //1001 (9)
       fmt.Println(a &^ b) //0100 (8)
   }
   ```

   For bit-shifting in Golang, `<<` means left shift and `>>` means right shift. So `n << x` is "n times 2, x times". And `y >> z` is "y divided by 2, z times"

   ```go
   package main
   
   import (
   	"fmt"
   )
   
   func main() {
       a := 8 //2^3
       fmt.Println(a << 3) //2^3 * 2^3 = 2^6 [64]
       fmt.Println(a >> 3) //2^3 / 2^3 = 2^0 [1]
   }
   ```

   

2. Numeric types: They are arithmetic types and represents integer types or floating point values throughout the program

   <u>Examples of integer (whole numbers) types are:</u> 

   - uint8 - Unsigned 8-bit integers (0 to 255)
   - uint16 - Unsigned 16-bit integers (0 to 65535)
   - uint32 - Unsigned 32-bit integers (0 to 4294967295)
   - uint64 - Unsigned 64-bit integers (0 to 18446744073709551615)
   - int8 - Signed 8-bit integers (-128 to 127)
   - int16 - Signed 16-bit integers (-32768 to 32767)
   - int32 - Signed 32-bit integers (-2147483648 to 2147483647)
   - int64 - Signed 64-bit integers (-9223372036854775808 to 9223372036854775807)

   <u>Examples of floating (can include potential decimal places) types are:</u>

   - float32 - IEEE-754 32-bit floating-point numbers
   - float64 - IEEE-754 64-bit floating-point numbers
   - complex64 - Complex numbers with float32 real and imaginary parts
   - complex128 - Complex numbers with float64 real and imaginary parts

   <u>Examples of other numeric types:</u>

   - byte - same as uint8
   - rune - same as int32
   - uint - 32 or 64 bits
   - int - same size as uint
   - uintptr - an unsigned integer to store the uninterpreted bits of a pointer value

3. String types: They represent the set of string values. Its value is a sequence of bytes. Strings are immutable types when created meaning cannot change the contents of the string. 

4. Derived types: They include (a) Pointer types, (b) Array types, (c) Structure types, (d) Union types and (e) Function types f) Slice types g) Interface types h) Map types  i) Channel Types

### <u>Variables</u>

A variable specifies a data type and contains a list of one or more variables of that type as follows - 

> var variable_list optional_data_type;

A static type variable declaration provides assurance to the compiler that there is one variable available with the given type and name so that the compiler can proceed for further compilation without requiring the complete detail of the variable. 

```go
package main

import "fmt"

func main() {
    var x float64
    x = 20.0
    fmt.Println(x)
    fmt.Printf("x is of type %T\n", x)
}

//End result will be printed as
// 20 
// x is of type float64
```

A dynamic type variable declaration requires the compiler to interpret the type of the variable based on the value passed to it. The compiler does not require a variable to have type statistically as a necessary requirement. 

*The assignment operator (=) us used to perform assignments. i.e. to assign or reassign values to already declared variables.*

*The short declaration operator (:=) performs short variable declarations, which are shorthand for regular variable declarations but without a specified type.* 

```go
package main

import "fmt"

func main() {
   var x float64 = 20.0

    y := 42 
   fmt.Println(x)
   fmt.Println(y)
   fmt.Printf("x is of type %T\n", x)
   fmt.Printf("y is of type %T\n", y)	
}

// End result will be printed as
// 20 
// 42
// x is of type float64
// y is of type int
```

A mixed variable declaration is variables of different types that can be declared in one go using type inference. 

```go
package main

import "fmt"

func main() {
   var a, b, c = 3, 4, "foo"  
	
   fmt.Println(a)
   fmt.Println(b)
   fmt.Println(c)
   fmt.Printf("a is of type %T\n", a)
   fmt.Printf("b is of type %T\n", b)
   fmt.Printf("c is of type %T\n", c)
}

// End result will be printed as
// 3 
// 4 
// foo
// a is of type int 
// b is of type int
// c is of type foo
```

### <u>Variable Shadowing</u>

A variable is said to be shadowing another variable if it "overrides" the variable in a more specific scope. Below is an example of shadowing: 

```go
func main() {
	n := 0 
    if true {
        n := 1
        n++
    }
    fmt.Println(n) //2
}
```

The statement `n := 1` declares a new variable which shadows the original `n` throughout the scope of the *if* statement. 



To help detect shadowed variables, we can use a command function in the command line terminal to give us a warning message in our code or programs. 

```
$ go vet -shadow main.go
main.go:4: declaration of "n" shadows declaration at main.go:2
```



### <u>Printing</u>

Below are the list of verbs which can be used for printing in Golang. 

General: 

> ```
> %v	the value in a default format
> 	when printing structs, the plus flag (%+v) adds field names
> %#v	a Go-syntax representation of the value
> %T	a Go-syntax representation of the type of the value
> %%	a literal percent sign; consumes no value
> ```

Boolean:

> ```
> %t	the word true or false
> ```

Integer: 

> ```
> %b	base 2
> %c	the character represented by the corresponding Unicode code point
> %d	base 10
> %o	base 8
> %O	base 8 with 0o prefix
> %q	a single-quoted character literal safely escaped with Go syntax.
> %x	base 16, with lower-case letters for a-f
> %X	base 16, with upper-case letters for A-F
> %U	Unicode format: U+1234; same as "U+%04X"
> ```

Floating-point and complex constituents: 

> ```
> %b	decimalless scientific notation with exponent a power of two,
> 	in the manner of strconv.FormatFloat with the 'b' format,
> 	e.g. -123456p-78
> %e	scientific notation, e.g. -1.234456e+78
> %E	scientific notation, e.g. -1.234456E+78
> %f	decimal point but no exponent, e.g. 123.456
> %F	synonym for %f
> %g	%e for large exponents, %f otherwise. Precision is discussed below.
> %G	%E for large exponents, %F otherwise
> %x	hexadecimal notation (with decimal power of two exponent), e.g. -0x1.23abcp+20
> %X	upper-case hexadecimal notation, e.g. -0X1.23ABCP+20
> ```

String and slice of bytes (treated equivalently with these verbs):

> ```
> %s	the uninterpreted bytes of the string or slice
> %q	a double-quoted string safely escaped with Go syntax
> %x	base 16, lower-case, two characters per byte
> %X	base 16, upper-case, two characters per byte
> ```

Slice:

> ```
> %p	address of 0th element in base 16 notation, with leading 0x
> ```

Pointer: 

> ```
> %p	base 16 notation, with leading 0x
> The %b, %d, %o, %x and %X verbs also work with pointers,
> formatting the value exactly as if it were an integer.
> ```

**The default format for %v is:**

> ```
> bool:                    %t
> int, int8 etc.:          %d
> uint, uint8 etc.:        %d, %#x if printed with %#v
> float32, complex64, etc: %g
> string:                  %s
> chan:                    %p
> pointer:                 %p
> ```

### <u>String Conversion</u>

To convert an integer to a string, use a package from the standard library called, "**strconv**". Below is the syntax on how to use the function called, "**FormatInt**" to convert integer values to string or vice versa: 

> func FormatInt(i int64, base int) string

Below is the syntax of another function called, "**Itoa**" which is a shorter function and performs the same functionality: 

> func Itoa(i int) string

<u>An example on how to convert integer to string:</u> 	

```go
package main

import (
  "fmt"
  "strconv"
)

func main() {
  i := 10
  s1 := strconv.FormatInt(int64(i), 10)
  s2 := strconv.Itoa(i)
  fmt.Printf("%v, %v\n", s1, s2)
}

// End result will be printed as
// 10, 10
```

### <u>Constants</u>

Constants are declared like variables, but with the `const` keyword. 

Constants can be character, string, boolean, or numeric values. 

Constants cannot be declared using the `:=` syntax. 

A `const` statement can appear anywhere a `var` statement can. 

A numeric constant has no type until it's given one, such as by an explicit conversion. 

<u>An example of declaring a constant:</u> 

```go
package main

import (  
    "fmt"
)

func main() {  
    const a = 50
    fmt.Println(a)
}
```

<u>An example of declaring a group of constants:</u> 

```go
package main

import (  
    "fmt"
)

func main() {  
    const (
        name = "John"
        age = 50
        country = "Canada"
    )
    fmt.Println(name)
    fmt.Println(age)
    fmt.Println(country)

}
```

**Constants cannot be reassigned again to any other value. If we try to run a program to reassign a constant value, the program will fail to run with compilation error.** 

<u>An example can be found below:</u> 

```go
package main

func main() {  
    const a = 55 //allowed
    a = 89 //reassignment not allowed
}
```

Any value enclosed between double quotes is a string constant in Go. For example, strings like `"Hello World"`, `"Sam"` are all constants in Go. 

What type does a string constant belong to? The answer is they are **untyped**.

```go
package main

import (  
    "fmt"
)

func main() {  
    const n = "Sam"
    var name = n
    fmt.Printf("type %T value %v", name, name)

}

// output value: 
// type string value Sam
```

**Untyped constants have a default type associated with them and they supply it if and only is a line of code demands it. In the statement `var name =n`, `name` needs a type and it gets it from the default type of the string constant `n` which is a string.**

An example below is to create a typed constant: 

```go
const typedhello string = "Hello World"
```

*typedhello* in the above code is a constant of type string. 

Boolean constants are two untyped constants `true` and `false`. Below is an example of boolean constants:

```go
package main

func main() {  
    const trueConst = true
    type myBool bool
    var defaultBool = trueConst //allowed
    var customBool myBool = trueConst //allowed
    defaultBool = customBool //not allowed
}
```

Numeric constants include integers, floats and complex constants. Below is an example of numeric constants: 

```go
package main

import (  
    "fmt"
)

func main() {  
    const a = 5
    var intVar int = a
    var int32Var int32 = a
    var float64Var float64 = a
    var complex64Var complex64 = a
    fmt.Println("intVar",intVar, "\nint32Var", int32Var, "\nfloat64Var", float64Var, "\ncomplex64Var",complex64Var)
}

// output value: 
// intVar 5 
// int32Var 5 
// float64Var 5 
// complex64Var (5+0i)
```

The `iota` keyword represents successive integer constants 0, 1, 2, and so forth. 

It resets to 0 whenever the word `const` appears in the source code and increments after each const specification. 

```go
const (
    C0 = iota
    C1 = iota
    C2 = iota
)

// To simplify the above
const (
	C0 = iota
    C1
    C2
)

fmt.Println(C0, C1, C2) // "0 1 2"
```

To start a list of constants at 1 instead of 0: 

```go
const (
    C1 = iota + 1
    C2
    C3
)
fmt.Println(C1, C2, C3) // "1 2 3"
```

To skip a value, use the blank identifier to skip a value in a list of constants: 

```go
const (
    C1 = iota + 1
    _
    C3
    C4
)
fmt.Println(C1, C3, C4) // "1 3 4"
```

### **<u>Arrays</u>**

An array is a data structure that consists of a collection of elements of a single type or simply a special variable, which can hole more than one value at a time. Different data types can be handled as elements in arrays such as **Int**, **String**, **Boolean**, and others. The index of the first element of any dimension of an array is 0, the index of the second element of any array dimension is 1, and  so on.

**<u>Syntax for array:</u>** 

```
Var array_name[length]Type
or
var array_name[length]Type{item1, item2, item3, ...itemN}
```

<u>Declaring an array:</u> 

```go
package main

import (
	"fmt"
	"reflect"
)

func main() {
	var intArray [5]int
	var strArray [5]string

	fmt.Println(reflect.ValueOf(intArray).Kind())
	fmt.Println(reflect.ValueOf(strArray).Kind())
}

// output value: 
// array 
// array
```

<u>Assign and access values in an array:</u> 

```go
package main

import "fmt"

func main() {
	var theArray [3]string
	theArray[0] = "India"  // Assign a value to the first element
	theArray[1] = "Canada" // Assign a value to the second element
	theArray[2] = "Japan"  // Assign a value to the third element

	fmt.Println(theArray[0]) // Access the first element value
	fmt.Println(theArray[1]) // Access the second element valu
	fmt.Println(theArray[2]) // Access the third element valu
}

// output value: 
// India
// Canada 
// Japan
```



We can initialize an array with pre-defined values using an array literal, also known as shorthand declaration. An array literal have the number of elements it will hold in square brackets, followed by the type of its elements.  

**<u>Syntax for shorthand declaration:</u>**

```
array_name:= [length]Type{item1, item2, item3, ...itemN}
```

<u>Below is an example of array literal:</u> 

```go
package main

import "fmt"

func main() {
	x := [5]int{10, 20, 30, 40, 50}   // Intialized with values
	var y [5]int = [5]int{10, 20, 30} // Partial assignment

	fmt.Println(x)
	fmt.Println(y)
}

// output
// [10 20 30 40 50]
// [10 20 30 0 0]
```



The three dots (...) in Golang is termed as Ellipsis which is used in the variadic function. A user is allowed to pass zero or more arguments in the variadic function. An example of the variadic function is `Printf` as it requires one fixed argument at the starting after that it can accept any number of arguments.

<u>(1) Initializing an Array with ellipsis:</u>

```go
package main
  
import "fmt"
  
func main() {
    sayHello()
    sayHello("Rahul")
    sayHello("Mohit", "Rahul", "Rohit", "Johny")
}
  
// using Ellipsis
func sayHello(names ...string) {
    for _, n := range names {
        fmt.Printf("Hello %s\n", n)
    }
}

// output value: 
// Hello Rahul
// Hello Mohit
// Hello Rahul
// Hello Rohit
// Hello Johny
```

 <u>(2) Initializing an Array with ellipsis:</u> 

```go
package main

import (
	"fmt"
	"reflect"
)

func main() {
	x := [...]int{10, 20, 30}

	fmt.Println(reflect.ValueOf(x).Kind())
	fmt.Println(len(x))
}

// output value: 
// array 
// 3
```

In Go language, we can create a multi-dimensional array, they are the arrays of arrays of the same type. 

**<u>Syntax for multi-dimensional array:</u>**

```
Array_name[Length1][Length2]..[LengthN]Type
```

<u>Create a multidimensional array using *Var keyword* or using *shorthand declaration* in the below example:</u>

```go
package main
  
import "fmt"
  
func main() {
  
// Creating and initializing 
// 2-dimensional array 
// Using shorthand declaration
// Here the (,) Comma is necessary
arr:= [3][3]string{{"C#", "C", "Python"}, 
                   {"Java", "Scala", "Perl"},
                    {"C++", "Go", "HTML"},}
  
// Accessing the values of the 
// array Using for loop
fmt.Println("Elements of Array 1")
for x:= 0; x < 3; x++{
for y:= 0; y < 3; y++{
fmt.Println(arr[x][y])
}
}
  
// Creating a 2-dimensional
// array using var keyword
// and initializing a multi
// -dimensional array using index
var arr1 [2][2] int
arr1[0][0] = 100
arr1[0][1] = 200
arr1[1][0] = 300
arr1[1][1] = 400
  
// Accessing the values of the array
fmt.Println("Elements of array 2")
for p:= 0; p<2; p++{
for q:= 0; q<2; q++{
fmt.Println(arr1[p][q])
  
}
}
}

// Output value:
// Elements of Array 1
// C#
// C
// Python
// Java
// Scala
// Perl
// C++
// Go
// HTML
// Elements of array 2
// 100
// 200
// 300
// 400
```

### **<u>Slices</u>**

Slices is a more powerful, flexible, convenient than an array, and is a lightweight data structure. Slice is a variable-length sequence which stores elements of a similar type, we **are not allowed to store different type of elements in the same slice**. 

A slice is a reference to an underlying array. It is allowed to store duplicate elements in the slice. 

The first index position in a slice is always 0 and the last one will be `(length of slice - 1)`. 

**<u>Syntax for declaration of slice:</u>**

```
[]T
or 
[]T{}
or 
[]T{value1, value2, value3, ...value n}
```

```
var my_slice[]int
```

A slice contains 3 components: 

1. Pointer - used to points to the first element of the array that is accessible through the slice. 
2. Length - total number of elements present in the array. 
3. Capacity - the maximum size up to which it can expand. 

<u>Example of slice:</u>

```go
package main
 
import "fmt"
 
func main() {
 
    // Creating an array
    arr := [7]string{"This", "is", "the", "tutorial",
                         "of", "Go", "language"}
 
    // Display array
    fmt.Println("Array:", arr)
 
    // Creating a slice
    myslice := arr[1:6]
 
    // Display slice
    fmt.Println("Slice:", myslice)
 
    // Display length of the slice
    fmt.Printf("Length of the slice: %d", len(myslice))
 
    // Display the capacity of the slice
    fmt.Printf("\nCapacity of the slice: %d", cap(myslice))
}

// output value: 
// Array: [This is the tutorial of Go language]
// Slice: [is the tutorial of Go]
// Length of the slice: 5
// Capacity of the slice: 6
```

In the above example, the length of the slice is 5, which means the total number of elements present in the slice is 5 and the capacity of the slice 6 means it can store a maximum of 6 elements in it. 



We can create a slice using the slice literal. The creation of slice literal is just like an array literal, but are not allowed to specify the size of the slice in the square braces[]. 

**<u>Syntax for slice literal:</u>**

```
var my_slice_1 = []string{"Geeks", "for", "Geeks"}
```

Creating a slice using a string literal, will first create an array and after that return a slice reference to it. 

```go
package main
 
import "fmt"
 
func main() {
 
    // Creating a slice
    // using the var keyword
    var my_slice_1 = []string{"Geeks", "for", "Geeks"}
 
    fmt.Println("My Slice 1:", my_slice_1)
 
    // Creating a slice
    //using shorthand declaration
    my_slice_2 := []int{12, 45, 67, 56, 43, 34, 45}
    fmt.Println("My Slice 2:", my_slice_2)
}

// output value:
// My Slice 1: [Geeks for Geeks]
// My Slice 2: [12 45 67 56 43 34 45]
```

**<u>Syntax for creating a slice using an array:</u>**

```
array_name[low:high]
```

For creating a slice from the given array, will need to specify the lower and upper bound, which means slice can take elements from the array starting from the lower bound to the upper bound. 

The default value of the lower bound is 0 and the default value of the upper bound is the total number of the elements present in the given array. 

<u>Example:</u>

```go
package main
 
import "fmt"
 
func main() {
 
    // Creating an array
    arr := [4]string{"Geeks", "for", "Geeks", "GFG"}
 
    // Creating slices from the given array
    var my_slice_1 = arr[1:2]
    my_slice_2 := arr[0:]
    my_slice_3 := arr[:2]
    my_slice_4 := arr[:]
 
    // Display the result
    fmt.Println("My Array: ", arr)
    fmt.Println("My Slice 1: ", my_slice_1)
    fmt.Println("My Slice 2: ", my_slice_2)
    fmt.Println("My Slice 3: ", my_slice_3)
    fmt.Println("My Slice 4: ", my_slice_4)
}

// output value:
// My Array:  	[Geeks for Geeks GFG]
// My Slice 1:  [for]
// My Slice 2:  [Geeks for Geeks GFG]
// My Slice 3:  [Geeks for]
// My Slice 4:  [Geeks for Geeks GFG]
```



Create a slice using the make() function. This function take 3 parameters: type, length and capacity. Generally, make() function is used to create an empty slice. 

**<u>Syntax to create a slice using make() function:</u>**

```
func make([]T, len, cap) []T
```

<u>Example:</u>

```go
package main
 
import "fmt"
 
func main() {
 
    // Creating an array of size 7
    // and slice this array  till 4
    // and return the reference of the slice
    // Using make function
    var my_slice_1 = make([]int, 4, 7)
    fmt.Printf("Slice 1 = %v, \nlength = %d, \ncapacity = %d\n",
                   my_slice_1, len(my_slice_1), cap(my_slice_1))
 
    // Creating another array of size 7
    // and return the reference of the slice
    // Using make function
    var my_slice_2 = make([]int, 7)
    fmt.Printf("Slice 2 = %v, \nlength = %d, \ncapacity = %d\n",
                   my_slice_2, len(my_slice_2), cap(my_slice_2))
     
}

// output value:
// Slice 1 = [0 0 0 0], 
// length = 4, 
// capacity = 7
// Slice 2 = [0 0 0 0 0 0 0], 
// length = 7, 
// capacity = 7
```

In Go language, we are allowed to create a nil slice that does not contain any element in it. So the capacity and the length of the slice is 0. Nil slice does not contain an array reference: 

```go
package main
 
import "fmt"
 
func main() {
 
    // Creating a zero value slice
    var myslice []string
    fmt.Printf("Length = %d\n", len(myslice))
    fmt.Printf("Capacity = %d ", cap(myslice))
 
}

// output value:
// Length = 0
// Capacity = 0
```


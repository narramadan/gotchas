# Go Gotchas

## Data types

* int, int8, int16, int64, and int64 - represents a whole number, which can be positive or negative.
* uint, uint8, uint16, uint32, and uint64 - represents a positive whole number.
* byte - alias for uint8 and is typically used to represent a byte of data.
* float32, float64 - represent numbers with a fraction. These types allocate 32 or 64 bits to store the value
* complex64, complex128 - represent numbers that have real and imaginary components. These types allocate 64 or 128 bits to store the value.
* bool - represents a Boolean truth with the values true and false.
* string - represents a sequence of characters.
* rune - represents a single Unicode code point. Unicode is complicated, but—loosely—this is the representation of a single character. The rune type is an alias for int32.

## iota

__iota__ identifier is used in const declarations to simplify definitions of incrementing numbers. Because it can be used in expressions, it provides a generality beyond that of simple enumerations.

```
const (
Watersports = iota
Soccer
Chess
)
--
type ByteSize float64

const (
    _           = iota // ignore first value by assigning to blank identifier
    KB ByteSize = 1 << (10 * iota)
    MB
    GB
    TB
    PB
    EB
    ZB
    YB
)
```

## * and & Operator

`&` goes in front of a variable when you want to get that variable's memory address. `*` goes in front of a variable that holds a memory address and resolves it.

`&` Operator gets the memory address where as `*` Opeartor holds the memory address of particular variable.

## Converting Floating-Point Values to Integers

```
import (
  "math"
)

math.Ceil
math.Floor
math.Round
math.RoundToEven
```

## Converstions & Parsing from Strings 

```
import (
  "math"
)

strconv.ParseBool - parses a string into a bool value. Recognized string values are "true", "false", "TRUE", "FALSE", "True", "False", "T", "F", "0", and "1"
strconv.ParseFloat - parses a string into a floating-point value with the specified size, as described in the “Parsing Floating-Point Numbers” section
strconv.ParseInt - parses a string into an int64 with the specified base and size. Acceptable base values are 2 for binary, 8 for octal, 16 for hex, and 10, as described in the “Parsing Integers” section
strconv.ParseUint - parses a string into an unsigned integer value with the specified base and size.
strconv.Atoi -  parses a string into a base 10 int and is equivalent to calling ParseInt(str, 10, 0)

strconv.Itoa(val) - returns a string representation of the specified int value, expressed using base 10.
FormatBool(val) - returns the string true or false based on the value of the specified bool.
FormatInt(val, base) - returns a string representation of the specified int64 value, expressed in the specified base.
FormatUint(val, base) - returns a string representation of the specified uint64 value, expressed in the specified base.
FormatFloat(val, format,precision, size) - returns a string representation of the specified float64 value, expressed using the specified format, precision, and size.
```

## Arrays, slice, maps

### Arrays

* Array literals
```
names := [3]string { "Kayak", "Lifejacket", "Paddle" }

names := [...]string { "Kayak", "Lifejacket", "Paddle" } - Explicit length is replaced with three periods (...), which tells the compiler to determine the array
length from the literal values.
```

* Comparing Arrays
```
names := [3]string { "Kayak", "Lifejacket", "Paddle" }
moreNames := [3]string { "Kayak", "Lifejacket", "Paddle" }

same := names == moreNames
fmt.Println("comparison:", same)
```

* Enumerating Arrays
```
names := [3]string { "Kayak", "Lifejacket", "Paddle" }

for index, value := range names {
  fmt.Println("Index:", index, "Value:", value)
}

for _, value := range names {
  fmt.Println("Value:", value)
}
```

* String array to comma-seperated string
```
reg := []string {"a","b","c"}

fmt.Println(strings.Join(reg[:], ","))
```

### Slices

slices is as a variable-length array because they are useful when you don’t know how many values you need to store or when the number changes over time.

* Defining slice
```
names := make([]string, 3)

names := []string {"Kayak", "Lifejacket", "Paddle"}
```

* Appending slice
```
names := []string {"Kayak", "Lifejacket", "Paddle"}

names = append(names, "Hat", "Gloves")

// Appending One Slice to Another
moreNames := []string { "Hat Gloves"}
appendedNames := append(names, moreNames...)

```

* Creating Slices from Existing Arrays
```
products := [4]string { "Kayak", "Lifejacket", "Paddle", "Hat"}

someNames := products[1:3]
allNames := products[:] - : is Range
```

* copying slice
```
products := [4]string { "Kayak", "Lifejacket", "Paddle", "Hat"}
allNames := products[1:]
someNames := make([]string, 2)

copy(someNames, allNames)

// output
someNames: [Lifejacket Paddle]
allNames [Lifejacket Paddle Hat]

// Specify range when copying
products := [4]string { "Kayak", "Lifejacket", "Paddle", "Hat"}
allNames := products[1:]
someNames := []string { "Boots", "Canoe"}

copy(someNames[1:], allNames[2:3]
```

* deleting slice
```
// There is no built-in function for deleting slice elements, but this operation can be performed using the ranges and the append function

products := [4]string { "Kayak", "Lifejacket", "Paddle", "Hat"}

deleted := append(products[:2], products[3:]...)
  fmt.Println("Deleted:", deleted)
}

// output
Deleted: [Kayak Lifejacket Hat]
```

* sorting slice
```
import (
  "fmt"
  "sort"
)

products := []string { "Kayak", "Lifejacket", "Paddle", "Hat"}
sort.Strings(products)

for index, value := range products {
  fmt.Println("Index:", index, "Value:", value)
}
```

* Length and Capacity
```
len(names) - length of a slice is how many values it can currently contain

cap(names) - capacity will always be at least the length but can be larger if additional capacity has been allocated with the make function
```

### Maps

```
products := make(map[string]float64, 10)

products["Kayak"] = 279
products["Lifejacket"] = 48.95

fmt.Println("Map size:", len(products))
fmt.Println("Price:", products["Kayak"]
```

```
products := map[string]float64 {
  "Kayak" : 279,
  "Lifejacket": 48.95,
}
```

* Checking for item in map
```
products := map[string]float64 {
  "Kayak" : 279,
  "Lifejacket": 48.95,
  "Hat": 0,
}

value, ok := products["Hat"]
if (ok) {
  fmt.Println("Stored value:", value)
} else {
  fmt.Println("No stored value")
}

if value, ok := products["Hat"]; ok {
  fmt.Println("Stored value:", value)
} else {
  fmt.Println("No stored value")
}
```

* Removing item from map
```
delete(products, "Hat")
```

* Enumerating the Contents of a Map
```
for key, value := range products {
  fmt.Println("Key:", key, "Value:", value)
}

// enumerate in order
import (
  "fmt"
  "sort"
)
func main() {
  products := map[string]float64 {
    "Kayak" : 279,
    "Lifejacket": 48.95,
    "Hat": 0,
  }
  keys := make([]string, 0, len(products))
  for key, _ := range products {
    keys = append(keys, key)
  }

  sort.Strings(keys)
  for _, key := range keys {
    fmt.Println("Key:", key, "Value:", products[key])
  }
}
```

## Functions

### Variadic Parameters

A variadic parameter accepts a variable number of values, which can make functions easier to use. 

```
func printSuppliers(product string, suppliers ...string ) {
  for _, supplier := range suppliers {
    fmt.Println("Product:", product, "Supplier:", supplier)
  }
}
```

### Using Pointers as Function Parameters
```
func swapValues(first, second *int) {
  fmt.Println("Before swap:", *first, *second)
  temp := *first
  *first = *second
  *second = temp
  fmt.Println("After swap:", *first, *second)
}

func main() {
  val1, val2 := 10, 20
  fmt.Println("Before calling function", val1, val2)

  swapValues(&val1, &val2)
  fmt.Println("After calling function", val1, val2)
}

// output
Before calling function 10 20
Before swap: 10 20
After swap: 20 10
After calling function 20 10
```

## Function types

Functions have a data type in Go, which means they can be assigned to variables and used as function parameters, arguments, and results.

```
package main

import "fmt"

func calcWithTax(price float64) float64 {
    return price + (price * 0.2)
}
func calcWithoutTax(price float64) float64 {
    return price
}

func main() {

    products := map[string]float64 {
        "Kayak" : 275,
        "Lifejacket": 48.95,
    }

    for product, price := range products {
        var calcFunc func(float64) float64
        if (price > 100) {
            calcFunc = calcWithTax
        } else {
            calcFunc = calcWithoutTax
        }
        totalPrice := calcFunc(price)
        fmt.Println("Product:", product, "Price:", totalPrice)
    }
}
```

We can use function types
* As Arguments to other functions
```
func printPrice(product string, price float64, calculator func(float64) float64 ) {
    fmt.Println("Product:", product, "Price:", calculator(price))
}
```
*  As Results
```
func selectCalculator(price float64) func(float64) float64 {
    if (price > 100) {
        return calcWithTax
    }
    return calcWithoutTax
}
```
* Creating Function Type Aliases
```
type calcFunc func(float64) float64

func printPrice(product string, price float64, calculator calcFunc) {
    fmt.Println("Product:", product, "Price:", calculator(price))
}
func selectCalculator(price float64) calcFunc {
    if (price > 100) {
        return calcWithTax
    }
    return calcWithoutTax
}
```
* Literal Function Syntax
```
func selectCalculator(price float64) calcFunc {
    withTax calcFunc = func (price float64) float64 {
        return price + (price * 0.2)
    }
    // or shorthand syntax
    withoutTax := func (price float64) float64 {
        return price
    }
}
printPrice(product, price, selectCalculator(price))
```
* Function Closures
Functions defined using the literal syntax can reference variables from the surrounding code, a feature known as closure.
Refer online for example

## Structs

```
type Product struct {
    name, category string
    price float64
}

kayak := Product {
    name: "Kayak",
    category: "Watersports",
    price: 275,
}

var lifejacket = new(Product) ~ var lifejacket = &Product{}

var kayak = Product { "Kayak", "Watersports", 275.00 }

func newProduct(name, category string, price float64) *Product {
    return &Product{name, category, price}
}
```

## Methods & Interfaces

### Method
```
type Product struct {
    name, category string
    price float64
}

func (product *Product) printDetails() {
    fmt.Println("Name:", product.name, "Category:", product.category,"Price", product.price)
}

p.printDetails()
```

pg 275

## Code block for scenarios

### Create array with field value from another struct array

```
type Person struct {
    Name string
    Age  int
}

func main() {
    people := []Person{
        {Name: "Alice", Age: 30},
        {Name: "Bob", Age: 25},
        {Name: "Charlie", Age: 35},
    }

    names := make([]string, len(people))
    for i, person := range people {
        names[i] = person.Name
    }

    fmt.Println(names)
}
```

### Filter array objects matching field value

```
func filterPeopleByAge(people []Person, age int) []Person {
    var filteredPeople []Person
    for _, person := range people {
        if person.Age == age {
            filteredPeople = append(filteredPeople, person)
        }
    }
    return filteredPeople
}
```

### Convert timestamp string to date string

```
package main

import (
	"fmt"
	"time"
)

func main() {
	// Given timestamp string
	timestamp := "2024-08-30T23:26:51.574+0000"

	// Parse the timestamp
	parsedTime, err := time.Parse("2006-01-02T15:04:05.000-0700", timestamp)
	if err != nil {
		fmt.Println("Error parsing timestamp:", err)
		return
	}

	// Format the date part
	datePart := parsedTime.Format("2006-01-02")
	fmt.Println("Date part:", datePart)
}
```

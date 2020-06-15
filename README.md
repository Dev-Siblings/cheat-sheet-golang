# Cheat Sheet Golang
A cheat sheet for quick reference.

### Hello World
```go
package main

import "fmt"

func main() {
    fmt.Println("Hello World")
}
```

### Variables
```go
func main() {
	var aIntVar int = 10
	var aInt16Var int16 = 10
	var aInt32Var int32 = 10
	var aInt64Var int64 = 10
	var aFloat32Var float32 = 1.4
	var aFloat64Var float64 = 4.121212
	var aStringVar string = "A String"
	var aBoolVar bool = false
	//we can change the values since it's a variable.

	//Use const to create constant
	const aIntConst int = 100
	const aFloatConst float64 = 10.1
	const aStringConst string = "A Constant String"
	const aBoolConst bool = true

	//Can also make use of := (short variable declaration) to assign value.
	aNewVariable := 17
	multilineString := `Multiline String`

	// fmt formatting options
	fmt.Printf(" %f \\n ", aFloat32Var) //print the float value
	fmt.Printf(" %T \\n ", aFloat32Var) //print the type
	fmt.Printf(" %d \\n ", aIntVar)     //print the int value
	fmt.Printf(" %T \\n ", aIntVar)     //print the type
	fmt.Printf(" %T \\n ", aBoolVar)    //print the type
}
```

### Operators
```go
func main() {
	x, y := 100, 20

	fmt.Println("x + y", x+y)
	fmt.Println("x - y", x-y)
	fmt.Println("x * y", x*y)
	fmt.Println("x / y", x/y)
	fmt.Println("x % y", x%y)

	fmt.Println("x > y", x > y)
	fmt.Println("x < y", x < y)
	fmt.Println("x >= y", x >= y)
	fmt.Println("x == y", x == y)
	fmt.Println("x != y", x != y)

	fmt.Println("x > 100 && y > 100", x > 100 && y > 100)
	fmt.Println("x > 100 && y > 100", x > 100 || y > 100)

	var isXGreaterThan100 = x > 100
	fmt.Println(isXGreaterThan100)

	var xIsNotGreaterThan100 = !isXGreaterThan100
	fmt.Println(xIsNotGreaterThan100)
}
```

### Loops
```go
func main() {
	// for loop
	for i := 1; i <= 10; i++ {
		fmt.Println(i)
	}

	//can use for loop as while loop
	index := 5
	for index > 1 {
		fmt.Println(index)
		index--
	}
}

```

### Function
```go
func main() {
	result := aFunction()
	fmt.Println(result)

    // Anonymous Function
	fmt.Println(anonFunction()())
}

func aFunction() int {
	return 10
}

func anonFunction() func() int {
	counter := 0
	return func() int {
		counter++
		return counter
	}
}
```

### Decision Making
```go
func main() {
	age := 29
	// if-else
	if age > 18 {
		fmt.Println("Can Vote")
	} else {
		fmt.Println("Cann't vote")
	}
	//switch
	switch age {
	case 16:
		fmt.Println("prepare for college")
	case 18:
		fmt.Println("don't rush")
	case 20:
		fmt.Println("get a job")
	}
}
```

### Array
```go
func main() {
	//Create an array
	var EvenNumbers [5]int
	EvenNumbers[0] = 1
	EvenNumbers[1] = 1
	EvenNumbers[2] = 1
	EvenNumbers[3] = 1
	EvenNumbers[4] = 1
	fmt.Println(EvenNumbers[2])
	// create array using short hand
	OddNumbers := [3]int{0, 1, 2}
	fmt.Println(OddNumbers[0])
	//Interate array
	for index, value := range EvenNumbers {
		fmt.Printf("index is %d and value is %d \\n", index, value)
	}
	// slicing array forward [startIndex: endIndex]
	// if we leave index empty it will startIndex = 0
	// and endIndex = length
	numbers := []int{1, 2, 3, 4, 5}
	// sliceing
	var slicedArray = numbers[1:3]
	fmt.Printf("%d \\n", slicedArray)
	// make
	var emptyArray = make([]int, 5, 10)
	fmt.Println(emptyArray)
	// copy
	copy(emptyArray, slicedArray)
	fmt.Println(emptyArray)
	// append
	preArr := []int{1, 2}
	result := append(preArr, 3, 4)
	fmt.Println(result)
}
```

### Map
```go
func main() {
	// key => String, value => int
	StudentsAge := make(map[string]int)
	StudentsAge["John"] = 21
	fmt.Println(len(StudentsAge))
	fmt.Println(StudentsAge["John"])
	// key => string, value => string
	SuperHeroRealNames := map[string]string{
		"Superman": "Clarke Kent",
		"Batman":   "Bruce",
	}
	fmt.Println(SuperHeroRealNames["Superman"])
	// key => string, value => map
	SuperHeroCompleteInfo := map[string]map[string]string{
		"Superman": map[string]string{
			"Realname": "Clarke",
			"City":     "Metropolis",
		},

		"Batman": map[string]string{
			"Realname": "Bruce",
			"City":     "Gotham",
		},
	}

	if temp, hero := SuperHeroCompleteInfo["Superman"]; hero {
		fmt.Println(temp["Realname"], temp["City"])
	}
}
```

### Pointers
```go
func main () {
  result := *getAPointer()
  fmt.Println("Result is", result)
}

func getAPointer () (myPointer *int) {
  someValue := 999
  return &someValue
}

a := new(int)
*a = 234

```

### Type Conversion
```go
someInt := 2
someFloat := float64(someInt)
someUint := uint(someFloat)
// Conversion: is made automatically by complier. Can be applied only when types are compatible. 
// Destination type must be larger than source.
```

### Struct

```go
// Memory boundaries are important (Bool is 1 byte can save anywhere, 
// int16 is 2 bytes can only save at 0,2,4,6 index, int32 is 4 byte can only save at index 0,4, 
// int64 is 8 byte can only save at index 0, 8.).

func main() {
	//implicit conversion when named type, need implicit conversion
	var b Bill
	var a Alice
	b = Bill(a)
	fmt.Println(a, b)

	// literal type, need not to show implicit conversion.
	r := struct {
		flag    bool
		counter int16
		pi      float32
	}{
		flag:    true,
		counter: 0,
		pi:      3.14,
	}
	b = r
	fmt.Println(r)
}

// Bill is something
type Bill struct {
	flag    bool
	counter int16
	pi      float32
}

// Alice is something
type Alice struct {
	flag    bool
	counter int16
	pi      float32
}

// Since struct are values type we need to pass the pointer (*).
// UpdateFlag the flag
func (a *Alice) UpdateFlag(flag bool) {
	a.flag = flag
}
```

### Interface
```go
func main() {
	rect := Rectangle{5, 5}
	circ := Circle{5}

	fmt.Println(getArea(circ))
	fmt.Println(getArea(rect))
}

// Shape is the interface
type Shape interface {
	area() float64
}

// Rectangle is the struct
type Rectangle struct {
	width  float64
	height float64
}

func (rect Rectangle) area() float64 {
	return rect.height * rect.width
}

// Circle is a struct
type Circle struct {
	radius float64
}

func (circ Circle) area() float64 {
	return circ.radius * 2
}

func getArea(shape Shape) float64 {
	return shape.area()
}
```

### Init function
```go
// it Can be used with in a package block and regardless of how many times that package is imported, 
// the initfunction will only be called once.
func init() {
	fmt.Println("init function call")
}

func main() {
	fmt.Println("main function call")
}
```

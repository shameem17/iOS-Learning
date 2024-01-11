# :rocket: Functions

Functions are self-contained chunks of code that perform a specific task. Every function in Swift has a type, consisting of the function’s parameter types and return type. We can use this type like any other type in Swift, which makes it easy to pass functions as parameters to other functions, and to return functions from functions. Functions can also be written within other functions to encapsulate useful functionality within a nested function scope.

## :point_right: Defining and Calling Functions

Syntax:

```swift
func function_name(parameterName: type) -> return type{
	//statements

	return value
}
```

Example of function with no parameter an no return value. 

```swift
func welcome(){
	print("Welcome to Swift Function")
}

//function call
welcome()
```
:point_right: function with parameter and no return value

```swift
//no return value
func welcome(name: String){
	print("Welcome \(name) to Swift Function")
}

//function call
welcome(name: "Asif")
```

:point_right: Function with return value. Suppose a function takes velocity and time as paramenter and returns the distance covered as a return value. 

```swift
//returns Double as a return value
func distance(velocity: Double, time: Double) -> Double{
	 //s = v*t 
	 let s = velocity * time
	 return s
}

//function call
//return value should be captured or printed
print(distance(5.2, 10))
```

:point_right: Multiple Return Value: Suppose a function takes a list as parameter and returns the min and max value.

```swift
unc minMax(list: [Int]) -> (min: Int, max: Int){
    if var mn: Int = list.first, var mx = list.first{
        for num in list{
            if(num>mx)
            {
                mx=num
            }
            if(mn>num){
                mn=num
            }
        }
        return (min: mn, max: mx)
    }
   return (-1,-1)
}

let minMaxResult = minMax(list: [1,2,-4,3,233,43])
print("min value =",minMaxResult.min)
print("max value =",minMaxResult.max)
```

:point_right: Implicit Return

```swift
func multiplier(num1: Int, num2: Int) -> Int{
    num1*num2 //function should contain only one line of statement
}

print("multiplier=",multiplier(num1: 3, num2: 2))
```

## :point_right: Argument Label and Parameter Name

```swift
//argument Label and parameter name
func greetPerson(with name: String) -> Void{  //name: parameter, with: argument label
    print("Hi \(name)")
}

//function call using argument label
greetPerson(with: "Alice")
//greetPerson(name: "Bob") //will show an error
```
Here ```with``` is the argument label and ```name``` is the parameter name. The function can be called using the argument lable. We can't parameter name where an argument label exist. Again there can be no argument lable. Example:

```swift
func getArea(_ length: Int, _ width: Int) -> Void{
    print("The area is \(length*width)")
}
//don't need to specify the parameter name as argument label is not specified
// if there is no argument lable then paramenter name work as argument name
getArea(4, 3)
```

## :point_right: Default Parameter value

The parameter value can be a default value. It is optional to call the function with the default paramenter. Example:

```swift
//pi is a default parameter
func circleArea(radious: Double, pi: Double = 3.1416){
    print("The area of circle is: \(pi*radious*radious)")
}

//function can be called with specifiygin pi and without pi
circleArea(radious: 2)
circleArea(radious: 2, pi: 3.14)

```

## :point_right: Variadic Parameters

One or more parameters of same type. Example:

```swift
//one or more numbers of type Double
func average(numbers: Double...) ->Double{
    var sum: Double  = 0
    var n = numbers.count
    for num in numbers{
        sum+=num
    }
    return sum/Double(n)
}

print("avg=",average(numbers: 1,2,3,4,4,5))
```

## :point_right: In-Out Function

Pass by reference. It can change the value of the paramenters passed. Example:

```swift
var name = "Alice"
print("Name before update \(name)") //name = Alice
func updateName(name: inout String){
    name = "Bob"
}

updateName(name: &name)
print("Name after update \(name)") //name = Bob
```


## :point_right: Function As a Type 

Functions in Swift can be used as a variable, can be passed to another function, even a function can be returned from a function.

:point_right: Use as a variable

```swift
func subtractTwoNumbers(num1: Int, num2: Int) -> Int{
    num1 - num2
}

//assign the function to a variable
let myFunc: (Int , Int) -> Int = subtractTwoNumbers

print("The subtraction function using variable = \(myFunc(30,4))")
```

:point_right: Use as a Parameter

```swift
func showResult(function: (Int, Int) -> Int, num1: Int, num2: Int){
    print("Result of function = \(function(num1,num2))")
}
//call the showResult by passing the subtraction function as parameter
showResult(function: subtractTwoNumbers, num1: 34, num2: 12)
```

**:point_right: Return Function**

Define a calculator function with returns adder, subtractor, divider or multiplier function based on the sign(operator) passed.

```swift
//adder function
func adder(num1: Double, num2: Double) -> Double{
	return num1 + num2
}

//subtructor function
func subtractor(num1: Double, num2: Double) -> Double{
	return num1 - num2
}
//divider function
func divider(num1: Double, num2: Double) -> Double{
	if num2 == 0{
		return 0 //for simplicity dividing by 0 is 0
	}
	return num1 / num2
}
//multiplier function
func multiplier(num1: Double, num2: Double) -> Double{
	return num1 * num2
}
```
Now define a calculator function which takes a sign as argument and returns a function depending on the sign. Then the returned function is used for appropiate calculation.

```swift
//define a calculator func
func calculator(sign: Character) -> (Int, Int) -> Int{
    if sign == "+"{
        return adder
    }
    else if sign == "-"{
        return subtractTwoNumbers
    }
    else if sign == "*"{
        return multiplier
    }
    return divider
}

var sign: Character = "+"
var getFunc = calculator(sign: sign)
print("Result of \(sign) function = \(getFunc(10,4))")


sign = "-"
getFunc = calculator(sign: sign)
print("Result of \(sign) function = \(getFunc(10,4))")

sign = "*"
getFunc = calculator(sign: sign)
print("Result of \(sign) function = \(getFunc(10,4))")

sign = "/"
getFunc = calculator(sign: sign)
print("Result of \(sign) function = \(getFunc(10,4))")
```

## Nested Functions

Function inside a function

```swift
func outerFunction(){
	func innerFunction(){
		print("This is inner function")
	}

	innerFunction()
	print("This is outer function")
}
outerFunction() 
```
The inner function can't be called outside the outer function. 


**:point_right: References**

1. [Swift Documentation](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/functions/)

2. [Hack With Swift](https://www.hackingwithswift.com/read/0/11/functions)





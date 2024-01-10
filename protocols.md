# :rocket: Protocols

A protocol defines a blueprint of methods, properties, and other requirements that suit a particular task or piece of functionality. A blueprint doesn't build the building. It simply maps the overall design requirements that the builders need to follow. Protocols have a similar function in Swift and can be passed around so that other struct or class or enum instances adopts the property and method requirements defined by it. 

Protocols in Swift is similar to instance in Java. Protocols help in multiple inheritance. 


### :point_right: Creating Protocols

Syntax:

```swift
protocol protocolName{
	var propertyName: type {getter or setter}
	func update()
}
```

Example of a Protocol named ```Person```

```swift
protocol Person{
	var name: String {get} //read only
	var age: Int {get set} //read write
	func display()
}
```

A class or struct conforming the protocol must implement the properties and methods of the protocol. A class implementing the ```Person``` protocol is blew:
```swift
class Student: Person{
	let name: String
	var age: Int
	init(name: String, age: Int){
		self.name = name
		self.age = age
	}
	func display(){
		print("\(name) is a Student")
	}
}
```

Creating an instance of ```Student``` class.

```swift
var student = Student(name: "Rifat", age: 23)
student.display() //output: Rifat is a student
```

Other classes can implement the protocol as their own.

```swift
//teacher class will conform protocol
class Teacher: Person{
	let name: String
	var age: Int
	var empId: Int

	init(name: String, age: Int, empId: Int){
		self.name = name
		self.age = age
		self.empId = empId
	}
	func display(){
		print("\(name) is a teacher with empId = \(empID)")
	}
}

var teacher = Teacher(name: "Salam", age: 45, empId: 344)
teacher.display() //output: Salam is a teacher with empId = 344

```

#### :point_right: Multiple Protocols
A class can conforms to multiple protocols. Example:

```swift
protocol Person{
	var name: String {get}
	var age: Int {get set}
	func personalInfo()
}

protocol Address{
	var city: String {get set}
	var country: String {get set}
	func addressInfo()
}

protocol Dept{
	var deptName: String {get set}
	var deptId: Int {get set}
	func deptInfo()
}
```
Not student class conforming all the three protocols:
```swift
//Student class will conforms to multiple protocols
class Student: Person, Address, Dept{
	let name: String
	var age: Int
	var city: String
	var country: String
	var deptName: String
	var deptId: Int

	init(name: String, age: Int, city: String, country: String, 
		deptName: String, deptId: Int){
			self.name = name
			self.age = age
			self.city = city
			self.coutry = country
			self.deptName = deptName
			self.deptId = deptId
		}
	func personalInfo(){
		print("Name: \(name), Age: \(age)")
	}
	func addressInfo(){
		print("\(name)'s Address:- City: \(city), Country: \(country)")
	}
	func deptInfo(){
		print("\(name) is in \(deptName) Department")
	}

}
```

Creating student instance.

```swift
var student = Student(name: "Sabbir", age: 19, city: "Dhaka", country: "Bangladesh", "deptName": "CSE", deptId: 43)
student.personalInfo()
student.addressInfo()
student.deptInfo()
```
#### :point_right: Protocol Inheritance

One protocol can be composed of multiple protocol i.e. one protocol can inherit multiple other protocol. In the above example Person, Address and Dept protocol can be inherited to ```StudentProtocol``` protocol. 

```swift
protocol StudentProtocol: Person, Address, Dept{
	   //property of StudentProtocol
		var studentId: String {get set}
		func studentInfo()
}

class Student: StudentProtocol{
	//needs to conform all the properties and methods of Person, Address, 
	   Dept and StudentProtocol
}
```

> **IMPORTANT** <br>
> Class init should be required init if the protocol has an initializer
>

Example:

```swift 
protocol Country{
	var name: String {get set}
	var capital: String {get set}
	init(name: String, capital: String)
}

class Location: Country{
	var name: String
	var capital: String

	//the init should be required
	required init(name: String, capital: String){
		self.name = name
		self.capital = capital
	}
}
```

#### :point_right: Struct Using Protocols
Using ```struct``` instead of ```class``` will results the same. ```struct``` don't need ```init```.

```swift
struct Student: StudentProtocol{
	//implements the methods and properties
}
```


#### :point_right: Enum Using Protocols
Enum can also use protocol. Example:

```swift 
protocol Togglable{
	//enum is pass by value
	//so we need mutable function to change the property

	mutable func toggle()
}
```

```enum``` can implement the ```Togglable``` protocol. 

```swift
enum OnOff: Togglable{
	case on
	case off

	mutalbe func toggle(){
		switch self{
			case .on:
			self = .off
			case .off:
			self = .on
		}
	}
}

var lightSwitch = OnOff.off
lightSwitch.toggle() //on
```

#### :point_right: Extension

A class can extend to another protocol to add extra behaviours. Example ```Student``` class can extend to another class ```Course```. 

```swift
protocol Course{
	var courseName: [String] {get set}
	func courseInfo(){

	}
}

extension Student: Course{
	var courseName: [String]{
		get{

		}
		set{

		}
	}
	func courseInfo(){
		//implement
	}

}
```


### :point_right: Protocol Type

- is: checks whether a type conforms to a certain protocol
- as?: downcast operator. it will return an optional of protocol type if the object confirms to the protocol
- as!: downcast operator, similar to as? but forces downcast and if it fails then a runtime error will occur

Example:
```swift
//check protocol
if student is Person{
	print("Student conforms Person Protocol")
}
//downcast protocol
let studentA = Student() //add init parameters
let testStudent = studentA as? Person //success as Student conforms Person protocol
print("testStudent is now a PersonProtocol")
//forced downcast
//if fail it will create runtime error
let testStudent = studentA as! Person //will fail if studentA don't conform Person protocol
```

## :point_right: Optional Protocol Requirements
We can define optional requirements for protocols. These requirements don’t have to be implemented by types that conform to the protocol. Optional requirements are prefixed by the ```optional``` modifier as part of the protocol’s definition. Optional requirements are available so that we can write code that interoperates with Objective-C. Both the protocol and the optional requirement must be marked with the ```@objc``` attribute. Note that ```@objc``` protocols can be adopted only by classes, not by structures or enumerations.

Example:
```swift
@objc protocol Countable{
	@objc optional var number: Int{get set}
	//here count is optional
	@objc optional func count() -> Int
}

class Data: Countable{
	
	var number: Int
	init(number: Int){
		self.number = number
	}
	//implementing count function is optional
	func count() -> Int{
		return self.number
	}
}

var data = Data(number: 43)
print(data.count()) //43
```
## :point_right: Built-in-Protocols

```Equatable```, ```Hashable```, ```Comparable``` etc.  synthesized implementation.
Example:

```swift
enum BallType: Equatable, Hashable, Comparable{
    case kids
    case socer
    case cricket
    case football
}
let kidsBall = BallType.kids
let footBall = BallType.football
let generalBall = BallType.kids

if generalBall == kidsBall{
    print("generalBall kidsBall are equal")
}

print(kidsBall < footBall) //comparison. uses raw value
```

## :point_right: Delegate

Delegation is a design pattern that enables a class or structure to hand off (or delegate) some of its responsibilities to an instance of another type. This design pattern is implemented by defining a protocol that encapsulates the delegated responsibilities, such that a conforming type (known as a delegate) is guaranteed to provide the functionality that has been delegated. Delegation can be used to respond to a particular action or to retrieve data from an external source without needing to know the underlying type of that source. Example:

```swift
protocol Driver {
    var name: String { get }
    func driveToDestination(_ destination: String, with food: String)
}

class DeliveryDriver: Driver {
    let name: String
    init(name: String) {
        self.name = name
    }
    func driveToDestination(_ destination: String, with food: String) {
        print("\(name) is driving to \(destination) to deliver \(food).")
    }
}

class LittleLemon {
    var deliveryDriver: Driver?
    func deliverFood(_ food: String, to destination: String) {
        if let deliveryDriver = deliveryDriver {
            deliveryDriver.driveToDestination(
                destination,
                with: food
            )
        } else {
            print("No delivery driver.")
        }
    }
}

let bob = DeliveryDriver(name: "Bob")
let alex = DeliveryDriver(name: "Alex")
let littleLemon = LittleLemon()
//no driver assigned
littleLemon.deliveryDriver = alex
littleLemon.deliverFood(
    "Super Spaghetti",
    to: "1 Spaghetti Lane"
)
littleLemon.deliveryDriver = bob
littleLemon.deliverFood(
    "Super Spaghetti",
    to: "2 Spaghetti Lane"
)
```



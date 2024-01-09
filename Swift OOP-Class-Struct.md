# :rocket: Swift OOP

<a href="https://github.com/shameem17/Swift/tree/master/Class/struct_class.playground"> ![code](https://img.shields.io/badge/Code-Playground-1769DE?style=for-the-badge&logo=codeium&labelColor=grey)</a>  <a href="https://github.com/shameem17/Swift/blob/master/Class/struct_class.swift"> ![code](https://img.shields.io/badge/Swift-Code-red?style=for-the-badge&logo=swift)</a>

There are 4 pillars of OOP. They are:

- Encapsulation
- Abstraction
- Inheritance
- Polymorphism

Let's start with ```struct```

## Struct :fire:
In Swift, a struct is used to store variables of different data types. For example,

Suppose we want to store the name and age of a person. We can create two variables: name and age and store value.
Syntax of ```struct```:

```swift
struct Person{
    var name: String
    var age: Int
}
```

Creating instance of ```struct```

```swift
var person = Person()
```

Changing property values:

```swift
person.name = "Alex"
person.age = 43
```
Create instance with initial value

```swift
var person = Person(name: "Smith", age: 25)
```

```struct``` with functions:

```swift
struct Person{
    var name: String
    var age: Int

    func display(){
        print("Name: \(name), age: \(age)")
    }
}
```

Accessing functions:

```swift
var person = Person(name: "Bob", age: 32)
person.display()
```

```struct```doesn't support OOP concepts.

> **Note**
> 
> Struct is pass by value.
> That is copying a new instance from an existing instance will not affect the initial instance
> Example: var person1 = person. Here person1 and person are two different instances
>


## Class :fire:

Classes can be compared to a real-world group to which certain items or objects or living beings belong and each of these has similar kinds of properties as present in the group. Eg — Think of Person as a group or class. Every Person is it, a man or woman has properties and attributes which are common to both. Class syntax in Swift

```swift
class Person{
    var name: String
    var age: Int
}
```
The ```UIView``` is an example of class for iOS. 

A class with some properties must have a constructor (i.e. ```init``` function).

```swift
class Person{
    var name: String
    var age: Int
    //init constructor
    init(name: String, age: Int){
        self.name = name
        self.age = age
    }
}
```

Creating objects and instances of class:

```swift
var person = Person(name: "Alice", age: 30)
```

Methods in class: (Encaptulation)

```swift
class Person{
    var name: String
    var age: Int
    //init constructor
    init(name: String, age: Int){
        self.name = name
        self.age = age
    }
    //method
    func info(){
        print("Name: \(name), Age: \(age)")
    }
}
```

Accessing methods

```swift 
person.info()
```

Class is pass by value. For example see the code below:

```swift
var person1 = Person(name: "Joe", age: 31)
print(person1.name) //output: Joe
var person2 = person1 //same instance
person2.name = "Smith" //changing person2 name will also change the name of person1
print(person1.name) //output : Smith
```

### Inheritance

Subclass (Derived Class) inherits the properties and methods from superclass (Base Class)

```swift
class Student: Person{
        //inherits the properties and methods of Person class
}
```

Now ```Student``` class has the properties ```name``` and ```age```. 

Creating instance of Student Class: 

```swift
var student = Student(name: "Student 1", age: 20)
student.display() //accessing parent class method
```


### Polymorphism

In subclass the properties and methods of superclass will act differently. Example:

```swift
class Person{
    var name: String
    var age: Int

    init(name: String, age: Int){
        self.name = name
        self.age = age
    }

    func info(){
        print("\(name) is a person")
    }
}

class Student: Person{
    var id: Int

    init(id: Int, name: String, age: Int){
        self.id = id
        //accessing super class function from subclass
        super.init(name: name, age: age)
    }

    //override the superclass function for polymorphis

    override func info(){
        print("\(name) is a student")
    }
}
```

Now let's see how the ```info``` methods perform differently for ```Person``` class instance and for ```Student``` class instance:

```swift
var person = Person(name: "Sabbir", age: 21)
var student = Student(id: 2, name: "Rifat", age: 18)
person.info() //output: Sabbir is a person
student.info() //output: Rifat is a student

```

Properties can also be overriden. Example:

```swift
class Animal{
    var sound: Stirng {
        "anmial sound"
    }
}

class Cat: Animal{
    //ovrriding sound property

    override var sound: String{
        "Cat Sound"
    }
}

var cat = Cat()
print(cat.sound) //output: Cat Sound
```


### Access Modifier

There are five types of access modifiers in Swift. The are:

1. private
2. fileprivate
3. internal (Default Access Modifier)
4. public
5. open 

This list represents the restrictive hierarchy i.e. private is the most restrictive and open is less restrictive. This is how access modifiers controls accessing of property:

**private:-** Allows the code within a code definition to access the code.
The private properties can only be accessed inside the containing class. Private property or methods can't be accessed outside the class.

**fileprivate:-**  Allows the defining source file to access the code. In the same file the other class can access the properties and methods

**internal:-** Allows source files from the defining module to access the code. Inside the same module, other class can access the properties and methods

**public:-** - Allows source files from other modules to access the code, however, other modules can’t subclass and override classes.

**open:-** Allows source files from other modules to access the code. Other modules can subclass and override classes and it is the difference between public and open access modifier.



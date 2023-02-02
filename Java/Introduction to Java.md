#java #programming 

---
# Object Oriented Programming
OOP refers to languages that use *objects* in programming as a *primary source* to *implement what is to happen in the code*. It aims to implement real-world entities like inheritance, hiding, polymorphism in programming. Its main objective is to bind together the data and the functions that operate on them so that no other part of the code can access this data except that function.

## OOP main concepts
1. Class
2. Object
3. Method and method passing
4. Pillars
	1. Abstraction
	2. Encapsulation
	3. Inheritance
	4. Polymorphism

## 1. Class
---
A class is a user-defined *blueprint* or prototype from which objects are created. It represents the sets of properties or methods that are common to all objects of one type.
A class declaration usually contains:
- *Modifiers* --> a class can be public or default
- *Class Name*
- *Superclass* --> the name of the class's parents (superclass), if any preceded by the word *extend*
- *Interfaces* --> A comma-separated list of interfaces implemented by the class preceded by the keyword *implements*
- *Code Body*

```java
public class MyClass extends MySuperClass implements InterfaceX {
	...
}
```

## 2. Object
---
Is a basic unit of OOP that represents *real-life entities*. A java program creates many objects which interact by invoking methods. The objects are what perform your code, they are the part of the code visible to viewer/user. An object is usually made of:
- *State* --> The attributes (and properties) of an object
- *Behavior* --> The methods (and response) of an object
- *Identity* --> Unique name
- *Method*  --> A collection of statements that perform a task.

```java
public class MyObj (){
	int a = 4
}

...

public class Main() {
	public static void main(String[] args) {
		MyObj Object_1 = new MyObj(); // Object creation
		System.out.println(Object_1.a) // Will print '4' to STDOUT
	}
}
```

## 3. Methods
---
They run some *code statements* in order to perform a *task*. They usually consist of:
-  **Access modifier** --> defines the access type of the method i.e. from where it can be accessed in your application. There are 4 type of access specifiers:
	- *public* --> Accessible in all classes in you application
	- *protected* --> Accessible within the package in which it is defined and in its subclasses (including subclasses declared outside the package)
	- *private* --> Accessible only within the class it is defined
	- *default* (or no identifiers) --> Accessible within the same class and package within which its class is defined

| Access Modifier | Within Class | Within Package | Outside Package by subclass only | Outside Package |
|:---------------:|:------------:|:--------------:|:--------------------------------:|:---------------:|
|     Private     |     Yes      |       No       |                No                |       No        |
|     Default     |     Yes      |      Yes       |                No                |       No        |
|    Protected    |     Yes      |      Yes       |               Yes                |       No        |
|     Public      |     Yes      |      Yes       |               Yes                |       Yes       |


- **Return type** --> The data type of the value returned by the method or *void* if it does not return anything
- **Method name** -->Self explanatory, it should always start with a lowercase letter
- **Parameter list** --> Comma separated list of arguments or none
- **Exception list** --> The exceptions you expect the method yo throw.
- **Method body** --> Code block

```java
public void MyMethod(String arg1, int arg2, MyObj arg3, ...) throws MyException {
 ...
}
```

## 4. Pillars of OOP
---
### Abstraction
Data abstraction is the property by virtue of which *only the essential details* are displayed to the user, the other *non-essential units are not displayed* to the user. Data Abstraction may also be defined as the process of identifying only the required characteristics of an object, ignoring the irrelevant details. 

The properties and behaviors of an object differentiate it from other objects of similar type and help in classifying and grouping them

> Abstraction is achieved by using ***interfaces*** and ***abstract*** classes.

### Encapsulation
It is defined as the wrapping up of data under a single unit. It is the mechanism that binds together code and data that gets manipulated. It is like a protective shield that prevents data from being accessed by code outside this shield

- The variables or data in a class is hidden from other classes and can be accessed only through member functions of the class in which they're declared
- Data is hidden from other classes. *Data-hiding* is the same as *encapsulation*

> Encapsulation can be achieved by declaring ***all variables*** in a class as ***private*** and then writing ***public methods*** to set and get their value.

### Inheritance
It is the mechanism in Java by which one class is allowed to inherit the features (fields and methods) of another class. Terminology:
- *Superclass*  --> the class whose feature are inherited  (also base/parent class)
- *Subclass* --> the class that inherits the other class (also derived/child class). A subclass can be expand with more fields and methods.

> Inheritance supports the concept of ***reusability***, and helps respect the DRY principle (Don't-Repeat-Yourself)

### Polymorphism
Polymorphism means *many forms*, and it occurs when there are many classes related to each other by inheritance. Polymorphism uses the methods inherited by the class to perform different tasks allowing to perform a single action in different ways.

```java
class Animal {
	public void animalSound() {
		System.out.println("Animal makes a sound")
	}
}

class Wolf extends Animal {
	public void animalSound() {
		System.out.println("Woof!")
	}
}
class Cat extends Animal {
	public void animalSound() {
		System.out.println("Meow!")
	}
}

class Main {
	public static void main(String[] argv) {
		Animal generic = new Animal(); // Animal object
		Animal wolf = new Wolf(); // Dog object
		Animal cat = new Cat(); // Cat object
		// note that all animals are declared as type 'Animal', this allowes flexibility
	}

}
```

---

*source: GeekForGeeks.com*

Next: [[Variables]]

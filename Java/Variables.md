---
created: 2024-01-11T15:04
updated: 2024-01-11T15:04
---
#java #javabasics

Previous: [[Introduction to Java]]

---
# Definition
A variable is a data container that saves data values during a Java program execution.
It is composed by two elements: `datatype` `variable_name` 
1. *datatype* --> Type of data that can be stored in this variable
2. *variable_name* --> Name of the variable

## Initialization
---
To initialize a variable you can extend the thing done when defining a variable. You need to simply give a value to your variable. So three elements are used: `datatyp` `variable_name` = `value`

```java
int sum = 20;
```

## Types of variables
---
There are three types of variables in Java
- **Local variables** --> defined within a block or method or constructor. They're created when the block is entered and destroyed after exiting the block. The *scope* of these variables exists only within the block in which they are declared. They *must be initialized* in order *to be used* in that block. 

```java
class MyClass {
	public static void main(String[] argv) {
		int var = 10;
		// var can be used here
	}
	// var is undefined
}
// var is undefined

```

- **Instance variables** --> non static variables and are declared in a class outside of any method, constructor or block. They're declared in a class and exist as long as the class instantiation exists. They *support* being defined with *access modifiers*. Initialization is not mandatory, they default to 0. They can be accessed only when an object is created.

```java
class MyClass {
	public String name;

	public MyClass() {
		this.name = "Myname";
	}
	public static void main(String[] argv) {
		MyClass obj = new MyClass();
		// obj.name -- is valid
	}
}
```

- **Static variables** --> also called *class variables*. They're declared using the *static* modifier outside any class and methods. There can be *only one static variable per class*, it does not depend on how many objects we create. They are created when the program starts and destroyed when it ends. Its *default* value is *0*. If we access a static variable like an instance variable (through an object), the compiler will show a warning message, which won’t halt the program. The compiler will replace the object name with the class name automatically. If we access a static variable without the class name, the compiler will automatically append the class name.

```java
class MyClass {
	public static String name = "name";
	
	public static void main(String[] argv) {
		System.out.println("My name is: " + MyClass.name);
	}
}
```

### Access modifiers
---
Static and instance variables support access modifiers and they can be accessed using the following rules:

| Modifier  | Package | Subclass | World |
| --------- | ------- | -------- | ----- |
| public    | Yes     | Yes      | Yes   |
| protected | Yes     | Yes      | No    |
| default   | Yes     | No       | No    |
| private   | No      | No       | No      |

Next: [[The java.lang.String class]]
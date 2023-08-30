#designpatterns 

---
# Design patterns
In [software engineering](https://en.wikipedia.org/wiki/Software_engineering), a **software design pattern** is a general, [reusable](https://en.wikipedia.org/wiki/Reusability "Reusability") solution to a commonly occurring problem within a given context in [software design](https://en.wikipedia.org/wiki/Software_design "Software design"). It is not a finished design that can be transformed directly into [source](https://en.wikipedia.org/wiki/Source_code "Source code") or [machine code](https://en.wikipedia.org/wiki/Machine_code "Machine code"). Rather, it is a description or template for how to solve a problem that can be used in many different situations. Design patterns are formalized [best practices](https://en.wikipedia.org/wiki/Best_practice "Best practice") that the programmer can use to solve common problems when designing an application or system. (source: [Wiki](https://en.wikipedia.org/wiki/Software_design_pattern))
## Singleton
The singleton design pattern is a design pattern that ensures a class has only one single instance and provides a global point of access to that instance. It is often used when you need to have a single instance of a class that controls some resource  or behavior throughout the entire lifetime of an application.

Key features:
1. **Single Instance:** The Singleton pattern guarantees that a class has only one instance. It achieves this by controlling the instantiation process, usually through a private constructor.    
2. **Global Access:** The single instance created by the Singleton pattern is globally accessible. This means that any part of the codebase can access this instance without needing to create new instances or pass references around.
3. **Lazy Initialization:** The Singleton instance is often created only when it's first needed, rather than during the application's startup. This approach is known as lazy initialization and helps conserve resources until the Singleton is actually required.
4. **Thread Safety:** Singleton implementations need to ensure thread safety, especially in multi-threaded environments. This is because multiple threads might try to access or create the Singleton instance simultaneously. Common techniques for achieving thread safety include using locks, synchronization, or employing double-checked locking.

E.g.:
```python
class Singleton:
    _instance = None
    
    def __init__(self):
        if Singleton._instance is not None:
            raise Exception("Singleton instance already exists. Use get_instance() method.")
        Singleton._instance = self

    @staticmethod
    def get_instance():
        if Singleton._instance is None:
            Singleton()
        return Singleton._instance

# Usage
singleton_instance_1 = Singleton.get_instance()
singleton_instance_2 = Singleton.get_instance()

print(singleton_instance_1 is singleton_instance_2)  # Outputs: True
```

It's worth noting that while the Singleton pattern provides global access to a single instance, it can also introduce **global state**, which might make *testing* and *maintenance* more **challenging**. Therefore, its usage should be carefully considered based on the specific requirements of the application.

## Observer
The Observer design pattern is a behavioral design pattern that establishes a one-to-many dependency between objects. In this pattern, when one object (called the subject) changes its state, all its dependents (observers) are notified and updated automatically. This allows the observers to react to changes in the subject's state without being tightly coupled to it.

Key features:
1. **Subject:** This is the object that maintains a list of its dependents (observers) and notifies them of any changes in its state. The subject typically provides methods to attach, detach, and notify observers.
2. **Observer:** The observer is the interface or base class that defines the update method. Concrete observer classes implement this method to receive updates from the subject. Observers are registered with the subject to receive notifications.
3. **Concrete Subject:** This is the actual subject object that holds the data and state that observers are interested in. It maintains a list of its observers and notifies them when its state changes.
4. **Concrete Observer:** Concrete observer classes implement the observer interface or inherit from the observer base class. They register themselves with a subject to receive updates and implement the update method to define their response to changes in the subject's state.

E.g.:
```python
class Observer:
    def update(self, message):
        pass

class ConcreteObserver(Observer):
    def update(self, message):
        print(f"Received update: {message}")

class Subject:
    def __init__(self):
        self._observers = []

    def attach(self, observer):
        self._observers.append(observer)

    def detach(self, observer):
        self._observers.remove(observer)

    def notify(self, message):
        for observer in self._observers:
            observer.update(message)

class ConcreteSubject(Subject):
    def set_state(self, state):
        self._state = state
        self.notify(f"State changed to {state}")

# Usage
observer1 = ConcreteObserver()
observer2 = ConcreteObserver()

subject = ConcreteSubject()
subject.attach(observer1)
subject.attach(observer2)

subject.set_state("New State")
```

The Observer pattern promotes loose coupling between subjects and observers, allowing for better scalability and maintainability in code. It's commonly used in scenarios where a change in one object's state needs to trigger actions in multiple other objects, such as in user interface components, event handling systems, and real-time data processing applications.

## Data Transfer Object (DTO)
A Data Transfer Object (DTO) is a design pattern used in software engineering to efficiently transport data between different layers or components of an application. Its primary purpose is to encapsulate data and provide a way to transfer it between different parts of a system, often across different boundaries like network communication or database interactions. The DTO pattern aims to optimize data transmission by reducing the number of calls and amount of data exchanged.

Key features of the Data Transfer Object (DTO) pattern:
1. **Data Encapsulation:** DTOs are simple objects that contain data fields and have minimal or no behavior. They are used to represent data structures, often mimicking the structure of the underlying data source or the requirements of a particular use case.
2. **Efficient Data Transfer:** When transmitting data across different layers or components, using DTOs can reduce the amount of data exchanged. This can improve performance by minimizing unnecessary data retrieval or serialization.
3. **Cross-Layer Communication:** DTOs facilitate communication between different layers of an application, such as between the presentation layer (user interface) and the backend services, or between the application layer and the data access layer.
4. **Decoupling and Versioning:** DTOs can help decouple the internal representation of data from its external representation. This can be especially useful when changes to the internal structure of data shouldn't impact the external communication interfaces. It also allows for better versioning of APIs and services.

E.g.:
```python
class UserDTO:
    def __init__(self, username, email):
        self.username = username
        self.email = email

# Usage
user_data = {"username": "john_doe", "email": "john@example.com"}
user_dto = UserDTO(username=user_data["username"], email=user_data["email"])

# Transmit user_dto to another component or layer

```

DTOs are particularly useful in scenarios where:

- The data to be transferred doesn't exactly match the data structure used internally in the application.
- Data needs to be aggregated from multiple sources before being transmitted.
- There is a need to optimize data transmission to improve performance, such as in distributed systems or when dealing with limited bandwidth.

However, it's important to use DTOs judiciously and not overly complicate the design of your application. In some cases, especially in smaller applications, the overhead of creating DTOs might outweigh the benefits.

## Adapter
The Adapter design pattern is a structural pattern that allows objects with incompatible interfaces to work together. It acts as a bridge between two incompatible interfaces, enabling them to collaborate without modifying their source code.

Key components:
- **Target:** Defines the interface that the client code uses to interact with.
- **Adaptee:** The class that has the interface incompatible with the Target's interface.
- **Adapter:** A class that implements the Target's interface and holds an instance of the Adaptee. It translates the calls from the Target's interface into calls to the Adaptee's interface.

E.g.: Imagine you have an existing class that calculates areas in square meters, and you want to use it in a new system that requires areas in square feet. An adapter can be created to convert between the two units.

## Template
The Template design pattern is a behavioral pattern that defines the structure of an algorithm but allows its steps to be overridden by subclasses. It promotes reusability and code consistency by providing a template or skeleton for an algorithm while allowing specific steps to be implemented by derived classes.

Key components:
- **AbstractClass:** Defines the template method, which consists of a series of method calls and abstract steps.
- **ConcreteClass:** Implements the abstract steps defined in the AbstractClass.

E.g.: In a game, you might have a template for character creation. The template method outlines the general steps like choosing a character model, setting attributes, and adding equipment. Subclasses for different character types (warrior, mage, archer) provide concrete implementations for each step.

## Decorator
The Decorator design pattern is a structural pattern that allows behavior to be added to individual objects, either statically or dynamically, without affecting the behavior of other objects from the same class. It's an alternative to subclassing for extending functionality.

Key components:

- **Component:** Defines the interface for objects that can have responsibilities added to them dynamically.
- **ConcreteComponent:** The class to which additional responsibilities can be added.
- **Decorator:** Maintains a reference to a Component object and conforms to its interface while adding additional behavior.
- **ConcreteDecorator:** Extends the behavior of the Component by adding specific features.

E.g.: Consider a text editor. The Component might be a basic text element, while the Decorators could add functionality like bold formatting, italics, and underline.

## Facade
The Facade design pattern is a structural pattern that provides a simplified interface to a complex system of classes, making it easier for clients to interact with the system. It acts as a higher-level interface that hides the complexities of the subsystem and presents a unified interface for the client.

E.g.: Consider a multimedia player that plays audio and video files. The multimedia player might internally utilize different subsystems for decoding audio and video formats. The Facade pattern can create a simplified interface that encapsulates the complexity of interacting with these subsystems, providing methods like `playAudio()` and `playVideo()`.
## Factory
The Factory design pattern is a creational pattern that provides an interface for creating objects in a super class, but allows subclasses to alter the type of objects that will be created. It abstracts the process of object creation and decouples the client code from the specifics of the created objects.

E.g.: A GUI framework might use a factory pattern to create various types of UI elements like buttons, text fields, and checkboxes. The factory could have methods like `createButton()`, `createTextField()`, etc., and specific implementations could create different styles of these elements.
## Iterator
The Iterator design pattern is a behavioral pattern that provides a way to access elements of a collection (such as an array or a list) sequentially without exposing the underlying structure of the collection. It separates the iteration logic from the collection itself.

E.g.: In programming languages, iterators are commonly used to traverse elements of arrays or collections. The iterator pattern encapsulates the traversal logic, allowing clients to iterate over the elements without needing to understand the internal structure of the collection.
## Abstract Factory
The Abstract Factory design pattern is a creational pattern that provides an interface for creating families of related or dependent objects without specifying their concrete classes. It's used when a system must be independent of how its objects are created, composed, and represented.

E.g.: Consider a user interface framework that needs to support different themes (e.g., light and dark). The abstract factory pattern could define interfaces for creating buttons, text fields, and other UI elements, and concrete implementations of the factory would create elements with a consistent theme.
## Proxy
The Proxy design pattern is a structural pattern that provides a surrogate or placeholder for another object to control its access. It acts as a intermediary between the client and the real object, adding an extra layer of control.

E.g.: A classic use of the proxy pattern is in virtual proxy scenarios, such as lazy loading of heavy resources. For instance, a virtual proxy for an image might only load the actual image data from disk when requested to display, thus optimizing memory usage.
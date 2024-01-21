---
created: 2024-01-11T15:04
updated: 2024-01-21T15:08
tags:
  - engineering
  - interview-questions
---
#engineering #designpatterns

---
# Architectural Design Patterns
An **architectural pattern** is a general, reusable resolution to a commonly occurring problem in [software architecture](https://en.wikipedia.org/wiki/Software_architecture "Software architecture") within a given context. The architectural patterns address various issues in [software engineering](https://en.wikipedia.org/wiki/Software_engineering "Software engineering"), such as [computer hardware](https://en.wikipedia.org/wiki/Computer_hardware "Computer hardware") performance limitations, [high availability](https://en.wikipedia.org/wiki/High_availability "High availability") and minimization of a [business risk](https://en.wikipedia.org/wiki/Business_risk "Business risk"). Some architectural patterns have been implemented within [software frameworks](https://en.wikipedia.org/wiki/Software_framework "Software framework"). (source: [Wiki](https://en.wikipedia.org/wiki/Architectural_pattern))

## Model View Controller (MVC)
The MVC pattern specifies that an application consists of a **data** model, **presentation** information and **control** information. It separates the view modules from the modules that interact with data.

![[MVC.png]]
### Model
The model contains<mark style="background: #FFB86CA6;"> only the application data, it does not have any kind of logic</mark> or business logic. It just manages data and how the communication with the database.
### View
The view defines the layer that <mark style="background: #FFB86CA6;">handles how data coming from the model is displayed</mark> to the user. It knows how to communicate with the model layer but does not manipulate it, it simply displays information to the user
### Controller
The controller sits between the model and the views, it is responsible for <mark style="background: #FFB86CA6;">manipulating data, for handling events, errors a</mark>nd it's where the business logic is located.

### Pros and Cons
**Pros:**
- Thanks to the separation of the 3 layers, developers can work on multiple things at once
- Things are logically grouped
- Since it is component-based, it makes the application more easily maintainable and less dependent on each other.
**Cons:**
- Steep learning curve
- You must learn many technologies to understand how the application works
- Higher level of abstraction.

## Layered
It's the easiest pattern and probably most used since it <mark style="background: #FFF3A3A6;">matches the traditional IT communication</mark> (TCP/IP protocol) and organizational structures.
Components are organized into horizontal layers, each layers performing a special role within the application. There isn't a standard number of layers but generally we can find 4 standard layers: *presentation*,  *business*, *persistence* and *database*. 
Each of these layers have their own role and responsibility, forming also a layer of abstraction around the work that needs to be done. Also each layer offers some kind of services that the layers above and under can use to interface and communicate with each other.

![[LayeredPattern.png]]
Each layer can be <mark style="background: #FFF3A3A6;">open or closed</mark>. If it's closed then every request *must* go through that layer, on the other hand, if it's open then a layer can be skipped. 

## Repository
It's a pattern that provides a way to<mark style="background: #FFF3A3A6;"> manage data access logic</mark> in a centralized location. It separates the logic that retrieves the data and maps it to the entity model from the business logic that operates on the model. The primary objective of the repository pattern is to <mark style="background: #FFF3A3A6;">simplify as much as possible the *data access code*</mark> allowing to handles massive amounts of data in an efficient way.
It is made out of three components:
- Repository interface
- Repository Implementation
- Repository Model

### Interface
<mark style="background: #FFF3A3A6;">Defines the operations</mark> that can be performed on the entity model, usually consisting of CRUD operations.
### Implementation
Represents the <mark style="background: #FFF3A3A6;">actual implementation</mark> of the interface and is the one responsible for the actual data access operations
### Entity Model
Represents the business entities of the app. It typically consists of one or more classes that <mark style="background: #FFF3A3A6;">map to database tables.</mark>

## Client Server
It represents a distributed application structure that facilitates communication between many clients and servers. Servers are the ones that wait for clients to make *requests* to them, and then they answer with a *response*. This is typical of the way internet works. 
When you try to connect to a web page, you make a *request* to a server that's listening for clients to connect somewhere in world and then it *processes* the request and returns a *response* containing all the information of the web page that later gets displayed by the browser.

## Pipe and Filter
As the name suggests, it is made by two components **pipes** and **filters**. Filters perform transformations on data and process the input they receive. Pipes work as connectors between components, they transfer the transform (or soon-to-be transformed) data from one component to the other.

![[PipeFilterDesign.png]]

Next: [[Design Patterns]]
#engineering

---

## Model View Controller (MVC)
The MVC pattern specifies that an application consists of a **data** model, **presentation** information and **control** information. It separates the view modules from the modules that interact with data.

![[MVC.png]]
### Model
The model contains only the application data, it does not have any kind of logic or business logic. It just manages data and how the communication with the database.
### View
The view defines the layer that handles how data coming from the model is displayed to the user. It knows how to communicate with the model layer but does not manipulate it, it simply displays information to the user
### Controller
The controller sits between the model and the views, it is responsible for manipulating data, for handling events, errors and it's where the business logic is located.

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
It's the easiest pattern and probably most used since it matches the traditional IT communication (TCP/IP protocol) and organizational structures.
Components are organized into horizontal layers, each layers performing a special role within the application. There isn't a standard number of layers but generally we can find 4 standard layers: *presentation*,  *business*, *persistence* and *database*. 
Each of these layers have their own role and responsibility, forming also a layer of abstraction around the work that needs to be done. Also each layer offers some kind of services that the layers above and under can use to interface and communicate with each other.

![[LayeredPattern.png]]
Each layer can be open or closed. If it's closed then every request *must* go through that layer, on the other hand, if it's open then a layer can be skipped. 

## Repository
It's a pattern that provides a way to manage data access logic in a centralized location. It separates the logic that retrieves the data and maps it to the entity model from the business logic that operates on the model. The primary objective of the repository pattern is to simplify as much as possible the *data access code* allowing to handles massive amounts of data in an efficient way.
It is made out of three components:
- Repository interface
- Repository Implementation
- Repository Model

### Interface
Defines the operations that can be performed on the entity model, usually consisting of CRUD operations.
### Implementation
Represents the actual implementation of the interface and is the one responsible for the actual data access operations
### Entity Model
Represents the business entities of the app. It typically consists of one or more classes that map to database tables.

## Client Server
It represents a distributed application structure that facilitates communication between many clients and servers. Servers are the ones that wait for clients to make *requests* to them, and then they answer with a *response*. This is typical of the way internet works. 
When you try to connect to a web page, you make a *request* to a server that's listening for clients to connect somewhere in world and then it *processes* the request and returns a *response* containing all the information of the web page that later gets displayed by the browser.

## Pipe and Filter
As the name suggests, it is made by two components **pipes** and **filters**. Filters perform transformations on data and process the input they receive. Pipes work as connectors between components, they transfer the transform (or soon-to-be transformed) data from one component to the other.

![[PipeFilterDesign.png]]

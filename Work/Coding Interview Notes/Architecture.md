# Architecture

Ones I've used
##### Boeing: 
###### MVC or MVP

##### Royall: 
###### Flutter Bloc library
- Presentation
- Business Logic
- Data
    - Repository
    - Data Provider
###### Spring Boot 
- Mic Architecture
	- Presentation
	- Business
	- Persistence
	- Database
- Dependency inversion principle
	- Inversion of control pattern
	- Dependency Injection pattern


### Basic Arch: MVC

###### Overview
1. Model
	1. Database that stores information
2. View
	1. Presents content from controller to users and sends back requests
3. Controller
	1. Handles requests/responses from view to model
	2. Interfaces between other two

###### Issues

1. MVC Is Stateful
- It only makes sense if the View, as well as the View-Model binding is stateful (so the Model can update the View when it changes)
    
2. MVC Has No Single Interpretation
- Every framework uses their own nuanced version.
    
3. How Does Logging Fit In?
- Where does application code that’s not clearly data-centric belong in the application?

### Multi-Threaded Request/Response vs. Single-Threaded Event Loop

##### Multi-Threaded Request/Response
- Used by Django, Java, etc.
- HTTP Protocol
- Stateless model
- If all threads are busy, remaining requests have to wait
	- Can be fixed with dynamic computing in Cloud but not for locally hosted solutions

###### Steps
-   Clients Send request to Web Server.
-   Web Server internally maintains a Limited Thread pool to provide services to the Client Requests.
-   Web Server is in infinite Loop and waiting for Client Incoming Requests
-   Web Server receives those requests.
    -   Web Server pickup one Client Request
    -   Pickup one Thread from Thread pool
    -   Assign this Thread to Client Request
    -   This Thread will take care of reading Client request, processing Client request, performing any Blocking IO Operations (if required) and preparing Response
    -   This Thread sends prepared response back to the Web Server
    -   Web Server in-turn sends this response to the respective Client.

###### Cons
- Handling more and more concurrent client’s request is bit tough.
- When Concurrent client requests increases, then it should use more and more threads, finally they eat up more memory.
- Sometimes, Client’s Request should wait for available threads to process their requests.
- Wastes time in processing Blocking IO Tasks.


##### Single-Threaded Event Loop

###### Steps
-   Clients Send request to Web Server.
-   Node JS Web Server internally maintains a Limited Thread pool to provide services to the Client Requests.
-   Node JS Web Server receives those requests and places them into a Queue. It is known as “Event Queue”.
-   Node JS Web Server internally has a Component, known as “Event Loop”. Why it got this name is that it uses indefinite loop to receive requests and process them. (See some Java Pseudo code to understand this below).
-   Event Loop uses Single Thread only. It is main heart of Node JS Platform Processing Model.
-   Even Loop checks any Client Request is placed in Event Queue. If no, then wait for incoming requests for indefinitely.
-   If yes, then pick up one Client Request from Event Queue
    -   Starts process that Client Request
    -   If that Client Request Does Not requires any Blocking IO Operations, then process everything, prepare response and send it back to client.
    -   If that Client Request requires some Blocking IO Operations like interacting with Database, File System, External Services then it will follow different approach
        -   Checks Threads availability from Internal Thread Pool
        -   Picks up one Thread and assign this Client Request to that thread.
        -   That Thread is responsible for taking that request, process it, perform Blocking IO operations, prepare response and send it back to the Event Loop
        -   Event Loop in turn, sends that Response to the respective Client.

###### Pros
1.  Handling more and more concurrent client’s request is very easy.
2.  Even though our Node JS Application receives more and more Concurrent client requests, there is no need of creating more and more threads, because of Event loop.
3.  Node JS application uses less Threads so that it can utilize only less resources or memory
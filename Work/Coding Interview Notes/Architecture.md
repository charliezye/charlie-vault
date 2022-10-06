# Architecture

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
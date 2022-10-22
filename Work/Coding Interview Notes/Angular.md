### Angular vs. React

##### Main Differences
1. Angular is a full featured framework while React is only concerned with UI components
2. Angular supports two-way data binding while React normally only has one-way data binding
	- Two listeners vs. only one, modifying UI input will change model state and vice versa for two-way
3. Angular has full support for dependency injection allowing separate life cycles for different stores
	- React does not support full DI each component has its own global state
4. Angular has incremental DOM, meaning new DOM is compared to old and only differences are applied, allocating memory only when necessary
	- React creates virtual DOM to compare instead
	- Changes can be made without needing to rewrite the full HTML document, ensuring rendering updates are speedier

##### Angular Advantages
- Increased efficiency
- Can handle routing within the framework, so switching from one view to another is simple
- Better support for Single Page Applications (SPAs)
	- No need to load whole new pages from the server meaning better performance and more dynamic experience
	- More effort to maintain state, implement navigation, and do meaningful performance monitoring

##### React Advantages
- Improved server-side rendering capability so more robust for content-focused apps
- Skills can be transferred to native development
- Ideal for managing huge loads with relative ease
- Faster speed with smaller bundle size
- Easier to switch between React versions
- Wide range of pre-built solutions
- More SEO friendly
- More stable program code due to one-way data binding

### Angular Core Concepts

[Angular basics site](https://angular.io/guide/what-is-angular)

##### Components

The building blocks that compose an application. 
Includes:
- TS class w/ @Component() decorator
- HTML template
- Styles

- Offers strong encapsulation and intuitive application structure
- Make application painless to unit test and can improve general readability of code

###### Code Example

``` ts
import { Component } from '@angular/core';

@Component({
  selector: 'hello-world',
  template: `
    <h2>Hello World</h2>
    <p>This is my first component!</p>
  `
})
export class HelloWorldComponent {
  // The code in this class drives the component's behavior.
}

// Usage of component in other templates:
<hello-world></hello-world>

// Rendered DOM of component
<hello-world>
    <h2>Hello World</h2>
    <p>This is my first component!</p>
</hello-world>
```

##### Templates
Every component has an HTML template that declares how that component renders.
- Angular adds syntax elements that extend HTML so you can add dynamic values from your component, e.g. dynamic text
``` ts
// Dynamic text value, notice double brackets
<p>{{ message }}</p>

// Value for message comes from component class
import { Component } from '@angular/core';

@Component ({
  selector: 'hello-world-interpolation',
  templateUrl: './hello-world-interpolation.component.html'
})
export class HelloWorldInterpolationComponent {
  fontColor = 'blue';
  sayHelloId = 1;
  canClick = false;
  message = 'Hello, World';
 
  sayMessage() {
	alert(this.message);
  }
}

// DOM
<p>Hello, World!</p>

```

###### Property Bindings
- Also supports property bindings to help set values for properties and attributes of HTML elements and pass values to presentation logic
	- Notice square brackets indicating binding to value in component class
	
``` ts
<p [id]="sayHelloId" [style.color]="fontColor"> You can set my color in the component! </p>
```

###### Event Listeners
- Can also declare event listeners for keystrokes, mouse movements, clicks, touches
	- Event name in parentheses and reference to method in component

``` ts
<button type="button" 
[disabled]="canClick" 
(click)="sayMessage()"> 
Trigger alert message 
</button>

// Method in component class
sayMessage() {
  alert(this.message);
}
```

###### Directives
- Add features to templates with directives, e.g. \*ngIf and \*ngFor
	- Can dynamically modify DOM structure or create greate user experiences
- Helps to cleanly separate logic from presentation

```ts
import { Component } from '@angular/core';
 
@Component({
  selector: 'hello-world-ngif',
  templateUrl: './hello-world-ngif.component.html'
})
export class HelloWorldNgIfComponent {
  message = "I'm read only!";
  canEdit = false;
 
  onEditClick() {
    this.canEdit = !this.canEdit;
    if (this.canEdit) {
      this.message = 'You can edit me!';
    } else {
      this.message = "I'm read only!";
    }
  }
}

// HTML File
<h2>Hello World: ngIf!</h2>
 
<button type="button" (click)="onEditClick()">Make text editable!</button>
 
<div *ngIf="canEdit; else noEdit">
    <p>You can edit the following paragraph.</p>
</div>
 
<ng-template #noEdit>
    <p>The following paragraph is read only. Try clicking the button!</p>
</ng-template>
 
<p [contentEditable]="canEdit">{{ message }}</p>
```


##### Dependency Injection

Makes a class independent of its dependencies by decoupling the usage of an object from its creation.
- Angular handles instantiation for you, only need to declare dependencies
- Enables replacement of dependencies without changing the class that uses them, reduces risk class must be changed because one of its dependencies changed

Consider this service illustrating dependency injection, **logger.service.ts** that logs a number to the console.
- Notice the mandatory @Injectable tag indicating this is a service to be DIed

```ts
import { Injectable } from '@angular/core';

@Injectable({providedIn: 'root'})
export class Logger {
  writeCount(count: number) {
    console.warn(count);
  }
}
```

Next is the component with a button to call the writeCount function
- The logger service is injected by adding it to the constructor
```ts
import { Component } from '@angular/core';
import { Logger } from '../logger.service';

@Component({
  selector: 'hello-world-di',
  templateUrl: './hello-world-di.component.html'
})
export class HelloWorldDependencyInjectionComponent  {
  count = 0;

  constructor(private logger: Logger) { }

  onLogMe() {
    this.logger.writeCount(this.count);
    this.count++;
  }
}
```

This way, services that may be used across different components or called from the database are in one place, and there is a single instance being called to so no data integrity issues.

##### Angular CLI Commands

The Angular CLI is the fastest, straightforward, and recommended way to develop Angular applications. The Angular CLI makes some tasks trouble-free. For example:

COMMAND	DETAILS
| Command     | Details                                                              |
| ----------- | --------------------------------------------------------------------- |
| ng build    | Compiles an Angular application into an output directory.             |
| ng serve    | Builds and serves your application, rebuilding on file changes.       |
| ng generate | Generates or modifies files based on a schematic.                     |
| ng test     | Runs unit tests on a given project.                                |
| ng e2e      | Builds and serves an Angular application, then runs end-to-end tests. |

The Angular CLI is a valuable tool for building out your applications.


##### First-party libraries

The many benefits of Angular really become clear when your application grows and you want to add functions such as site navigation or user input. Use the Angular platform to incorporate one of the many first-party libraries that Angular provides.

Some of the libraries available to you include:

| Library                                                   | Details                                                                                                                                        |
| --------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- |
| [Angular Router](https://angular.io/guide/router)         | Advanced client-side navigation and routing based on Angular components. Supports lazy-loading, nested routes, custom path matching, and more. |
| [Angular Forms](https://angular.io/guide/forms-overview)  | Uniform system for form participation and validation.                                                                                          |
| [Angular HttpClient](https://angular.io/guide/http)       | Robust HTTP client that can power more advanced client-server communication.                                                                   |
| [Angular Animations](https://angular.io/guide/animations) | Tools for building Progressive Web Applications (PWA) including a service worker and Web application manifest.                                 |
| [Angular Schematics](https://angular.io/guide/schematics) | Automated scaffolding, refactoring, and update tools that simplify development at large scale.                                                 |

These libraries expand your application's capabilities while also letting you focus more on the features that make your application unique. Add these libraries knowing that they're designed to integrate flawlessly into and update simultaneously with the Angular framework.

These libraries are only required when they can help you add features to your applications or solve a particular problem.
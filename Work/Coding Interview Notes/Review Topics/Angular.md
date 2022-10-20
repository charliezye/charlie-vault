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
    message = 'Hello, World!';
}

// DOM
<p>Hello, World!</p>

```
- Also supports property bindings to help set values for properties and attributes of HTML elements and pass values to presentation logic

``` ts

```

##### Dependency Injection

Makes a class independent of its dependencies by decoupling the usage of an object from its creation.
- Enables replacement of dependencies without changing the class that uses them, reduces risk class must be changed because one of its dependencies changed
- 
Here are some basic interview questions and answers for an angular developer:

**What are components?**

**Answer:**

**what are services? give any one?**

**Answer:**

**how you create rounting in angular between components?**

**Answer:**

**What is route guard in Angular?**

**Answer:**

** What is difference between subject and behavior?**

**Answer:**

**What is Angular Framework?**

**Answer:** 
Angular is a TypeScript-based open-source front-end platform that makes it easy to build web, mobile and desktop applications. The major features of this framework include declarative templates, dependency injection, end to end tooling which ease application development.


**What is the difference between AngularJS and Angular?**

**Answer:** 
Angular is a completely revived component-based framework in which an application is a tree of individual components.

Here are some of the major differences in tabular format:- 

AngularJS	                                                    Angular
It is based on MVC architecture	                            This is based on Service/Controller
It uses JavaScript to build the application	Uses            TypeScript to build the application
Based on controllers concept	                            This is a component based UI approach
No support for mobile platforms	                            Fully supports mobile platforms
Difficult to build SEO friendly application	                Ease to build SEO friendly applications


**What is TypeScript?**

**Answer:**
TypeScript is a strongly typed superset of JavaScript created by Microsoft that adds optional types, classes, async/await and many other features, and compiles to plain JavaScript. Angular is written entirely in TypeScript as a primary language. You can install TypeScript globally as
npm install -g typescript
Let's see a simple example of TypeScript usage:-
function greeter(person: string) {
    return "Hello, " + person;
}

let user = "ramsant";

document.body.innerHTML = greeter(user);
The greeter method allows only string type as argument.

**Write a pictorial diagram of Angular architecture?**

**Answer:** 
The main building blocks of an Angular application are shown in the diagram below:- ScreenShot


**What are the key components of Angular?**

**Answer:**
Angular has the key components below,
Component: These are the basic building blocks of an Angular application to control HTML views.
Modules: An Angular module is a set of angular basic building blocks like components, directives, services etc. An application is divided into logical pieces and each piece of code is called as "module" which perform a single task.
Templates: These represent the views of an Angular application.
Services: Are used to create components which can be shared across the entire application.
Metadata: This can be used to add more data to an Angular class.


**What are directives?**

**Answer:** 
Directives add behaviour to an existing DOM element or an existing component instance.

import { Directive, ElementRef, Input } from '@angular/core';

@Directive({ selector: '[myHighlight]' })
export class HighlightDirective {
    constructor(el: ElementRef) {
       el.nativeElement.style.backgroundColor = 'yellow';
    }
}
Now this directive extends HTML element behavior with a yellow background as below

<p myHighlight>Highlight me!</p>


**What are components?**

**Answer:** 
Components are the most basic UI building block of an Angular app, which form a tree of Angular components. These components are a subset of directives. Unlike directives, components always have a template, and only one component can be instantiated per element in a template. Let's see a simple example of Angular component
import { Component } from '@angular/core';

@Component ({
   selector: 'my-app',
   template: ` <div>
      <h1>{{title}}</h1>
      <div>Learn Angular6 with examples</div>
   </div> `,
})

export class AppComponent {
   title: string = 'Welcome to Angular world';
}

**What is a template?**

**Answer:**
 A template is a HTML view where you can display data by binding controls to properties of an Angular component. You can store your component's template in one of two places. You can define it inline using the template property, or you can define the template in a separate HTML file and link to it in the component metadata using the @Component decorator's templateUrl property.

Using inline template with template syntax,

import { Component } from '@angular/core';

@Component ({
   selector: 'my-app',
   template: '
      <div>
         <h1>{{title}}</h1>
         <div>Learn Angular</div>
      </div>
   '
})

export class AppComponent {
   title: string = 'Hello World';
}
Using separate template file such as app.component.html

`import { Component } from '@angular/core';

@Component ({
   selector: 'my-app',
   templateUrl: 'app/app.component.html'
})

export class AppComponent {
   title: string = 'Hello World';
}`


**What is a module?**

**Answer:** 
Modules are logical boundaries in your application and the application is divided into separate modules to separate the functionality of your application. 
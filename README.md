# Introduction to Angular
- https://angular.io/

# What is Angular?
- https://angular.io/docs
Angular is a platform that makes it easy to build applications with the web. Angular combines declarative templates, dependency injection, end to end tooling, and integrated best practices to solve development challenges. Angular empowers developers to build applications that live on the web, mobile, or the desktop.

# Quick Start
- https://angular.io/guide/quickstart

# Prerequisites

## Node.js
- https://nodejs.org
- As an asynchronous event driven JavaScript runtime, Node is designed to build scalable network applications.
- Download and install: https://nodejs.org/en/download

## NPM
- https://www.npmjs.com/
- npm is the package manager for JavaScript and the world’s largest software registry. Discover packages of reusable code and assemble them in powerful new ways.
- Most used command:
```
npm install
npm update
npm uninstall
```

## CLI
- https://cli.angular.io/
- The Angular CLI makes it easy to create an application that already works, right out of the box. It already follows our best practices!
- Installation:
```npm install -g @angular/cli```

## Typescript
- https://www.typescriptlang.org/
- Typescript is a typed superset of JavaScript that compiles to plain JavaScript

# First Angular Application and Anatomy
- Creating: ```ng new [application_name]```
- Running: ```ng serve --open```

## Anatomy
- https://angular.io/guide/file-structure/

## Important folders/files:

| Folder/Files | Description |
-------------- | -----------
| /angular.json	| CLI configuration defaults for all projects in the workspace, including configuration options for build, serve, and test tools that the CLI uses, such as TSLint, Karma, and Protractor. |
| /package.json	| Configures npm package dependencies that are available to all projects in the workspace |
| /node_modules	| Provides npm packages to the entire workspace. |
| /src/app/app-routing.module.ts | Routing configurations |
| /src | The project source code and files |
| /src/app | Application components |
| /src/assets | Contains image files and other asset files to be copied as-is when you build your application. |
| /src/environments | Contains build configuration options for target environments. |
| /src/index.html | The main HTML page that is served when someone visits your site. The CLI automatically adds all JavaScript and CSS files when building your app, so you typically don't need to add any <script> or<link> tags here manually. |
| /src/styles.css | Global styles |
| /src/main.ts | The main entry point for your app. Compiles the application with the JIT compiler and bootstraps the application's root module (AppModule) to run in the browser. |
| /src/app/ | Contains your app's logic and data. Angular components, templates, and styles go here. | 
| /src/app/app.component.ts | Defines the logic for the app's root component, named AppComponent. The view associated with this root component becomes the root of the view hierarchy as you add components and services to your app. | 
| /src/app/app.component.html | Defines the HTML template associated with the root AppComponent. |
| /src/app/app.component.css | Defines the base CSS stylesheet for the root AppComponent. |
| /src/app/app.component.spec.ts | Defines a unit test for the root AppComponent. |
| /src/app/app.module.ts | Defines the root module, named AppModule, that tells Angular how to assemble the application. |
| /src/app/ | Contains image files and other asset files to be copied as-is when you build your application.	Contains image files and other asset files to be copied as-is when you build your application. |

## Files to inspect
- /angular.json
- /package.json
- /src/app/app.module.ts
- /src/app/app-routing.module.ts
- /src/index.html
  - `<app-root></app-root>`
- /src/styles.css
- /src/app/app.component.ts
- /src/app/app.component.html
- /src/app/app.component.css
  - `selector: 'app-root'`
- /src/app/app.component.spec.ts
- /node_modules

# Preparing for a new project

## Cleaning files

### app.component.html
```
<div style="text-align:center">
  <h1>Learning Angular</h1>
</div>
```

### app.component.ts
```
import { Component } from '@angular/core';
@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent {
}
```

## Creating a component
- command: `ng generate component data-binding`
- output:
```
CREATE src/app/data-binding/data-binding.component.html (31 bytes)
CREATE src/app/data-binding/data-binding.component.spec.ts (664 bytes)
CREATE src/app/data-binding/data-binding.component.ts (292 bytes)
CREATE src/app/data-binding/data-binding.component.css (0 bytes)
```
- Inspect each file

## Adding the component to the Application
- Add the component `selector` as an HTML tag to the `app.component.html`

### app.component.html
```
<div style="text-align:center">
  <h1>Learning Angular</h1>
</div>
<app-data-binding></app-data-binding>
```

# Basics about data binding and HTML template
- Data binding is one of the most powerful and important features in any software development language.
- It allows us to define communication between the component and view.
- So we can say that data binding is passed from component to view and from view to the component.

## Showing component properties with interpolation
  - Use the double curly braces: `{{property / expression}}`

### HTML template
```
<p>
  User Name: {{user_name}} has {{user_name.length}} characters
</p>
```

### Component class
```
import { Component } from '@angular/core';
@Component({
  selector: 'app-data-binding',
  templateUrl: './data-binding.component.html',
  styleUrls: ['./data-binding.component.css']
})
export class DataBindingComponent {
  user_name: string;
  constructor() { 
    this.user_name = "Jose";
  }
}
```

## Showing data with interpolation looping thru collections
- Use `*ngFor="let element of collection"` directive

### HTML template
```
<ul>
  <li *ngFor="let name of names">{{name}} has {{name?.length}} characters</li>
</ul>
```

### Component class
```
import { Component } from '@angular/core';
@Component({
  selector: 'app-data-binding',
  templateUrl: './data-binding.component.html',
  styleUrls: ['./data-binding.component.css']
})
export class DataBindingComponent {
  names: string[];
  constructor() { 
    this.names = ['Jose', 'Leila', 'Artur'];
  }
}
```

## Showing components conditionally and the ng-container tag
https://angular.io/guide/structural-directives
- Use `*ngIf='condition'` directive
- The <ng-template> is an Angular element for rendering HTML. It is never displayed directly.

### HTML template
```
<ul *ngIf="names.length >= 4">
  <!-- 
       One structural directive per host element: *ngIf or *ngFor
       The ng-container allow us to by-pass that
    -->
  <ng-container *ngFor="let name of names">
      <li *ngIf="name.length > 4">{{name}} has {{name.length}} characters</li>
  </ng-container>
</ul>
```

### Components class
```
import { Component } from '@angular/core';
@Component({
  selector: 'app-data-binding',
  templateUrl: './data-binding.component.html',
  styleUrls: ['./data-binding.component.css']
})
export class DataBindingComponent {
  names: string[];
  constructor() { 
    this.names = ['Jose', 'Leila', 'Artur'];
    //this.names.push("Rodrigues");
  }
}
```

## Binding a method to a button click
- Use the notation: (event)="method($event)"

### HTML template
```
<button (click)="addName($event)">Add Name</button>
<ul>
  <li *ngFor="let name of names">{{name}} has {{name?.length}} characters</li>
</ul>
```

### Component class
```
import { Component } from '@angular/core';
@Component({
  selector: 'app-data-binding',
  templateUrl: './data-binding.component.html',
  styleUrls: ['./data-binding.component.css']
})
export class DataBindingComponent {
  names: string[];
  constructor() { 
    this.names = [];
  }
  addName (event) {
    debugger;
    alert("Add User button clicked!");
  }
}
```

## Getting user input using a template reference variable
- A template reference varible provide direct access to an element from within the template.
- To declare a template reference variable, precede an identifier with a hash (or pound) character (#).

### HTML template
```
<input type="text" #newName>
<button (click)="addName(newName)">Add Name</button>
<ul>
  <li *ngFor="let name of names">{{name}} has {{name?.length}} characters</li>
</ul>
```

### Component class
```
import { Component } from '@angular/core';
@Component({
  selector: 'app-data-binding',
  templateUrl: './data-binding.component.html',
  styleUrls: ['./data-binding.component.css']
})
export class DataBindingComponent {
  names: string[];
  constructor() { 
    this.names = [];
  }
  addName (newName: any) {
    debugger;
    this.names.push(newName.value);
    newName.value = '';
  }
}
```

## Getting user input by binding a HTML component to a component property
- Use the two way databind decorator: `[(ngModel)]="component_property"`
- Change the `app.module.ts` file to add the Forms module
  - Add the import clause
  - Add FormsModule to the imposts array

### app.module.ts
```
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { AppRoutingModule } from './app-routing.module';
import { AppComponent } from './app.component';
import { DataBindingComponent } from './data-binding/data-binding.component';
import { FormsModule } from '@angular/forms';

@NgModule({
  declarations: [
    AppComponent,
    DataBindingComponent
  ],
  imports: [
    BrowserModule,
    AppRoutingModule,
    FormsModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

### HTML template
```
<input type="text" [(ngModel)]="newName" />
<button (click)="addName()">Add Name</button>
<p>New name value: {{newName}}</p>
<ul>
  <li *ngFor="let name of names">{{name}} has {{name?.length}} characters</li>
</ul>
```

### Component class
```
import { Component } from '@angular/core';
@Component({
  selector: 'app-data-binding',
  templateUrl: './data-binding.component.html',
  styleUrls: ['./data-binding.component.css']
})
export class DataBindingComponent {
  names: string[];
  newName: string;
  constructor() { 
    this.names = [];
    this.newName = "";
  }
  addName () {
    this.names.push(this.newName);
    this.newName = '';
  }
}
```

## Get user input from the $event object
- The $event represents the DOM event and carry a payload of information about the event/component

### HTML template
```
<input type="text" [(ngModel)]="newName" (keyup)="newNameOnKey($event)"/>
<button (click)="addName()">Add Name</button>
<p>New name value: {{newName}}</p>
<ul>
  <li *ngFor="let name of names">{{name}} has {{name?.length}} characters</li>
</ul>
```

### Component class
```
import { Component } from '@angular/core';
@Component({
  selector: 'app-data-binding',
  templateUrl: './data-binding.component.html',
  styleUrls: ['./data-binding.component.css']
})
export class DataBindingComponent {
  names: string[];
  newName: string;
  constructor() { 
    this.names = [];
    this.newName = "";
  }
  addName () {
    this.names.push(this.newName);
    this.newName = '';
  }
  newNameOnKey(event: KeyboardEvent) {
    console.log(event.key + " " + event.keyCode);
    if (event.key === "Enter") {
      this.addName();
    }
  }
}
```

## Key event filtering (with key.enter)
- The (keyup) event handler hears every keystroke. Sometimes only the Enter key matters, because it signals that the user has finished typing.

### HTML template
```
<input type="text" [(ngModel)]="newName" (keyup.enter)="addName()"/>
<button (click)="addName()">Add Name</button>
<button (click)="deleteNames()">Delete names</button>
<p>New name value: {{newName}}</p>
<ul>
  <li *ngFor="let name of names">{{name}} has {{name?.length}} characters</li>
</ul>
```

### Component class
```
import { Component } from '@angular/core';
@Component({
  selector: 'app-data-binding',
  templateUrl: './data-binding.component.html',
  styleUrls: ['./data-binding.component.css']
})
export class DataBindingComponent {
  names: string[];
  newName: string;
  constructor() { 
    this.names = [];
    this.newName = "";
  }
  addName() {
    this.names.push(this.newName);
    this.newName = '';
  }
  deleteNames() {
    this.names = [];
  }
}
```

[Next](Components.md)

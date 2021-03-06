# Architecture Overview
https://angular.io/guide/architecture
- The basic building blocks of an Angular application are NgModules, which provide a compilation context for components.
- NgModules collect related code into functional sets; an Angular app is defined by a set of NgModules.
- An app always has at least a root module (AppModule) that enables bootstrapping, and typically has many more feature modules.
- Components define views, which are sets of screen elements that Angular can choose among and modify according to your program logic and data.
- Components use services, which provide specific functionality not directly related to views. Service providers can be injected into components as dependencies, making your code modular, reusable, and efficient.

# Components

## Input parameters binding to component property
- Child component
  - Add the Input to the import clause from '@angular/core'
  - Create a propert with the decorator @Input()
- Parent component
  - Change the tag adding the child component to pass the input parameter using the annotation: `[parameter_name] = "property/expression"`
  - If the input parameter value is just a string (not a property), it has to be delimited (by ' ' or " " )

### Child component HTML template: `data-binding.component.html`
```
<input type="text" [(ngModel)]="newName"/>
<button (click)="addName()">{{addButtonLabel}}</button>
<p *ngIf="newName">New name value: {{newName}}</p>
<ul>
  <li *ngFor="let name of names">{{name}} has {{name?.length}} characters</li>
</ul>
```

### Child Component class: `data-binding.component.ts`
```
import { Component, OnInit, Input } from '@angular/core';
@Component({
  selector: 'app-data-binding',
  templateUrl: './data-binding.component.html',
  styleUrls: ['./data-binding.component.css']
})
export class DataBindingComponent implements OnInit {
  @Input() addButtonLabel: string = "Add";
  names: string[];
  newName: string;
  constructor() { 
    this.names = [];
    this.newName = "";
  }
  ngOnInit() {}
  addName () {
    this.names.push(this.newName);
    this.newName = '';
  }
}
```

### Parent component HTML template: `app.component.html`
```
<app-data-binding [addButtonLabel] = "'Click to Add a Name'"></app-data-binding>
<app-data-binding [addButtonLabel] = "'Add Name'"></app-data-binding>
<app-data-binding></app-data-binding>
```

## Input parameters binding to set/get method
- Child component
  - Create a private attribute and the set and get methods under the @Input decorator
- Parent component
  - Change the tag adding the child component to pass the input parameter using the annotation: `[parameter_name] = "property/expression"`
  - If the input parameter value is just a string (not a property), it has to be delimited (by ' ' or " " )

### Child component HTML template: `data-binding.component.html`
```
<div style="border-style: solid">
  <h2>Child component</h2>
  <input type="text" [(ngModel)]="newName"/>
  <button (click)="addName()">{{addButtonLabel}}</button>
  <ul>
    <li *ngFor="let name of names">{{name}} has {{name?.length}} characters</li>
  </ul>
</div>
```

### Child component class: `data-binding.component.ts`
```
import { Component, Input } from '@angular/core';
@Component({
  selector: 'app-data-binding',
  templateUrl: './data-binding.component.html',
  styleUrls: ['./data-binding.component.css']
})
export class DataBindingComponent {
  private _addButtonLabel = 'Add';

  @Input()
  set addButtonLabel(label: string) {
    this._addButtonLabel = label;
  }
  get addButtonLabel(): string {
    return this._addButtonLabel;
  }

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

### Parent component HTML template: `app.component.html`
```
<p>Add Button label: {{addButtonLabel}}</p>
<button (click)="changeLabel(addButtonLabelInput.value)">Change 'addButtonLabel'</button>
<input type="text" #addButtonLabelInput>
<app-data-binding 
  [addButtonLabel]="addButtonLabel">
</app-data-binding>
```

### Parent component class: `app.component.ts`
```
import { Component } from '@angular/core';
@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent {
  names: string[];
  addButtonLabel = 'Add a new name';
  constructor() { }
  namesOuput(event: string[]) {
    this.names = event;
  }
  changeLabel(newLabel: string) {
    this.addButtonLabel = newLabel;
  }
}
```

## Output parameters and EventEmitter
- On the child component
  - Add the Output to the import clause from '@angular/core'
  - Create a property of the type EventEmitter<return_type> and tag with the @Output() decorator
  - Define a method to return (emit) the output value to the parent component
- On the parent component
  - Add a tag binding the output parameter to a method
  - Implement the method to receive the output parameter from the child component
  
### Child component HTML template: `data-binding.component.html`
```
<input type="text" [(ngModel)]="newName"/>
<button (click)="addName()">{{addButtonLabel}}</button>
<ul>
  <li *ngFor="let name of names">{{name}} has {{name?.length}} characters</li>
</ul>
<button (click)="namesOuput()">Return names</button>
```

### Child component class: `data-binding.component.ts`
```
import { Component, Input, Output, EventEmitter } from '@angular/core';
@Component({
  selector: 'app-data-binding',
  templateUrl: './data-binding.component.html',
  styleUrls: ['./data-binding.component.css']
})
export class DataBindingComponent {
  @Input() addButtonLabel: string = "Add";
  @Output() onNamesOuput: EventEmitter<string[]> = new EventEmitter<string[]>();
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
  namesOuput(event: string[]) {
    this.onNamesOuput.emit(this.names);
    this.names = [];
  }
}
```

### Parent component HTML template: `app.component.html`
```
<app-data-binding (onNamesOuput)="namesOuput($event)"> </app-data-binding>
<h3>Names</h3>
<ul>
    <li *ngFor="let name of names">{{name}} has {{name?.length}} characters</li>
</ul>
```

### Parent component class: `app.component.ts`
```
import { Component } from '@angular/core';
@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent {
  names: string[];
  constructor() { }
  namesOuput(event: string[]) {
    this.names = event;
  }
}
```

# Component lifecycle
- https://angular.io/guide/lifecycle-hooks
- A component has a lifecycle managed by Angular.
- ngOnInit
  - Initialize the directive/component after Angular first displays the data-bound properties and sets the directive/component's input properties.
  - Called once, after the first ngOnChanges().
- ngOnChanges
  - Respond when Angular (re)sets data-bound input properties.
  - The method receives a SimpleChanges object of current and previous property values.
  - Called before ngOnInit() and whenever one or more data-bound input properties change.
- ngDoCheck
  - Detect and act upon changes that Angular can't or won't detect on its own.
  - Called during every change detection run, immediately after ngOnChanges() and ngOnInit().
- ngAfterContentInit
  - Respond after Angular projects external content into the component's view / the view that a directive is in.
  - Called once after the first ngDoCheck().
- ngAfterContentChecked
  - Respond after Angular checks the content projected into the directive/component.
  - Called after the ngAfterContentInit() and every subsequent ngDoCheck().
- ngAfterViewInit
  - Respond after Angular initializes the component's views and child views / the view that a directive is in.
  - Called once after the first ngAfterContentChecked().
- ngAfterViewChecked	
  - Respond after Angular checks the component's views and child views / the view that a directive is in.
  - Called after the ngAfterViewInit() and every subsequent ngAfterContentChecked().
- ngOnDestroy
  - Cleanup just before Angular destroys the directive/component.
  - Unsubscribe Observables and detach event handlers to avoid memory leaks.
  - Called just before Angular destroys the directive/component.

## ngOnInit
- https://angular.io/api/core/OnInit
  - A lifecycle hook that is called after Angular has initialized all data-bound properties of a directive.
- Add OnInit to the `@angular/core` import clause
- Add `implements OnInit` to the component class declaration
- Implements the method `ngOnInit()`

### Child component HTML template: `data-binding.component.html`
```
<input type="text" [(ngModel)]="newName"/>
<button (click)="addName()">Add Name</button>
<button (click)="deleteNames()">Delete Names</button>
<ul>
  <li *ngFor="let name of names">{{name}} has {{name?.length}} characters</li>
</ul>
```

### Child component class: `data-binding.component.ts`
```
import { Component, OnInit } from '@angular/core';
@Component({
  selector: 'app-data-binding',
  templateUrl: './data-binding.component.html',
  styleUrls: ['./data-binding.component.css']
})
export class DataBindingComponent implements OnInit {
  names: string[];
  newName: string;
  constructor() {
    // Constructors should be used only to inject dependencies or initialize attributes 
  }
  addName () {
    if (this.newName) {
      this.names.push(this.newName);
      this.newName = '';
    }
  }
  deleteNames() {
    this.names = [];
  }
  ngOnInit() {
    debugger;
    this.names = ['Jose', 'Leila', 'Artur'];
    this.newName = "";
  }
}
```

### Parent component HTML template: `app.component.html`
```
<button (click)="showHideNames()">{{showHideNamesFlag ? 'Hide' : 'Show'}} Names</button>
<div>
  <app-data-binding *ngIf="showHideNamesFlag"></app-data-binding>
</div>
```

### Parent component class: `app.component.html`
```
import { Component } from '@angular/core';
@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent {
  showHideNamesFlag: boolean = true;
  showHideNames() {
    this.showHideNamesFlag = !this.showHideNamesFlag;
  }
}
```

## ngOnDestroy
- https://angular.io/api/core/OnDestroy
  - A lifecycle hook that is called when a directive, pipe, or service is destroyed.
- Add OnDestroy to the `@angular/core` import clause
- Add `implements OnDestroy` to the component class declaration
- Implements the method `ngOnInit()`

### Child component class: `data-binding.component.ts`
```
import { Component, OnInit, OnDestroy } from '@angular/core';
@Component({
  selector: 'app-data-binding',
  templateUrl: './data-binding.component.html',
  styleUrls: ['./data-binding.component.css']
})
export class DataBindingComponent implements OnInit, OnDestroy {
  names: string[];
  newName: string;
  constructor() { }
  addName () {
    if (this.newName) {
      this.names.push(this.newName);
      this.newName = '';
    }
  }
  deleteNames() {
    this.names = [];
  }
  ngOnInit() {
    debugger;
    this.names = ['Jose', 'Leila', 'Artur'];
    this.newName = "";
  }
  ngOnDestroy() {
    debugger;
    this.names = null; // Pretending we are releasing resources
    console.log('Component destroyed');
  }
}
```

## ngOnChanges
- https://angular.io/api/core/OnChanges
  - A lifecycle hook that is called when any data-bound input property of a directive changes.
- Add OnChanges and SimpleChanges to the `@angular/core` import clause
- Add `implements OnChanges` to the component class declaration
- Implements the method `ngOnChanges(changes: SimpleChanges)`

### Child component HTML template: `data-binding.component.html`
```
<p>{{firstName}}</p>
<p>{{lastName}}</p>
```

### Child component class: `data-binding.component.ts`
```
import { Component, Input, OnChanges, SimpleChanges  } from '@angular/core';
@Component({
  selector: 'app-data-binding',
  templateUrl: './data-binding.component.html',
  styleUrls: ['./data-binding.component.css']
})
export class DataBindingComponent implements OnChanges {
  @Input() firstName: string;
  @Input() lastName: string;
  constructor() {
  }
  ngOnChanges(changes: SimpleChanges) {
    console.log(changes);
    for (let propName in changes) {
      let chng = changes[propName];
      let cur  = JSON.stringify(chng.currentValue);
      let prev = JSON.stringify(chng.previousValue);
      console.log(`${propName}: currentValue = ${cur}, previousValue = ${prev}`);
    }
  }
}
```

### Parent component HTML template: `app.component.html`
```
<input type="text" #first_name />
<input type="text" #last_name />
<button (click)="saveName(first_name.value, last_name.value)">Update Name</button>
<app-data-binding 
  [firstName]='firstName'
  [lastName]='lastName'>
</app-data-binding>
```

### Parent component class: `app.component.html`
```
import { Component } from '@angular/core';
import { last } from '@angular/router/src/utils/collection';
@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent {
  firstName: string = "";
  lastName: string = "";
  saveName(firstName: string, lastName: string) {
    this.firstName = firstName;
    this.lastName = lastName;
  }
}
```

## Styling: CSS

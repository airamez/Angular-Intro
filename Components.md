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

### Child HTML template
```
<input type="text" [(ngModel)]="newName"/>
<button (click)="addName()">{{addButtonLabel}}</button>
<p *ngIf="newName">New name value: {{newName}}</p>
<ul>
  <li *ngFor="let name of names">{{name}} has {{name?.length}} characters</li>
</ul>
```

### Child Component class
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

### Parent component HTML template
```
<app-data-binding [addButtonLabel] = "'Click to Add a Name'"></app-data-binding>
<app-data-binding [addButtonLabel] = "'Add Name'"></app-data-binding>
<app-data-binding></app-data-binding>
```

## Input parameters binding to set/get method
- Child component
  - Create a private attribute and the set and get methods under the @Input decorator
- Parent component
  - Change the tag adding the child component to pass the input parameter using the annotation:
    `[parameter_name] = "property/expression"`
  - If the input parameter value is just a string (not a property), it has to be delimited (by ' ' or " " )

### Child component HTML template
```
<div style="border-style: solid">
  <h1>Child component</h1>
  <input type="text" [(ngModel)]="newName"/>
  <button (click)="addName()">{{addButtonLabel}}</button>
  <ul>
    <li *ngFor="let name of names">{{name}} has {{name?.length}} characters</li>
  </ul>
</div>
```

### Child component class
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

### Parent component HTML
```
<p>Add Button label: {{addButtonLabel}}</p>
<button (click)="changeLabel(addButtonLabelInput.value)">Change 'addButtonLabel'</button>
<input type="text" #addButtonLabelInput>
<app-data-binding 
  [addButtonLabel]="addButtonLabel">
</app-data-binding>
```

### Parent component class
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

## Output paramters and EventEmitter
- On the child component
  - Add the Output to the import clause from '@angular/core'
  - Create a property of the type EventEmitter<return_type> and tag with the @Output() decorator
  - Define a method to return (emit) the output value to the parent component
- On the parent component
  - Add a tag binding the output parameter to a method
  - Implement the method to receive the output parameter from the child component
  
### Child component HTML template
```
<input type="text" [(ngModel)]="newName"/>
<button (click)="addName()">{{addButtonLabel}}</button>
<ul>
  <li *ngFor="let name of names">{{name}} has {{name?.length}} characters</li>
</ul>
<button (click)="namesOuput()">Return names</button>
```

### Child component class
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

### Parent component HTML template
```
<div style="text-align:center">
    <h1>Learning Angular</h1>
</div>
<app-data-binding (onNamesOuput)="namesOuput($event)"> </app-data-binding>
<h1>Names</h1>
<ul>
    <li *ngFor="let name of names">{{name}} has {{name?.length}} characters</li>
</ul>
```

### Parent component class
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

# Architecture Overview
https://angular.io/guide/architecture
- The basic building blocks of an Angular application are NgModules, which provide a compilation context for components.
- NgModules collect related code into functional sets; an Angular app is defined by a set of NgModules.
- An app always has at least a root module (AppModule) that enables bootstrapping, and typically has many more feature modules.
- Components define views, which are sets of screen elements that Angular can choose among and modify according to your program logic and data.
- Components use services, which provide specific functionality not directly related to views. Service providers can be injected into components as dependencies, making your code modular, reusable, and efficient.

# Components
## Input paramters
- Add the Input to the import clause from '@angular/core'
- Create a propert with the decorator @Input()
- Change the tag adding the component to pass the input parameter
### Component class
```
import { Component, OnInit, Input } from '@angular/core';
@Component({
  selector: 'app-data-binding',
  templateUrl: './data-binding.component.html',
  styleUrls: ['./data-binding.component.css']
})
export class DataBindingComponent implements OnInit {
  @Input() 
  addButtonLabel: string = "Add";
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
### HTML template
```
<input type="text" [(ngModel)]="newName"/>
<button (click)="addName()">{{addButtonLabel}}</button>
<p *ngIf="newName">New name value: {{newName}}</p>
<ul>
  <li *ngFor="let name of names">{{name}} has {{name?.length}} characters</li>
</ul>
```
## Parent component HTML template
```
<div style="text-align:center">
  <h1>Learning Angular</h1>
</div>
<app-data-binding [addButtonLabel] = "'Click to Add a Name'"></app-data-binding>
<app-data-binding [addButtonLabel] = "'Add Name'"></app-data-binding>
<app-data-binding></app-data-binding>
```




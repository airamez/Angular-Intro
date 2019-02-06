
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

## First Angular Application and Anatomy
- Creating: ```ng new [application_name]```
- Running: ```ng serve --open```

## Anatomy
- https://angular.io/guide/file-structure/

### Important folders/files:

| Folder/Files | Description |
-------------- | -----------
| /package.json	| Configures npm package dependencies that are available to all projects in the workspace |
| /angular.json	| CLI configuration defaults for all projects in the workspace, including configuration options for build, serve, and test tools that the CLI uses, such as TSLint, Karma, and Protractor. |
| /node_modules	| Provides npm packages to the entire workspace. |
| /src | The project source code and files |
| /src/app | Application components |
| /src/assets | Contains image files and other asset files to be copied as-is when you build your application. |
| /src/environments | Contains build configuration options for target environments. |
| /src/	index.html | The main HTML page that is served when someone visits your site. The CLI automatically adds all JavaScript and CSS files when building your app, so you typically don't need to add any <script> or<link> tags here manually. |
| /src/	main.ts | The main entry point for your app. Compiles the application with the JIT compiler and bootstraps the application's root module (AppModule) to run in the browser. |
| /src/app/ | Contains your app's logic and data. Angular components, templates, and styles go here. | 
| /src/app/app.component.ts | Defines the logic for the app's root component, named AppComponent. The view associated with this root component becomes the root of the view hierarchy as you add components and services to your app. | 
| /src/app/app.component.html | Defines the HTML template associated with the root AppComponent. |
| /src/app/app.component.css | Defines the base CSS stylesheet for the root AppComponent. |
| /src/app/app.component.spec.ts | Defines a unit test for the root AppComponent. |
| /src/app/app.module.ts | Defines the root module, named AppModule, that tells Angular how to assemble the application. |
| /src/app/ | Contains image files and other asset files to be copied as-is when you build your application.	Contains image files and other asset files to be copied as-is when you build your application. |

# Architecture Overview
## Modules
## Components
## Templates, Directives, and data binding
## Services and dependency injection
## Routing



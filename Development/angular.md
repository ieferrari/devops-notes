# Angular
Basic commands and cheat sheet

***
## Angular CLI
Install, check version, and start a new App:

    npm install -g @angular/cli -g
    ng -v  
    ng new myApp --style scss --routing


angular.json  controls the behaviour of the cli

compile the code with webpack and open a browser

    ng serve -o

### Components
to create a new component:

    ng generate component --help  # to see options
    ng generate component myComponent  [options]
    ng g c myComponent [options]

  check the compiled front-end in /src/app

#### binding attributes
in myComponent.ts:

```typescript
is_disabled = true;
myTitle = "Example";
```

in myComponent.html:

```html
<h1> {{myTitle}} </h1>
<button [disabled]="is_disabled">
  button
</button>
```

#### binding events:
in myComponent.ts, inside class myComponentComponent{}

```typescript
myTitle = "Example";
changeTitle(){
  this.myTitle="New Title"
}
```


in myComponent.html:

```html
<h1> {{myTitle}} </h1>
<button (click)="changeTitle()">
  button
</button>
```
### directives

in myFile.html:

```html
<div *ngIf="is_disabled"> ... </div>

<h2 [nGClass]="{
    'green': my.var === "green_car",
    'red': my.var === "red_car"
  }">
  myTitle
</h2>

<div *ngFor="let title of title_list">
 {{title}}
</div>
```

to create your own custom directives, use:

    ng g d myNewCustomDirective


### Pipes
check: https://fknop.gitbook.io/angular-pipes/

    {{3.141516 | number }}
    renders: 3.141

to create custom pipes:

    ng g pipe my_custom_pipe



### Tests
defined inside spec file


    ng test


### Add packages

add libraries or packages. Example for progressive webapps:

    ng add @angular/pwa


### Build
Package and bundle all the app to deploy on production. as lightweight and fast as possible.
Check build options inside the **angular.json** file

(architect >> build >> configurations >> production >> [options])

    ng build

You can find the output  files in the **/dist** folder

### Udate
to update the packages in an app just run:

    ng update

### Docs
to search specific [topic] in the documentation:

    ng doc [topic]

***
## Angular components
component: controller for user interface


### Interpolate




## Don't use DOM
because it does not exists in movile apps, so your code wont be portable

  ~~document.querySelector("#example").innerHTML="some text"~~

***
## Routers
set url path to different components

in app-routing.module.ts:

```typescript
import {MyCompComponent} from './myComp';

const routes: Routs=[
  {path: 'new/url/route', component:  MyCompComponent}
];

```

***
## Interact with APIs using HTTP client

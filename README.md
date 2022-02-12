# Angular Monorepo Project

Angular Monorepo Project - tutorial:

https://kgotgit.medium.com/monorepo-pattern-setting-up-angular-workspace-for-multiple-applications-in-one-single-repository-4e14bc0d0cc0


## Create Angular Workspace ng-beehive-monorepo
```
ng new ng-beehive-monorepo --create-application false
```

## Create all sub-application(s)
```
// create beehive-RGB sub-applciation
ng g application beehive-RGB --routing --style=scss

// create beehive-RG sub-applciation
ng g application beehive-RG --routing --style=scss

// create beehive-red sub-applciation
ng g application beehive-red --routing --style=scss

// create beehive-green sub-applciation
ng g application beehive-green --routing --style=scss

// create beehive-blue sub-applciation
ng g application beehive-blue --routing --style=scss
```

## Create library project(s)

```
// Create library project lib-beehive-RG-shared
ng g lib lib-beehive-RG-shared

// Create library project lib-beehive-UI-shared
ng g lib lib-beehive-UI-shared

// Create library project lib-beehive-RGB-shared
ng g lib lib-beehive-RGB
```

## Add package.json to start each sub-application

```
"start:beehive-blue":"ng serve --project=beehive-blue --port 4000",

"start:beehive-red":"ng serve --project=beehive-red --port 4100",

"start:beehive-green":"ng serve --project=beehive-green --port 4300",

"start:beehive-RGB":"ng serve --project=beehive-RGB --port 4400",

"start:beehive-RG":"ng serve --project=beehive-RG --port 4500"
```

## Add modules and components in beehive-red sub-application

```
// create module bee-red-happy along with routing
ng g m pages/bee-red-happy --routing --project=beehive-red

// create bee-blue-happy component
ng g c pages/bee-red-happy --project=beehive-red
```

## Update the routes to add a mapping between /beehive-red-happy path to BeeRedHappyComponent

```
const routes: Routes = [
  {path:'',component:BeeRedHappyComponent}
];
```

## Update AppRoutingModule as below to lazily load modules. This allows us to run the beehive-red sub-project as a standalone application

```
const routes: Routes = [
{"path":"pages/beehive-red-happy",loadChildren:()=>import('./pages/bee-red-happy/bee-red-happy.module').then(mod=>mod.BeeRedHappyModule)},
{"path":"",redirectTo:"pages/beehive-red-happy",pathMatch:'full'},
{"path":"**",redirectTo:"pages/beehive-red-happy",pathMatch:'full'}
];
```
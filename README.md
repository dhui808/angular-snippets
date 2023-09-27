# angular-snippets
### Compiler dependency error
    Delete package-lock.json and node_modules
    npm i --save --legacy--peer-deps
### webpack bundle not shown in browser
    add: "sourceMap":true and "optimization":false under architect -> build-> options in your angular.json.
    
### Angular modules/files loading sequence
    angular.json:
        "index": "src/index.html",
        "main": "src/main.ts",
    main.js is loaded first:
        platformBrowserDynamic().bootstrapModule(AppModule)
    The first module that is to be loaded (bootstraped) is AppModule, then is reads app.module.ts
    app.module.ts:
        bootstrap: [AppComponent]
    app.component.ts:
        selector: 'myapp-root',
        template: `<router-outlet></router-outlet>`,
    index.html:
        <body><myapp-root></myapp-root></body>
        
### Context Root Path
    To use /hello as the root path the Angular application:
    package.json:
        No change
    angular.json:
        "outputPath": "dist/hello",
        "baseHref": "/hello/",
        
    Copy dist/hello folder to Tomcat and the browser is able to load all assets from /hello folder.
    It also works with the webpack-dev-server.
    
### what frameworks/APIs does Angular use to consume REST APIs?
    HTTP client module
        RxJS: HTTP client is built on top of RxJS, to easily manage asynchronous data streams
        Interceptors can modify requests and responses before they are sent or received.
        Error handling
        Caching
        
### Set up  Local development environment
    Upgrading Node.js to latest version - Windows (including npm)
      https://nodejs.org/en/download/
      nodejs: v18.14.2
      npm: 8.19.2
      Angular CLI: 15.2.1
      
    Install the Angular CLI
    (To allow PowerShell)
    Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned
    
    npm install -g @angular/cli
    ng version
    
    npm uninstall -g @angular/cli
    npm cache clean --force

    Create a workspace and initial application
    ng new my-app-v14
    
    Run the application
    cd my-app-v14
    ng serve --open

    The browser is open at http://localhost:4200
    
    Build project
    ng build
    
    Run from web server
    Open Web Server for Chrome
    Point folder at dist/my-app-v14
    Open the browser at http://localhost:4200

### Interface
    In Angular, an interface defines a data object
### Format data with pipes
    <h2>{{hero.name | uppercase}} Details</h2>
### Two-way binding with [(ngModel)]
    <input id="name" [(ngModel)]="hero.name" placeholder="name">

    ngModel belongs to FormsModule, which must be declared in @NgModule in AppModule class in app.module.ts.

## Tutorial
### Create new Angular project
    npm install -g @angular/cli
    
    From PowerShell:
    Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned
    Get-ExecutionPolicy -Scope CurrentUser
    
    ng new angular-auth-jwt-example
    cd angular-auth-jwt-example
    ng serve --open
    
### Create Component
    ng generate component Home --standalone --inline-template --skip-tests
    
### Add the new component to the app's layout
    In app.component.ts:
    import { HomeComponent } from './home/home.component';
    
    Update the imports array property:
    imports: [
        HomeComponent,
    ],
    
    Update the template property:
### Add features to the component
### Create a new Angular interface
    Interfaces are custom data types 
    ng generate interface housinglocation
    Add import statement to the referencing component
    Create a single instance of the new interface in the component
### Add an input parameter to the component
    To receive data from a parent component, a child component must mark a class property with the @Input() decorator.
    To mark an interface as the input for a child component:
    export class HousingLocationComponent {
        @Input() housingLocation!: HousingLocation;
    }

    The other way of passing data from parent component to the child component is to use routing path parameter.
    
### Add a property binding to a component’s template
    <app-housing-location [housingLocation]="housingLocation"></app-housing-location>
    The syntax is [attribute] = "value"
### Send data from parent component to child component
### Add an interpolation (dynamic value) to a component’s template
    Using the {{ expression }} in Angular templates
    template: `
      <section class="listing">
        <img class="listing-photo" [src]="housingLocation.photo" alt="Exterior photo of {{housingLocation.name}}">
        <h2 class="listing-heading">{{ housingLocation.name }}</h2>
        <p class="listing-location">{{ housingLocation.city}}, {{housingLocation.state }}</p>
      </section>
      `,
  
  The parent component HomeComponent to the passes a HousingLocation object to the child component HousingLocationComponent.
  The child component passes housingLocation to its template (html).
  The template accesses the object's properties.
### Use *ngFor in template to list objects in component
    *ngFor is the the equivalent of a "for" loop
### Create Angular services and Dependency Injection
    ng generate service housing --skip-tests
    
    In home.component.ts
    import { Component, inject } from '@angular/core';
    import { HousingService } from '../housing.service';
    
    housingLocationList: HousingLocation[] = [];
    housingService: HousingService = inject(HousingService);

    constructor() {
      this.housingLocationList = this.housingService.getAllHousingLocations();
    }
### Add routes to the application
    Routing is the ability to navigate from one component in the application to another.
    
    In the src/app directory, create a file called routes.ts
    In main.ts
    import { provideRouter } from '@angular/router';
    import routeConfig from './app/routes';
    Update the call to bootstrapApplication to include the routing configuration:
    bootstrapApplication(AppComponent,
    {
        providers: [
          provideProtractorTestingSupport(),
          provideRouter(routeConfig)
        ]
      }
    ).catch(err => console.error(err));

    In src/app/app.component.ts, update the component to use routing:
    import { RouterModule } from '@angular/router';
    imports: [
      HomeComponent,
      RouterModule,
    ],
    In the template property, replace the <app-home></app-home> tag with the <router-outlet> directive 
    and add a link back to the home page. 
    
    Add route to new component:
    In routes.ts
    import { Routes } from '@angular/router';
    import { HomeComponent } from './home/home.component';
    import { DetailsComponent } from './details/details.component';
    const routeConfig: Routes = [
      {
        path: '',
        component: HomeComponent,
        title: 'Home page'
      },
      {
        path: 'details/:id',
        component: DetailsComponent,
        title: 'Home details'
      }
    ];

    export default routeConfig;
### Integrate details page into application
    Connect the details page to the app and navigate to the details page.
    In housing-location.component.ts
    import { RouterModule } from '@angular/router';
    imports: [CommonModule, RouterModule],
    In template:
    <a [routerLink]="['/details', housingLocation.id]">Learn More</a>
    The value assigned to the routerLink is an array with two entries: the static 
    portion of the path and the dynamic data.
    
    Get route parameters from the DetailsComponent
    Customize the DetailComponent
    
    Add navigation back to the HomeComponent
    
### Add a Form that collects user data 
    Add a method to your the service that receives the form data and sends it to the data's destination.
    
    Add the form functions to the page
    import { FormControl, FormGroup, ReactiveFormsModule } from '@angular/forms';
    imports: [CommonModule, ReactiveFormsModule],
    Create the form object
    applyForm = new FormGroup({
      firstName: new FormControl(''),
      lastName: new FormControl(''),
      email: new FormControl('')
    });
    Add a method to handle submit button click event.
    (uses the nullish coalescing operator to default to empty string if the value is null.)
    submitApplication() {
      this.housingService.submitApplication(
        this.applyForm.value.firstName ?? '',
        this.applyForm.value.lastName ?? '',
        this.applyForm.value.email ?? ''
      );
    }
    Add the form's markup to the template.
    <form [formGroup]="applyForm" (submit)="submitApplication()">
        <label for="first-name">First Name</label>
        <input id="first-name" type="text" formControlName="firstName">

        <label for="last-name">Last Name</label>
        <input id="last-name" type="text" formControlName="lastName">

        <label for="email">Email</label>
        <input id="email" type="email" formControlName="email">
        <button type="submit" class="primary">Apply now</button>
      </form>
### Add the search feature
    filterResults(text: string) {
      if (!text) {
        this.filteredLocationList = this.housingLocationList;
      }

      this.filteredLocationList = this.housingLocationList.filter(
        housingLocation => housingLocation?.city.toLowerCase().includes(text.toLowerCase())
      );
    }
### Add HTTP communication
    Configure the JSON server
    
    use a local web server (json-server)
    use asynchronous service methods to retrieve data.
    
### *ngFor and *ngIf
    <h2>My Heroes</h2>
    <ul class="heroes">
      <li *ngFor="let hero of heroes">
        <button [class.selected]="hero === selectedHero" type="button" (click)="onSelect(hero)">
          <span class="badge">{{hero.id}}</span>
          <span class="name">{{hero.name}}</span>
        </button>
      </li>
    </ul>
    
    <div *ngIf="selectedHero">
      <h2>{{selectedHero.name | uppercase}} Details</h2>
      <div>id: {{selectedHero.id}}</div>
      <div>
        <label for="hero-name">Hero name: </label>
        <input id="hero-name" [(ngModel)]="selectedHero.name" placeholder="name">
      </div>
    </div>
###  ngOnInit lifecycle hook
    ngOnInit(): void {
      this.getHeroes();
    }
### Observable Service for asychrounous calls
    Observable is one of the key classes in the RxJS library
    import { Observable, of } from 'rxjs';
        getHeroes(): Observable<Hero[]> {
      const heroes = of(HEROES);
      return heroes;
    }

    Subscribe in the calling component
    getHeroes(): void {
      this.heroService.getHeroes()
          .subscribe(heroes => this.heroes = heroes);
    }
### Add the AppRoutingModule if not generated yet
    ng generate module app-routing --flat --module=app
### Add RouterOutlet
### Add a navigation link using routerLink
### The backtick characters
    The backtick ( ` ) characters define a JavaScript template literal, i.e. the expression will be evaluated.
    getHero(id: number): Observable<Hero> {
      const hero = HEROES.find(h => h.id === id)!;
      this.messageService.add(`HeroService: fetched hero id=${id}`);
      return of(hero);
    }
### RxJS pipe()
    RxJS pipe() is both a standalone function and a method on the Observable interface that can be used to 
    combine multiple RxJS operators to compose asynchronous operations. 
    The pipe() function takes one or more operators and returns an RxJS Observable.
### RxJS tap()
    RxJS tap() operator is a utility operator that returns an observable output that is identical to the source 
    observable but performs a side effect for every emission on the source observable.
    getHeroes(): Observable<Hero[]> {
      return this.http.get<Hero[]>(this.heroesUrl)
        .pipe(
          tap(_ => this.log('fetched heroes')),
          catchError(this.handleError<Hero[]>('getHeroes', []))
        );
    }

    All components must also be declared in @NgModule 
    
    

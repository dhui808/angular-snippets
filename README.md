# angular-snippets

### Context Root Path
    To use /hello as the root path the Angular application:
    package.json:
        "build": "ng build --base-href /hello/",
        "dev": "lite-server --baseDir=dist/hello/",
        "start": "ng serve --open"
    angular.json:
        "outputPath": "dist/hello",
        "baseHref": "/hello",
        
    Copy dist/hello folder to Tomcat and the browser is able to load all assets from /hello folder.
    It also works in lite-server or the  webpack-dev-server.

    Note that angular.json baseHref does not have the trailing slash. This is the key that allows
    lite-server and the  webpack-dev-server to work. Adding the trailing slash will cause these two
    servers failing to find the assets.
    
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

    ngModel belongs to FormsModule, which must be declared in @NgModule in app.module.ts.
    All components must also be declared in @NgModule 
    
    

# angular-snippets
### Set up  Local development environment
    Upgrading Node.js to latest version - Windows (including npm)
      https://nodejs.org/en/download/
      v16.15.1
    
    Install the Angular CLI
    (To allow PowerShell)
    Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned
    
    npm install -g @angular/cli
    ng version
    
    Create a workspace and initial application
    ng new my-app-v14
    
    Run the application
    cd my-app-v14
    ng serve --open

    The browser is open at http://localhost:4200
    
    Build project
    ng build
    

### Error: src/main.ts:10:14 - error TS7015: Element implicitly has an 'any' type because index expression is not of type 'number'. if (window['ngRef']) {
    const _window = window as any;
    if (_window['ngRef']) {
      _window.destroy();
    }
    _window['ngRef'] = ref;

### Create Angular project with Stackblitz
[Stackblitz](https://stackblitz.com/)  
    
    polyfills.ngtypecheck.ts not found
    Modify src/tsconfig.app.json and src/tsconfig.spec.json, removing polyfills.*.ts and test.ts
    Success!
    Or copy src/polyfills.ts and src/styles.scss from other projects.
    
### Webpack module is not found
    delete package-lock.json
    delete node_modules
    delete dist (if exist)

    npm cache clean --force

    npm install
### The Angular Compiler requires TypeScript >=4.4.2 and <4.6.0 but 4.9.5 was found instead
    npm i -D typescript@4.5.4
    

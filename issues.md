### Error: src/main.ts:10:14 - error TS7015: Element implicitly has an 'any' type because index expression is not of type 'number'. if (window['ngRef']) {
    const _window = window as any;
    if (_window['ngRef']) {
      _window.destroy();
    }
    _window['ngRef'] = ref;

###

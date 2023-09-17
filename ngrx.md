### Resources
[Ngrx Essentials](https://this-is-angular.github.io/ngrx-essentials-course/docs)  

### Registering root state in app.module.ts
    @NgModule({
      imports: [
        StoreModule.forRoot({ game: scoreboardReducer })
      ],
    })
### Registering root state using a standalone API in main.ts
    bootstrapApplication(AppComponent, {
      providers: [
        provideStore(),
        provideState({ name: 'game', reducer: scoreboardReducer })
      ],
    });

### Registering feature state in app.module.ts
    feature states register additional keys and values in that object.
    @NgModule({
      imports: [
        StoreModule.forRoot({})
      ],
    })

### Registering feature state using a standalone API in main.ts
    bootstrapApplication(AppComponent, {
      providers: [
        provideStore()
      ],
    });

    This registers your application with an empty object for the root state:
    {}

    Now in scoreboard.module.ts
    import { scoreboardFeatureKey, scoreboardReducer } from './reducers/scoreboard.reducer';
  
    @NgModule({
      imports: [
        StoreModule.forFeature(scoreboardFeatureKey, scoreboardReducer)
      ],
    })
    export class ScoreboardModule {}

    Or Using the Standalone API in the route config game-routes.ts
    import { scoreboardFeatureKey, scoreboardReducer } from './reducers/scoreboard.reducer';
 
    export const routes: Route[] = [
      {
        path: 'scoreboard',
        providers: [
          provideState({ name: scoreboardFeatureKey, reducer: scoreboardReducer })
        ]
      }
    ];

    Add the ScoreboardModule to the AppModule to load the state eagerly in app.module.ts.
    @NgModule({
      imports: [
        StoreModule.forRoot({}),
        ScoreboardModule
      ],
    })

    Or Using the Standalone API, register the feature state on application bootstrap in main.ts:
    bootstrapApplication(AppComponent, {
      providers: [
        provideStore({ [scoreboardFeatureKey]: scoreboardReducer }),
      ]
    });

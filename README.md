# Angular2Routing

## Basic Things to consider

1.  Each feature area resides in its own folder.
2.  Each feature has its own Angular feature module.
3.  Each area has its own area root component.
4.  Each area root component has its own router outlet and child routes.
5.  Feature area routes rarely (if ever) cross with routes of other features.

## make the service call on load of the component.

#### The ActivatedRoute.params property is an Observable of route parameters. The params emits new id values when the user navigates to the component. In ngOnInit you subscribe to those values, set the selectedId, and get the heroes.

```
import { Router, ActivatedRoute, Params } from '@angular/router';
import 'rxjs/add/operator/switchMap';
import { Observable } from 'rxjs/Observable';

export class HeroListComponent implements OnInit {
  heroes: Observable<Hero[]>;

  private selectedId: number;

  constructor(
    private service: HeroService,
    private route: ActivatedRoute,
    private router: Router
  ) {}

  ngOnInit() {
    this.heroes = this.route.params
      .switchMap((params: Params) => {
        this.selectedId = +params['id'];
        return this.service.getHeroes();
      });
  }
}
```


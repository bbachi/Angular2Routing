# Angular2Routing

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

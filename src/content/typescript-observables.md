# Types in your observables

- `Observable<T>` value is a generic type `T`
- `T` can be anything you want
- It helps you with compile errors
- Forces you return a known object
- Easy to develop since you know what to expect

---

# RxJS Generic Arguments

- The [operators](https://github.com/ReactiveX/rxjs/tree/master/src/operator) page is one of the best sources of available generic arguments
- Use Typescript interfaces for everything

```ts
interface ICat {
  name: string;
  age: number;
  purr: () => void;
}

const myCat$ = Observable.of<ICat>({
  name: 'Midnight',
  age: 8,
});
// this ^ fails with:
// Type '{ name: string; age: number; }' is not assignable to type 'ICat'.
```

---

## Redux Side-effect handler example 

- A side-effect handler in Redux could look like:

```ts
interface Action { type: string; }
interface PayloadAction extends Action { payload: any;} 

const myAction$ = Observable.of({ type: 'MY_ACTION' });

myAction$.mergeMap<Action, PayloadAction>(() => {
  return Observable.ajax('http://get.some.json')
    .map<any, PayloadAction>(result => ({
      type: 'MY_PAYLOAD_ACTION',
      payload: result,
    }))
    .catch<any, PayloadAction>(err => Observable.of({
      type: 'MY_ERROR_ACTION',
      payload: err,
    }));
});
```

---
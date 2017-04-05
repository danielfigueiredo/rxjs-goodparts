# Types in your observables

---

## Advantages of having types

- It helps you with compile errors
- Forces you return a known object
- Easy to develop since you know what to expect

---

## Generic parameters

- `Observable<T>` value is a generic type `T`
- `T` can be anything you want
- Each operator has its own parameter

---

## Where can I find the available parameters?

- The [operators](https://github.com/ReactiveX/rxjs/tree/master/src/operator) page is one of the best sources of available generic arguments

---

## Generic Arguments

- Making sure you have an observable that returns a known type
- Provide the arguments when generating the observable

---

- It fails! Ops, I'm not a Cat

```ts
interface ICat { name: string; age: number; purr: () => void; }

const myCat$ = Observable.of<ICat>({ name: 'Midnight', age: 8 });
// this ^ fails with:
// Type '{ name: string; age: number; }' is not assignable to type 'ICat'.
```

---

## Making things slightly more complicated

- Combining, transforming, and merging

---

## How to provide arguments to a `map` operation?

---

### Map has two generic parameters:

- The type of the observable you are receiving
- The type of the observable your are returning

---

## Mapping from Cat to Dog

- Provide the generic arguments

```ts
interface IDog { name: string; age: number; bark: () => string; }
interface ICat { name: string; age: number; purr: () => void; }

Observable.ajax('http://get-some-cat.json')
  .map<ICat, IDog>(myCat => ({
    name: myCat.name,
    age: myCat.age,
    bark: () => '!!!',
  }));

```


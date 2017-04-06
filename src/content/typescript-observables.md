## Types in your observables

---

## Advantages of having types

- It helps you with compile errors
- Forces you return a known object
- Easy to develop since you know what to expect

---

## Generic parameters

- `Observable` has a generic parameter `<T>`
- `T` can be anything you want
- Each operator also has its own parameter(s)

---

## Generic Arguments

- Providing the generic arguments makes your Observable be typed


---

- It fails! Ops, I'm not a Cat

```ts
interface ICat { name: string; age: number; purr: () => void; }

const myCat$ = Observable.of<ICat>({ name: 'Midnight', age: 8 });
// this ^ fails with:
// Type '{ name: string; age: number; }' is not assignable to type 'ICat'.
```

---

## Making things more complicated

- Observables can be combined, transformed, and merged
- Some operators changes the type from X to Y

---

## How to provide arguments to a `map` operation?

---

### Map has two generic parameters:

- The type of the observable you are receiving
- The type of the observable your are returning

---

## Mapping from Cat to Dog

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


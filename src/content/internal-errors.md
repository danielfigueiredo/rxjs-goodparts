# Internal RxJS Errors

---

## RxJS errors used to be vague and cryptic (5.0.0-beta.6)


```ts
  Rx.Observable.from(['anteater', 'bear', 'cheetah', 'donkey', 'tester'])
    .take(4)
    .map(() => 'item')
    .flatMap(term => {})
    .subscribe((result) => {
      this.result = result.artists.items
    });
```

- `TypeError: Cannot read property 'Symbol(Symbol.iterator)' of undefined`

---

## RxJS errors have come a long way since then (5.2.0)

```ts 
  Rx.Observable.from(['anteater', 'bear', 'cheetah', 'donkey', 'tester'])
    .take(4)
    .map(() => 'item')
    .flatMap(term => {})
    .subscribe((result) => {
      this.result = result.artists.items
    });
```
- `Uncaught TypeError: You provided 'undefined' where a stream was expected. You can provide an Observable, Promise, Array, or Iterable.`

---

## RxJS 5 Github Issues

- Even looking through the issues on Github (https://github.com/ReactiveX/rxjs/issues)...
the only issue regarding vague error messages (https://github.com/ReactiveX/rxjs/issues/2151) is already solved


---

## The most vague errors these days is...

```ts
this.searchField = new Control();
  this.searchField.valueChanges
    .debounceTime(400)
    .flatMap(term => this.searchService.search(term))
    .subscribe((result) => {
      this.result = result.artists.items
    });
```

- `this.searchField.valueChanges.debounceTime is not a function`

---

## My professional opinion?

- Make sure you're using the latest version of RxJS.
- Also... great job to the RxJS community for adding such great error handling.

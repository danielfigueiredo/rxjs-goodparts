# Common Operators

---

## Creating observables

- `Observable.of(a, b, c)` pass multi-arguments to create
- `Observable.from([a, b, c])` pass iterable (ex. array) to create

---

## Common array like operators

- `filter()` only values that pass comparison carry on
- `map()` allows to map values into different ones
- `reduce()` normal reduce, only emits on complete
- `take()` good if you only want to take X events and then ditch it

---

## Useful for browser events!

- `debounce()` waits X amount of time till last one finishes before continuing
- `throttle()` waits X amount of time between calls

---

## Useful for combining observables

- `switchMap()` cancels all non finished calls and carries on with current one
- `mergeMap()` returns a new observable that will be used henceforth
- `zip()` outputs continuously matching streams
- `combineLatest()` whenever a change happens, take latest from all and continue on

---

## Useful utilities

- `toArray()` waits until array is done and combines into 1 array
- `share()` allows you to say at this point, whenever subscribers go from 0 to 1, use what last evaluation was

---

## In case of errors

- `retry()` will retry until no errors occur, or retry a bunch of times

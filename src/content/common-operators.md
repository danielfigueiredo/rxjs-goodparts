# Common Operators

---

## Creating observables

- `Observable.of(a, b, c)` pass multi-arguments to create
- `Observable.from([a, b, c])` pass iterable (ex. array) to create

---

## Array like operators

- `filter()` only values that pass comparison carry on
- `map()` allows to map values into different ones
- `reduce()` normal reduce, only emits on complete
- `scan()` basically a reduce, except does onNext values
- `pluck()` allows to take a prop off and continue on with it, multi args for nested
- `take()` good if you only want to take 1 and then ditch it, take(1) is good for http requests to make sure they finish
- `do()` anything performed in here won't effect your obserable (good for debugging)

---

## Useful for events

- `debounce()` waits X amount of time till last one finishes before continuing.  If kept typing would not call
- `throttle()` waits X amount of time between calls, if kept typing, would call every X amount of time

---

## Useful for combining observables

- `switchMap()` cancels all previously non finished calls through the stream, and carries on with current one
- `mergeMap()` returns a new observable that the current observable will continue on with
- `zip()` outputs continuously matching streams (will keep going to end if all inputs have outputs
- `combineLatest()` whenever a change happens in any input args, take latest from all and continue on
- `withLastestFrom()` whenever an event is fired, take the latest values from the streams in the input args

---

## Useful utils

- `toArray()` waits until array is done and combines into 1 array
- `share()` allows you to say at this point, whenever subscribers go from 0 to 1, use what last evaluation was

---

## In case of errors

- `retry()` will retry until no errors occur, or retry a bunch of times

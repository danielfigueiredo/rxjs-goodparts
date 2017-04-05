# Performance and RxJS

---

## JS Array operators vs RxJS operators

---

## The test setup

```ts
const inputData = Array(1000000).fill(1).map(() => Math.floor(Math.random() * 10000));

function test(label, testFn, input) {
  const start = Date.now();
  const result = testFn(input);
  const end = Date.now();
  const seconds = parseFloat((end - start) / 1000).toFixed(2);
  console.log(`${label} took ${seconds}s and had result of ${result}`);
}

test('Array', testArray, inputData);
test('RxJS', testRx, inputData);
```

---

## Array

```ts
function testArray(input) {
  return input
    .filter((el) => el % 2 === 0)
    .map((el) => el * 5)
    .reduce((total, next) => total + next, 0);
}
```

---

## RxJS

```ts
function testRx(input) {
  let value;

  Rx.Observable.from(input)
    .filter((el) => el % 2 === 0)
    .map((el) => el * 5)
    .reduce((total, next) => total + next, 0)
    .subscribe((result) => { value = result; });

  return value;
}
```

---

## Results

- `Array took 0.14s and had result of 12498033630`
- `RxJS took 0.08s and had result of 12498033630`

---

# Why?

---

## RxJS works like a funnel

- Each element goes through all operators
- Array function iterates the whole array every time

---

<div style="text-align: center; height: 500px;">
 <img src="content/images/rxjs-diagram.jpg" alt="What is RxJS?" title="RxJS Diagram">
</div>

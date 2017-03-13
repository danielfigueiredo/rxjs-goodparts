# Speed of RxJS

---

## The test setup

```ts
const inputData = Array(1000000).fill(1).map(() => Math.floor(Math.random() * 10000));

test('Array', testArray, inputData);
test('RxJS', testRx, inputData);

function test(label, testFn, input) {
  const start = Date.now();
  const result = testFn(input);
  const end = Date.now();
  const seconds = parseFloat((end - start) / 1000).toFixed(2);

  console.log(`${label} took ${seconds}s and had result of ${result}`);
}
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
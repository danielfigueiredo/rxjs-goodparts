## Wait! What if an error happens?

---

<div style="text-align: center;">
  <img src="content/images/ohnoes.jpg" alt="Oh noes" title="Oh noes">
</div>

---

## Errors go through the onError channel

---

## They halt the sequence

---

## There are two levels of errors: class and instance

---

## Class level errors

- Swallowing errors

---

## Try remotes or use cached version

```ts
const source$ = Observable.catch(
  Observable.ajax.get('http://stream1'),
  Observable.ajax.get('http://stream2'),
  Observable.from(local.get('default')
);
```

- If one of the gets are successful, then nothing else happens
- It only moves to the next attempt if an error happens

---

## Ignoring errors

- Execute series of independent events no matter what
- `onErrorResumeNext` operator
- Takes in any number of Observables to be executed

---

- Data will be whatever is emitted from each Observable
- Result of function1, function2, etc.

```ts
const source$ = Observable.onErrorResumeNext(
  Utils.myFunction1(),
  Utils.myFunction2(),
  Utils...
);
const log = source.subscribe(data => console.log(data));
```

---

## Instance level errors

- Deals with errors from a specific Observable
- `catch` function callback
- Callback should return an Observable

---

- On error the source emits the observable returned from `catch`
- In this case an object that contains the error with a message

```ts 
const url = 'http://myresource.com';
const source$ = Observable.ajax.get(url);
  .catch(err => Observable.from({ err, errMsg: 'My error description' }));
```

---

## Finally reminder!

- Like regular try catches, you can use `finally`
- `finally` vs `complete` callback
- Runs after completed, regardless the output
- Common use case: clean up resources

---

- Let's say `getData` keeps firing until all data is read
- `socket` will be closed even if an error happens

```ts
const socket = SocketUtil.getSocket();
DbUtils.getData()
  .subscribe(data => socket.send(data))
  .catch(err => log(err)
  .finally(() => socket.close();
```


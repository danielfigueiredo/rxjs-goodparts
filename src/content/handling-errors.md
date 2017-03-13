# Handling errors with RxJS

- Errors goes through the onError channel
- They halt the sequence
- There are two levels of errors: class and instance
- Obvious options: ignore errors or deal with them

---

## Class level errors

- Swallowing errors
- Example: Try remotes or use cached version

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

## Instance level errors

- Deals with errors from a specific Observable
- `catch` function callback

```ts 
const url = 'http://myresource.com';
const source$ = Observable.ajax.get(url);
  .catch(err => {
    // do something and return an Observable
    return Observable.from({
      err,
      errMsg: 'My error description'
    });
  });
```
- On error the source emits the observable returned from `catch`
- In this case an object that contains the error with a message

---

## Ignoring errors

- Execute series of independent events no matter what
- `onErrorResumeNext`: ignore errors and continue
- Let's say functions from utils returns observables

```ts
const source$ = Observable.onErrorResumeNext(
  Utils.myFunction1(),
  Utils.myFunction2(),
  Utils...
);
const log = source.subscribe(
  data => console.log(data)
);
```

- Data will be whatever is emitted from each Observable 

---

## Delaying errors with multiple sources

- Leaving errors to the end
- Flattens sequences without being interrupted by one erroneous source

```ts
const source$ = Observable.mergeDelayError(
  Utils.myFunction1(), // logs 'Function1'
  Utils.myFunction2(), // throws Error('boom!')
  Utils.myFunction3()  // logs 'Function2'
);
source$.subscribe(() => {
  x => console.log('Emits: ', x),
  err => console.log('Error: ', err)
});
```

- This would print 'Emits: Function1', 'Emits: Function1', 'Error: boom!'

---

## Finally reminder!

- `finally` to runs after the observable is completed
- `finally` vs `complete` callback
- Usage example: clean up resources
- Let's say `getData` keeps firing until all data is read: 

```ts
const socket = SocketUtil.getSocket();
DbUtils.getData()
  .subscribe(data => socket.send(data))
  .catch(err => log(err)
  .finally(() => socket.close();
```

- `socket` will be close after observable is completed


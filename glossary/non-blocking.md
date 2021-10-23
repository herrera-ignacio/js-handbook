# [Blocking vs Non-Blocking](https://nodejs.org/en/docs/guides/blocking-vs-non-blocking/)

* Blocking
* Non-Blocking
* Blocking vs Non-Blocking example
* Dangers of Mixing Blocking and Non-Blocking Code

## Blocking

**Blocking** is when the execution of additional JavaScript in the Node.js (Event Loop) process must wait until
a non-JavaScript operation completes. Thus, blocking methods execute **synchronously**

> In Node.js, JavaScript that exhibits poor performance due to being CPU intensive rather than waiting on a non-JavaScript
> operation, such as I/O, isn't typically referred to as _blocking_.

Synchronous methods in the Node.js standard library that use _libuv_ are the most commonly used _blocking_ operations.
_Native modules_ may also have blocking methods.

Using the File System module as an example, this is a _synchronous_ file read:

```javascript
const fs = require('fs');
const data = fs.readFileSync('/file.md'); // blocks here until file is read
```

## Non-Blocking

All the I/O methods in the Node.js standard library provide **asynchronous versions**, which are **non-blocking**,
and accept callback functions.

Using the previous example from File System module, here's an equivalent _asynchronous_ file read:

```javascript
const fs = require('fs');
fs.readFile('/file.md', (err, data) => {
  if (err) throw err;
});
```

The _synchronous_ example may appear simpler than the _asyonchronous_ one but has the disadvantage of _blocking_ the
execution of any additional JavaScript until the entire file is read. Note that in the _synchronous_ version if an error
is thrown it will need to be caught or the process will crash. In the _asynchronous_ it is up to the author to decide
whether an error should throw or not.

## Blocking vs Non-Blocking Example

Consider the following example:

```javascript
const fs = require('fs');
const data = fs.readFileSync('/file.md'); // blocks here until file is read
console.log(data);
moreWork(); // will run after console.log
```

And here is a similar, but not equivalent asynchronous example:

```javascript
const fs = require('fs');
fs.readFile('/file.md', (err, data) => {
  if (err) throw err;
  console.log(data);
});
moreWork(); // will run before console.log
```

In this last example, `fs.readFile()` is **non-blocking** so JavaScript execution can continue and `moreWork()` will be
called without waiting for the file read to complete. This is a **key design choice that allows for higher throughput**.

## Dangers of Mixing Blocking and Non-Blocking Code

There are some patterns that **should be avoided when dealing with I/O**. Consider the following example:

```javascript
const fs = require('fs');
fs.readFile('/file.md', (err, data) => {
	if (err) throw werr;
	console.log(data);
});
fs.unlinkSync('/file.md');
```

In the above example, `fs.unlinkSync()` is likely to be run before `fs.readFile()`,
which would delete `file.md` before it actually read.

A better way to write this, which is completely **non-blocking** and guaranteed to execute in the correct order is:

```javascript
const fs = require('fs');
fs.readFile('/file.md', (readFileErr, data) => {
  if (readFileErr) throw readFileErr;
  console.log(data);
  fs.unlink('/file.md', (unlinkErr) => {
    if (unlinkErr) throw unlinkErr;
  });
});
```

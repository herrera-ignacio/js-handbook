# Concurrency and Throughput

## Overview

**JavaScript's execution** in Node.js is **single threaded**, so _concurrency_ refers to the Event Loop's
capacity to execute JavaScript callback functions after completing other work.

Any code that is expected to run in a concurrent manner must allow the Event Loop to continue running
as non-JavaScript operations, like I/O, are occurring.

> The Event Loop is different from models in many other languages where additional threads may be created to handle
> concurrent work.

## Example

As an example, let's consider a case where each request to a web server takes 50ms to complete,
and 45ms of that 50ms is database I/O that can be done asynchronously.

Choosing _non-blocking_ asynchronous operations frees up that 45ms per request to handle other requests.
This is a significant difference in capacity just by choosing to use _non-blocking_ methods instead of _blocking_ methods.

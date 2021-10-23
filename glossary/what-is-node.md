# What is Node.js?

Node.js is a **asynchronous event-driven** _JavaScript Runtime_ built on top of Chrome's [V8](https://v8.dev/) JavaScript and WebAssembly Engine,
written in C++. It implements _ECMAScript_ and _WebAssembly_. V8 can run standalone, or can be embedded into any
C++ application.

* Asynchronous
* Event Driven Architecture
* Multi-threading & Multi-processing

## Asynchronous

> V8 uses [libuv](https://libuv.org) for asynchronous I/O.

Many connections can be handled _concurrently_. In contrast to toda's more common concurrency model, in which OS threads are employed,
Javascript uses _callbacks_.

> Thread-based networking is relatively inefficient and very difficult to use.

Furthermore, users of Node.js are free from worries of dead-locking the process, since there are no locks.

Almost no function in Node.js directly performs I/O, so the process never blocks excepts when the I/O is performed using
synchronous methods of Node.js standard library.

> Because nothing blocks, scalable systems are very reasonable to develop in Node.js.

## Event Driven Architecture

The _Event Model_ in Node relies on _listeners_ to listen for events and _emitters_ to emit events periodically.

> Event-driven architectures are build on the **publish-susbscribe** or **observer** pattern.

_Events_ are actions or occurrences that happen, which the system tells you about so you can respond to them in some way
if desired.

> Node makes use of functions like `on()` to register an event listener, and `once()` to register an event listener that unregisters after it
> has run once.

Whenever we have a listener that runs when an event fires, we say we are **registering an event handler/listener**.
The listener listens out for the event happening, and the handler is the code that is run in response to it happening.

> Web events are not part of the core JavaScript specification, they are defined as part of the APIs built into the browsers.

## Multi-threading & Multi-processing

Node.js being designed without threads doesn't mean you can't take advantage of multiple cores in your environment.

Child processes can be spawned using [Child processes API](https://nodejs.org/dist/latest-v14.x/docs/api/child_process.html).
They are built upon the same interface as the [Cluster module](https://nodejs.org/dist/latest-v14.x/docs/api/cluster.html),
which allows you to share sockets between processes to enable load balancing over your cores.

You can as well handle threads with [Worker threads API](https://nodejs.org/dist/latest-v14.x/docs/api/worker_threads.html)

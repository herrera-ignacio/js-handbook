# Callback Pattern

A _callback_ is a function called at the completion of a given task; this prevents any blocking,
and allows other code to be run in the meantime.

> Node.js, being an asynchronous platform, doesn't wait around for things like file I/O to finish.
> Callbacks are the foundation of Node.js, they give you an _interface_ with which to say, _"and when
> you're done doing that, do all this."_.

Callbacks allow you to have as many IO operations as your OS han handle happening at the same time.
They give you the ability to be able to continue working and not just sit still and wait until
the blocking operations come back.

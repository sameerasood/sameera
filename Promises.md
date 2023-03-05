# Promises
## Await Async explanation 

Computers are designed to run many programs at together ("concurrently").
When we look inside Task Manager (Windows) or Activity Monitor (MacOS) we can see many programs that are active together.
However, when we are taught to write programs we are shown how to write them sequentially. We imagine there is a single "thread of execution" that steps sequentially through the code executing the instructions one-by-one. And this is something of a paradox - the computer is capable of running thousands of programs concurrently but our sequential code can't make any use of that fact!

So there has been a concerted attempt to support multiple threads of execution in modern programming languages. The challenge has been to get the benefit of concurrency without getting in a hopeless mess of deadlocks, races, and memory corruption. And it has taken quite a few attempts to find a mechanism that works well.
Javascript has settled on an event-based model, so that execution is triggered by the arrival of an event. So instead of there being a single-long running thread of execution, there is a sequence of much shorter threads of execution that each handle a single event.
What actually is an event? It's a small packet of information about something that has happened. And, we can set listeners for events, which are just functions that are run when an event of the right type happens.

**What adds an event to the queue?**
Normally the web browser does, it's not something that happens inside Javascript. However you can add an event using setTimeout.
But Promises are a neat way of organising events and listeners that simplifies our code. The idea is that a promise wraps code that will generate an event into an object. You can then attach listeners to that object using .then().  And the whole idea is that when promises 'resolve' the listeners are then invoked.

However, although promises and .then() do make code a bit neater, it's still pretty messy. And the reason is that once a Javascript function runs, it continues running without interruption, until it finishes. And that is why it is not possible for an ordinary Javascript function to wait until a promise resolves - because nothing else can happen while it is waiting!

What coders wanted was the ability for a function to suspend its execution midway through and resume it at a later date. In other languages, this kind of function is called a coroutine. So Javascript programmers had coroutine envy.

**This is where async functions come in.**
This introduces something that looks like a function and works like a coroutine. Because coroutines can suspend their execution, it is possible for them to await the resolution of a promise. When the promise resolves, the coroutine is resumed from where it left off.

**The effect is that instead of writing a .then() chain with a bunch of arrow functions**, all you need to do is write a series of awaits, which looks a lot more natural.

Note that an ordinary Javascript function cannot use await because it cannot be suspended. The best it can do is run an async function and get back a promise, which will resolve when the async function finishes. It is possible to attach a .then() listener to it though.

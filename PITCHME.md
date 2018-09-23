# Coroutines, Promises and Event Loops, Oh My! Getting Asynchronous with PHP

Simon Frost

Senior Backend Magento Engineer, Magium Commerce

@ProcessEight

http://github.com/ProcessEight

---

# About me

Senior Backend Magento Engineer, Magium Commerce

2x Magento Certified

Working with PHP for ten years, Magento for six

@ProcessEight

http://github.com/ProcessEight

---

## Flow of Execution: The synchronous model

In synchronous programming:

@ul

* We issue a statement,
* We wait for it to complete...
* ..and then move on to the next statement.

@ulend

Therefore, the order of execution is predictable

---

## Flow of Execution: The asynchronous model

In asynchronous programming

@ul

* We issue a statement
* While we are waiting for it to complete, we can perform other tasks
* When it has finished, we run a callback function

@ulend

This does mean the order of execution is not predictable

---

## 'Calculations are fast, input/output is slow.'

So why wait? Asynchronous programming allows us to move onto something else (i.e. Continue the flow of execution) whilst waiting for I/O

---

## What it is (Asynchronous), What it isn't (parallel execution/multi-threaded)

@ul

* Asynchronous programming allows us to continue execution whilst waiting for operations to complete
* Parallel execution/multi-threading means two or more operations can be processed at the same time

@ulend

Note:
- PHP runs in a single thread, so there is no parallel execution. 
- In the asynchronous model, tasks are not being run in parallel, instead, each task is being executed bit by bit, little by little.
- It may look like things run in parallel because the program continuously switches between different parts of tasks and processes them.
- Disadvantages of threads (See Learning Event-Driven PHP ebook p14)

---

## Why use PHP?

@ul

- PHP _can_ be used to build asynchronous applications 

- You don't need to learn a whole new language and ecosystem

- No magic or special extensions required - this is the same PHP you're already using

- Need to re-tool your whole stack and deployment framework for the new languages

@ulend

---

## Approaches to Async programming in PHP

@ul

* AmPHP
    * Pros: Mature, well documented, uses co-routines
    * Cons: Requires extension

* ReactPHP
    * Pros: Mature, active project, no PHP extensions needed
    * Cons: Limited feature set, no co-routines

@ulend

---

## Paradigm shift

Async programming gives us a different set of tools to work with

We need to adopt a different way of thinking about how we design programs

---

## The event-driven approach

@ul

Event-driven programming implements the Reactor Pattern

It represents an application flow control that is determined by events or changes in state.

Therefore you cannot say exactly when anything in your program is going to happen.

@ulend

---

@ul

Subscribe to events (callbacks)

React to events

Rinse, repeat

@ulend

---

## Blocking vs. Non-blocking

I/O is blocking. The program waits until the I/O operation has finished.

Therefore we must avoid I/O at all costs.

---

## Co-routines

Co-routines are interruptible (or pausable) functions. The main difference between Co-routines and plain Generators is that data or exceptions can be 'sent' into the Co-routine, whereas a simple Generator can only produce output.

---

## Promises

@ul

- A Promise is a temporary placeholder used as a result whenever the result is not immediately available.

- Once the result is ready, an event is emitted, which can be subscribed to and acted upon.

@ulend

---

## Events / Event Loop

@ul

- The event loop is used to subscribe to events and then act on them once they are dispatched.

- The loop continues running until no more events are dispatched (i.e. There is nothing more to do). 

@ulend

---

## How to solve common problems in Magento using async techniques:

---

## Bulk operations, e.g. Image processing

---

## Indexing

---

## Bulk saves/deletes

---

## Data import/export?

How does this differ from Async Bulk API community project?

---

## The integration (the 2 million prices):

---

Explain business case: The different price-affecting criteria, any other relevant details

---

Explain the basic architecture of the solution

---

Briefly cover which tools, libraries, frameworks were used. Keep it vague/brief. It is not important to go into detail.

ReactPHP
RecoilPHP

---

Side by side demos (not live) of sync solution and async solution, demonstrating how long it takes to import an API response.
Remember, there's no 'magic' here - this is plain PHP, no extensions needed, just used asynchronously

---

Link to demo implementation or smaller demos which demo each concept (proof of concept apps) in GitHub

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

## What it is (Asynchronous), What it isn't (multi-threaded)

Disadvantages of threads (See Learning Event-Driven PHP ebook p14)

---

## Why not use NodeJS or Go?

Need to re-tool your whole stack and deployment framework for the new languages

Need to learn a whole new language and language ecosystem

---

## Flow of Execution: The synchronous model

Programs are executed top-to-bottom

The order of execution is predictable

---

## Flow of Execution: The asynchronous model

Subscribe to events

React to events

Rinse, repeat

The order of execution is not predictable

---

## 'calculations are fast, input/output is slow.'

So why wait? Async allows us to move onto something else (i.e. Continue the flow of execution) whilst waiting for I/O

---

## Approaches to Async programming in PHP

* AmPHP
    * Pros: Mature, well documented, uses co-routines
    * Cons: Requires extension

* ReactPHP
    * Pros: Mature, active project, no PHP extensions needed
    * Cons: Limited feature set, no co-routines

---

## Paradigm shift

Async programming gives us a different set of tools to work with

We need to adopt a different way of thinking about how we design programs

---

## Blocking vs. Non-blocking

I/O is blocking. The program waits until the I/O operation has finished.

Therefore we must avoid I/O at all costs.

---

## Coroutines

Coroutines are interruptible (or pausable) functions. They are implemented in PHP using Generators and the yield keyword. The main difference between Coroutines and plain Generators is that data or exceptions can be 'sent' into the Coroutine, whereas a simple Generator can only produce output.

---

## Promises

A Promise is a temporary placeholder used as a result whenever the result is not immediately available.

Once the result is available, then an event is emitted, which code can listen to act upon.

---

## Events / Event Loop

In event-driven programming, the event loop is used to subscribe to events and then act on them once they are dispatched.

The loop continues running until no more events are dispatched (i.e. There is nothing to do). 

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

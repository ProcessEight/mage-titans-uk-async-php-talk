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

In synchronous programming:

@ul

* We issue a statement,
* We wait for it to complete...
* ..and then move on to the next statement.

@ulend

Note:
- Let's kick off with what we already know
- Therefore, the order of execution is predictable

---

In asynchronous programming:

@ul

* We issue a statement
* While we are waiting for it to complete, we can perform other tasks
* When it has finished, we run a callback function

@ulend

Note:
This does mean the order of execution is not predictable

---

## Calculations are fast.

## Input/output is slow.

Note:
Async programming takes advantage of this idea
CPU cycles are measured in nanoseconds, whereas I/O cycles are measured in milliseconds

---

## Asynchronous != parallel 

## or multi-threaded 

Note:
- PHP runs in a single thread, so there is no parallel execution. 
- In the asynchronous model, tasks are not being run in parallel, instead, each task is being executed bit by bit, little by little.
- It may look like things run in parallel because the program continuously switches between different parts of tasks and processes them.
- Asynchronous programming allows us to continue execution whilst waiting for operations to complete
- Parallel execution/multi-threading means two or more operations can be processed at the same time
- Disadvantages of threads (See Learning Event-Driven PHP ebook p14)

---

- Async programming gives us a different set of tools to work with

@ul

- We need to adopt a different way of thinking about how we design programs

@ulend

Note:
- e.g. Avoiding blocking (I/O) operations

---

## Why use PHP?

@ul

- You don't need to learn a whole new language and ecosystem

- No magic or special extensions required - this is the same PHP you're already using

- No need to re-tool your whole stack and deployment framework

@ulend

Note:
- Use what you are already using (i.e. PHP, stack, deployment)

---

## Approaches to Async programming in PHP

@ul

* AmPHP
    * Pros: Mature, well documented
    * Cons: Requires extension

* ReactPHP
    * Pros: Mature, active project, no PHP extensions needed
    * Cons: Limited feature set

@ulend

Note:
- Whilst there were a lot of libraries to implement async in PHP, these two are now the most up-to-date and frequently maintained

---

## Asynchronous programming concepts

---

## Blocking vs. Non-blocking

I/O is blocking. The program waits until the I/O operation has finished.

Therefore we must avoid I/O at all costs.

Note:
- Avoid blocking by using promises
- Or by forking the process using `exec`

---

## Promises

@ul

- A Promise is a temporary placeholder used as a result whenever the result is not immediately available.

- Once the result is ready, an event is emitted, which can be subscribed to and acted upon.

- Promises are a way of managing callbacks and avoiding 'callback hell'

@ulend

Note:
- Instead of having multiple nested callbacks, Promises can only ever be one level deep
- They are still executed asynchronously

---

## Co-routines

@ul

- Co-routines are interruptible (or pausable) functions. 

- They can be used to wrap promises, so that code which calls co-routines can be written in a synchronous fashion

@ulend

---

## Event Loop

@ul

- The event loop is used to subscribe to events and then act on them once they are dispatched.

- The loop continues running until no more events are dispatched (i.e. There is nothing more to do). 

@ulend

---

## The event-driven approach

@ul

* Event-driven programming implements the Reactor Pattern

* It represents an application flow control that is determined by events or changes in state.

* Therefore you cannot say exactly when anything in your program is going to happen.

@ulend

---

## How to solve common problems in Magento using async techniques

---

## Bulk image processing

---

## Bulk saves/deletes

---

## Data import/export?

Note:
- How does this differ from Async Bulk API community project?

---

## The integration 

---

## The problem

Price-affecting criteria:

* Base price
* Tier price
* Customer Group
* Product Group

Note:
- Explain business case: The different price-affecting criteria, any other relevant details

---

## The approach

Split the process into four stages:

@ul

- Query API

- Validate response

- Calculate prices according to clients' business logic

- Save prices

@ulend

Note:
Explain the basic architecture of the solution

---

## The tools used

* ReactPHP Components:
    * EventLoop
    * Promise
    * Stream
    * ChildProcess 
* RecoilPHP

Note:
Briefly cover which tools, libraries, frameworks were used. 
Keep it brief. 
It is not important to go into detail at this point

---

Side by side demos (not live) of sync solution and async solution, demonstrating how long it takes to import an API response, both syncly and asyncly. 

Note:
- Remember, there's no 'magic' here - this is plain PHP, no extensions needed
- We're just using it asynchronously

---

Link to demo implementation or smaller demos which demo each concept (proof of concept apps) in GitHub

---

## Thank you!

`<?= $questions ?? exit(0); ?>`

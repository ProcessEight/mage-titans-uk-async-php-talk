## Coroutines, Promises and Event Loops, Oh My! Getting Asynchronous with PHP

Simon Frost

---

# About me

Senior Backend Magento Engineer, Magium Commerce

2x Magento Certified

@ProcessEight

http://github.com/ProcessEight

Note:
Working with PHP for ten years, Magento for six

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

## Programming Asynchronously

@ul

- Async programming gives us a different set of tools to work with

- We need to adopt a different way of thinking about how we design programs

@ulend

Note:
- e.g. Avoiding blocking (I/O) operations

---

## Core concepts

Note:
- These concepts are the tools we can use to build async programs

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

- They can be used to wrap promises, so that code which calls co-routines can be written in a more synchronous fashion

@ulend

---

## Event Loop

@ul

- The event loop is used to subscribe to events and then act on them once they are dispatched.

- The loop continues running until no more events are dispatched (i.e. There is nothing more to do). 

@ulend

---

## Blocking vs. Non-blocking

- A 'blocking' operation is one which blocks program execution.

- E.g. I/O is blocking. The program has to wait until the I/O operation has finished.

- Therefore we must avoid blocking operations where possible.

- Unavoidable 'blocking' operations, like file system access, can be wrapped in a Promise, or forked into a new child process which continues in the background 

Note:
- Avoid blocking by using promises
- Or by forking the process using `exec`

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

## The event-driven approach

@ul

* Event-driven programming implements the Reactor Pattern

* It represents an application flow control that is determined by events or changes in state.

* Therefore you cannot say exactly when anything in your program is going to happen.

* Both AmPHP and ReactPHP implement the Reactor Pattern

@ulend

---

### The 'Hello World' of asynchronous PHP

---

```php
// Create the event loop
$loop = React\EventLoop\Factory::create();

// Create a new web server which will dispatch the following response 
// for every request it receives
$server = new React\Http\Server(function (Psr\Http\Message\ServerRequestInterface $request) {
    // Our generic response
    return new React\Http\Response(
        200,
        array('Content-Type' => 'text/plain'),
        "Hello World!\n"
    );
});

// Start a new server listening on port 8080
$socket = new React\Socket\Server(8080, $loop);
$server->listen($socket);

echo "Server running at http://127.0.0.1:8080\n";

// Start the loop; Run the program
$loop->run();
```
@[01-02]
@[04-06]
@[7-12]
@[15-17]
@[21-23]
---

```bash
# Start the server in one window
$ php -f react-hello-world-server.php
Server running at http://127.0.0.1:8080
```
@[02]
@[03]

---

```bash
# Send a request to it in another
$ curl http://127.0.0.1:8080
Hello World!
```
@[02]
@[03]

---

## Novel ways to use async techniques in Magento

---

## Bulk image processing

@ul

* The sync way:
    * Process images in sequence. Finish one before starting another.

* The async way:
    * Fork a new process for each image resize or upload operation.

@ulend

Note:
- Forking processes is recommended when working with the filesystem in async programs, because of blocking issues
- Fork the process so it runs in the background
- Using the ChildProcess React component

---

## Bulk database CRUD operations 

@ul

* The sync way:
    * Load the whole resultset into memory, then process it

* The async way
    * Load each row of the result into memory one at a time, then process it
 
```php
$stream = $connection->queryStream('SELECT * FROM user');
$stream->on('data', function ($row) {
    echo $row['name'] . PHP_EOL;
});
$stream->on('end', function () {
    echo 'Completed.';
});
```

@ulend

Note:
- The `react/mysql` library was used here

---

## Data import/export

@ul

* The sync way:
    * Load the whole file/dataset into memory, then start processing it 

* The async way:
    * Use the `ReactPHP Stream` component to read and write large files/datasets asynchronously, i.e. One chunk at a time

@ulend

Note:
- How does this differ from Async Bulk API community project?

---

## Integrating Async PHP with Magento

---

## The 'microservice' approach

@ul

* All the async code is located outside Magento
* The microservice communicates with Magento via the API

@ulend

Note:
- More of an all-or-nothing approach

---

## The 'isolation' approach

@ul

* Async code is only used in isolated locations


@ulend

Note:
- Not all to take advantage of all async advantages
- A compromise

---

## Summary

@ul

- Using asynchronous programming libraries like ReactPHP, we can drastically cut down on the amount of memory our scripts consume
- Which also can massively improve performance

@ulend

---

## Thank you!

`<?= $questions ?? exit(0); ?>`

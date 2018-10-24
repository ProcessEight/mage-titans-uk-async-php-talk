# Through the looking glass: Adventures in Asynchronous PHP

## Slide 2

## Slide 3

Hello, my name is Simon Frost and I am a senior backend Magento Engineer at a UK-based agency called Magium Commerce.

I have been working with PHP for over ten years and with Magento since v1.4 and online you can find me under the handle Process Eight.

## Slide 4

So I have been working on an integration with an ERP system.

In order to improve the performance of this integration I started investigating techniques for improving PHP performance.

Now, Asynchronous Programming is the one I found most promising and I want to share with you what I found, how it helped me and how it could help you.

## Slide 5

I'll introduce the idea of async programming first, then explain how we can use it in PHP and finally show how I used async programming to improve the performance of that ERP integration.

## Slide 6

What do we mean by async then?

## Slide 7

Well, it can mean many things. The definition we are interested in is: 'Occurrence of events outside the main flow of execution and ways to manage such events'.

These "outside" events could be the arrival of signals, or they could be actions instigated by a program that take place concurrently with program execution, without the program halting whilst waiting for results​.

That definition might sound a bit abstract, but we are already familiar with asynchronicity even if we don't know it or recognise it.

For example, Ajax is often used to load a page asynchronously.

The Event/Observer pattern, employed in Magento 1 and 2, is an example of an asynchronous programming design pattern.

Batch processing using queues is another example, where the items to be processed are not processed immediately, but are queued and processed at some point in the future.

So the concept of 'asynchronicity' can be implemented in different ways.

## Slide 8

How can we use async to write better performing programs? We'll start with an example of how most programs work; A statement is issued, for example to connect to a database, read a file or connect to an API.

Then the program has to wait until the results of that statement are ready - this stage is known as 'blocking' because the program is blocked. Execution can't continue until the results are returned.

After the program receives and processes the results, only then can the program move on and execute the next statement.

The program continues like this until the end of the program is reached.

## Slide 9

Now in an asynchronous program, we start from the same point by executing a statement.

However, whilst the program is waiting for the results of that statement, it can continue and execute another statement whilst it is waiting for the results of previous statements.

Once the results of previous statements are ready, the program can then process the results.

The program continues until all the results have been returned and processed.

## Slide 10

The big takeaway from the previous two slides is that if a program is dealing with a lot of database calls, file reads or writes, API calls, which we can collectively call 'input/output' operations, then the sync approach can be quite inefficient, as the program is basically idling whilst waiting for the I/O to complete.

Whilst the performance of hardware has massively improved, the speed of programming languages has not kept pace.

Async programming aims to take advantage of these circumstances, by maximising CPU usage and minimising I/O.

## Slide 11

So now we've established async programming as a way of better utilising our hardware, let's take a deeper look at what it involves. 

## Slide 12

In order to take advantage of this increase in the speed of CPUs, we need to adjust our thinking when it comes to writing programs in an asynchronous fashion.

Let's have a look at some of the tools we can use to help us do this. 

## Slide 13

Promises are temporary placeholders which stand in for the result of an operation.

They work in a similar way to callbacks in other languages. 

Promises emit events when certain conditions are met, for example when it is ready to return a result or if an error occurs.

The program can subscribe to these events and react appropriately.

## Slide 14

Co-routines are methods which can be interrupted or paused.

Exceptions can also be 'thrown in' to co-routines, which means they can be used to write async code using a more sync-style syntax.

## Slide 15

The Event Loop is a key part of the Reactor Pattern, which is one way of programming asynchronously.

## Slide 16

The Event Loop leads us neatly onto Event-Driven Programming, which is one way of programming asyncly.

The big take away from this slide is that in Event-Driven Programming, you cannot say when exactly something will happen, which is about the opposite of sync programming.

## Slide 17

How can we use these tools and why should we use PHP?

## Slide 18

There are several advantages to using PHP rather than a different language.

I think these reasons are the most compelling.

Many of the PHP projects which support async programming use core PHP language features, so there is no magic or special extensions required.

Remember this is the same PHP we are all used to - We're just using it in a different way.

## Slide 19

There are PHP libraries and frameworks​ which are designed to help you write async programs with PHP.

There were a lot of libraries to implement event driven programming in PHP, however, work on that goal has now coalesced around these projects​.

These projects are now the most up-to-date and frequently maintained​.

## Slide 20

OK, now that we've learnt a bit of theory, let's take a look at how we can bring Async, PHP and Magento together.

## Slide 21

Now these criteria are subjective, depending on the way that async has been implemented within the app.

There are lots of tasks in Magento which can benefit from using an async approach. 

Over the next few slides, I'll show you some examples.

## Slide 22

We can break up a task to resize hundreds of images and then fork new processes to run each of these smaller tasks - essentially pseudo-multi-threading.

## Slide 23

We can use the 'mysql' component of the ReactPHP project in order to break up a query returning a large result set into smaller queries, which are returned as soon as they are ready.

This is all hidden behind a simple interface, so we don't have to worry about the asynchronicity - we just have to process the results as they are returned to us.

Alternatively, we can use the same 'child-process' approach that Magento has used with their Async Indexing feature.

## Slide 24

The sync way is limited by the memory you have available at the time the script runs​. 

The async way is limited only by the amount of memory it takes to process one line of the file at a time​.

Obviously, this allows us to process ridiculously large (think GB).

Of course, this approach is not suitable if the rows in a file must be read in a certain order (i.e. Importing config products).

## Slide 25

For the final part of this presentation I'll show you how we used these examples we've just seen to make an ERP integration more efficient​.

## Slide 26

There will be other ways of doing this, but this is the solution we chose​.

The flow chart we produced to map their price logic was unreal. Four sides of A3!​

The clients wanted some imports to run hourly - unfortunately, some of these processes took so long to process, due to the volume of data, that they would overlap.

## Slide 27

The solution I came up with was to use the example of async batch processing, forking new processes to run child tasks

## Slide 28

As you can see from these screenshots, the sync version of the command used 54MB to import over 2,000 prices, whereas the async version used just 34MB.

So our async command uses 40% less memory to do the same task!

It's the same output, it just uses less memory.

## Slide 29

The solution I came up with was another example of async batch processing, but in this example I added an option to determine how many child threads should be used.

## Slide 30

As we can see here, the sync version of the command took just under 13 minutes to process 3422 images.

The async version, with 3 child processes, took just under 5 minutes. When using six child processes it took just over three minutes to process 3422 images.

That's more than four times faster to do the same amount of work!

## Slide 31

Well, I hope that you found this talk interesting and useful. 

## Slide 32

To summarise, then, async can help us take the same PHP code and squeeze even more performance out of it. 

However, it's not a magic bullet and how much benefit you get from this will largely depend on what your app is doing. 

## Slide 33

Thank you for listening. If there is not enough time for questions now, you can catch up with me during the breaks and at the after party.

# Through the looking glass: Adventures in Asynchronous PHP

## Slide 2

## Slide 3

Hello, my name is Simon Frost and I am a senior backend Magento Engineer at a UK-based agency called Magium Commerce.

Online you can find me under the handle Process Eight.

## Slide 4

So I have been working on an integration with an ERP system.

In order to improve the performance of this integration I started investigating techniques for improving PHP performance.

Asynchronous Programming is the one I found most promising and I want to share with you what I found, how it helped me and how it could help you.

## Slide 5

I'll introduce the idea of async programming first, then explain how we can use it in PHP and finally show how I used async programming to improve the performance of an ERP integration.

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

Let's explore how we can use this concept to write programs. We'll start with an example of how most programs work; A statement is issued, for example to connect to a database, read a file or connect to an API.

Then the program has to wait until the results of that statement are ready - this stage is known as 'blocking' because the program is blocked.

After the results have been returned and processed, only then can the program move on and execute the next statement.

The program continues like this until the end of the program is reached.

## Slide 9

Now in an asynchronous program, we start from the same point by executing a statement.

However, whilst the program is waiting for the results of that statement, it can continue and execute another statement whilst it is waiting for the results of previous statements.

Once the results of previous statements are ready, the program then processes the results at that point.

## Slide 10

If the program is dealing with a lot input/output, then this can be quite inefficient, as the program is basically idling whilst waiting for the I/O to complete.

## Slide 2

## Slide 2

## Slide 2

## Slide 2

## Slide 2

## Slide 2

## Slide 2

## Slide 2

## Slide 2

## Slide 2

## Slide 2

## Slide 2

## Slide 2

## Slide 2

## Slide 2

## Slide 2

## Slide 2

## Slide 2

## Slide 2

## Slide 2

## Slide 2

## Slide 2

## Slide 2

## Slide 2

## Slide 2

## Slide 2

## Slide 2


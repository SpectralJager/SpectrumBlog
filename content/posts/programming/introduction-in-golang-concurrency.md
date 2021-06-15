+++
author = "Spectral Jager"
categories = ["programming"]
date = 2021-06-14T05:55:03Z
img = "https://miro.medium.com/max/1106/1*z93yvlIYe2kMObUaPxYTCg.png"
summary = "Goroutine is one of the best part of golang and i want introduce it for you and mayby show something new"
tags = ["Concurrency", "Golang"]
title = "Introduction in Golang concurrency."

+++
**Hi there, stranger, welcome to the SpectrumBlog. Today we will talk about Golang concurrency.**

## What is Concurrency?

### Introduction

In IT and Computer Science word **concurrency** can means different things to different peoples. You also may have heard the words as 'asynchronous', 'parallel' or 'threaded'. For some peoples those words means the same thing, but its not right.

> _Concurrency_ - In computer science is the ability of different parts or units of a program, algorithm, or problem to be executed out-of-order or at the same time simultaneously partial order, without affecting the final outcome ([Wiki](https://en.wikipedia.org/wiki/Concurrency_(computer_science)))

or

> _Concurrency_ it is a program's ability to do two or more tasks that run individually of each other, at about the same time, but remain part of the same program

### Compare with Parallelism

Parallelism means that an application splits its tasks up into smaller sub-tasks which can be processed in parallel, for instance on multiple CPUs at the exact same time.

What is the difference between parallel programming and concurrent programming?

You may get concurrency in a single core CPU, but for parallelism you are requiring hardware with multiple processing units. We can make conclusion that parallelism is a specific kind of concurrency where task are really running in the same time.

The main difference between those two definitions is:

* in concurrent systems, multiple actions can be in progress (may not be executed) at the same time.
* Meanwhile, multiple actions are simultaneously executed in parallel systems.

**Concurrency is about dealing with lots of things at once. Parallelism is about doing lots of things at once.**

### Common issues

Several problems may arise in concurrency like:

* Shared resource can be accessed by several threads concurrently. So the sequence of access to that resource is important. When a thread tries to read a shared variable, another thread may change the value of the shared variable. That may cause inconsistency.
* Concurrency code is usually difficult to get right. Usually it takes a some time to get it working as it should be, and even then it's not uncommon for bugs to exists in code for years before they will have reviled.
* Race conditions - when two or more operations must execute in the correct order, but that order not written or guarantied in the program.
* Deadlock - one in which all concurrent processes are waiting on one another.

## Concurrency in Golagn.

### Introduction

![...](https://miro.medium.com/max/11000/1*aSPCO92xpe9Z564-ExeaAw.png)

Concurrent programming is a large topic but it’s also one of the most interesting aspects of the Go language.

Go encourages a other approach in which shared values are passed around on channels and, in fact, never actively shared by separate threads of execution. Only one goroutine has access to the value at any given time. Data races cannot occur, by design. To encourage this way of thinking we have reduced it to a slogan

_Do not communicate by sharing memory; instead, share memory by communicating._

This approach can be taken too far. Reference counts may be best done by putting a mutex around an integer variable, for instance. But as a high-level approach, using channels to control access makes it easier to write clear, correct programs.

Although Go’s approach to concurrency originates in Hoare’s Communicating Sequential Processes (CSP), it can also be seen as a type safe generalization of Unix pipes

### Goroutines

![...](https://miro.medium.com/max/5216/1*dD8qcmhpjUlKxZ1GHmX1AQ.png)

Golang provides Goroutines as a way to handle operations concurrently.

GO routine can be understood as a light weight thread. The cost for creating and running GO routine is 2 KB stack size, so there can be thousands of GO routines running simultaneously in a GO application.

All the program contains at least one Go routine, it is the Main Go Routine. One thing that is to be known is that, all the other GO routines are actually running inside this main GO routine. So if this main GO routine is terminated then all the other GO routines also gets terminated.

To run a function as a goroutine, call that function prefixed with the `go` statement.

    go someFunc() // run gouroutine,
    // or using lambda func
    go func(){
    	...
    } ()

When a new Goroutine is started, the goroutine call returns immediately. Unlike functions, the control does not wait for the Goroutine to finish executing. The control returns immediately to the next line of code after the Goroutine call and any return values from the Goroutine are ignored.

The main Goroutine should be running for any other Goroutines to run. If the main Goroutine terminates then the program will be terminated and no other Goroutine will run.

    package main
    
    import "fmt"
    
    func main() {
      go func() {
      	fmt.Println("in the goroutin")
      } ()
      fmt.Println("Out of the goroutin")
    }

Output:

    Out of the goroutin

This program consists of two goroutines. The first goroutine is implicit and is the main function itself. The second goroutine is created when we call `go func(){...}()`. Normally when we invoke a function our program will execute all the statements in a function and then return to the next line following the invocation. With a goroutine we return immediately to the next line and don't wait for the function to complete.

### Chanels

![...](https://i.stack.imgur.com/kSx6w.png)

The most natural way to fetch a value from a goroutine is channels.Go channels are like pipes, that connect concurrent goroutines. You can send values into channels from one goroutine and receive those values into another goroutine or in a synchronous function.

Channels can be thought as a medium using which GO routines can communicate. Data can be sent or received by using channels. Receiving or sending of data in channel is blocking by nature. Each channel has type defined to it. Data type other than the defined ones cannot be written or read.

Basically, the direction of the arrow with respect to the channel specifies whether the data is sent `chanName <- data` or received `variable := <- chanName`.

There are 2 types of channels called buffered `make(chan type, capacityOfBuffer)` and unbuffered `make(chan type)`. There are some differences between them.

There is a given capacity to hold data in the buffered channel. But unbuffered channel does not have the capacity to hold more than one data. That means, only one piece of data fits through the unbuffered channel at a time.

By default, writing and reading from an unbuffered channel is blocking operation. When one goroutine sends data, it is blocked until other goroutines receive data from the channel. It is the same for the receiving part. When one goroutine tries to receive data from the channel, it is blocked until a data sent to the channel. It is kind of the same for the buffered channel. Sender goroutine is blocked when capacity is full until other goroutines fetch the data from the channel.

Here is an example program using channels:

    package main
    
    import (
    	"fmt"
    	"time"
    )
    
    func ping(c chan string) {
    	for {
    		fmt.Println("ping")
    		c <- "ping"
    	}
    }
    
    func pong(c chan string) {
    	for {
    		if <-c == "ping" {
    			fmt.Println("pong")
    			time.Sleep(time.Second * 1)
    		}
    	}
    }
    
    func main() {
    	var c chan string = make(chan string)
    
    	go ping(c)
    	go pong(c)
    
    	fmt.Scanln()
    }

This program will print “ping” and "pong" forever (hit enter to stop it). A channel type is represented with the keyword chan followed by the type of the things that are passed on the channel (in this case we are passing strings). The <- (left arrow) operator is used to send and receive messages on the channel. c <- "ping" means send "ping". <- c means receive a message.

A sender can close a channel to indicate that no more values will be sent. Receivers can test whether a channel has been closed by assigning a second parameter to the receive expression:

v, ok := <-ch

ok is false if there are no more values to receive and the channel is closed.

The loop for i := range ch receives values from the channel repeatedly until it is closed.

Note: Only the sender should close a channel, never the receiver. Sending on a closed channel will cause a panic.

Another note: Channels aren’t like files; you don’t usually need to close them. Closing is only necessary when the receiver must be told there are no more values coming, such as to terminate a range loop.

package main

import (
"fmt"
)

func fibonacci(n int, c chan int) {
x, y := 0, 1
for i := 0; i < n; i++ {
c <- x
x, y = y, x+y
}
close(c)
}

func main() {
c := make(chan int, 10)// buffered chanel
go fibonacci(cap(c), c)
for i := range c {
fmt.Println(i)
}
}

### Select

The select statement lets a goroutine wait on multiple communication operations.

A select blocks until one of its cases can run, then it executes that case. It chooses one at random if multiple are ready.

Go has a special statement called select which works like a switch but for channels:

    func main() {
      c1 := make(chan string)
      c2 := make(chan string)
    
      go func() {
        for {
          c1 <- "1"
          time.Sleep(time.Second * 4)
        }
      }()
    
      go func() {
        for {
          c2 <- "2"
          time.Sleep(time.Second * 1)
        }
      }()
    
      go func() {
        for {
          select {
          case msg := <- c1:
            fmt.Printf("message from first chanel: %s\n", msg)
          case msg := <- c2:
          	fmt.Printf("message from second chanel: %s\n", msg)
          }
        }
      }()
    
      fmt.Scanln()
    }

This program prints “1” every 4 seconds and “2” every 1 seconds. select picks the first channel that is ready and receives from it (or sends to it). If more than one of the channels are ready then it randomly picks which one to receive from. If none of the channels are ready, the statement blocks until one becomes available.

The select statement is often used to implement a timeout:

    select {
          case msg := <- c1:
            fmt.Printf("message from first chanel: %s\n", msg)
          case msg := <- c2:
          	fmt.Printf("message from second chanel: %s\n", msg)
          case <- time.After(10 * time.Second):
      		fmt.Println("timeout")
    }

### WaitGroup

The WaitGroup type of sync package, is used to wait for the program to finish all goroutines launched from the main function. It uses a counter that specifies the number of goroutines, and Wait blocks the execution of the program until the WaitGroup counter is zero.

* The `Add` method is used to add a counter to the WaitGroup.
* The `Done` method of WaitGroup is scheduled using a defer statement to decrement the WaitGroup counter.
* The `Wait` method of the WaitGroup type waits for the program to finish all goroutines.

**The Wait method is called inside the main function, which blocks execution until the WaitGroup counter reaches the value of zero and ensures that all goroutines are executed.**

    package main
    
    import (
    	"fmt"
    	"sync"
    )
    
    func main() {
    	var wg sync.WaitGroup
    
    	wg.Add(1)
    	go func() {
    		fmt.Println(1)
    		wg.Done()
    	}()
    
    	wg.Add(1)
    	go func() {
    		fmt.Println(2)
    		wg.Done()
    	}()
    
    	wg.Wait() // wait untill all routins done
    }

### Size of Goroutines

[Source](https://tpaschalis.github.io/goroutines-size/)

Anyone learning Go has heard that “goroutines are like lightweight threads” and that “it’s okay to launch hundreds, thousands of goroutines”. Some people learn that “a goroutine takes up around 2 kilobytes”, most likely referencing the Go 1.4 release notes, and even fewer learn that this represents its initial stack size.

The Goroutine scheduler is a work-stealing scheduler introduced back in Go 1.1 by Dmitry Vyukov and the Go team. Its design document is available here and discusses possible future improvements. There are lots of great resources to grok how it works in depth, but the main thing to understand is that it tries to manage G’s, M’s and P’s ; goroutines, machine threads and processors.

* A “G” is simply a Golang goroutine.
* An “M” is an OS thread that can be either executing something or idle.
* A “P” can be thought as a CPU in the OS’ scheduler; it represents the resources required to execute our Go code, such as a scheduler, or a memory allocator state.

These are represented in the runtime as structs of type g, type m, or type p.

The scheduler’s main responsibility is to match each G (the code we want to execute) to an M (where to execute it) and a P (the rights and resources to execute)

When an M stops executing our code, it returns its P to the idle P pool. To resume executing Go code, it must re-acquire it. Similarly, when a goroutine exits, the G object is returned to a pool of free Gs, and can later be reused for some other goroutine.

By this time, you’re either probably wondering Hmm, so what is the size of this stack?, or you’ve already guessed that the 2 kilobytes refer exactly to this stack size!

A goroutine starts with a 2-kilobyte minimum stack size which grows and shrinks as needed without the risk of ever running out.

Essentially, before executing any function Go checks whether the amount of stack required for the function it’s about to execute is available; if not a call is made to runtime.morestack which allocates a new page and only then the function is executed. Finally, when that function exits, its return arguments are copied back to the original stack frame, and any unneeded stack space is released.

While the minimum stack size is defined as 2048 bytes, the Go runtime does also not allow goroutines to exceed a maximum stack size; this maximum depends on the architecture and is 1 GB for 64-bit and 250MB for 32-bit systems.

If this limit is reached a call to runtime.abort will take place.

## sources and useful links

 1. [Concurrency — An Introduction to Programming in Go](https://www.golang-book.com/books/intro/10)
 2. [Concurrency in GO and Golang Concurrency Tutorial with Examples  - golangprograms.com](https://www.golangprograms.com/go-language/concurrency.html)
 3. [Concurrency and Channels in Go](https://medium.com/trendyol-tech/concurrency-and-channels-in-go-bbc4dea75286)
 4. [Chapter 8 Concurrency](http://www.golangbootcamp.com/book/concurrency)
 5. [Goroutines – Concurrency in Golang](https://www.geeksforgeeks.org/goroutines-concurrency-in-golang/)
 6. [Understanding GO Routine and Channel](https://medium.com/wesionary-team/understanding-go-routine-and-channel-b09d7d60e575)
 7. [Goroutines](https://golangbot.com/goroutines/)
 8. [Goroutines and Waitgroup  - golangprograms.com](https://www.golangprograms.com/goroutines.html)
 9. [What is a goroutine? And what is their size?](https://tpaschalis.github.io/goroutines-size/)
10. [Go Concurrency Patterns: Pipelines and cancellation](https://blog.golang.org/pipelines)
11. [Concurrency vs. Parallelism — A brief view](https://medium.com/@itIsMadhavan/concurrency-vs-parallelism-a-brief-review-b337c8dac350)
+++
author = "Spectral Jager"
categories = ["programming"]
date = 2021-06-14T05:55:03Z
draft = true
img = "https://www.freecodecamp.org/news/content/images/size/w2000/2020/02/golang-gopher-2.jpg"
summary = ""
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
Parallelism means that an application splits its tasks up into smaller subtasks which can be processed in parallel, for instance on multiple CPUs at the exact same time.

What is the difference between parallel programming and concurrent programming?

You may get concurrency in a single core CPU, but for parallelism you are requiring hardware with multiple processing units. We can make conclusion that parallelism is a specific kind of concurrency where task are really running in the same time.

The main difference between those two difinitions is:
- in concurrent systems, multiple actions can be in progress (may not be executed) at the same time.
- Meanwile, multiple actions are simultaneously executed in parallel systems.

**Concurrency is about dealing with lots of things at once. Parallelism is about doing lots of things at once.**

### Common issues
Several problems may arise in concurrency like:

- Shared resource - can be accessed by several threads concurrently. So the sequence of access to that resource is important. When a thread tries to read a shared variable, another thread may change the value of the shared variable. That may cause inconsistency.

- Concurrency code is by standard difficult to get right. Usually it takes a some time to get it working as it should be, and even then it's not uncommon for bugs to exists in code for years before they will have reviled.

- Race conditions - when two or more operations must execute in the correct order, but that order not written or guarantied in the program.

- Deadlock - one in which all concurrent processes are waiting on one another.

## Concurrency in Golagn.
### Introduction
Concurrent programming is a large topic but it’s also one of the most interesting aspects of the Go language.

Go encourages a other approach in which shared values are passed around on channels and, in fact, never actively shared by separate threads of execution. Only one goroutine has access to the value at any given time. Data races cannot occur, by design. To encourage this way of thinking we have reduced it to a slogan

*Do not communicate by sharing memory; instead, share memory by communicating.*

This approach can be taken too far. Reference counts may be best done by putting a mutex around an integer variable, for instance. But as a high-level approach, using channels to control access makes it easier to write clear, correct programs.

Although Go’s approach to concurrency originates in Hoare’s Communicating Sequential Processes (CSP), it can also be seen as a type safe generalization of Unix pipes

### Goroutines
Golang provides Goroutines as a way to handle operations concurrently.

To run a function as a goroutine, call that function prefixed with the go statement.

The go keyword makes the function call to return immediately, while the function starts running in the background as a goroutine and the rest of the program continues its execution. The main function of every Golang program is started using a goroutine, so every Golang program runs at least one goroutine.

Goroutines are functions or methods that run concurrently with other functions or methods. Goroutines can be thought of as light weight threads. The cost of creating a Goroutine is tiny when compared to a thread. Hence it's common for Go applications to have thousands of Goroutines running concurrently. 

When a new Goroutine is started, the goroutine call returns immediately. Unlike functions, the control does not wait for the Goroutine to finish executing. The control returns immediately to the next line of code after the Goroutine call and any return values from the Goroutine are ignored.

The main Goroutine should be running for any other Goroutines to run. If the main Goroutine terminates then the program will be terminated and no other Goroutine will run.


GO routine is a function or method which is capable of being executed simultaneously with relation to any other GO routine present in a program. The main difference between a normal function and a go routine is that the main program doesn’t wait for the GO routine to be finished which is not true in case of normal function. Go routine is a non-blocking function which starts executing on it’s own once called.

GO routine can be understood as a light weight thread. The cost for creating and running GO routine is low so there can be thousands of GO routines running simultaneously in a GO application. Each GO routine is only some kb stack size.

All the program contains at least one Go routine, it is the Main Go Routine. One thing that is to be known is that, all the other GO routines are actually running inside this main GO routine. So if this main GO routine is terminated then all the other GO routines also gets terminated.

As I mentioned earlier, if the main GO routine is terminated, all the GO routine will also get terminated. And in our case, this is what’s happening. When a GO routine is started, unlike the normal function it doesn’t wait for it to return. Instead, GO routine is returned immediately and the control is passed to the following line.

https://miro.medium.com/max/1106/1*z93yvlIYe2kMObUaPxYTCg.png

Go language provides a special feature known as a Goroutines. A Goroutine is a function or method which executes independently and simultaneously in connection with any other Goroutines present in your program. Or in other words, every concurrently executing activity in Go language is known as a Goroutines. You can consider a Goroutine like a light weighted thread. The cost of creating Goroutines is very small as compared to the thread. Every program contains at least a single Goroutine and that Goroutine is known as the main Goroutine. All the Goroutines are working under the main Goroutines if the main Goroutine terminated, then all the goroutine present in the program also terminated. Goroutine always works in the background.

Advantages of Goroutines

    Goroutines are cheaper than threads.
    Goroutine are stored in the stack and the size of the stack can grow and shrink according to the requirement of the program. But in threads, the size of the stack is fixed.
    Goroutines can communicate using the channel and these channels are specially designed to prevent race conditions when accessing shared memory using Goroutines.
    Suppose a program has one thread, and that thread has many Goroutines associated with it. If any of Goroutine blocks the thread due to resource requirement then all the remaining Goroutines will assign to a newly created OS thread. All these details are hidden from the programmers.

Goroutines have other advantages like startup time. Goroutines are started faster than threads.

Goroutines are created with only 2 KB stack size.

Concurrency in Golang is the ability for functions to run independent of each other. A goroutine is a function that is capable of running concurrently with other functions. When you create a function as a goroutine, it has been treated as an independent unit of work that gets scheduled and then executed on an available logical processor. The Golang runtime scheduler has feature to manages all the goroutines that are created and need processor time. The scheduler binds operating system's threads to logical processors in order to execute the goroutines. By sitting on top of the operating system, scheduler controls everything related to which goroutines are running on which logical processors at any given time.

Goroutines — A goroutine is a function that runs independently of the function that started it.

Go has rich support for concurrency using goroutines and channels.

A goroutine is a function that is capable of running concurrently with other functions. To create a goroutine we use the keyword go followed by a function invocation:

package main

import "fmt"

func f(n int) {
  for i := 0; i < 10; i++ {
    fmt.Println(n, ":", i)
  }
}

func main() {
  go f(0)
  var input string
  fmt.Scanln(&input)
}

This program consists of two goroutines. The first goroutine is implicit and is the main function itself. The second goroutine is created when we call go f(0). Normally when we invoke a function our program will execute all the statements in a function and then return to the next line following the invocation. With a goroutine we return immediately to the next line and don't wait for the function to complete. This is why the call to the Scanln function has been included; without it the program would exit before being given the opportunity to print all the numbers.

### Chanels
The most natural way to fetch a value from a goroutine is channels. Channels are the pipes that connect concurrent goroutines. You can send values into channels from one goroutine and receive those values into another goroutine or in a synchronous function.

Channels can be thought as a medium using which GO routines can communicate. Data can be sent or received by using channels. Receiving or sending of data in channel is blocking by nature. Each channel has type defined to it. Data type other than the defined ones cannot be written or read.

Basically, the direction of the arrow with respect to the channel specifies whether the data is sent or received.

Goroutines are good and easy to use. But how they communicate? We have learned a term called “shared resource” in the previous chapter. Do the goroutines access to a shared resource? The answer is No.

The philosophy behind the Go’s concurrency is different.

    Do not communicate by sharing memory; instead, share memory by communicating. (https://blog.golang.org/codelab-share)

It is not preferred to use a shared resource in Go. Instead use channels to communicate goroutines. Go’s concurrency model relies on CSP (Communicating Sequential Processes, 1978). This approach ensures that only one goroutine access to the data at a given time. Let’s see how to use go channels.

Go channels are like pipes. One goroutine sends data, other goroutines receive that data from the other side. There are 2 types of channels called buffered and unbuffered. There are some differences between them.

There is a given capacity to hold data in the buffered channel. But unbuffered channel does not have the capacity to hold more than one data. That means, only one piece of data fits through the unbuffered channel at a time.

By default, writing and reading from an unbuffered channel is blocking operation. When one goroutine sends data, it is blocked until other goroutines receive data from the channel. It is the same for the receiving part. When one goroutine tries to receive data from the channel, it is blocked until a data sent to the channel. It is kind of the same for the buffered channel. Sender goroutine is blocked when capacity is full until other goroutines fetch the data from the channel.

Go channels are highly recommended to use in Go applications when dealing with concurrency. But if your problem can not be solved with channels, you may still use other solutions by sync package. This package provides low-level components like mutexes.

Channels — A channel is a pipeline for sending and receiving data. Channels provide a way for one goroutine to send structured data to another.

By default, sends and receives block wait until the other side is ready. This allows goroutines to synchronize without explicit locks or condition variables.

Channels provide a way for two goroutines to communicate with one another and synchronize their execution. Here is an example program using channels:

package main

import (
  "fmt"
  "time"
)

func pinger(c chan string) {
  for i := 0; ; i++ {
    c <- "ping"
  }
}

func printer(c chan string) {
  for {
    msg := <- c
    fmt.Println(msg)
    time.Sleep(time.Second * 1)
  }
}

func main() {
  var c chan string = make(chan string)

  go pinger(c)
  go printer(c)

  var input string
  fmt.Scanln(&input)
}

This program will print “ping” forever (hit enter to stop it). A channel type is represented with the keyword chan followed by the type of the things that are passed on the channel (in this case we are passing strings). The <- (left arrow) operator is used to send and receive messages on the channel. c <- "ping" means send "ping". msg := <- c means receive a message and store it in msg. The fmt line could also have been written like this: fmt.Println(<-c) in which case we could remove the previous line.

Using a channel like this synchronizes the two goroutines. When pinger attempts to send a message on the channel it will wait until printer is ready to receive the message. (this is known as blocking) Let's add another sender to the program and see what happens. Add this function:

func ponger(c chan string) {
  for i := 0; ; i++ {
    c <- "pong"
  }
}

And modify main:

func main() {
  var c chan string = make(chan string)

  go pinger(c)
  go ponger(c)
  go printer(c)

  var input string
  fmt.Scanln(&input)
}

The program will now take turns printing “ping” and “pong”.

A sender can close a channel to indicate that no more values will be sent. Receivers can test whether a channel has been closed by assigning a second parameter to the receive expression: after

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
    c := make(chan int, 10)
    go fibonacci(cap(c), c)
    for i := range c {
        fmt.Println(i)
    }
}


- Channel Direction

We can specify a direction on a channel type thus restricting it to either sending or receiving. For example pinger's function signature can be changed to this:

func pinger(c chan<- string)

Now c can only be sent to. Attempting to receive from c will result in a compiler error. Similarly we can change printer to this:

func printer(c <-chan string)

A channel that doesn't have these restrictions is known as bi-directional. A bi-directional channel can be passed to a function that takes send-only or receive-only channels, but the reverse is not true.

It's also possible to pass a second parameter to the make function when creating a channel:

c := make(chan int, 1)

This creates a buffered channel with a capacity of 1. Normally channels are synchronous; both sides of the channel will wait until the other side is ready. A buffered channel is asynchronous; sending or receiving a message will not wait unless the channel is already full.

### Select
The select statement lets a goroutine wait on multiple communication operations.

A select blocks until one of its cases can run, then it executes that case. It chooses one at random if multiple are ready.

Go has a special statement called select which works like a switch but for channels:

func main() {
  c1 := make(chan string)
  c2 := make(chan string)

  go func() {
    for {
      c1 <- "from 1"
      time.Sleep(time.Second * 2)
    }
  }()

  go func() {
    for {
      c2 <- "from 2"
      time.Sleep(time.Second * 3)
    }
  }()

  go func() {
    for {
      select {
      case msg1 := <- c1:
        fmt.Println(msg1)
      case msg2 := <- c2:
        fmt.Println(msg2)
      }
    }
  }()

  var input string
  fmt.Scanln(&input)
}

This program prints “from 1” every 2 seconds and “from 2” every 3 seconds. select picks the first channel that is ready and receives from it (or sends to it). If more than one of the channels are ready then it randomly picks which one to receive from. If none of the channels are ready, the statement blocks until one becomes available.

The select statement is often used to implement a timeout:

select {
case msg1 := <- c1:
  fmt.Println("Message 1", msg1)
case msg2 := <- c2:
  fmt.Println("Message 2", msg2)
case <- time.After(time.Second):
  fmt.Println("timeout")
}

time.After creates a channel and after the given duration will send the current time on it. (we weren't interested in the time so we didn't store it in a variable) We can also specify a default case:

select {
case msg1 := <- c1:
  fmt.Println("Message 1", msg1)
case msg2 := <- c2:
  fmt.Println("Message 2", msg2)
case <- time.After(time.Second):
  fmt.Println("timeout")
default:
  fmt.Println("nothing ready")
}

The default case happens immediately if none of the channels are ready.

### WaitGroup
The WaitGroup type of sync package, is used to wait for the program to finish all goroutines launched from the main function. It uses a counter that specifies the number of goroutines, and Wait blocks the execution of the program until the WaitGroup counter is zero.

The Add method is used to add a counter to the WaitGroup.

The Done method of WaitGroup is scheduled using a defer statement to decrement the WaitGroup counter.

The Wait method of the WaitGroup type waits for the program to finish all goroutines.

The Wait method is called inside the main function, which blocks execution until the WaitGroup counter reaches the value of zero and ensures that all goroutines are executed.

package main

import (
	"fmt"
	"io/ioutil"
	"log"
	"net/http"
	"sync"
)

// WaitGroup is used to wait for the program to finish goroutines.
var wg sync.WaitGroup

func responseSize(url string) {
	// Schedule the call to WaitGroup's Done to tell goroutine is completed.
	defer wg.Done()

	fmt.Println("Step1: ", url)
	response, err := http.Get(url)
	if err != nil {
		log.Fatal(err)
	}

	fmt.Println("Step2: ", url)
	defer response.Body.Close()

	fmt.Println("Step3: ", url)
	body, err := ioutil.ReadAll(response.Body)
	if err != nil {
		log.Fatal(err)
	}
	fmt.Println("Step4: ", len(body))
}

func main() {
	// Add a count of three, one for each goroutine.
	wg.Add(3)
	fmt.Println("Start Goroutines")

	go responseSize("https://www.golangprograms.com")
	go responseSize("https://stackoverflow.com")
	go responseSize("https://coderwall.com")

	// Wait for the goroutines to finish.
	wg.Wait()
	fmt.Println("Terminating Program")

### Size of Goroutines
I’m pretty sure that anyone learning Go has heard that “goroutines are like lightweight threads” and that “it’s okay to launch hundreds, thousands of goroutines”. Some people learn that “a goroutine takes up around 2 kilobytes”, most likely referencing the Go 1.4 release notes, and even fewer learn that this represents its initial stack size.

And while all those statements are true, I’d like to show why is that, explore what exactly is a goroutine, how much space it takes, and provide starting points for anyone to poke around the Go internals.

For this exploration I’ll be using the Go 1.14 release branch, so all code snippets will point there.
The Goroutine scheduler

The Goroutine scheduler is a work-stealing scheduler introduced back in Go 1.1 by Dmitry Vyukov and the Go team. Its design document is available here and discusses possible future improvements. There are lots of great resources to grok how it works in depth, but the main thing to understand is that it tries to manage G’s, M’s and P’s ; goroutines, machine threads and processors.

A “G” is simply a Golang goroutine.
An “M” is an OS thread that can be either executing something or idle.
A “P” can be thought as a CPU in the OS’ scheduler; it represents the resources required to execute our Go code, such as a scheduler, or a memory allocator state.

These are represented in the runtime as structs of type g, type m, or type p.

The scheduler’s main responsibility is to match each G (the code we want to execute) to an M (where to execute it) and a P (the rights and resources to execute)

When an M stops executing our code, it returns its P to the idle P pool. To resume executing Go code, it must re-acquire it. Similarly, when a goroutine exits, the G object is returned to a pool of free Gs, and can later be reused for some other goroutine.

By this time, you’re either probably wondering Hmm, so what is the size of this stack?, or you’ve already guessed that the 2 kilobytes refer exactly to this stack size!

A goroutine starts with a 2-kilobyte minimum stack size which grows and shrinks as needed without the risk of ever running out.

This excellent post by Dave Cheney explains how this works in more detail. Essentially, before executing any function Go checks whether the amount of stack required for the function it’s about to execute is available; if not a call is made to runtime.morestack which allocates a new page and only then the function is executed. Finally, when that function exits, its return arguments are copied back to the original stack frame, and any unneeded stack space is released.

While the minimum stack size is defined as 2048 bytes, the Go runtime does also not allow goroutines to exceed a maximum stack size; this maximum depends on the architecture and is 1 GB for 64-bit and 250MB for 32-bit systems.

If this limit is reached a call to runtime.abort will take place. Exceeding this stack size is very easy with a recursive function; all you have to do is

## sources and usefull links

1. [](https://www.golang-book.com/books/intro/10)
2. [](https://www.golangprograms.com/go-language/concurrency.html)
3. [](https://medium.com/trendyol-tech/concurrency-and-channels-in-go-bbc4dea75286)
4. [](http://www.golangbootcamp.com/book/concurrency)
5. [](https://www.geeksforgeeks.org/goroutines-concurrency-in-golang/)
6. [](https://eax.me/go-goroutines/)
7. [](https://medium.com/wesionary-team/understanding-go-routine-and-channel-b09d7d60e575)
8. [](https://golangbot.com/goroutines/)
9. [](https://www.golangprograms.com/goroutines.html)
10. [](https://tpaschalis.github.io/goroutines-size/)
11. [](https://blog.golang.org/pipelines)
12. [](https://medium.com/@itIsMadhavan/concurrency-vs-parallelism-a-brief-review-b337c8dac350)
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
**Hi there, stranger, welcome to the SpectrumBlog. Today I will briefly talk about Golang concurrency and waiting group.**

## What is Concurrency?

![...](https://i.giphy.com/media/7NOwsFG42paAb9yICU/giphy.webp)

How usually execute a synchronous program? Lets imagine you are cooking, you start by looking at recipe, then do first thing, then second and ets. You can't start doing others steps while you haven't end your previous step. You can't to begin cut vegetables while you don't yet took the meat out of the oven.

Isn't it ridiculous? Why you must stay and wait while meet be ready, while some part of your program is executing and don't start other part that don't depends from it?

Here is coming concurrency.

> In computer science, **concurrency** is the ability of different parts or units of a program, algorithm, or problem to be executed out-of-order or in partial order, without affecting the final outcome. ([Wikipedia](https://en.wikipedia.org/wiki/Concurrency_(computer_science)))

You just put your meat in the oven and start doing another things, when meat is ready you back to it and use with other components. Same with the program, you divide your code on subprograms, run them at the same time, wait while they done and maybe use result of their work.

### Difference between Concurrency and Parallelism

**Concurrency not equal Parallelism!**

> * **Concurrency** is when two or more tasks can start, run, and complete in overlapping time periods. It doesn't necessarily mean they'll ever both be running at the same instant. For example, multitasking on a single-core machine.
> * **Parallelism** is when tasks literally run at the same time, e.g., on a multi-core processor.
>   from [Stack Overflow](https://stackoverflow.com/questions/1050222/what-is-the-difference-between-concurrency-and-parallelism)

![...](https://sergeyzhuk.me/assets/images/posts/asyncphp-myths/concurrent-vs-parallel.png)
![...](https://miro.medium.com/max/659/1*bvgViDDOKC3HikokiROgYQ.png)

## Concurrency in Go. Introduction in Goroutines.

![...](https://miro.medium.com/max/800/1*qBiZD7mvwkNcIGDrkyZeCQ.jpeg)

Instead of threads, Golang uses goroutines. They are divided onto small numbers of OS threads, those exist only in the virtual space of go runtime.

Go has a segmented stack that grows when needed. That means it is controlled by Go runtime, not OS.

For using goroutines you just need place keywork 'go' before a **function**, that you want to start in different routine:

```golang
package main

import (
	"fmt"
    "time"
)

func main(){
	greatingMsg := "Hi there"
    go func() {
    	fmt.Println(greatingMsg, " First")
    }
    fmt.Println(greatingMsg, " Second")
    time.Sleep(1 * time.Second) // wait 1s that give routine print msg 
}
```

Output:

        Hi there!  Second
        Hi there!  First

**Remember: Main func will not wait while your goroutines will have done.**

E.x.:

1. We comment Sleep function, as result executed only second greeting

    package main
    
    import (
    	"fmt"
    )
    
    func main(){
    	greetingMsg := "Hi there"
        go func() {
        	fmt.Println(greetingMsg, " First")
        }
        fmt.Println(greetingMsg, " Second")
        //time.Sleep(1 * time.Second)
    }

Output:

    	Hi there!  Second

1. All in different goroutines

    package main
    
    import (
    	"fmt"
    )
    
    func main(){
    	greetingMsg := "Hi there"
        go func() {
        	fmt.Println(greetingMsg, " First")
        }
        go fmt.Println(greetingMsg, " Second")
    }

Output:

    	

### WaitGroup.

You can wait of execution of your goroutines with `time.Sleep`, but you can't always to know how long your function will execute. On the help going `sync.WaitGroup`. That function allow us add out routine in group and wait while all added routines done their jobs.

    package main
    
    import (
    	"fmt"
    	"sync"
    )
    
    func main() {
    	greatingMsg := "Hi there!"
    	var group sync.WaitGroup
    	group.Add(1)
    	go func() {
    		fmt.Println(greatingMsg, " First")
    		group.Done()
    	}()
    	group.Add(1)
    	go func() {
    		fmt.Println(greatingMsg, " Second")
    		group.Done()
    	}()
    	group.Wait()
    }

Output:

        Hi there!  Second
        Hi there!  First

## Additional Resources

1. [Concurrency and Channels in Go](https://medium.com/trendyol-tech/concurrency-and-channels-in-go-bbc4dea75286)
2. [A Tour of Go: Concurrency](https://tour.golang.org/concurrency/1)
3. [Concurrency With Golang Goroutines](https://tutorialedge.net/golang/concurrency-with-golang-goroutines/)
4. [Concurrency in Go](https://www.youtube.com/watch?v=LvgVSSpwND8)
+++
author = "Spectral Jager"
categories = ["programming"]
date = 2021-06-14T05:55:03Z
draft = true
img = "https://www.freecodecamp.org/news/content/images/size/w2000/2020/02/golang-gopher-2.jpg"
summary = ""
tags = ["Concurrency", "Golang"]
title = "Introduction in Golang concurrency. Description and common issues."

+++
**Hi there, stranger, welcome to the SpectrumBlog. Today We will talk about Golang concurrency.**

## What is Concurrency?

In IT and Computer Science word **concurrency** can means different things to different peoples. You also may have heard the words as 'asynchronous', 'parallel' or 'threaded'. For some peoples those words means the same thing, but its not right.

> _Concurrency_ - In computer science is the ability of different parts or units of a program, algorithm, or problem to be executed out-of-order or at the same time simultaneously partial order, without affecting the final outcome ([Wiki](https://en.wikipedia.org/wiki/Concurrency_(computer_science)))

![...](https://static.packt-cdn.com/products/9781789343052/graphics/ad090261-5969-4caa-b7ca-393d30c54548.png)

### Common issues

Concurrency code is by standard difficult to get right. Usually it takes a some time to get it working as it should be, and even then it's not uncommon for bugs to exists in code for years before they will have reviled.

Here some of them:

- *Race conditions* - when two or more operations must execute in the correct order, but that order not written or guarantied in the program.
![...](https://www.rapitasystems.com/files/multithreaded_testing.jpg)

Ex:
```
var someValue int
go func(){
	someValue += 10
} ()
if someValue == 10{ // can't predict, will execute that block or not
	fmt.Println("Value = 10")
}
```

- *Deadlock* - one in which all concurrent processes are waiting on one another.

![...](https://miro.medium.com/max/1200/1*yvJjqOwI4epwA1RrlpP_6Q.png)
Ex:
```
func main() {
    ch := make(chan int)
    ch <- 1 // stop execution and waiting reading from chanel
    fmt.Println(<-ch) // will not be executed
}
```

- *Peoples* - when you introduce new functionality or bugs fix, it could be difficult to determine the how make things right. 

### Difference between Concurrency and Parallelism


## Additional Resources

1. [Concurrency and Channels in Go](https://medium.com/trendyol-tech/concurrency-and-channels-in-go-bbc4dea75286)
2. [A Tour of Go: Concurrency](https://tour.golang.org/concurrency/1)
3. [Concurrency With Golang Goroutines](https://tutorialedge.net/golang/concurrency-with-golang-goroutines/)
4. [Concurrency in Go](https://www.youtube.com/watch?v=LvgVSSpwND8)
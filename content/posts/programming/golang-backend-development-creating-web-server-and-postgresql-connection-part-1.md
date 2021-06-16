+++
author = "Spectral Jager"
categories = ["programming"]
date = 2021-06-16T07:50:40Z
img = "https://images.unsplash.com/photo-1565273601018-d1da7cfed4f7?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1"
summary = "In that article i will show you how to create a simple http web server, handle requests, make response."
tags = ["Webserver", "Backend", "Golang"]
title = "Golang Backend development: Creating Web server ( Part 1 )"

+++
**Hi there, Stranger, welcome to the SpectrumBlog. Today we will talk about Golang HTTP Web server.**

## Web Server.

### Introduction. What a web server?

Under web server could be means two things:

1. Hardware, that store some files and web server software.
2. Application/Software, that manage files (like images, html files) on the hardware server and send that data to the client with help of protocols, like http.

In that article we will work with http web server.

### Simple Golang web server.

Lets start coding.

First at all we need bind our server on some port and listen requests. For creating web server we will use standard golang package `http` and `gorilla/mux`.

    package main
    
    import (
    	"log" // for loggin condition of our server
    	"net/http" // for creating web server
    
    	"github.com/gorilla/mux" // for creating dynamic routes, 
        						 //that will help us in the next articles
    )
    
    func HelloWorld(w http.ResponseWriter, r *http.Request) { // our handle function
    	// where 'w' is our response
        // 'r' is request
    	log.Println("Riched endpoint 'HelloWorld'") // Loggin, that Somebody make request to '/'
    }
    
    func main() {
    	router := mux.NewRouter() // Creating router for managing routes
    	router.HandleFunc("/", HelloWorld) // bind our endpoint 'HelloWorld' to url '/'
    	const addr = ":8000" // define addres and port of our server, that we will listen
    	log.Printf("Starting server. Listening on %s ...", domain) // Loggin, that we have started server
    	err := http.ListenAndServe(domain, router) // start server
    	log.Fatal(err) // If something goes wrong, log error
    }

Lets start our server. In the console we get:

    Starting server. Listening on :8000 ...

Going to the browser and trying access `127.0.0.1:8000/`:

    Riched endpoint 'HelloWorld'

In the browser we have got status 200 and white screen.

### Make response.

Its cool, but we want not just get request from client, but also send him back. For that we just need write some data into our response:

    package main
    
    import (
    	"log" // for loggin condition of our server
    	"net/http" // for creating web server
    
    	"github.com/gorilla/mux" // for creating dynamic routes, 
        						 //that will help us in the next articles
    )
    
    func HelloWorld(w http.ResponseWriter, r *http.Request) { // our handle function
    	// where 'w' is our response
        // 'r' is request
    	log.Println("Riched endpoint 'HelloWorld'") // Loggin, that Somebody make request to '/'
        // make response
        body := "<h1>Hello World!</h1>" // Create our response body
        w.Write([]byte(body)) // Write it into the response
    }
    
    func main() {
    	router := mux.NewRouter() // Creating router for managing routes
    	router.HandleFunc("/", HelloWorld) // bind our endpoint 'HelloWorld' to url '/'
    	const addr = ":8000" // define addres and port of our server, that we will listen
    	log.Printf("Starting server. Listening on %s ...", domain) // Loggin, that we have started server
    	err := http.ListenAndServe(domain, router) // start server
    	log.Fatal(err) // If something goes wrong, log error
    }

Run the program, refresh our page and see sentence `Hello World!`.

## Links

1. [MDN: What is a web server?](https://developer.mozilla.org/en-US/docs/Learn/Common_questions/What_is_a_web_server)
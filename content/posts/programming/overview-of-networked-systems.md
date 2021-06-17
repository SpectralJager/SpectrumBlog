+++
author = "Spectral Jager"
categories = ["programming"]
date = 2021-06-16T17:24:45Z
draft = true
img = ""
summary = ""
tags = ["IP", "OSI", "TCP", "Networking"]
title = "Overview of networked systems: 5+1 basic things that allow you understand networking."

+++
In the digital age most devices (over 10.07 billions on statistic of 2020 year [(statista.com)](https://www.statista.com/statistics/1183457/iot-connected-devices-worldwide/)) communicate with each other over computer networks. It could be computers, smartphones, printers, scanners etc, that connected through a transmission medium such as wires, cables. 

# What is COMPUTER NETWORK?
Here we come to definition of *computer network* - is a connection between two or more nodes (could be a single computer devices or other networks). Those connections not always are reliable or secure. 

## Main terms of computer network.
Three main therms, that helps to describe computer network:
	1. *Bandwidth* - is the amount of data we can send over a network connection in an interval of time
    2. *Latency* - is a measure of the time that passes between sending a network resource request and receiving a response
    3. Transmission modes:
    	- *Simplex* -- single flows in **ONE** direction and **ONLY** one node transmit and the other receives.
        - *Half Duplex* -- each node can transmit and receive but **NOT** at the same time.
        - *Full Duplex* -- both nodes transmit and receive simultaneously.

## Ways of connections.
The way of connection of nodes in a network called *topology*. Its could be simple connection between two nodes to comples layouts of nodes.

Base type of topology:
	1. Point-to-Point. Its type describet by **direct communication between two nodes** with a common link. Transfer data going in multiple ways: Simplex, Half Duplex or Full Duplex.
    ![point-to-point](https://www.myworkingnet.com/wp-content/uploads/2021/02/Point-to-Point-Network-Topology.png)
    2. Daisy Chain. Its series of point-to-point connections, when data going from sender to receiver through internal nodes. 
    ![daisy chain](https://i.pinimg.com/originals/db/cc/d1/dbccd1be7e8731070d2fbf888a8807ae.png)
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
The way of connection of nodes in a network called *topology*. Its could be simple connection between two nodes to complexs layouts of nodes.

Base types of topology:
	1. Point-to-Point. Its type describet by **direct communication between two nodes** with a common link. Transfer data going in multiple ways: Simplex, Half Duplex or Full Duplex.
    ![point-to-point](https://www.myworkingnet.com/wp-content/uploads/2021/02/Point-to-Point-Network-Topology.png)
    2. Daisy Chain. Its series of point-to-point connections, when data going from sender to receiver through internal nodes (they called *hops*). 
    ![daisy chain](https://i.pinimg.com/originals/db/cc/d1/dbccd1be7e8731070d2fbf888a8807ae.png)
    3. Bus. Its when nodes share common network link (known as *backbone*). All nodes get the same trafic and be accessed by any node.
    ![bus](https://i.pinimg.com/originals/d9/a9/74/d9a97433e7fff183ce32c70f80152720.png)
    4. Ring. Its closed loop of daisy chain. Transmission mode is simplex. Aggregate network bandwidth is bottlenecked by the weakest link between two nodes.
    ![ring](https://www.myworkingnet.com/wp-content/uploads/2021/02/Ring-Topology-1024x645.png)
    5. Star. Individual point-to-point connection with the center node (*hub* or *switch*). The aggregate central bandwidth forms a network bottleneck for large clusters. 
    ![star](https://www.myworkingnet.com/wp-content/uploads/2020/01/Star-topology.png)
    6. Mesh. Every node in the network connect to each other.
    ![mesh](https://www.myworkingnet.com/wp-content/uploads/2021/02/Mesh-Topology-1024x632.png)
    
## Internet service provider (ISP)
![ISP](https://upload.wikimedia.org/wikipedia/commons/thumb/9/9f/Internet_Connectivity_Access_layer.svg/800px-Internet_Connectivity_Access_layer.svg.png)

An ISP its an organization that provides a services as the access point or the gateway to the internet.
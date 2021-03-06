+++
author = "Spectral Jager"
categories = ["programming"]
date = 2021-06-16T17:24:45Z
img = "https://images.unsplash.com/photo-1522071820081-009f0129c71c?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1050&q=80"
summary = "In that article we will talk about computer networking, typologies, and basic networking terms. Also will briefly describe OSI and TCP/IP models, ISP."
tags = ["IP", "OSI", "TCP", "Networking"]
title = "Overview of networked systems: basic things that allow you to understand computer networking."

+++
In the digital age most devices (over 10.07 billions on statistics of 2020 year [(statista.com)](https://www.statista.com/statistics/1183457/iot-connected-devices-worldwide/)) communicate with each other over computer networks. It could be computers, smartphones, printers, scanners etc, that are connected through a transmission medium such as wires, cables.

Computer Network is an important part of our live, that allows us to order various products from home, self-study, spend fun time and other different things. I also could say it helps us survive in the modern world.

![...](https://images.unsplash.com/photo-1483389127117-b6a2102724ae)

# What is computer network?

Here we come to the definition of _computer network_ - is a connection between two or more nodes (could be a single computer device or other networks). Those connections are not always are reliable or secure.

## Main terms of computer network.

Three main therms, that helps to describe computer network:

1. _Bandwidth_ - is the amount of data we can send over a network connection in an interval of time
2. _Latency_ - is a measure of the time that passes between sending a network resource request and receiving a response
3. Transmission modes:
   * _Simplex_ -- single flows in **ONE** direction and **ONLY** one node transmit and the other receives.
   * _Half Duplex_ -- each node can transmits and receive but **NOT** at the same time.
   * _Full Duplex_ -- both nodes transmit and receive simultaneously.

## Ways of connections.

The way of connection of nodes in a network called _topology_. It could be a simple connection between two nodes to complex layouts of nodes.

Base types of topology:

1. Point-to-Point. Its type is described by **direct communication between two nodes** with a common link. Transfer data going in multiple ways: Simplex, Half Duplex or Full Duplex.
![point-to-point](https://www.myworkingnet.com/wp-content/uploads/2021/02/Point-to-Point-Network-Topology.png)
2. Daisy Chain. Its series of point-to-point connections, when data goes from sender to receiver through internal nodes (they are called _hops_).
![daisy chain](https://i.pinimg.com/originals/db/cc/d1/dbccd1be7e8731070d2fbf888a8807ae.png)
3. Bus. It's when nodes share a common network link (known as _backbone_). All nodes get the same traffic and be accessed by any node.
![bus](https://i.pinimg.com/originals/d9/a9/74/d9a97433e7fff183ce32c70f80152720.png)
4. Ring. Its closed loop of daisy chain. Transmission mode is simplex. Aggregate network bandwidth is bottlenecked by the weakest link between two nodes.
![ring](https://www.myworkingnet.com/wp-content/uploads/2021/02/Ring-Topology-1024x645.png)
5. Star. Individual point-to-point connection with the center node (_hub_ or _switch_). The aggregate central bandwidth forms a network bottleneck for large clusters.
![star](https://www.myworkingnet.com/wp-content/uploads/2020/01/Star-topology.png)
6. Mesh. Every node in the network connects to each other.
![mesh](https://www.myworkingnet.com/wp-content/uploads/2021/02/Mesh-Topology-1024x632.png)

## Internet service provider (ISP)

![ISP](https://upload.wikimedia.org/wikipedia/commons/thumb/9/9f/Internet_Connectivity_Access_layer.svg/800px-Internet_Connectivity_Access_layer.svg.png)

An ISP is an organization that provides a service as the access point or the gateway to the internet.

Types of ISP:

1. Access providers -- provide Internet access.
2. Mailbox providers -- provide services for hosting electronic mail domains with access to storage for mail boxes.
3. Hosting ISPs -- email, web-hosting or online storage services (other may include virtual server, cloud services or physical server).
4. Transit ISPs -- _Access provider for Access provider_. ISPs themselves pay upstream ISPs for Internet access.
5. Virtual ISPs -- an operation that purchases services from another ISP.
6. Free ISPs -- a service provider that provides service free of charge.
7. Wireless ISP -- an Internet service provider with a network based on wireless networking.

# Open System Interconnection (OSI) and Transmission Control Protocol (TCP).

The OSI is a conceptual framework used to describe the functions of a networking system. It characterizes computing functions into a universal set of rules and requirements in order to support interoperability between different products and software. The OSI model is split into 7 different layers (from down to up): Physical, Data Link, Network, Transport, Session, Presentation and Application.

It's just a theoretical model that was developed by researchers. It only exists on paper. Meanwhile the internet is based on TCP/IP, which is a "simplified" implementation or inspired by the OSI model.

![OSI](https://media.fs.com/images/community/wp-content/uploads/2017/11/comparison-of-OSI-and-TCPIP.jpg)

The Transmission Control Protocol/Internet Protocol (TCP/IP) model is the conceptual model and set of communications protocols used in the Internet and similar computer networks.

TCP/IP contains 4 layers, whose payloads are also known as segments or datagrams:

1. Link layer -- operate within the scope of the local network connection to which a host is attached. Used to move packets between the Internet layer interfaces of two different hosts on the same link.
2. Internet layer -- a group of protocols, methods and specifications that are used to transport network packets from original host to across network, if necessary, to the destination host specified by an IP address.
3. Transport layer -- establishes basic data channels that applications use for task-specific data exchange.
   * TCP -- a connection-oriented protocol.
   * User Datagram Protocol (UDP) -- a connectionless protocol.
4. Application layer -- includes the protocols used by most applications for providing user services or exchanging application data over the network connection established by the lower lever protocols.

# Conclusion

In that article we talked about computer networking, typologies, and basic networking terms. Also briefly described OSI and TCP/IP models, ISP.

It's just the tip of the iceberg. For future and deeper learning i could recommend:

1. [Computer Networking: A Top-Down Approach](https://www.amazon.co.uk/dp/0133594149)
2. [Computer Networks](https://www.amazon.co.uk/dp/9332518742)
3. [Computer Networking Course - Network Engineering](https://www.youtube.com/watch?v=qiQR5rTSshw)
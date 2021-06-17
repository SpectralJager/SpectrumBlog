+++
author = "Spectral Jager"
categories = ["programming"]
date = 2021-06-16T17:24:45Z
draft = true
img = ""
summary = ""
tags = ["IP", "OSI", "TCP", "Networking"]
title = "Overview of networked systems"

+++
- In the digital age most of devices communicate over computer networks. 
- A computer network is a connections between two or more nodes (computer devices). 
- Not always those connections reliable or secure.
- The way of connection of nodes in a network called topology. From simple single connection btw two nodes to complex layouts of nodes.
- base types of topology
	- point ot point, uncommon, direct communication btw two nodes
    - daisy chain, series of point-to-point, intermediat nodes calls *hops*, uncommon
    - bus, nodes share common network link, uncommon, all nodes get same trafic
    - ring, closed loop, trafic transfer in single direction, if one node on the way will fail transfer data, it will never reach its destination
    - star, individual point-to-point connection with nodes and center node 
    - mesh, every nodes conected to each other
- Bandwidth is the amount of data we can send over a network connection in an interval of time
- Internet service provider (ISP)
- Latency is a measure of the time that passes between sending a network resource request and receiving a response
- Content delivery network (CDN)
- Open system interconnection (OSI)
- Protocols are rules and procured that determine the format and order of data sent over a network
- Transmission control protocol (TCP)
- OSI layers
	7. Applicaton layer
    6. Presentation layer, preper data for network layer and present data for application layer
    5. Session layer, manage the connection life cycle btw nodes on a network
    4. Transport layer, controls and coordinates the transfer of data btw two nodes thile maintaining the reliability of the transfer
    3. Network layer, responsible for transmiting data btw nodes
    2. Data link layer, habdles data transfers btw two directly connected nodes
    1. Physical layer, converst bits from the network stack to electrical/optic/radio signals suitable for the underlying physical medium and from the physical medium back into bits
- transmission rate is mesering in bits per second
- bytes per second use when describes amount of transfered data
- Encapsulation is a method of hiding implementation details or making onlyrelevant details available to the recipient
- payload/message body/service data unit is data that traveling down the stack
- When the payload moves up the stack, each layer strips the header information from the previous stack
- horizontal communication is communicaton btw server and client on the same layer
- TCP is a layer 4 protocol, whose payloads are also knows as segments or datagrams
- Internet Protocol (IP) at layer 3, payload is known as a packet
- Layer 2 payload known as frame
- Media acccess control (MAC) is a unique name for node's network interface
- Frame check sequence (FCS) is a checksum to facilitate error detection
- TCP/IP using end-to-end principle
- TCP layers
	1. Application layer { Application, Presentation, Session }
    2. Transport layer
    3. Internet/Network layer
    4. Link layer { Data, Physical }


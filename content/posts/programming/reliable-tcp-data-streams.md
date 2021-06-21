+++
author = "Spectral Jager"
categories = ["programming"]
date = 2021-06-21T07:46:57Z
img = "https://www.meme-arsenal.com/memes/fa883143a2e966b506f2f80b272a36d6.jpg"
summary = "TCP allows you to reliably stream data between nodes on a network, because it overcomes the effects of packet loss or receiving packet out of order."
tags = ["Networking", "TCP"]
title = "Reliable TCP data Streams"

+++
TCP allows you to reliably stream data between nodes on a network, because it overcomes the effects of packet loss or receiving packet out of order.

TCP session allows you to deliver a stream of data of any size to a recipient and receive confirmation that the recipient received the data.

TCP connection uses a three-way handshake to introduce the client to the server and then server to the client. The handshake creates an established TCP session over which the client and server exchange data:

* As the first step of the handshake, the client sends a packet with the synchronize (SYN) flag to the server.
* Next, the server responds with its own packet, with both the acknowledgment (ACK) and SYN flags set.
* At the end the client replies with an ACK packet to acknowledge the server’s SYN packet, completing the three-way handshake.

The receive buffer is a block of memory reserved for incoming data on a network connection.

The window size is the number of bytes the sender can transmit to the receiver buffer without requiring an acknowledgment.

For gracefully terminating TCP connection either side should initiate the termination sequence by sending a finish (FIN) packet.
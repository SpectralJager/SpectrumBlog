+++
author = "Spectral Jager"
categories = ["programming"]
date = 2021-06-19T07:53:36Z
img = "https://sitechecker.pro/wp-content/uploads/2019/04/ip-address.png"
summary = "The Internet Protocol (IP) is a set of rules that dictate the format of data sent over a network -- specifically, the Internet."
tags = ["Networking", "IP"]
title = "Notes: Resource location and traffic routing"

+++
The Internet Protocol (IP) is a set of rules that dictate the format of data sent over a network -- specifically, the Internet. IP addresses identify nodes on a network at the internet layer of the TCP/IP stack, and you use them to facilitate communication between nodes. Function of IP addresses as like postal addresses: nodes send packets to other nodes by addressing packets to the destination node’s IP address. Also packet headers include the IP address of the origin node as well.

We have two versions of IP addresses in use: IPv4 and IPv6.

# IPv4 Addressing

IPv4 addresses are 32-bit numbers arranged in four groups of 8 bits (octets) separated by decimal points and in  a result give us over four billion possible addresses.

> RFCs use the term ‘octet’ as a disambiguation of the term ‘byte’, because a bute’s storage size has historically been platform dependent.

IPv4 contains two components: 
a network ID -- informs the network devices (routers) responsible for shuttling packets toward their destination about the next appropriate hop in the transmission.
a host ID -- like your street address. It identifies a group of nodes whose address is part of the same network.

IPv4’s network and host IDs allow you to subdivide the modre than four billion IPv4 addresses into smaller groups. Subnets are all IP addresses in these smaller networks, share the same network ID but have unique host IDs. The size of the network dictates the number of host IDs and the number of individual IP addresses in the network.

Classless Inter-Domain Routing (CIDR) allows you to allocate networks by indicating the number of bits in the network ID by appending a network prefix to each IP address, consisting of forward slash and an integer (192.168.0.1/16). 

> RFC 1918 details the private address space of 10.0.0.0/8, 172.16.0.0/12, 192.168.0.0/16 for use in local networks. Also each host has the 127.0.0.0/8 subnet designated as its local subnet ( also known as ‘localhost’)

## Ports and Socket addresses

The OS uses ports to uniquely identify data transmission between nodes for the purposes of multiplexing the outgoing application data and demultiplexing the incoming data back to the proper application.

Ports are 16-bit unsigned integers. From 0 to 1023 are well known as assigned to common service by the Internet Assigned Numbers Authority (IANA). 1024 - 49151 for lesser common services, 49152 - 65532 for client socket addresses.

## Network Address Translation

The way to address the Ipv4 shortage is by using Network Address Translation (NAT), a process that allows numerous nodes to share the same public IPv4 address. For it you need a firewall, load balancer or router.

## Unicasting, Multicasting, Broadcasting

unicating is sending packets from one IP address to another IP address
multicasting is sending a single message to group of nodes
broadcasting is sending a message to all nodes in a network.

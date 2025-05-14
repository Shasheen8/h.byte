---
title: What is Subnetting?
date: Wed, 10 Nov 2021 14:30:00 +0000
---
When connected to the internet, every device is assigned a unique IP address. A network is more efficient as a delivery service when a message travels with as few hops as possible. When data packets travel between networks, they will be routed by subnets so that the data packets take an efficient route to their final destination. An IP address determines the address of the data packet, whether it be at the source or destination. Every Ip address has two parts and the first part indicates the network the address belongs to, and the second shows the device in the network. However, the first part of an IP address can change based on its network class. So if an IP address makes it simple for the internet router to find the right network for data to route into, why do we need Subnetting?A million devices could be connected to a particular network. It could take several hops and significant time for the data to reach the correct address, which is where subnetting comes in handy. Subnetting trims down the IP addresses to practice within a range of devices. Subnetting helps in organizing the network to overcome network congestion. When network traffic increases within parts of the network, it groups these parts into one section so that the traffic does not unnecessarily hop across the entire network. Subnetting also efficiently designates IP addresses and prevents a vast number of IP addresses from going unused. How do we use subnetting? 

Given an IP Address. 
Example: 30.40.200.120

An address is made of 32 binary bits divisible in a network piece and host piece with the help of a subnet mask. 

32 bits are divided into four octets. Each is separated by a period (.), and the octet holds a value of 2^0

Binary octets convert to decimal. 

    1     1      1     1     1     1     1    1

  128    64     32    16     8     4     2    1

IP addresses represented as binary and decimal

        30.       40.      200.      120     

  00011110. 00101000. 11001000. 01111000
IP addresses are divided into three classes: A, B, and C.Class A: IP addresses lie between 0.0.0.0 and 127.255.255.255.Class B: IP addresses lie between 128.0.0.0 and 191.255.255.255.Class C: IP addresses lie between 192.0.0.0 and 223.255.255.255.These IP address classes help formulate subnet masking. Based on classes A, B, C, here are the default masks:Class A: 255.0.0.0Class B: 255.255.0.0Class C: 255.255.255.0Subnetting creates several logical networks that live within a single class network. When a major network is separated into smaller subnets, it establishes an interconnecting subnetwork. For example:

Given a class C network of 215.20.9.0, the natural subnet mask would be 255.255.255.0215.20.9.0       - 11010111.00010100.00001001.00000000

255.255.255.224  - 11111111.11111111.11111111.11100000

                   --------------------------|sub|----

With the three bits from the original portion, it creates eight subnets. With the remaining five host ID bits, each subnet can have up to 32 host addresses, 30 of which can be assigned to a device as hosts ids of all zeros or all ones are not allowed.

215.20.9.0 255.255.255.224 host address range 1 to 30

215.20.9.32 255.255.255.224 host address range 33 to 62

215.20.9.64 255.255.255.224 host address range 65 to 94

215.20.9.96 255.255.255.224 host address range 97 to 126

215.20.9.128 255.255.255.224 host address range 129 to 158

215.20.9.160 255.255.255.224 host address range 161 to 190

215.20.9.192 255.255.255.224 host address range 193 to 222

215.20.9.224 255.255.255.224 host address range 225 to 254

The more bits one uses in the subnet, the more subnets there will be available.
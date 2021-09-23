# The internet

## What to know

* Network communication forms the basis of how networked applications function
* Communication between networked applications can be thought of as the interaction of multiple different protocols (i.e., system of rules)

## Focal points

* Build a general picture of the network infrastructure
  * Have a high-level picture of how the network infrastructure functions
* Be aware of the limitations of the physical network
  * Higher-level protocols (i.e., TCP, HTTP) rely on the underlying network infrastructure to function
  * They are bound to the limitations of that infrastructure, such as network bandwidth and latency
* Understand that protocols are system of rules
  * Protocols are logical sets of rules that facilitate network functionality
* Learn that IP enables communication between devices
  * The Internet Protocol (IP) is a key part of internet functionality

## Internet

* The internet is a network of networks
* A **network**, at the most basic level, is two devices connected in such a way that they can communicate and exchange data
* A **local area network** is multiple computers connected via a network bridging device, such as a hub or switch
  * As a side note, [most home routers are a combination of three networking components: router, a firewall, and a switch](https://www.howtogeek.com/99001/htg-explains-routers-and-switches/)
  * Also, historically, people relied on hubs because they were cheaper
  * The hub sends frames to every single device, which isn't very efficient
  * A switch ensures the frame is sent only to the intended device
  * The low price of hubs is due to hubs not examining or managing any of the incoming traffic
  * Very few hubs are even still manufactured
* Routers enable **inter-network communication** by directing network traffic to other networks
* The internet is the conglomeration of all these networks

## Protocols

* Protocols are a set of rules governing the exchange or transmission of data
* Protocols ensure networks of disparate components can communicate
* There are numerous different protocols that are used to communicate over the internet, such as IP, TCP, HTTP, Ethernet
* Different protocols can address different aspects of network communication, or address the same aspect in a different way or a specific use-case
* Protocols that address the same aspect can be thought of as groups, with *layers* of groups in an overall system
* For instance, in the case of human speech:
  * *Syntactical rules* that govern the *structure* (i.e., order of words) in a message
  * *Message transfer rules* that control the *flow* and *order* of a message
    * There could be variations for classroom settings or conversation with friends
* For networks, there are two popular models:
  * OSI
    * 7 layers — Application, Presentation, Session, Transport, Network, Data Link, Physical
    * Grouped in terms of function
  * Internet Protocol Suite (i.e/, TCP/IP or DoD)
    * 4 layers — Application, Transport, Internet, Link
    * Grouped in terms of communication scope

![Protocols in networked applications](https://da77jsbdz4r05.cloudfront.net/images/ls170/layered-system-osi-tcp-ip-comparison.png)

* A Protocol Data Unit (i.e., PDU) is an amount or block of data transferred over a network
* Different protocol layers refer to PDUs by different names
  * At the Data Link/ Link layer, PDU is known as a frame
  * At the Network/ Internet layer, PDU is known as a packet
  * At the Transport layer, PDU is known as a segment or datagram
* PDU consists of a header, a data payload, and in some cases a trailer／footer
  * The header and trailer provides protocol-specific metadata about the PDU
    * The Internet Protocol (IP) packet header contains the source and destination IP address
  * Data payload is the data for the specific protocol
    * Data payload is how encapsulation in network models is implemented
    * The entire PDU for a protocol is encapsulated in the data payload of a PDU for a layer below
    * For example, the HTTP request at the Application layer is encapsulated in the payload of a TCP segment at the Transport layer
    * This creates separation between protocols at different layers, which provides a level of abstraction (i.e., different protocols can be utilized without concerning about the layers below)
    * The lower layer is providing a 'service' to the layer above

![PDU](https://da77jsbdz4r05.cloudfront.net/images/ls170/layered-system-encapsulation.png)

## Layers of protocols

* Physical network layer:
  * The physical network (layer 1 of OSI) consists of tangible pieces like networked devices, cables, wires. Even radio waves in wireless networks exist in the physical realm
  * This level involves real-world limitations like the speed of light or the distance a radio wave can reach
  * These limitations determine the physical characteristics of a network, which influences how higher-level protocols function
  * This layer is concerned with the transfer of bits (i.e., binary data)
  * Performance characteristics:
    * Latency — the time it takes from data to get from point A to B
    * Bandwidth — the amount of data that can be sent in a particular unit of time (typically 1 second)
  * Latency can also be thought of as measure of delay, and can be thought of as the sum of all the delays below:
    * Propagation delay — [amount of time it takes for the first bit to travel from sender to receiver](https://www.apposite-tech.com/blog/latency/)
    * Transmission delay — [amount of time it takes to push all packets into the wire](https://en.wikipedia.org/wiki/Transmission_delay)
    * Processing delay — [amount of time it takes routers to process the packet header](https://en.wikipedia.org/wiki/Processing_delay)
    * Queuing delay — [amount of time the data waits in queue](https://en.wikipedia.org/wiki/Queuing_delay)
  * Some other terms:
    * Last-mile latency — the delays that occur closest to the end point
      * At the network edge, the hops are frequent and shorter
      * It can be thought of as the entry point into a network like a home or corporate LAN
    * Round-trip Time (RTT) — length of time for a signal to be sent added to the length of time of an acknowledgement to be received
  * Hops — The journey of a piece of data consists of 'hops' between nodes. These nodes are routers that process and forward the data
  * The bandwidth a connection receives is the lowest amount (i.e., bottleneck) of the overall connection
* Link/ data link layer:
  * The most commonly used protocol at this layer is the Ethernet protocol
  * The two most important aspects are **framing** and **addressing**
  * Ethernet Frames:
    * Ethernet frames are PDUs, and encapsulate data from the Internet/ Network layer above
    * Ethernet frame adds logical structure to the binary data at the physical layer
    * Components of a frame:
      * Preamble and SFD — non-official components that notifies the receiving device to expect frame data
      * Source and destination MAC address
        * The MAC address is linked to a physical device and usually doesn't change
        * It is a 'burned-in' address
      * Length — Indicates the size of the data payload
      * DSP, SSAP, Control: Identifies the network protocol used in the data payload
      * Data payload — Encapsulated PDU for the Internet/ Network layer
      * Frame Check Sequence — checksum to ensure entire frame is received (no retransmission function)
    * There is an interframe gap (IFG) between transmission of each frame (approx one millionth of a second)
    * The differences between ethernet standards are not significant
* Internet/ Network layer:
  * The Internet Protocol (IP) is the predominant protocol used in this layer
  * IP is used to route data between different networks
  * The layer exists because MAC address aren't scalable:
    * They are physical rather than logical (i.e., each address is tied to a specific device, meaning that if the location of a device changes it is hard to track)
    * They are flat rather than hierarchical (i.e., it cannot be broken down into sub-divisions)
  * The protocol allows for:
    * Rerouting capability via IP addressing
    * Encapsulation of data into packets
  * Components of a data packet:
    * Header
      * Version — IPv4 or IPv6
      * ID, Flags, Fragment Offset — relating to fragmentation of a Transport PDU that is too large
      * Time to Live (TTL) — Maximum hops before a packet is dropped
      * Protocol — Protocol for data payload (e.g., TCP, UDP)
      * Checksum — Drops packet if checksums don't align (no retransmission function)
      * Source Address — 32-bit IP of sender
      * Destination Address — 32-bit IP of receiver
    * Data payload — encapsulation of the TCP segment/ UDP datagram from the Transport layer
  * IP address is a unique address used to identify a device or *host* on the internet
  * IP addresses are logical in nature as they are not tied to a specific device, and can be assigned to devices as they join a network
    * Range is defined by a network hierarchy, where overall network is split into logical subnetworks
  * IPv4 address are 32 bits in length, and divided into four sections of eight bits each
    * Each section ranges from `0` to `255` since 2 to the power of 8 is 256
    * Total number of possible IPv4 addresses is 4.3 billion (2 to the power of 32)
  * IPv6 uses 128-bit addresses (eight 16-bit blocks, which is hexadecimal)
    * This is due to the IPv4 addresses eventually being depleted
  * The network address is used to identify a specific network segment
  * The splitting of a network into parts is referred to as sub-netting
    * All routers store a local routing table

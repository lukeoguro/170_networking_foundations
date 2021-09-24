# The transport layer

## What to focus on

* Learn how transport layers protocols enable communication between processes
  * Spend time learning what multiplexing and demultiplexing are
  * Learn how ports work with IP addresses to provide this functionality
* Learn that network reliability is engineered
  * The internet 'works' because of technologies that have been designed and engineered
* Understand the trade-offs
  * Learn about TCP and UDP and their trade-offs

## Transport layer

* IP provides the infrastructure for inter-network communication between *hosts*
* The transport layer provides end-to-end communication between applications
* The idea of transmitting multiple signals over a single channel is *multiplexing*
* *Multiplexing* takes place through network ports
* Ports are identifiers for a specific process running on a host
* All PDUs include source and destination ports in the header
* A socket can be thought of as the combination of IP address and port number (i.e., communication end-point)
* At the implementation level, a socket can be a mechanism for local/ inter-process communication
* Implementation of sockets become socket objects, using the Berkley sockets API model with commands like `bind()`, `listen()`, `accept()`, `connect()`
* Sockets can be used to make connections, which helps with understanding the difference between connection-oriented communication and connectionless communication
* A connectionless system processes any incoming messages as they arrive and send any responses as necessary with `listen()`
* A socket object establishes a connection-oriented system, and allows for order of messages, acknowledgements of receipt, retransmissions, etc.

## TCP

* Lower layers of network systems are inherently unreliable
* Specifically, Ethernet and IP have checksums but simply drop the data if it is corrupt
* Stop-and-wait protocol covers fundamental elements for reliable data transfer:
  * In order delivery — data is received in the order that it was sent
  * Error detection (data integrity) — corrupt data is identified with checksum
  * Handling data loss (retransmission of lost data) — missing data is retransmitted based on acknowledgements and timeouts
  * Handling duplication (de-duplication) — duplicate data is eliminated using sequence numbers
* Multiple messages can be sent at the same time to pipeline for performance (i.e., *pipelining*)
  * There is the Go-Back-N and Selective Repeat approach
* TCP provides abstraction for reliable network communication and hides complexity from application layer
* Segments are the PDU of TCP, and have important components in the header that ensures reliability:
  * Checksum — used for error detection
  * Sequence number and acknowledgement number — used for in-order delivery, handling data loss, and handling duplication
* TCP is connection-oriented, establishes connection with a Three-way handshake with `SYN` and `ACK` flags, and terminates with the Four-way handshake with `FIN`
* Sender cannot send any application data until `ACK` segment is sent — this means there is a round-trip of latency before any data can be sent
* TCP provides mechanisms for:
  * Flow control — mechanism to prevent sender from overwhelming receiver
    * WINDOW field of header shows how much data the sender should send
  * Congestion avoidance — mechanism to prevent sender/receiver from overwhelming underlying network
    * Network congestion occurs when there is more data being transmitted than there is network capacity for processing and transmitting
    * If there are many dropped data packets and retransmission, TCP reduces transmission window
* TCP has some disadvantages:
  * Latency overhead due to handshake process
  * HOL (Head-of-Line) blocking — relates to issues in delivering or processing messages in a sequence
    * While in-order delivery is an aspect of TCP reliability, any retransmission causes later segments to be buffered, which leads to increased queuing delay

## UDP

* PDU of UDP is Datagram
  * Header has only four fields of Source port, destination port, length, checksum
* No guarantee for message delivery, delivery order, congestion avoidance or flow-control mechanisms, no connection state tracking
* Advantages:
  * Speed — Less latency without handshake and HOL blocking
  * Flexibility — choose how to deal with features at the application level
* Video calling applications and video games are examples

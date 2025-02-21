
# Computer Networks and the Internet
## What is Internet ?
### Nut and Bolts description
- The internet is a computer network that connects billions of computing devices throughout the world.
- End systems or hosts are connected together by a network of `communication links` and `packet switches`
- One end system sends packages of information to the other end system which are known as `packets` and are reassembled to original data at the destination end system
- A packet switch takes a packet arriving on one of its incoming communication links and forwards that packet on one of its outgoing communication links.
- Two most prominent types in today's Internet are `routers` and `link-layer siwtches` 
- Link layers switches are used in access networks, while router are typically used in network core.
- End system access the internet through `Internet service provider (ISPs)`
- Internet run protocols that control the sending and receiving of information within the internet.
- The `Transmission Control Protocol (TCP)` and `Internet Protocol (IP)` are two most important protocols in the internet.
- The IP protocol specifies the format of the packets that are sent and received among routers and end systems.
- Internet standards are developed by the Internet Engineering Task Force. The IETF standard documents are called as `request for comments (RFCs)`
### Services Description
- We can also describe the Internet as an infrastructure that provides services to applications.
- The applications are said to be `distributed applications` since they involve multiple end systems that exchange data with each other
- End systems attached to the Internet provide a `socket interface` that specifies how a program running on one end system asks the Internet infrastructure to deliver data to a specific destination program running on another end system.
### What is Protocol
- Can be simply understood as a set of rules that are followed in manner to have or initiate a communication between two computers
- All activity in the Internet that involves two or more communicating remote entities are governed by a protocol
- A  `protocol` defines the format and the order of messages exchanged between tow or more communicating entities, as well as the actions taken on the transmission and/or receipt of a message or other event
## The Networking Edge
### Access Network
- The network that physically connects an end system to the first router also known as the edge router on a path from end system to other distant end system
- DSL ( Digital Subscriber Line) DSLAM (Digital Subscriber Line Access Multiplexer)
- CMTS ( Cable Modem Termination system)
### Physical Media
- For each transmitter-receiver pair, the bit is sent by propagating electromagnetic waves or optical pulse across a `physical medium`
- `guided media` : the waves are guided along a solid medium. With unguided media , the waves propagate in the atmosphere and in outer space
- Twisted-Pair copper wire
	- Telephone wires
- Coaxial Cable
	- TV cable
	- Coaxial cable can be used as a guided `shared medium`
- Fiber Optics
- Terrestrial Radio channels
- Satellite Radio channels
## The Network Core
### Packet switching
- Packets are transmitted over each communication link at a rate equal to the full transmission rate of the link. So if a source end system or a packet switch is sending a packet of L bits over a link with transmission rate R bits/sec then the time to transmit the packet is L/R seconds
#### Store and Forward Transmission
- Store and forward transmission means that the packet switch must receive the entire packet before it can begin to transmit the first bit onto the outbound link.
#### Queuing Delays and Packet Loss
- Each packet switch has multiple links attached to it . For each attached link , the packet switch has an output buffer ( also called as output queue ), which stores packets that the router is about to send into that link.
- If an arriving packet needs to be transmitted onto a link but finds the link busy with the transmission of another packet, the arriving packet must wait in the output buffer. Thus suffers `queuing delays`.
- Since the amount of buffer space is finite, an arriving packet may find that the buffer is completely full with other packet waiting for transmission. In this case `packet loss` will occur - either the arriving packet or one of the already queued packets will be dropped.
#### Forwarding Tables and Routing Protocols
- When a packet arrives at a router in the network , the router examines a portion of the packet's destination address and forwards the packet to an adjacent router. More specifically, each router has a `forwarding table` that maps destination address to that router's outbound links.
- Internet has a number of special `routing protocols` that are used to automatically set the forwarding tables.
### Circuit Switching
- In circuit switched network, the resources needed along a path (buffers, link, transmission rate) to provide for communication between the end systems are reserved for the duration of the communication session between the end systems.
#### Multiplexing in circuit-switched networks
- A circuit in a link is implemented with either `frequency-divison multiplexing (FDM)` or `time-divison multiplexing (TDM)`
- Proponents of packet switching have always argued that circuit switching is wasteful because the dedicated circuits are idle during `silent periods`
## Delay, Loss, and Throughput in Packet-Switched Networks
- The most important delays are `nodal processing delay` , `transmission delay` , `propagation delay` and together , these delays accumulate to give a `total nodal delay`
- The time required to examine the packet's header and determine where to direct the packet is part of `processing delay` typically in microseconds
- At the queue, the packet experiences a `queuing delay` as it waits to be transmitted onto the link typically microseconds to milliseconds
- `Transmission delay` is L/R typically microseconds to milliseconds
- The time required to propagate from the beginning of the link to router X is `propagation delay` typically in order of milliseconds
## Protocol Layers and Their Service Models
### Protocol Layering
- Network designer organize protocols and the network hardware and software that implements the protocols in layers. 
- The service that a layer offers to the layer above  the so called `service model` of a layer.
### Application Layer
- HTTP Protocol ( for web document request and transfer)
- SMTP ( transfer of e-mail messages )
- FTP ( which provides for the transfer of files between two end systems )
### Transport Layer
- Two transport protocols TCP and UDP
### Network Layer
- The Internet's network layer is responsible for moving network-layer packets known as `datagram` from one host to another
- Includes IP protocol 
### Link Layer
### Physical Layer


# APPLICATION LAYER
## Principles of Network Applications
### Network Application Architectures
- The application architecture is completely different from the network architecture and is designed by the application developer and dictates how the application is structured over the various end systems
- Mostly either it would be `client server` architecture or it would be `P2P peer-to-peer` architecture
- In a client server architecture , there is an always-on host called the sever which services requests from many other hosts called clients
- Characteristic of the client-server architecture is that the server has a fixed, well-known address, called an `IP address`
- In a `P2P architecture` there is minimal (or no) reliance on dedicated server in data centers. Instead the application exploits direct communication between pairs of intermittently connected hosts, called peers
- The peers are not owned by the service provider , but are instead desktops and laptops controlled by users.
- Because the peers communicate without passing through a dedicated server , the architecture is called peer-to-peer.
### Process Communicating 
- In context of a communication session between a pair of processes , the process that initiates the communication ( that it , initially contacts the other process at the beginning of the session ) is labeled as the client. The process that waits to be contacted to begin the session is the server.
- A process sends message into, and receives messages from , the network through a software interface called a `socket`.
- A socket is the interface between the application layer and the transport layer within the host > It is also referred to as the `Application Programming Interface (API)` between the application and network.
- The application developer has control of everything on the application-layers side of the socket but has little control of the transport layer side of the socket. The only control the developer has on the transport layer side is the choice of transport protocol and perhaps the ability to fix few transport layer parameters such as that the maximum buffer size and maximum segment size.
- `IP address` acts as the Address for the host to which the message is intended to sent and the `Port no` acts as the Address for the process within the intended host the message is to be sent
### Transport Services Available to Applications
- We can broadly classify the possible services along four dimensions : reliable data transfer , throughput , timing and security.
### Transport Services Provided by the Internet
#### TCP services
- The TCP service model includes a connection-oriented service and a reliable data transfer service. When an application invokes TCP and its transport protocol, the application receives both of these services from TCP.
- Connection-oriented service. TCP has the client and server exchange transport layer control information with each other before the application-level messages begin to flow. This so-called handshaking procedure alerts the client and server, allowing them to prepare for an onslaught of packets. After the handshaking phase, a TCP connection is said to exist between the sockets of the two processes. The connection is a full-duplex connection in that the two processes can send messages to each other over the connection at the same time. When the application finishes sending messages, it must tear down the connection.
- Reliable data transfer service. The communicating processes can rely on TCP to deliver all data sent without error and in the proper order. When one side of the application passes a stream of bytes into a socket, it can count on TCP to deliver the same stream of bytes to the receiving socket, with no missing or duplicate bytes.
- TCP also includes a congestion-control mechanism, a service for the general welfare of the Internet rather than for the direct benefit of the communicating processes. The TCP congestion-control mechanism throttles a sending process (client or server) when the network is congested between sender and receiver. TCP congestion control also attempts to limit each TCP connection to its fair share of network bandwidth.
#### UPD services
- UDP is a no-frills, lightweight transport protocol, providing minimal services. UDP is connectionless, so there is no handshaking before the two processes start to communicate. UDP provides an unreliable data transfer service—that is, when a process sends a message into a UDP socket, UDP provides no guarantee that the message will ever reach the receiving process. Furthermore, messages that do arrive at the receiving process may arrive out of order.
- UDP does not include a congestion-control mechanism, so the sending side of UDP can pump data into the layer below (the network layer) at any rate it pleases. (Note, however, that the actual end-to-end throughput may be less than this rate due to the limited transmission capacity of intervening links or due to congestion).

**Today's internet can often provide satisfactory service to the time-sensitive applications, but it cannot provide any timing or throughput guarantees.**
### Application Layer Protocols
- An application-layer protocol defines how an application’s processes, running on different end systems, pass messages to each other.
- Some application-layer protocols are specified in RFCs and are therefore in the public domain. For example, the Web’s application-layer protocol, HTTP (the Hyper-Text Transfer Protocol)
- It is important to distinguish between network applications and application-layer protocols. An application-layer protocol is only one piece of a network application
## The Web and HTTP
### Overview of HTTP
- HTTP is implemented in two programs: a client program and a server program
- The client program and server program, executing on different end systems, talk to each other by exchanging HTTP messages
- HTTP defines the structure of these messages and how the client and server exchange the messages
- A Web page (also called a document) consists of objects. An object is simply a file—such as an HTML file, a JPEG image, a Javascript file, a CCS style sheet file, or a video clip—that is addressable by a single URL
- HTTP uses TCP as its underlying transport protocol (rather than running on top of UDP).
- It is important to note that the server sends requested files to clients without storing any state information about the client.
- Because an HTTP server maintains no information about the clients, HTTP is said to be a `stateless protocol`
### Non-persistent vs Persistent Connections
- we define the `round-trip time (RTT),` which is the time it takes for a small packet to travel from client to server and then back to the client.
### HTTP Message Format
- There are two types of HTTP messages, request messages and response messages
- The first line of an HTTP request message is called the `request line` ; the subsequent lines are called the `header lines`.
- The request line has three fields: the method field, the URL field, and the HTTP version field
- Response message has three sections: an initial status line, six header lines, and then the entity body.
### User - Server Interaction : Cookies
- HTTP uses cookies. Cookies, defined in [RFC 6265], allow sites to keep track of users.
- Cookie technology has four components:
	- a cookie header line in the HTTP response message
	- a cookie header line in the HTTP request message
	- a cookie file kept on the user’s end system and managed by the user’s browser
	- a back-end database at the Web site.
- Think of cookie as a anonymous user identity stored and understood by an server as a cookie for identification
### Web Caching 
- A Web cache—also called a proxy server—is a network entity that satisfies HTTP requests on the behalf of an origin Web server.
- The Web cache has its own disk storage and keeps copies of recently requested objects in this storage.
- HTTP has a mechanism that allows a cache to verify that its objects are up to date. This mechanism is called the conditional GET [RFC 7232].
- An HTTP request message is a so-called conditional GET message if (1) the request message uses the GET method and (2) the request message includes an `If-Modified-Since`: header line.
### HTTP/2
- The primary goals for HTTP/2 are to reduce perceived latency by enabling request and response multiplexing over a single TCP connection, provide request prioritization and server push, and provide efficient compression of HTTP header fields.
- HTTP/2 changes how the data is formatted and transported between the client and server.
- sending all the objects in a Web page over a single TCP connection has a Head of Line (HOL) blocking problem
- One of the primary goals of HTTP/2 is to get rid of (or at least reduce the number of) parallel TCP connections for transporting a single Web page
- The HTTP/2 solution for HOL blocking is to break each message into small frames, and interleave the request and response messages on the same TCP connection
- The ability to break down an HTTP message into independent frames, inter leave them, and then reassemble them on the other end is the single most important enhancement of HTTP/2.
- The framing is done by the framing sub-layer of the HTTP/2 protocol.
- Message prioritization allows developers to customize the relative priority of requests to better optimize application performance.
- the framing sub-layer organizes messages into parallel streams of data destined to the same requestor. 
- When a client sends concurrent requests to a server, it can prioritize the responses it is requesting by assigning a weight between 1 and 256 to each message. The higher number indicates higher priority. 
- Using these weights, the server can send first the frames for the responses with the highest priority. In addition to this, the client also states each message’s dependency on other messages by specifying the ID of the message on which it depends.
- Another feature of HTTP/2 is the ability for a server to send multiple responses for a single client request. That is, in addition to the response to the original request, the server can push additional objects to the client, without the client having to request each one
### HTTP/3
- QUIC, discussed in Chapter 3, is a new “transport” protocol that is implemented in the application layer over the bare-bones UDP protocol. QUIC has several features that are desirable for HTTP, such as message multiplexing (interleaving), per-stream flow control, and low-latency connection establishment
## Electronic Mail in the Internet
- Internet mail system has three major components: `user agents`, `mail servers`, and the `Simple Mail Transfer Protocol (SMTP)`
- User agents allow users to read, reply to, forward, save, and compose messages.
- Mail servers form the core of the e-mail infrastructure
- SMTP is the principal application-layer protocol for Internet electronic mail. It uses the reliable data transfer service of TCP to transfer mail from the sender’s mail server to the recipient’s mail server
## DNS - The Internet's Directory Service
- One identifier for a host is its `hostname`. hosts are also identified by so-called `IP addresses`.
- An IP address consists of four bytes and has a rigid hierarchical structure
- An IP address is hierarchical because as we scan the address from left to right, we obtain more and more specific information about where the host is located in the Internet
### Services Provided by DNS
- This is the main task of the Internet’s domain name system (DNS). The DNS is :
	- a distributed database implemented in a hierarchy of DNS servers
	- an application-layer protocol that allows hosts to query the distributed database. 
	- The DNS servers are often UNIX machines running the Berkeley Internet Name Domain (BIND) software [BIND 2020]. The DNS protocol runs over `UDP` and uses port 53.
- DNS provides a few other important services in addition to translating host names to IP addresses:
	- `Host Aliasing` : can provide more mnemonic hostname for canonical hostnames
	- `Mail server aliasing`
	- `Load distribution` : alias hostname can have multiple servers and DNS on request could send multiple addresses but rotates the ordering of the addresses within each reply.
### Overview of How DNS Works
- Centralized Design of DNS would have these following issues
	- A single point of failure
	- Traffic Volume
	- Distant Centralized database
	- Maintenance
- In order to deal with the issue of scale, the DNS uses a large number of servers, organized in a hierarchical fashion and distributed around the world.
- To a first approximation, there are three classes of DNS servers—root DNS servers, top-level domain (TLD) DNS servers, and authoritative DNS servers—organized in a hierarchy
### DNS Records and Messages
- The DNS servers that together implement the DNS distributed database store resource records (RRs), including RRs that provide hostname-to-IP address mappings
- A resource record is a four-tuple that contains the following fields: `(Name, Value, Type, TTL)`
- TTL is the time to live of the resource record
- The meaning of Name and Value depend on Type:
	- if Type = A the name is a hostname and value is the IP address for the hostname
	- if Type = NS the name is a domain and the value is the hostname for the authoritative DNS server 
	- if Type = CNAME the value is a canonical hostname for the hostname Name
	- if Type = MX the value is the canonical name of a mail server that has alias hostname Name
- How would you like to send a DNS query message directly from the host you’re working on to some DNS server? This can easily be done with the `nslookup` program, which is available from most Windows and UNIX platforms.
- A `registrar` is a commercial entity that verifies the uniqueness of the domain name
## Peer-to-Peer File Distribution
- Bit Torrent 
- Rarest first
- 4 unchoked
- 1 optimistically unchoked
## Video Streaming and Content Distribution Networks
- Dynamic Adaptive Streaming over HTTP (DASH)
- Content Distribution Networks (CDNs)
- A CDN manages servers in multiple geographically distributed locations, stores copies of the videos (and other types of Web content, including documents, images, and audio) in its servers, and attempts to direct each user request to a CDN location that will provide the best user experience


# TRANSPORT LAYER

**Residing between the application and network layers, the transport layer is a central piece of the layered network architecture. It has the critical role of providing communication services directly to the application processes running on different hosts.**
## Introduction and Transport-Layer Services
- A transport layer protocol provides for logical communication between application processes running on different host. Could be understood as that the application process don't worry about the physical transfer it only sees the transport layer and nothing beyond that.
- Transport Layer Protocols are implemented in the end systems not in network routers.
- On the sending side, the transport layer converts the application layer messages it receives from a sending application process into transport layer packets, known as transport layer **Segments** 
- It’s important to note that network routers act only on the network-layer fields of the datagram; that is, they do not examine the fields of the transport-layer segment encapsulated with the datagram.
### Relationship between Transport and Network Layers
- A transport-layer protocol provides logical communication between *processes* running on different hosts, a network-layer protocol provides logical- communication between *hosts* 
- The services that a transport protocol can provide are often constrained by the service model of the underlying network-layer protocol
- Nevertheless, certain services can be offered by a transport protocol even when the underlying network protocol doesn’t offer the corresponding service at the network layer.
### Overview of the Transport Layer in the Internet
- The Internet’s network-layer protocol has a name—IP, for Internet Protocol. IP provides logical communication between hosts. The IP service model is a best-effort delivery service. This means that IP makes its “best effort” to deliver segments between communicating hosts, but it makes no guarantees. In particular, it does not guarantee segment delivery, it does not guarantee orderly delivery of segments, and it does not guarantee the integrity of the data in the segments. For these reasons, IP is said to be an unreliable service. We also mention here that every host has at least one network-layer address, a so-called IP address.
- The most fundamental responsibility of UDP and TCP is to extend IP’s delivery service between two end systems to a delivery service between two processes running on the end systems
- Extending host-to-host delivery to process-to-process delivery is called transport-layer multiplexing and demultiplexing
- UDP and TCP also provide integrity checking by including error detection fields in their segments’ headers. These two minimal transport-layer services—process-to-process data delivery and error checking—are the only two services that UDP provides!
- TCP, on the other hand, offers several additional services to applications. First and foremost, it provides reliable data transfer. TCP ensures that data is delivered from sending process to receiving process, correctly and in order. TCP also provides congestion control.
## Multiplexing and Demultiplexing
- Each transport-layer segment has a set of fields in the segment for this purpose. At the receiving end, the transport layer examines these fields to identify the receiving socket and then directs the segment to that socket. This job of delivering the data in a transport-layer segment to the correct socket is called **demultiplexing**.
- The job of gathering data chunks at the source host from different sockets, encapsulating each data chunk with header information (that will later be used in demultiplexing) to create segments, and passing the segments to the network layer is called **multiplexing**.
- UDP socket is fully identified by a two-tuple consisting of a destination IP address and a destination port number.
- One subtle difference between a TCP socket and a UDP socket is that a TCP socket is identified by a four-tuple: (source IP address, source port number, destination IP address, destination port number).
## Connectionless Transport : UDP
- Aside from the multiplexing/demultiplexing function and some light error checking, it adds nothing to IP. UDP takes messages from the application process, attaches source and destination port number fields for the multiplexing/demultiplexing service, adds two other small fields, and passes the resulting segment to the network layer.
- Note that with UDP there is no handshaking between sending and receiving transport-layer entities before sending a segment. For this reason, UDP is said to be connectionless.
- some applications are better suited for UDP for the following reasons :
	- Finer application-level control over what data is sent, and when : UDP sends data immediately once it receives where as TCP has a congestion control mechanism that throttles the transport layer TCP sender when one or more links between the source and destination becomes excessively congested.
	- No connection establishment.
	- No connection state. TCP maintains connection state in the end systems. This connection state includes receive and send buffers, congestion-control parameters, and sequence and acknowledgment number parameters.
	- Small packet header overhead
### UDP Segment Structure
- Source Port , Destination Port , Length , Checksum , Data(message)
- The UDP checksum provides for error detection. That is, the checksum is used to determine whether bits within the UDP segment have been altered as it moved from source to destination.
- UDP at the sender side performs the 1s complement of the sum of all the 16-bit words in the segment, with any overflow encountered during the sum being wrapped around. This result is put in the checksum field of the UDP segment.
- At the receiver, all four 16-bit words are added, including the checksum. If no errors are introduced into the packet, then clearly the sum at the receiver will be 1111111111111111. If one of the bits is a 0, then we know that errors have been introduced into the packet.
- You may wonder why UDP provides a checksum in the first place, as many link-layer protocols (including the popular Ethernet protocol) also provide error checking. The reason is that there is no guarantee that all the links between source and destination provide error checking; that is, one of the links may use a link-layer protocol that does not provide error checking. Furthermore, even if segments are correctly transferred across a link, it’s possible that bit errors could be introduced when a segment is stored in a router’s memory. Given that neither link-by-link reliability nor in-memory error detection is guaranteed, UDP must provide error detection at the transport layer, on an end-end basis, if the end-end data transfer service is to provide error detection
- This is an example of the celebrated **end-end principle** in system design , which states that since certain functionality (error detection, in this case) must be implemented on an end-end basis: *“functions placed at the lower levels may be redundant or of little value when compared to the cost of providing them at the higher level.”*
- Because IP is supposed to run over just about any layer-2 protocol, it is useful for the transport layer to provide error checking as a safety measure. Although UDP provides error checking, it does not do anything to recover from an error.
## Principles of Reliable Data Transfer
- This is appropriate since the problem of implementing reliable data transfer occurs not only at the transport layer, but also at the link layer and the application layer as well.
- With a reliable channel, no transferred data bits are corrupted (flipped from 0 to 1, or vice versa) or lost, and all are delivered in the order in which they were sent. This is precisely the service model offered by TCP to the Internet applications that invoke it.
- It is the responsibility of a **reliable data transfer protocol** to implement this service abstraction. This task is made difficult by the fact that the layer below the reliable data transfer protocol may be unreliable.
### Building a Reliable Data Transfer Protocol
**Self-Note : Practice FSM diagrams when you do the revision again** 
#### Reliable Data Transfer over a perfectly Reliable Channel : rdt1.0
- The protocol itself, which we’ll call rdt1.0, is trivial.
- The sending side of rdt simply accepts data from the upper layer via the rdt_send(data) event, creates a packet containing the data (via the action make_pkt(data)) and sends the packet into the channel. In practice, the rdt_send(data) event would result from a procedure call (for example, to rdt_send()) by the upper-layer application
- On the receiving side, rdt receives a packet from the underlying channel via the rdt_rcv(packet) event, removes the data from the packet (via the action extract (packet, data)) and passes the data up to the upper layer (via the action deliver_data(data)). In practice, the rdt_rcv(packet) event would result from a procedure call (for example, to rdt_rcv()) from the lower layer protocol.
- In this simple protocol, there is no difference between a unit of data and a packet. Also, all packet flow is from the sender to receiver; with a perfectly reliable channel there is no need for the receiver side to provide any feedback to the sender since nothing can go wrong! Note that we have also assumed that the receiver is able to receive data as fast as the sender happens to send data. Thus, there is no need for the receiver to ask the sender to slow down!
#### Reliable Data Transfer over a Channel with Bit Errors: rdt2.0
- A more realistic model of the underlying channel is one in which bits in a packet may be corrupted. Such bit errors typically occur in the physical components of a network as a packet is transmitted, propagates, or is buffered. We’ll continue to assume for the moment that all transmitted packets are received (although their bits may be corrupted) in the order in which they were sent.
- This message-dictation protocol uses both positive acknowledgments and negative acknowledgments. These control messages allow the receiver to let the sender know what has been received correctly, and what has been received in error and thus requires repeating. In a computer network setting, reliable data transfer protocols based on such retransmission are known as ARQ *(Automatic Repeat reQuest)* protocols.
- Fundamentally, three additional protocol capabilities are required in ARQ protocols to handle the presence of bit errors:
	- Error detection - Similar to UDP
	- Receivers Feedback - The Positive ACK and Negative ACK
	- Retransmission - A Packet that is received in error at the receiver will be retransmitted by the sender
- **FSM DIAGRAM HERE rdt2.0**
- Thus, the sender will not send a new piece of data until it is sure that the receiver has correctly received the current packet. Because of this behavior, protocols such as rdt2.0 are known as stop-and-wait protocols.
- Protocol rdt2.0 may look as if it works but, unfortunately, it has a fatal flaw. In particular, we haven’t accounted for the possibility that the ACK or NAK packet could be corrupted!
- Unfortunately, our slight oversight is not as innocuous as it may seem. Minimally, we will need to add checksum bits to ACK/NAK packets in order to detect such errors. The more difficult question is how the protocol should recover from errors in ACK or NAK packets. The difficulty here is that if an ACK or NAK is corrupted, the sender has no way of knowing whether or not the receiver has correctly received the last piece of transmitted data.
- A simple solution to this new problem (and one adopted in almost all existing data transfer protocols, including TCP) is to add a new field to the data packet and have the sender number its data packets by putting a **sequence number** into this field.
- The receiver then need only check this sequence number to determine whether or not the received packet is a retransmission.
- , our fixed version of rdt2.0. The rdt2.1 sender and receiver FSMs each now have twice as many states as before. This is because the protocol state must now reflect whether the packet currently being sent (by the sender) or expected (at the receiver) should have a sequence number of 0 or 1.
- **FSM HERE rdt2.1**
#### Reliable Data Transfer over a Lossy Channel with Bit Error : rdt3.0
- Suppose now that in addition to corrupting bits, the underlying channel can lose packets as well, a not-uncommon event in today’s computer networks
- Two additional concerns must now be addressed by the protocol: how to detect packet loss and what to do when packet loss occurs.
- Here, we’ll put the burden of detecting and recovering from lost packets on the sender. Suppose that the sender transmits a data packet and either that packet, or the receiver’s ACK of that packet, gets lost. In either case, no reply is forthcoming at the sender from the receiver. If the sender is willing to wait long enough so that it is certain that a packet has been lost, it can simply retransmit the data packet.
- But how long must the sender wait to be certain that something has been lost? The sender must clearly wait at least as long as a round-trip delay between the sender and receiver (which may include buffering at intermediate routers) plus whatever amount of time is needed to process a packet at the receiver. In many networks, this worst-case maximum delay is very difficult even to estimate, much less know with certainty. Moreover, the protocol should ideally recover from packet loss as soon as possible; waiting for a worst-case delay could mean a long wait until error recovery is initiated.
- From the sender’s viewpoint, retransmission is a panacea. The sender does not know whether a data packet was lost, an ACK was lost, or if the packet or ACK was simply overly delayed. In all cases, the action is the same: retransmit. Implementing a time-based retransmission mechanism requires a countdown timer that can interrupt the sender after a given amount of time has expired. The sender will thus need to be able to (1) start the timer each time a packet (either a first-time packet or a retransmission) is sent, (2) respond to a timer interrupt (taking appropriate actions), and (3) stop the timer.
- **FSM HERE rdt3.0**
- Because packet sequence numbers alternate between 0 and 1, protocol rdt3.0 is sometimes known as the alternating-bit protocol.
### Pipelined Reliable Data Transfer Protocols
- Protocol rdt3.0 is a functionally correct protocol, but it is unlikely that anyone would be happy with its performance, particularly in today’s high-speed networks. At the heart of rdt3.0’s performance problem is the fact that it is a stop-and-wait protocol.
- Since the many in-transit sender-to-receiver packets can be visualized as filling a pipeline, this technique is known as pipelining. Pipelining has the following consequences for reliable data transfer protocols :
	- The range of sequence numbers must be increased, since each in-transit packet (not counting retransmissions) must have a unique sequence number and there may be multiple, in-transit, unacknowledged packets.
	- The sender and receiver sides of the protocols may have to buffer more than one packet. Minimally, the sender will have to buffer packets that have been transmit ted but not yet acknowledged. Buffering of correctly received packets may also be needed at the receiver, as discussed below.
	- The range of sequence numbers needed and the buffering requirements will depend on the manner in which a data transfer protocol responds to lost, corrupted, and overly delayed packets. Two basic approaches toward pipelined error recovery can be identified: Go-Back-N and selective repeat.
### Go-Back-N (GBN)
- In a Go-Back-N (GBN) protocol, the sender is allowed to transmit multiple packets (when available) without waiting for an acknowledgment, but is constrained to have no more than some maximum allowable number, N, of unacknowledged packets in the pipeline
- **Extended FSM description of the GBN here**
### Selective Repeat (SR)

**TODO : will fill this section later SR AND GBN**
## Connection-Oriented Transport : TCP
### The TCP Connection
- TCP is said to be connection-oriented because before one application process can begin to send data to another, the two processes must first “handshake” with each other—that is, they must send some preliminary segments to each other to establish the parameters of the ensuing data transfer. As part of TCP connection establishment, both sides of the connection will initialize many TCP state variables associated with the TCP connection.
- The TCP “connection” is not an end-to-end TDM or FDM circuit as in a circuit switched network. Instead, the “connection” is a logical one, with common state residing only in the TCPs in the two communicating end systems. Recall that because the TCP protocol runs only in the end systems and not in the intermediate network elements (routers and link-layer switches), the intermediate network elements do not maintain TCP connection state. In fact, the intermediate routers are completely oblivious to TCP connections; they see datagrams, not connections.
- A TCP connection provides a **full-duplex service**. A TCP connection is also always *point-to-point,* that is, between a single sender and a single receiver
- The first two segments carry no payload, that is, no application-layer data; the third of these segments may carry a payload. Because three segments are sent between the two hosts, this connection-establishment procedure is often referred to as a **three-way handshake**
- Once the data passes through the door, the data is in the hands of TCP running in the client. TCP directs this data to the connection’s **send buffer**
- From time to time, TCP will grab chunks of data from the send buffer and pass the data to the network layer.
- The maximum amount of data that can be grabbed and placed in a segment is limited by the **maximum segment size (MSS)**.
- The MSS is typically set by first determining the length of the largest link-layer frame that can be sent by the local sending host (the so-called **maximum transmission unit, MTU**)
- TCP pairs each chunk of client data with a TCP header, thereby forming TCP segments.
### TCP Segment Structure
- The TCP segment consists of header fields and a data field. The data field contains a chunk of application data. As mentioned above, the MSS limits the maxi mum size of a segment’s data field.
- A TCP segment header also contains the following fields:
	- 32 bit sequence number field and 32 bit acknowledgement number field
	- 16 bit receive window field used for flow control which is used to indicate the number of bytes that a receiver is willing to accept
	- 4 bit header length field
	- optional field
	- 6 bit flag field. The *ACK* bit is used to indicate that the value carried in the acknowledgement field is valid , The *RST* , *SYN* , *FIN* bits are used for connection setup and teardown 
	- Setting the *PSH* bit indicates that the receiver should pass the data to the upper layer immediately. Finally, the *URG* bit is used to indicate that there is data in this segment that the sending-side upper layer entity has marked as “urgent.”
#### Sequence Numbers and Acknowledgement Numbers
- TCP views data as an unstructured, but ordered, stream of bytes.
- TCP’s use of sequence numbers reflects this view in that sequence numbers are over the stream of transmitted bytes and not over the series of transmitted segments .The sequence number for a segment is therefore the byte-stream number of the first byte in the segment.
- Each of the segments that arrive from Host B has a sequence number for the data flowing from B to A. *The acknowledgment number that Host A puts in its segment is the sequence number of the next byte Host A is expecting from Host B.*  
- Because TCP only acknowledges bytes up to the first missing byte in the stream, TCP is said to provide cumulative acknowledgments.
- Interestingly, the TCP RFCs do not impose any rules here and leave the decision up to the programmers implementing a TCP implementation. There are basically two choices: either (1) the receiver immediately discards out-of-order segments (which, as we discussed earlier, can simplify receiver design), or (2) the receiver keeps the out-of-order bytes and waits for the missing bytes to fill in the gaps.
- EstimatedRTT = (1 – α)  EstimatedRTT + α  SampleRTT   ( α is generally 1/8)
- DevRTT = (1 – β) DevRTT + β | SampleRTT – EstimatedRTT |  ( β is generally 1/4)
- TimeoutInterval = EstimatedRTT + 4 DevRTT
- Have a style of GBN but sends the package only for which the the timeout has happened
- Flow Management - have RcvBuffer and rwnd(receive window) = spare room for the RcvBuffer
- when rwnd = 0 the sender can not send data and it periodically sends 0 space data to check whether rwnd got some space back again if it gets it starts sending data
### TCP Connection Management
- Furthermore, many of the most common network attacks—including the incredibly popular SYN flood attack exploit vulnerabilities in TCP connection management.
- The client application process first informs the client TCP that it wants to establish a connection to a process in the server. The TCP in the client then proceeds to establish a TCP connection with the TCP in the server in the following manner:
	- The client-side TCP first sends a special TCP segment to the server-side TCP. This special segment contains no application-layer data. But one of the flag bits in the segment’s header the SYN bit, is set to 1. For this reason, this special segment is referred to as a SYN segment. In addition, the client randomly chooses an initial sequence number (*client_isn*) and puts this number in the sequence number field of the initial TCP SYN segment.
	- Once the IP datagram containing the TCP SYN segment arrives at the server host (assuming it does arrive!), the server extracts the TCP SYN segment from the datagram, allocates the TCP buffers and variables to the connection, and sends a connection-granted segment to the client TCP. This connection-granted segment also contains no application-layer data. However, it does contain three important pieces of information in the segment header. First, the SYN bit is set to 1. Second, the acknowledgment field of the TCP segment header is set to client_isn+1. Finally, the server chooses its own initial sequence number (server_isn) and puts this value in the sequence number field of the TCP segment header. The connection-granted segment is referred to as a **SYNACK** segment.
	- Upon receiving the SYNACK segment, the client also allocates buffers and variables to the connection. The client host then sends the server yet another segment; this last segment acknowledges the server’s connection-granted segment (the client does so by putting the value server_isn+1 in the acknowledgment field of the TCP segment header). The SYN bit is set to zero, since the connection is established. This third stage of the three-way handshake may carry client-to server data in the segment payload.
- Either of the two processes participating in a TCP connection can end the connection. When a connection ends, the “resources” (that is, the buffers and variables) in the hosts are deallocated.
- The client application process issues a close command. This causes the client TCP to send a special TCP segment to the server process. This special segment has a flag bit in the segment’s header, the FIN bit.
- When the server receives this segment, it sends the client an acknowledgment segment in return. The server then sends its own shutdown segment, which has the FIN bit set to 1. Finally, the client acknowledges the server’s shutdown segment. At this point, all the resources in the two hosts are now deallocated.
- During the life of a TCP connection, the TCP protocol running in each host makes transitions through various **TCP states**.
## Principles of Congestion Control

TODO: 


# THE NETWORK LAYER : DATA PLANE
## Overview of Network Layer
- The primary data-plane role of each router is to forward datagrams from its input links to its output links
- The primary role of the network control plane is to coordinate these local, per-router forwarding actions so that datagrams are ultimately transferred end-to-end, along paths of routers between source and destination hosts
### Forwarding and Routing : The Data and Control Planes
- The primary role of the network layer is deceptively simple—to move packets from a sending host to a receiving host. To do so, two important network-layer functions can be identified:
	- *Forwarding*. When a packet arrives at a router’s input link, the router must move the packet to the appropriate output link.
	- *Routing*. The network layer must determine the route or path taken by packets as they flow from a sender to a receiver. The algorithms that calculate these paths are referred to as **routing algorithms**. Routing is implemented in the control plane of the network layer
- A key element in every network router is its forwarding table. A router forwards a packet by examining the value of one or more fields in the arriving packet’s header, and then using these header values to index into its forwarding table.
- The value stored in the forwarding table entry for those values indicates the outgoing link interface at that router to which that packet is to be forwarded.
#### Control Plane : The Traditional Approach
- the routing algorithm determines the contents of the routers’ forwarding tables. In this example, a routing algorithm runs in each and every router and both forwarding and routing functions are contained within a router.
- the routing algorithm function in one router communicates with the routing algorithm function in other routers to compute the values for its forwarding table. How is this communication performed? By exchanging routing messages containing routing information according to a routing protocol!
#### Control Plane : The SDN Approach
- an alternative approach in which a physically separate, remote controller computes and distributes the forwarding tables to be used by each and every router.
- control-plane routing functionality is separated from the physical router—the routing device performs forwarding only, while the remote controller computes and distributes forwarding tables.
- How might the routers and the remote controller communicate? By exchanging messages containing forwarding tables and other pieces of routing information. The control-plane approach is at the heart of software-defined networking (SDN), where the network is “software-defined” because the controller that computes forwarding tables and interacts with routers is implemented in software.
### Network Service Model
- The network service model defines the characteristics of end-to-end delivery of packets between sending and receiving hosts. Let’s now consider some possible services that the network layer could provide. These services could include:
	- Guaranteed delivery. This service guarantees that a packet sent by a source host will eventually arrive at the destination host.
	- Guaranteed delivery with bounded delay. This service not only guarantees delivery of the packet, but delivery within a specified host-to-host delay bound (for example, within 100 msec).
	- In-order packet delivery. This service guarantees that packets arrive at the destination in the order that they were sent.
	- Guaranteed minimal bandwidth. This network-layer service emulates the behavior of a transmission link of a specified bit rate (for example, 1 Mbps) between sending and receiving hosts. As long as the sending host transmits bits (as part of packets) at a rate below the specified bit rate, then all packets are eventually delivered to the destination host.
	- Security. The network layer could encrypt all datagrams at the source and decrypt them at the destination, thereby providing confidentiality to all transport-layer segments.
- **The Internet’s network layer provides a single service, known as best-effort service**. With best-effort service, packets are neither guaranteed to be received in the order in which they were sent, nor is their eventual delivery even guaranteed. There is no guarantee on the end-to-end delay nor is there a minimal bandwidth guarantee. It might appear that best-effort service is a euphemism for no service at all—a network that delivered no packets to the destination would satisfy the definition of best-effort delivery service!
## What's Inside a Router?
- Four router components can be identified:
	- *Input ports*. An input port performs several key functions. It performs the physical layer function of terminating an incoming physical link at a router. An input port also performs link-layer functions needed to interoperate with the link layer at the other side of the incoming link; this is represented by the middle boxes in the input and output ports. Perhaps most crucially, a lookup function is also performed at the input port; this will occur in the rightmost box of the input port. It is here that the forwarding table is consulted to determine the router output port to which an arriving packet will be forwarded via the switching fabric. Control packets (for example, packets carrying routing protocol information) are forwarded from an input port to the routing processor. Note that the term “port” here—referring to the physical input and output router interfaces
	- *Switching fabric*. The switching fabric connects the router’s input ports to its output ports. This switching fabric is completely contained within the router—a network inside of a network router!
	- *Output ports*. An output port stores packets received from the switching fabric and transmits these packets on the outgoing link by performing the necessary link-layer and physical-layer functions. When a link is bidirectional an output port will typically be paired with the input port for that link on the same line card.
	- *Routing processor*. The routing processor performs control-plane functions. In traditional routers, it executes the routing protocols maintains routing tables and attached link state information, and computes the forwarding table for the router. In SDN routers, the routing processor is responsible for communicating with the remote controller in order to receive forwarding table entries computed by the remote controller, and install these entries in the router’s input ports. The routing processor also performs the network management functions
- A router’s input ports, output ports, and switching fabric are almost always implemented in hardware
- While the data plane operates at the nanosecond time scale, a router’s control functions—executing the routing protocols, responding to attached links that go up or down, communicating with the remote controller (in the SDN case) and performing management functions—operate at the millisecond or second timescale. These control plane functions are thus usually implemented in software and execute on the routing processor (typically a traditional CPU).
### Input Port Processing and Destination-Based Forwarding
- With this style of forwarding table, the router matches a **prefix** of the packet’s destination address with the entries in the table; if there’s a match, the router forwards the packet to a link associated with the match
- If a prefix doesn’t match any of the first three entries, then the router forwards the packet to the default interface
- When there are multiple matches, the router uses the **longest prefix matching rule**; that is, it finds the longest matching entry in the table and forwards the packet to the link interface associated with the longest prefix match.
- Once a packet’s output port has been determined via the lookup, the packet can be sent into the switching fabric. In some designs, a packet may be temporarily blocked from entering the switching fabric if packets from other input ports are currently using the fabric. A blocked packet will be queued at the input port and then scheduled to cross the fabric at a later point in time.
- Although “lookup” is arguably the most important action in input port processing, many other actions must be taken: (1) physical- and link-layer processing must occur, as discussed previously; (2) the packet’s version number, checksum and time-to-live field must be checked and the latter two fields rewritten; and (3) counters used for network management (such as the number of IP datagrams received) must be updated.
### Switching
- The switching fabric is at the very heart of a router, as it is through this fabric that the packets are actually switched (that is, forwarded) from an input port to an output port. Switching can be accomplished in a number of ways : 
	- Switching via memory : 
		- The simplest, earliest routers were traditional computers, with switching between input and output ports being done under direct control of the CPU (routing processor). Input and output ports functioned as traditional I/O devices in a traditional operating system. An input port with an arriving packet first signaled the routing processor via an interrupt. The packet was then copied from the input port into processor memory. The routing processor then extracted the destination address from the header, looked up the appropriate output port in the forwarding table, and copied the packet to the output port’s buffers.
		- In this scenario, if the memory bandwidth is such that a maximum of B packets per second can be written into, or read from, memory, then the overall forwarding throughput (the total rate at which packets are transferred from input ports to out put ports) must be less than B/2.
		- Note also that two packets cannot be forwarded at the same time, even if they have different destination ports, since only one memory read/write can be done at a time over the shared system bus.
	- Switching via a bus :
		- In this approach, an input port transfers a packet directly to the output port over a shared bus, without intervention by the routing processor. This is typically done by having the input port pre-pend a switch-internal label (header) to the packet indicating the local output port to which this packet is being transferred and transmitting the packet onto the bus.
		- All output ports receive the packet, but only the port that matches the label will keep the packet. The label is then removed at the output port, as this label is only used within the switch to cross the bus. If multiple packets arrive to the router at the same time, each at a different input port, all but one must wait since only one packet can cross the bus at a time.
		- Because every packet must cross the single bus, the switching speed of the router is limited to the bus speed; in our roundabout analogy, this is as if the roundabout could only contain one car at a time. Nonetheless, switching via a bus is often sufficient for routers that operate in small local area and enterprise networks
	- Switching via an interconnection network : 
		- One way to overcome the bandwidth limitation of a single, shared bus is to use a more sophisticated interconnection network, such as those that have been used in the past to interconnect processors in a multiprocessor computer architecture. 
		- A crossbar switch is an interconnection net work consisting of 2N buses that connect N input ports to N output ports Each vertical bus intersects each horizontal bus at a cross point , which can be opened or closed at any time by the switch fabric controller (whose logic is part of the switching fabric itself).
		- Thus, unlike the previous two switching approaches, cross bar switches are capable of forwarding multiple packets in parallel. A crossbar switch is **non-blocking**—a packet being forwarded to an output port will not be blocked from reaching that output port as long as no other packet is currently being forwarded to that output port
		- However, if two packets from two different input ports are destined to that same output port, then one will have to wait at the input, since only one packet can be sent over any given bus at a time
- More sophisticated interconnection networks use multiple stages of switching elements to allow packets from different input ports to proceed towards the same output port at the same time through the multi-stage switching fabric
- A router’s switching capacity can also be scaled by running multiple switching fabrics in parallel. In this approach, input ports and output ports are connected to N switching fabrics that operate in parallel.
### Output Port Processing
- Output port processing takes packets that have been stored in the output port’s memory and transmits them over the output link. This includes selecting (i.e., scheduling) and de-queuing packets for transmission, and performing the needed link-layer and physical-layer transmission functions.
### Where Does Queuing Occur?
- The location and extent of queuing (either at the input port queues or the output port queues) will depend on the traffic load, the relative speed of the switching fabric, and the line speed.
#### Input Queuing
- But what happens if the switch fabric is not fast enough (relative to the input line speeds) to transfer all arriving packets through the fabric without delay? In this case, packet queuing can also occur at the input ports, as packets must join input port queues to wait their turn to be transferred through the switching fabric to the output port.
- This phenomenon is known as **head-of-the-line (HOL) blocking** in an input-queued switch—a queued packet in an input queue must wait for transfer through the fabric (even though its output port is free) because it is blocked by another packet at the head of the line.
#### Output Queuing
- Thus, packet queues can form at the output ports even when the switching fabric is N times faster than the port line speeds. Eventually, the number of queued packets can grow large enough to exhaust available memory at the output port.
- When there is not enough memory to buffer an incoming packet, a decision must be made to either drop the arriving packet (a policy known as drop-tail) or remove one or more already-queued packets to make room for the newly arrived packet.
- A number of proactive packet-dropping and -marking policies (which collectively have become known as active queue management (AQM) algorithms) have been proposed and analyzed
- One of the most widely studied and implemented AQM algorithms is the Random Early Detection (RED) algorithm
- A consequence of such queuing is that a packet scheduler at the output port must choose one packet, among those queued, for transmission
#### How much Buffering is Enough?
- For many years, the rule of thumb for buffer sizing was that the amount of buffering (B) should be equal to an average round-trip time (RTT) times the link capacity (C) B = RTT . C
- More recent theoretical and experimental efforts , however, suggest that when a large number of independent TCP flows (N) pass through a link, the amount of buffering needed is B = RTT . C /sqrt(N) . In core networks, where a large number of TCP flows typically pass through large backbone router links, the value of N can be large, with the decrease in needed buffer size becoming quite significant.
- **Bufferbloat** occurs when excessive buffering **causes consistently long delays**, even when there is no congestion.
### Packet Scheduling
#### FIFO
- If there is not sufficient buffering space to hold the arriving packet, the queue’s packet-discarding policy then determines whether the packet will be dropped (lost) or whether other packets will be removed from the queue to make space for the arriving packet, as discussed above.
#### Priority Queuing 
- Under priority queuing, packets arriving at the output link are classified into priority classes upon arrival at the queue
- In practice, a network operator may configure a queue so that packets carrying network management information (for example, as indicated by the source or destination TCP/UDP port number) receive priority over user traffic
#### Round Robin and Weighted Fair Queuing (WFQ)
- Under the round robin queuing discipline, packets are sorted into classes as with priority queuing. However, rather than there being a strict service priority among classes, a round robin scheduler alternates service among the classes. In the simplest form of round robin scheduling, a class 1 packet is transmitted, followed by a class 2 packet, followed by a class 1 packet, followed by a class 2 packet, and so on. A so-called work-conserving queuing discipline will never allow the link to remain idle whenever there are packets (of any class) queued for transmission.
- A generalized form of round robin queuing that has been widely implemented in routers is the so-called weighted fair queuing (WFQ) discipline
- Here, arriving packets are classified and queued in the appropriate per-class waiting area. As in round robin scheduling, a WFQ scheduler will serve classes in a circular manner—first serving class 1, then serving class 2, then serving class 3, and then (assuming there are three classes) repeating the service pattern. WFQ is also a work-conserving queuing discipline and thus will immediately move on to the next class in the service sequence when it finds an empty class queue.
## The Internet Protocol (IP) : IPv4, Addressing, IPv6 and More
### IPv4 Datagram Format
- The key fields in the IPv4 datagram are the following:
	- *Version number*. These 4 bits specify the IP protocol version of the datagram. By looking at the version number, the router can determine how to interpret the remainder of the IP datagram. Different versions of IP use different datagram formats.
	- *Header length*. Because an IPv4 datagram can contain a variable number of options (which are included in the IPv4 datagram header), these 4 bits are needed to determine where in the IP datagram the payload (for example, the transport layer segment being encapsulated in this datagram) actually begins
	- *Type of service*. The type of service (TOS) bits were included in the IPv4 header to allow different types of IP datagrams to be distinguished from each other. For example, it might be useful to distinguish real-time datagrams (such as those used by an IP telephony application) from non-real-time traffic (e.g., FTP). The specific level of service to be provided is a policy issue determined and configured by the network administrator for that router
	- *Datagram length*. This is the total length of the IP datagram (header plus data), measured in bytes. Since this field is 16 bits long, the theoretical maximum size of the IP datagram is 65,535 bytes. However, datagrams are rarely larger than 1,500 bytes, which allows an IP datagram to fit in the payload field of a maximally sized Ethernet frame.
	- *Identifier, flags, fragmentation offset*. These three fields have to do with so-called IP fragmentation, when a large IP datagram is broken into several smaller IP data grams which are then forwarded independently to the destination, where they are reassembled before their payload data is passed up to the transport layer at the destination host.
	- *Time-to-live*. The time-to-live (TTL) field is included to ensure that datagrams do not circulate forever (due to, for example, a long-lived routing loop) in the network. This field is decremented by one each time the datagram is processed by a router. If the TTL field reaches 0, a router must drop that datagram.
	- *Protocol*. This field is typically used only when an IP datagram reaches its final destination. The value of this field indicates the specific transport-layer protocol to which the data portion of this IP datagram should be passed.
	- *Header checksum*. The header checksum aids a router in detecting bit errors in a received IP datagram. The header checksum is computed by treating each 2 bytes in the header as a number and summing these numbers using 1s complement arithmetic.
	- *Source and destination IP addresses*. When a source creates a datagram, it inserts its IP address into the source IP address field and inserts the address of the ultimate destination into the destination IP address field. Often the source host determines the destination address via a DNS lookup
	- *Options*. The options fields allow an IP header to be extended. Header options were meant to be used rarely—hence the decision to save overhead by not including the information in options fields in every datagram header
	- *Data (payload)*. Finally, we come to the last and most important field—the raison d’etre for the datagram in the first place! In most circumstances, the data field of the IP datagram contains the transport-layer segment (TCP or UDP) to be delivered to the destination. However, the data field can carry other types of data, such as ICMP messages
### IPv4 Addressing
 - The boundary between the host and the physical link is called an **interface**. Now consider a router and its interfaces. Because a router’s job is to receive a datagram on one link and forward the datagram on some other link, a router necessarily has two or more links to which it is connected.
 - Because every host and router is capable of sending and receiving IP datagrams, IP requires each host and router interface to have its own IP address. *Thus, an IP address is technically associated with an interface, rather than with the host or router containing that interface*
 - These addresses are typically written in so-called **dotted-decimal notation**, in which each byte of the address is written in its decimal form and is separated by a period (dot) from other bytes in the address. For example, consider the IP address 193.32.216.9. The 193 is the decimal equivalent of the first 8 bits of the address; the 32 is the decimal equivalent of the second 8 bits of the address, and so on. Thus, the address 193.32.216.9 in binary notation is 11000001 00100000 11011000 00001001
 - Each interface on every host and router in the global Internet must have an IP address that is globally unique (except for interfaces behind NATs ) 
 - In IP terms, this network interconnecting three host interfaces and one router interface forms a **subnet**. (A subnet is also called an IP network or simply a network in the Internet literature.)
 - IP addressing assigns an address to this subnet: 223.1.1.0/24, where the /24 (“slash-24”) notation, sometimes known as a **subnet mask**, indicates that the leftmost 24 bits of the 32-bit quantity define the subnet address.
 - For a general interconnected system of routers and hosts, we can use the following recipe to define the subnets in the system: *To determine the subnets, detach each interface from its host or router, creating islands of isolated networks, with interfaces terminating the end points of the isolated networks. Each of these isolated networks is called a subnet.*
 - The Internet’s address assignment strategy is known as **Classless Interdomain Routing** (CIDR—pronounced cider)
 - CIDR generalizes the notion of subnet addressing. As with subnet addressing, the 32-bit IP address is divided into two parts and again has the dotted-decimal form a.b.c.d/x, where x indicates the number of bits in the first part of the address.
 - The x most significant bits of an address of the form a.b.c.d/x constitute the network portion of the IP address, and are often referred to as the prefix (or network prefix) of the address.
 - The remaining 32-x bits of an address can be thought of as distinguishing among the devices within the organization, all of which have the same network prefix.
 - Before CIDR was adopted, the network portions of an IP address were constrained to be 8, 16, or 24 bits in length, an addressing scheme known as **classful addressing**
 - We would be remiss if we did not mention yet another type of IP address, the IP broadcast address 255.255.255.255. When a host sends a datagram with destination address 255.255.255.255, the message is delivered to all hosts on the same subnet.
#### Obtaining a Block of Address
- In order to obtain a block of IP addresses for use within an organization’s subnet, a network administrator might first contact its ISP, which would provide addresses from a larger block of addresses that had already been allocated to the ISP. For example, the ISP may itself have been allocated the address block 200.23.16.0/20. The ISP, in turn, could divide its address block into eight equal-sized contiguous address blocks and give one of these address blocks out to each of up to eight organizations that are supported by this ISP, ex: 200.23.16.0/23
#### Obtaining a Host Address: The Dynamic Host Configuration Protocol
- Host addresses can also be configured manually, but typically this is done using the **Dynamic Host Configuration Protocol (DHCP)**
- DHCP allows a host to obtain (be allocated) an IP address automatically. A network administrator can configure DHCP so that a given host receives the same IP address each time it connects to the network, or a host may be assigned a temporary IP address that will be different each time the host connects to the network. In addition to host IP address assignment, DHCP also allows a host to learn additional information, such as its *subnet mask*, the address of its first-hop router (often called the default *gateway*), and the address of its *local DNS server*.
- Because of DHCP’s ability to automate the network-related aspects of connecting a host into a network, it is often referred to as a **plug-and-play** or **zeroconf** (zero-configuration) protocol.
- DHCP is a client-server protocol. A client is typically a newly arriving host wanting to obtain network configuration information, including an IP address for itself. In the simplest case, each subnet  will have a DHCP server. If no server is present on the subnet, a DHCP relay agent (typically a router) that knows the address of a DHCP server for that network is needed.
- For a newly arriving host, the DHCP protocol is a four-step process : 
	- *DHCP server discovery.* The first task of a newly arriving host is to find a DHCP server with which to interact. This is done using a DHCP discover message, which a client sends within a UDP packet to port 67. The UDP packet is encapsulated in an IP datagram. But to whom should this datagram be sent? The host doesn’t even know the IP address of the network to which it is attaching, much less the address of a DHCP server for this network. Given this, the DHCP client creates an IP datagram containing its DHCP discover message along with the broadcast destination IP address of 255.255.255.255 and a “this host” source IP address of 0.0.0.0. The DHCP client passes the IP datagram to the link layer, which then broadcasts this frame to all nodes attached to the subnet
	- *DHCP server offer(s)*. A DHCP server receiving a DHCP discover message responds to the client with a DHCP offer message that is broadcast to all nodes on the subnet, again using the IP broadcast address of 255.255.255.255.
	- *DHCP request*. The newly arriving client will choose from among one or more server offers and respond to its selected offer with a *DHCP request message*, echoing back the configuration parameters.
	- *DHCP ACK*. The server responds to the DHCP request message with a DHCP ACK message, confirming the requested parameters.
### Network Address Translation (NAT)
- The NAT-enabled router does not look like a router to the outside world. Instead the NAT router behaves to the outside world as a single device with a single IP address.
- Nat Translation Table only for home address port to the destination address port 
- During translation NAT uses internal port to configure and send back responses using this mapped internal port to the home device that has requested the information from the external public IP
### IPv6
- A prime motivation for this effort was the realization that the 32-bit IPv4 address space was beginning to be used up, with new subnets and IP nodes being attached to the Internet at a breathtaking rate. To respond to this need for a large IP address space, a new IP protocol, IPv6, was developed.
#### IPv6 Datagram Format
- *Expanded addressing capabilities*. IPv6 increases the size of the IP address from 32 to 128 bits. This ensures that the world won’t run out of IP addresses. Now, every grain of sand on the planet can be IP-addressable. In addition to unicast and multicast addresses, IPv6 has introduced a new type of address, called an **anycast address**, that allows a datagram to be delivered to any one of a group of hosts. (This feature could be used, for example, to send an HTTP GET to the nearest of a number of mirror sites that contain a given document.)
- *A streamlined 40-byte header*. As discussed below, a number of IPv4 fields have been dropped or made optional. The resulting 40-byte fixed-length header allows for faster processing of the IP datagram by a router. A new encoding of options allows for more flexible options processing.
- *Flow labeling*. IPv6 has an elusive definition of a flow. RFC 2460 states that this allows “labeling of packets belonging to particular flows for which the sender requests special handling, such as a non-default quality of service or real-time service.”

- we notice that several fields appearing in the IPv4 datagram are no longer present in the IPv6 datagram:
	- *Fragmentation/reassembly*. IPv6 does not allow for fragmentation and reassembly at intermediate routers; these operations can be performed only by the source and destination. If an IPv6 datagram received by a router is too large to be forwarded over the outgoing link, the router simply drops the datagram and sends a “Packet Too Big” ICMP error message  back to the sender. The sender can then resend the data, using a smaller IP datagram size. Fragmentation and reassembly is a time-consuming operation; removing this functionality from the routers and placing it squarely in the end systems considerably speeds up IP forwarding within the network.
	- *Header checksum*. Because the transport-layer (for example, TCP and UDP) and link-layer (for example, Ethernet) protocols in the Internet layers perform check summing, the designers of IP probably felt that this functionality was sufficiently redundant in the network layer that it could be removed. Once again, fast processing of IP packets was a central concern.
	- *Options*. An options field is no longer a part of the standard IP header. However, it has not gone away. Instead, the options field is one of the possible next headers pointed to from within the IPv6 header. That is, just as TCP or UDP protocol headers can be the next header within an IP packet, so too can an options field. The removal of the options field results in a fixed-length, 40-byte IP header
#### Transitioning from IPv4 to IPv6
- The approach to IPv4-to-IPv6 transition that has been most widely adopted in practice involves **tunneling**. The basic idea behind tunneling—a key concept with applications in many other scenarios beyond IPv4-to-IPv6 transition is following. 
- Suppose two IPv6 nodes (in this example, B and E in Figure 4.27) want to interoperate using IPv6 datagrams but are connected to each other by intervening IPv4 routers. We refer to the intervening set of IPv4 routers between two IPv6 routers as a tunnel, as illustrated in Figure 4.27. With tunneling, the IPv6 node on the sending side of the tunnel (in this example, B) takes the entire IPv6 datagram and puts it in the data (payload) field of an IPv4 datagram. This IPv4 datagram is then addressed to the IPv6 node on the receiving side of the tunnel (in this example, E) and sent to the first node in the tunnel (in this example, C). The intervening IPv4 routers in the tunnel route this IPv4 datagram among themselves, just as they would any other datagram, blissfully unaware that the IPv4 datagram itself contains a complete IPv6 datagram. The IPv6 node on the receiving side of the tunnel eventually receives the IPv4 datagram (it is the destination of the IPv4 datagram!), determines that the IPv4 datagram contains an IPv6 datagram (by observing that the protocol number field in the IPv4 datagram is 41, indicating that the IPv4 payload is a IPv6 datagram), extracts the IPv6 datagram, and then routes the IPv6 datagram exactly as it would if it had received the IPv6 datagram from a directly connected IPv6 neighbor.
## Generalized Forwarding and SDN

## Middleboxes

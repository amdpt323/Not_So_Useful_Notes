
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
- . A `registrar` is a commercial entity that verifies the uniqueness of the domain name
## Peer-to-Peer File Distribution
- Bit Torrent 
- Rarest first
- 4 unchoked
- 1 optimistically unchoked
## Video Streaming and Content Distribution Networks
- Dynamic Adaptive Streaming over HTTP (DASH)
- Content Distribution Networks (CDNs)
- A CDN manages servers in multiple geographically distributed locations, stores copies of the videos (and other types of Web content, including documents, images, and audio) in its servers, and attempts to direct each user request to a CDN location that will provide the best user experience
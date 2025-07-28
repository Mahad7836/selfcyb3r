# Intro to Networking

Understanding networking is crucial in the context of penetration testing. Networking layers play a key role in how data flows across a network. The OSI model and TCP/IP model are two key frameworks used to understand the flow of data in networking.

OSI Model (Open Systems Interconnection)
The OSI model divides the communication process into seven distinct layers. These layers define how data is transmitted and received across a network.

Layer 7 - Application Layer:

Provides services and protocols for network applications (e.g., HTTP, FTP, DNS).

Ensures communication between user applications.

Layer 6 - Presentation Layer:

Translates data into a format that the application layer can understand.

Handles encryption, compression, and translation.

Layer 5 - Session Layer:

Manages sessions and ensures that communication between two devices is synchronized.

Supports multiple connections without interference.

Layer 4 - Transport Layer:

Handles data transport and ensures data integrity.

Common protocols: TCP (Transmission Control Protocol) and UDP (User Datagram Protocol).

TCP: Connection-based, reliable, ensures packets reach their destination.

UDP: Connectionless, faster but less reliable.

Layer 3 - Network Layer:

Routes data to the correct destination using IP addresses (e.g., IPv4, IPv6).

Determines the best route for data transfer.

Layer 2 - Data Link Layer:

Responsible for physical addressing using MAC addresses.

Ensures error-free data transfer between nodes.

Layer 1 - Physical Layer:

Deals with the physical transmission of data over the network (electrical signals, light pulses).

# TCP/IP Model:
The TCP/IP model is the foundation of most real-world networking systems, and it's similar to the OSI model but with fewer layers (4 layers instead of 7). This model is used in practice for data transmission over the internet.

Layers of the TCP/IP Model:

Application Layer: Corresponds to OSI's Application, Presentation, and Session layers.

Transport Layer: Equivalent to OSI's Transport layer. Key protocols: TCP and UDP.

Internet Layer: Equivalent to OSI's Network layer. Responsible for IP addressing and routing.

Network Interface Layer: Combines OSI's Data Link and Physical layers, dealing with the transmission of data over physical hardware.

Comparison with OSI Model:
The layers in the TCP/IP model combine the OSI layers:

Application Layer (OSI 7, 6, 5) = Applications and Protocols (e.g., HTTP, DNS, FTP).

Transport Layer (OSI 4) = Transmission reliability and flow control (e.g., TCP, UDP).

Internet Layer (OSI 3) = Routing and addressing (e.g., IP addresses).

Network Interface Layer (OSI 2, 1) = Physical and data link transmission (e.g., Ethernet, Wi-Fi).

# TCP (Transmission Control Protocol)
TCP is a key protocol in the transport layer of the TCP/IP model. It ensures reliable, connection-based data transmission. The most important feature of TCP is the Three-Way Handshake, which establishes a stable connection between two computers before they begin data transfer.

Three-Way Handshake Process:

SYN (Synchronize): The client sends a request to initiate a connection.

SYN-ACK (Synchronize-Acknowledgement): The server responds to acknowledge the connection request.

ACK (Acknowledgement): The client acknowledges the server’s response, completing the handshake.

After the three-way handshake, data is transmitted reliably, with mechanisms for ensuring that any lost or corrupted data is retransmitted.

# Why Networking Models Matter:
The OSI model is more of a theoretical framework that helps in understanding how data flows and is handled at each layer.

The TCP/IP model is the practical, real-world implementation used in most network systems, including the internet.

Learning both models is useful for understanding different perspectives: theoretical (OSI) and practical (TCP/IP).

In penetration testing, understanding these models helps in identifying potential attack vectors at each layer and understanding how attacks can impact different stages of data transfer.

# Conclusion
The knowledge of networking layers, both in the OSI model and TCP/IP model, plays a fundamental role in offensive security. Understanding tools like Gobuster for enumeration and grasping protocols like TCP for reliable communication forms the backbone of most penetration testing methodologies. This combination of theoretical and practical knowledge will allow you to identify vulnerabilities, understand network traffic, and more effectively carry out security assessments.
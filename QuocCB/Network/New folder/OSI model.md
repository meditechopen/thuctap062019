#### Application layer

The application layer is a layer in the Open Systems Interconnection (OSI) seven-layer model and in the TCP/IP protocol suite.
It consists of protocols that focus on process-to-process communication across an IP network and provides a firm communication interface and end-user services.

The application layer is the seventh layer of the OSI model and the only one that directly interacts with the end user.

The application layer provides many services, including:

- Simple Mail Transfer Protocol
- File transfer
- Web surfing
- Web chat
- Email clients
- Network data sharing
- Virtual terminals
- Various file and data operations


The application layer provides full end-user access to a variety of shared network services for efficient OSI model data flow. This layer has many responsibilities, including error handling and recovery, data flow over a network and full network flow. It is also used to develop network-based applications.

More than 15 protocols are used in the application layer, including File Transfer Protocol, Telnet, Trivial File Transfer Protocol and Simple Network Management Protocol.

#### Presentation layer

The presentation layer is layer 6 of the 7-layer Open Systems Interconnection (OSI) model.
It is used to present data to the application layer (layer 7) in an accurate, well-defined and standardized format. 

The presentation layer is sometimes called the syntax layer.

The presentation layer is responsible for the following:

- Data encryption/decryption
- Character/string conversion
- Data compression
- Graphic handling


The presentation layer mainly translates data between the application layer and the network format. Data can be communicated in different formats via different sources. Thus, the presentation layer is responsible for integrating all formats into a standard format for efficient and effective communication. 

The presentation layer follows data programming structure schemes developed for different languages and provides the real-time syntax required for communication between two objects such as layers, systems or networks. The data format should be acceptable by the next layers; otherwise, the presentation layer may not perform correctly. 

Network devices or components used by the presentation layer include redirectors and gateways.



#### Session layer

In the OSI model, the Session layer is the fifth layer, which control the connection beween multiple computers. The session layer tracks the dialog between computers, which are also called sessions.
This layer establishes, controls and ends the session between local and remote applications.

The session layer manages a session by initiating the opening and closing of sessions between end-user application processes.
This layer also controls single or multiple connections for each end-user application, and directly communicates with both the presentation and the transport layers.
The services offered by the session layer are generally implemented in application environments using remote procedure calls (RPCs).

The session layer supports full-duplex and half-duplex operations and creates procedures for checkpointing, adjournment, restart and termination.
The session layer is also responsible for synchronizing information from different sources. For example, sessions are implemented in live television programs in which the audio and video streams emerging from two different sources are merged together.
This avoids overlapping and silent broadcast time. 

#### Transport layer

The transport layer is the layer in the open system interconnection (OSI) model responsible for end-to-end communication over a network.
It provides logical communication between application processes running on different hosts within a layered architecture of protocols and other network components.

The transport layer is also responsible for the management of error correction, providing quality and reliability to the end user.
This layer enables the host to send and receive error corrected data, packets or messages over a network and is the network component that allows multiplexing.

In the OSI model, the transport layer is the fourth layer of this network structure.

Transport layers work transparently within the layers above to deliver and receive data without errors. The send side breaks application messages into segments and passes them on to the network layer. The receiving side then reassembles segments into messages and passes them to the application layer.

The transport layer can provide some or all of the following services:

- Connection-Oriented Communication: Devices at the end-points of a network communication establish a handshake protocol to ensure a connection is robust before data is exchanged. The weakness of this method is that for each delivered message, there is a requirement for an acknowledgment, adding considerable network load compared to self-error-correcting packets. The repeated requests cause significant slowdown of network speed when defective byte streams or datagrams are sent.
- Same Order Delivery: Ensures that packets are always delivered in strict sequence. Although the network layer is responsible, the transport layer can fix any discrepancies in sequence caused by packet drops or device interruption.
- Data Integrity: Using checksums, the data integrity across all the delivery layers can be ensured. These checksums guarantee that the data transmitted is the same as the data received through repeated attempts made by other layers to have missing data resent.
- Flow Control: Devices at each end of a network connection often have no way of knowing each other's capabilities in terms of data throughput and can therefore send data faster than the receiving device is able to buffer or process it. In these cases, buffer overruns can cause complete communication breakdowns. Conversely, if the receiving device is not receiving data fast enough, this causes a buffer underrun, which may well cause an unnecessary reduction in network performance.
- Traffic Control: Digital communications networks are subject to bandwidth and processing speed restrictions, which can mean a huge amount of potential for data congestion on the network. This network congestion can affect almost every part of a network. The transport layer can identify the symptoms of overloaded nodes and reduced flow rates.
- Multiplexing: The transmission of multiple packet streams from unrelated applications or other sources (multiplexing) across a network requires some very dedicated control mechanisms, which are found in the transport layer. This multiplexing allows the use of simultaneous applications over a network such as when different internet browsers are opened on the same computer. In the OSI model, multiplexing is handled in the service layer.
- Byte orientation: Some applications prefer to receive byte streams instead of packets; the transport layer allows for the transmission of byte-oriented data streams if required.

#### Network layer

The network layer is the third level of the Open Systems Interconnection Model (OSI Model) and the layer that provides data routing paths for network communication.
 Data is transferred in the form of packets via logical network paths in an ordered format controlled by the network layer. 

Logical connection setup, data forwarding, routing and delivery error reporting are the network layer’s primary responsibilities.

The network layer is considered the backbone of the OSI Model. It selects and manages the best logical path for data transfer between nodes. This layer contains hardware devices such as routers, bridges, firewalls and switches, but it actually creates a logical image of the most efficient communication route and implements it with a physical medium. 

Network layer protocols exist in every host or router. The router examines the header fields of all the IP packets that pass through it.

Internet Protocol and Netware IPX/SPX are the most common protocols associated with the network layer.

In the OSI model, the network layer responds to requests from the layer above it (transport layer) and issues requests to the layer below it (data link layer).

#### Datalink layer

The data link layer is used for the encoding, decoding and logical organization of data bits. Data packets are framed and addressed by this layer, which has two sublayers.

The data link layer's first sublayer is the media access control (MAC) layer.
It is used for source and destination addresses.
The MAC layer allows the data link layer to provide the best data transmission vehicle and manage data flow control.

The data link layer's second sublayer is the logical link control.
It manages error checking and data flow over a network.

The data link layer frame includes source and destination addresses, data length, start signal or indicator and other related Ethernet information to enhance communication.
This layer's main responsibility is to transfer data frames between nodes over a network.

#### Physical Layer

The physical layer is the first layer of the Open System Interconnection Model (OSI Model).
The physical layer deals with bit-level transmission between different devices and supports electrical or mechanical interfaces connecting to the physical medium for synchronized communication. 

This layer plays with most of the network’s physical connections - wireless transmission, cabling, cabling standards and types, connectors and types, network interface cards, and more - as per network requirements.
However, the physical layer does not deal with the actual physical medium (like copper, fiber).


# Packet-Sniffer

How are we sniffing the packets?
1. Create a new file called basic-packet-sniffer-linux.py and open it in your editor.

2. Import the required modules:
     import socket
     import struct
     import textwrap
     import binascii
     import struct
     import sys
3. Now we can create an INET raw socket:
conn = socket.socket(socket.PF_PACKET, socket.SOCK_RAW, socket.ntohs(3))

4. Linux provides Packet sockets to sniff the link layer packet at the application,
generally also known as raw sockets, but i would like to make a distinction here
that packet socket are use to send and receive the packets at data link layer(layer
2) and where as raw sockets are use to send the raw packet till layer 3 and can
only receive specific protocols like icmp at application layer.

Traditionally the protocol specific processing is done inside the kernel and only
the data is send/receive by the application, In this case application has no access
to any of the protocol header because it is added/removed by the kernel, The IP
packet contains Ethernet header, IP header and data, the final packet is
constructed by appending the header for each layer, User only needs to put the
data in socket, construction of the header is done inside the kernel.

socket(PF_PACKET,SOCK_RAW,protocol)

a. Domain (or FAMILY) — PF_PACKET

b. the socket type can be SOCK_RAW or SOCK_DGRAM (SOCK_DGRAM is used
in packet socket then application receives the packet without ethernet header, If
SOCK_RAW is used then application receives the complete frame include link
layer header)

c. Protocol — is use to filter only specific types of packet, like if protocol is
ETH_P_IP then only IP packets are received, to receive all protocol packets,
application can register with ETH_P_ALL protocol, Protocol Id’s are defined

5. Pass the data through filter and parser

6. Next, start an infinite loop to receive data from the socket:

7. Now run the program with Python:





HERE IS OUTPUT

![Screenshot from 2021-06-26 22-35-14](https://user-images.githubusercontent.com/60472408/123836619-84ce5a00-d927-11eb-9d53-9e4ca7ea5706.png)

README
The command line syntax for this program is:
./rawhttpget [URL]

The receive socket is of type SOCK_STREAM/IPPROTO_IP and  the send socket is of type SOCK_RAW/IPPROTO_RAW.

The following required features of IP have been implemented:

Checksums of incoming packets are validated in the unpack_ip_packet method.

While building the IP header the correct version, source and destination IP addresses header length and total length,
protocol identifier, and checksum are correctly set.

If an invalid IP packet is encountered (wrong checksum, invalid source IP of the packet, protocol identifier).

The following features of TCP have been implemented:

Checksums of incoming packets are verified.

For outgoing packets, a pseudo header is built according to TCP specifications and the checksum is calculated and set.
Since we are only supporting HTTP, the destination port is fixed to 80 and source port is chosen randomly .
Code correctly handles three way handshake and teardown.

if a packet is not acknowledged within 1 minute, the packet is assumed to be lost and is retransmit.
Congestion window starts at 1, and is incremented the after receiving a successful ACK, up to a fixed maximum of 1000.
 In case of a packet drop or a timeout the congestion window is reset to 1.

 All incoming packets are checked for valid checksums and in-order sequence numbers.
 If  data is received from the remote server for three minutes the connection is torn down.
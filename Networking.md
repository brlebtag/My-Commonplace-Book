[< Back](https://github.com/brlebtag/My-Commonplace-Book)

# Networking Knowledge

## TCPv4
* The `Window field` in the TCPv4 packet is the <ins>receive window</ins> of the <ins>sender</ins>. On the other hand, when the other side receives this packet, Window field will become its <ins>send window</ins>.

* During 3-way handshake, the `window field` stores the sender's receive window size that will be used by the TCP protocol of the other side. In the option field, there is also `window scale` field, which expands the size of receive window. It is a tow byte field but only 14 (of 16) bits can be used to scale the window size (up to 1GB).

* Nothing will be transmitted bigger than the `Maximum segment size` but a big window size allows the other size to send more packets without acknowledgement.

* TCP Stack will create a connected socket, ready to be accepted, only after the 3-way handshake. Therefore, as far as I know, you cannot control this process (3-way handshare) programmatically.

### Fragmentation
* No packet will be transmitted bigger than the MTU of the next hop, although there is no mechanism to prevent sending a packet bigger than the MTU size. The packet will be truncated by the other side.

* When the packet is bigger than the next hop, IP will split the packet into new packets limited by the MTU of the next hope and drop (delete) the original packet. The `IP ID` will be the same in each new packet. Each packet, excluding the last one will have `More Fragments`bit set to 1. The last packet will have the `More Fragments` bit set to 0.

* Reassembly is only performed by the endpoint (receiver side).

* Most protocols these days set `Don't Fragment` bit set to 1. So, normally fragmentation is rare. In IPv6 there is no fragmentation.

### Zero Window

* `TCP ACK` is not the same thing as <ins>consuming the data</ins>. The receiver can acknowledge the data but not immediately consume it.

* When Wireshark says that `TCP window specified by the receiver is now completely full`, it means that wireshark has computed the window size of the sender and realized it is full. It must have captured the 3-way handshake, otherwise, this information is wrong. It is always good to capture the 3-way handshake.

* I've noticed that `TCP Zero Window segment` is normal between 0 and 10 times. These results came from testing 1GB file transfers between PC and Android devices in a WLAN environment. More than this, it is a connection problem.

* When there is a `TCP Zero Window segment` situation, the sender side will periodically send `TCP ACK` packets to check if there is still a connection and to poll the other side's situation (receive buffer size). The other side will (if still alive) reply with another `TCP ACK` with current status (receive buffer size) (it can still be zero or another value). Each time the sender side send a ACK packet it will double the waiting time.

* `Silly Window Syndrome (SWS)` is caused when the receive buffer is shrinking (the other size is advertising smaller and smaller buffer size) and there is no mechanism to avoid advertising small packets or any other mechanism in the sender side to avoid sending small and inefficient packet size. `Nagle algoritm` helps avoiding this problem (in the sender side). On the other hand, if the receiver side has only a small receive window, it can close the window entirely (returns zero window) and wait the buffer to be free and have more space.

## Collision Avoidance

* `Collision Avoidance` controls the burst of data being sent and only happens in the sender's size, however, it is limited by the <ins>receiver's receive windo</ins>.

* It does not influence (i.e. reduce) the receiver's receive window. The Receive window is <ins>only reduced if the receiver is clogged</ins>.

## Wifi-Direct
* Android uses IP range for wifi direct 192.168.49.1/24. Group Owner (GO) is always 192.168.49.1 (it is hard-coded in the codebase). On the other hand. Windows uses 192.168.137.1/24 (/24 is my supposition). Group Owner is 192.168.137.1.

* Android limits in the code to 5 Group Clients (GC). Manufactures can change this value. Nothing prevents it. Android will randomly select IP for Group clients. Windows seems to start backwards but it did not search further.

* To turn a **Windows** PC into a hosted device, first check if the device supports hosted network by issuing the command `netsh wlan show drivers` in <ins>administrator mode </ins>  and see if `Hosted network supported: Yes`, if `No`, nothing can be done. Then, execute the commnad `netsh wlan set hostednetwork mode=allow ssid=SOME_SSID key=SOME_KEY` followed by `netsh wlan start hostednetwork`. You can now see the SSID in the network tab and connect to the network using <ins>SOME_KEY</ins> as specified.

## TCP Offload Engine (TOE)
* Sometimes you may observe some discrepancies in packet size (such as a packet bigger than MSS or MTU). Chances are that the operation system is using TOE. It can use `Large receive offload (LRO)`, which basically groups packets into larger ones to improve overall throughput. The size of packet will depend on the traffic speed. Larger traffic equals to larger packets (up to ~65K which it is the maximum TCP segment). It can also use `Large send offload (LSO)`, which allows operation system to pass a bigger TCP segment (usually ~65K) to be further split into smaller TCP segments (limited by MSS). Because wireshark sits after LRO act or after LSO has acted, it will capture packets with strange larger packets. However, nothing is transfered with segments bigger than MSS (and ultimately bigger than MTU).

## Useful Commands

### Wireshark
* To check for IP fragmentation use: ` ip.flags.mf == 1 or ip.frag_offset gt 0` or `ip[6:2]&3fff or icmp[1]==4` (more complete).

### TShark
* To list all interfaces use: `tshark(.exe) -D`
* To capture network traffic: `tshark(.exe) -f file.pcap -i 6 -s 100` (capture all network traffic from interface _6_ in file _file.pcap_ and limit the size of each packet to _100 bytes_).

### Windows

* To check `Max Speed` of the wifi card run `netsh wlan show interfaces` or `Get-NetAdapter | select interfaceDescription, name, status, linkSpeed`
* To check `MTU size` run `netsh ipv4 show interfaces` or `netsh interface ipv4 show subinterfaces`
* I observed when using winsock2 that sequential sockets with port 0 will be assigned sequential ports by the OS. Not sure if that also would happen with Linux or other OSs.

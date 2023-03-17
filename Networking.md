[< Back](https://github.com/brlebtag/My-Commonplace-Book)

# Networking Knowledge

## TCPv4
* The `Window field` in the TCPv4 packet is the <ins>receive window</ins> of the <ins>sender</ins>. On the other hand, when the other side receives this packet, Window field will become its <ins>send window</ins>.

* During 3-way handshake, the `window field` stores the sender's receive window size that will be used by the TCP protocol of the other side. In the option field, there is also `window scale` field, which expands the size of receive window. It is a tow byte field but only 14 (of 16) bits can be used to scale the window size (up to 1GB).

* Nothing will be transmitted bigger than the `Maximum segment size` but a big window size allows the other size to send more packets without acknowledgement.

* When Wireshark says that `TCP window specified by the receiver is now completely full`, it means that wireshark has computed the window size of the sender and realized it is full. It must have captured the 3-way handshake, otherwise, this information is wrong. It is always good to capture the 3-way handshake.

* I've noticed that `TCP Zero Window segment` is normal between 0 and 10 times. These results came from testing 1GB file transfers between PC and Android devices in a WLAN environment. More than this, it is a connection problem.

## Wifi-Direct
* Android uses IP range for wifi direct 192.168.49.1/24. Group Owner (GO) is always 192.168.49.1 (it is hard-coded in the codebase). On the other hand. Windows uses 192.168.137.1/24 (/24 is my supposition). Group Owner is 192.168.137.1.

* Android limits in the code to 5 Group Clients (GC). Manufactures can change this value. Nothing prevents it. Android will randomly select IP for Group clients. Windows seems to start backwards but it did not search further.

## Useful Commands

### Windows

* To check max speed of the wifi card: `netsh wlan show interfaces` or `Get-NetAdapter | select interfaceDescription, name, status, linkSpeed`

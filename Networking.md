# Networking Knowledge

## Wifi-Direct
* Android uses IP range for wifi direct 192.168.49.1/24. Group Owner (GO) is always 192.168.49.1 (it is hard-coded in the codebase). On the other hand. Windows uses 192.168.137.1/24 (/24 is my supposition). Group Owner is 192.168.137.1.

* Android limits in the code to 5 Group Clients (GC). Manufactures can change this value. Nothing prevents it. Android will randomly select IP for Group clients. Windows seems to start backwards but it did not search further.

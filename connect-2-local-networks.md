# Connect 2 Local Networks keeping the internet on 3rd network

## Network structure

1. Laptop has LAN and WIFI
2. LAN directly connected to 192.168.1.0 network mask 255.255.255.0 with router on 192.168.1.1
3. Other local network existed connected to LAN 2. It is on 10.1.1.0 with mask 255.255.255.0
4. WIFI card with internet gateway 192.168.1.101

## Goal

I need configure my laptop to connect to internet and connect to both LANs.

## Configuration

1. Set WIFI card TCP/IP default gateway to be 192.168.1.101
2. Set LAN card TCP/IP default gateway to empty.
3. Only 1 gateway should be set on all the network cards of the laptop.
4. Add manual route to routes table  

`
route add -p 10.1.1.0 mask 255.255.255.0 192.168.1.1 if 3
`  

destination subnet 10.1.1.0  
destination mask 255.255.255.0  
gateway 192.168.1.1  
interface 3 # this is my LAN interface number. it can be retrieved from "route print"  
persist the route -p  

**To delete the route**  
`
route delete 10.1.1.0
`

## Reference

[Route Article](https://www.mydigitallife.net/how-to-add-route-to-tcpip-routing-table-with-windows-routing-and-remote-access-console-or-dos-prompt/#:~:text=How%20to%20Add%20a%20Route%20on%20Windows%2010,rules%20is%20added%20correctly.Note%3A%20If%20any...%20See%20More.)

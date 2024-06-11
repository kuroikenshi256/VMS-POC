# VMS-POC

Step 1: Add Network Devices

    Add a Router:
      
    Add Switches:
        Go to Network Devices > Switches.
        Add the following switches to the workspace:
            Switch 1 for the camera network.
            Switch 2 for the VMS server.
            Switch 3 for client workstations.

    Add PCs and Webcams:
            PCs for the VMS server and client workstations.
            Video Cameras for IP cameras.

Step 3: Connect the Devices

    Connect the Switches to the Router:
        Select Connections (lightning bolt icon) and choose Copper Straight-Through.
        Connect:
            Router GigabitEthernet0/0 to Switch 1 GigabitEthernet0/1.
            Router GigabitEthernet0/1 to Switch 2 GigabitEthernet0/1.
            Router GigabitEthernet0/2 to Switch 3 GigabitEthernet0/1.

    Connect Devices to Switches:
        Switch 1 (Cisco 2960):
            Connect each Webcam to different ports (e.g., FastEthernet0/2 to FastEthernet0/6).
        Switch 2 (Cisco 3560):
            Connect a PC (VMS server) to FastEthernet0/2.
        Switch 3 (Cisco 3650):
            Connect each PC (client workstations) to different ports (e.g., FastEthernet0/2 to FastEthernet0/4).

Step 4: Configure IP Addresses
1. Router Configuration

    Assign IP Addresses to Router Interfaces:
        Click on the Router, go to CLI, and configure:
   ...
enable
configure terminal
interface GigabitEthernet0/0
ip address 192.168.10.1 255.255.255.0
no shutdown
exit
interface GigabitEthernet0/1
ip address 192.168.20.1 255.255.255.0
no shutdown
exit
interface GigabitEthernet0/2
ip address 192.168.30.1 255.255.255.0
no shutdown
end
write memory
...
   

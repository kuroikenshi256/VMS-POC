# VMS-POC
Here is the Topology for this VMS network
![image](https://github.com/kuroikenshi256/VMS-POC/assets/172290817/dbfa2756-df38-4949-a49d-cbfc65333bd2)

Step 1: Add Network Devices

    Add a Router:
        Drag and drop a Router to the workspace .

    Add Switches:
        Add three switches to the workspace:
            Switch 1 for the camera network.
            Switch 2 for the VMS server.
            Switch 3 for the client workstations.

    Add PCs and Webcams:
        Drag and drop:
            PCs to represent the VMS server and client workstations.
            Webcams from End Devices to simulate IP cameras.

Step 3: Connect the Devices

    Connect the Switches to the Router:
     Using RJ45, CAT5e or CAT6
        Connect:
            Router GigabitEthernet0/0 to Switch 1 GigabitEthernet0/1.
            Router GigabitEthernet0/1 to Switch 2 GigabitEthernet0/1.
            Router GigabitEthernet0/2 to Switch 3 GigabitEthernet0/1.

    Connect Devices to Switches:
        Connect each Webcam to different ports on Switch 1.
        Connect the PC (VMS server) to Switch 2.
        Connect the PCs (client workstations) to Switch 3.

Step 4: Configure IP Addresses
1. Router Configuration

    Assign IP Addresses:
        Click on the Router, go to CLI, and configure:

        plaintext

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

2. Configure IP Addresses on Webcams

    Webcams Configuration:
        Click on each Webcam, go to Config.
        Under Settings, set IP addresses in the 192.168.10.x range (e.g., 192.168.10.2, 192.168.10.3, etc.).

3. Configure IP Addresses on End Devices

    VMS Server:
        Click on the PC connected to Switch 2.
        Go to Desktop > IP Configuration.
        Set the IP address to 192.168.20.2, subnet mask to 255.255.255.0, and default gateway to 192.168.20.1.

    Client Workstations:
        Click on each PC connected to Switch 3.
        Go to Desktop > IP Configuration.
        Set IP addresses in the 192.168.30.x range (e.g., 192.168.30.2, 192.168.30.3, etc.), subnet mask to 255.255.255.0, and default gateway to 192.168.30.1.

Step 5: Configure Switches
1. Switch 1 for Camera Network

    Basic Configuration:
        Click on Switch 1, go to CLI, and configure:

        plaintext

    enable
    configure terminal
    hostname Switch1
    interface vlan 1
    ip address 192.168.10.254 255.255.255.0
    no shutdown
    end
    write memory

Configure VLAN (Optional):

    Create a VLAN for cameras:

    plaintext

        enable
        configure terminal
        vlan 10
        name Cameras
        exit
        interface range FastEthernet0/2-24
        switchport mode access
        switchport access vlan 10
        end

2. Switch 2 for VMS Server

    Basic Configuration:
        Click on Switch 2, go to CLI, and configure:

        plaintext

    enable
    configure terminal
    hostname Switch2
    interface vlan 1
    ip address 192.168.20.254 255.255.255.0
    no shutdown
    end
    write memory

Enable Routing (Optional):

    Enable IP routing to support inter-VLAN routing:

    plaintext

        enable
        configure terminal
        ip routing
        end

3. Switch 3 for Client Network

    Basic Configuration:
        Click on Switch 3, go to CLI, and configure:

        plaintext

    enable
    configure terminal
    hostname Switch3
    interface vlan 1
    ip address 192.168.30.254 255.255.255.0
    no shutdown
    end
    write memory

Configure VLAN (Optional):

    Create a VLAN for client devices:

    plaintext

        enable
        configure terminal
        vlan 30
        name Clients
        exit
        interface range FastEthernet0/2-24
        switchport mode access
        switchport access vlan 30
        end

Step 6: Set Up and Configure Webcams

    Click on Each Webcam:
        Go to the Webcam in the workspace.
        Click on Config and set up the device.

    Configure Network Settings:
        Under Network Settings, assign the camera an IP address that matches the camera network (e.g., 192.168.10.2).
        Set the default gateway to the router's IP (192.168.10.1).

    Configure Streaming Settings:
        Under Services, you might be able to configure settings for streaming or sending video feeds. Set the destination to the VMS server’s IP address (192.168.20.2).

Step 7: Test Connectivity

    Ping from VMS Server to Webcams:
        Open the Command Prompt on the VMS server (PC connected to Switch 2).
        Use the ping command to check connectivity with each webcam:

        plaintext

    ping 192.168.10.2
    ping 192.168.10.3

Ping from Client Workstations to VMS Server:

    Open the Command Prompt on the client PCs connected to Switch 3.
    Use the ping command to check connectivity with the VMS server:

    plaintext

        ping 192.168.20.2

    Verify Video Streams:
        From client PCs, access the VMS server. If the VMS server is configured with video management software, you should be able to view live feeds from the webcams.

Step 8: Save Your Configuration

    Document Network Configuration:
        Note down the IP addressing scheme and any specific settings for future reference.

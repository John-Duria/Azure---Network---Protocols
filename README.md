<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, HTTP/S, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10 (21H2)
- Ubuntu Server 20.04

<h2>Task</h2>

- Step 1. Create resources (Windows 10 and Ubuntu Server) 
- Step 2. Observe ICMP Traffic
- Step 3. Observe SSH Traffic
- Step 4. Observe DHCP Traffic
- Step 5. Observe DNS Traffic
- Step 6. Observe RDP Traffic

<h2>Actions and Observations</h2>

Creating a Resource Group and Deploying Windows 10 and Ubuntu Linux VMs steps:

Step 1: Create a Resource Group using the step-by-step tutorial on how to use Microsoft Azure to create a Resource Group on my repository.

Step 2: Create a Windows 10 Virtual Machine (VM)

    In the Azure Portal, search for and select "Virtual machines".
    Click "+ Create" to create a new virtual machine.
    Fill in the required details (e.g., VM name, region, image, size).
    Under "Resource group", select the resource group created in Step 1 (MyResourceGroup).
    Choose "Create new" for the Virtual Network and Subnet.
    Follow the prompts to complete the VM configuration.
    Click "Review + create" and then "Create" to deploy the VM.

Step 3: Create a Linux (Ubuntu) VM

    Repeat Steps 2-4 from the Windows VM creation process.
    Specify a different VM name, OS disk type, and select Ubuntu Server as the image.
    Use the same resource group (MyResourceGroup).
    This time, select "Use existing" for the Virtual Network and Subnet.
    Complete the configuration and deploy the Ubuntu VM.
You should get a similar output below.
![image](https://github.com/John-Duria/Azure---Network---Protocols/assets/168502429/34390e2c-9eab-43cf-8ff2-aed08e2e276a)
<br />

Exploring Network Analysis on a Windows 10 VM: Using Remote Desktop, Wireshark, and Observing ICMP Traffic steps:

Step 1: Use Remote Desktop to Connect to Your Windows 10 VM

    Retrieve Windows VM Public IP:
        In the Azure Portal, go to your Windows 10 VM's overview.
        Note down the "Public IP address" listed.

    Connect via Remote Desktop:
        Open Remote Desktop Connection on your local machine.
        Enter the Windows VM's public IP address.
        Click "Connect" and enter your VM credentials to establish the remote desktop session.

Step 2: Install Wireshark on Windows 10 VM

    Download Wireshark:
        Inside the Windows 10 VM, open a web browser.
        Go to the Wireshark download page.
        Download the installer suitable for your Windows version (64-bit recommended).

    Install Wireshark:
        Run the downloaded Wireshark installer.
        Follow the installation prompts to complete the setup.
        Make sure to select the option to install WinPcap or Npcap (required for packet capture).

Step 3: Open Wireshark and Filter for ICMP Traffic

    Launch Wireshark:
        Open Wireshark from the Start menu.

    Start Capturing Packets:
        Select the network interface connected to the Azure virtual network.
        Click on "Start" to begin capturing packets.

    Apply ICMP Filter:
        In the Wireshark capture window, enter icmp in the display filter box and press Enter.
        This will filter and display only ICMP (ping) traffic.

Step 4: Ping the Ubuntu VM from Windows 10 VM

    Retrieve Ubuntu VM Private IP:
        In the Azure Portal, go to your Ubuntu VM's overview.
        Note down the "Private IP address" listed.

    Ping the Ubuntu VM:
        Open Command Prompt or PowerShell on the Windows 10 VM.
        Use the command:

        bash

        ping <Ubuntu_VM_Private_IP>

        Observe the ICMP ping requests and replies in Wireshark.

Step 5: Ping a Public Website from Windows 10 VM

    Ping a Public Website:
        In the Command Prompt or PowerShell of the Windows 10 VM, execute:

        bash

        ping www.google.com

        Observe the outgoing ICMP traffic to Google in Wireshark.

Step 6: Test ICMP Traffic with Network Security Group (NSG) Rules

    Disable Incoming ICMP Traffic to Ubuntu VM:
        In the Azure Portal, navigate to your Ubuntu VM's networking settings.
        Open the associated "Network Security Group" (NSG).
        Disable the "Inbound ICMP" rule.

    Observe ICMP Traffic and Ping Activity:
        Back in the Windows 10 VM, observe Wireshark and ping activity to the Ubuntu VM. ICMP packets should be dropped.

    Re-enable Incoming ICMP Traffic:
        Enable the "Inbound ICMP" rule in the NSG for the Ubuntu VM.

    Observe ICMP Traffic and Ping Activity (Restored):
        Back in the Windows 10 VM, observe Wireshark and ping activity again. ICMP packets should now be received successfully.

    Stop the Ping Activity:
        Press Ctrl+C in the Command Prompt or PowerShell to stop the continuous ping.
<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

<p>
<img src="https://i.imgur.com/DJmEXEB.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
</p>
<br />

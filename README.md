<p align="center">
<img src="https://i.imgur.com/Ua7udoS.png" alt="Traffic Examination"/>
</p>

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>
In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. 

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

- Task 1. Creating a Resource Group and Deploying Windows 10 and Linux Ubuntu Server VMs.
- Task 2. Exploring Network Analysis on a Windows 10 VM: Using Remote Desktop, Wireshark, and Observing ICMP Traffic.
- Task 3. How to use Wireshark to capture and analyze SSH traffic.
- Task 4. How to capture and analyze DHCP traffic using Wireshark.
- Task 5. How to capture and analyze DNS (Domain Name System) traffic using Wireshark.
- Task 6. How to capture and analyze Remote Desktop Protocol (RDP) traffic using Wireshark.

<h2>Actions and Observations</h2>

<h3>Task 1: Creating a Resource Group and Deploying Windows 10 and Linux Ubuntu Server VMs steps:</h3>

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

<h3>Task 2: Exploring Network Analysis on a Windows 10 VM: Using Remote Desktop, Wireshark, and Observing ICMP Traffic steps:</h3>

Step 1: Use Remote Desktop to Connect to Your Windows 10 VM

    In the Azure Portal, go to your Windows 10 VM's overview.
    Note down the "Public IP address" listed.
    Open Remote Desktop Connection on your local machine.
    Enter the Windows VM's public IP address.
    Click "Connect" and enter your VM credentials to establish the remote desktop session.
    
![image](https://github.com/John-Duria/Azure---Network---Protocols/assets/168502429/5f7b7575-585c-4e8d-8e17-793e8cd4aade)

Step 2: Install Wireshark on Windows 10 VM

    Inside the Windows 10 VM, open a web browser.
    Go to the Wireshark download page.
    Download the installer suitable for your Windows version (64-bit recommended).
    Run the downloaded Wireshark installer.
    Follow the installation prompts to complete the setup.
    Make sure to select the option to install WinPcap or Npcap (required for packet capture).

Step 3: Open Wireshark and Filter for ICMP Traffic

    Open Wireshark from the Start menu.
    Select the network interface connected to the Azure virtual network.
    Click on "Start" to begin capturing packets.
    In the Wireshark capture window, enter icmp in the display filter box and press Enter.
    This will filter and display only ICMP (ping) traffic.

![image](https://github.com/John-Duria/Azure---Network---Protocols/assets/168502429/009c3306-3cff-474f-b507-e82b9b02368c)

Step 4: Ping the Ubuntu VM from Windows 10 VM

    
    In the Azure Portal, go to your Ubuntu VM's overview.
    Note down the "Private IP address" listed.
    Open Command Prompt or PowerShell on the Windows 10 VM.
    Use the command:ping <Ubuntu_VM_Private_IP>
    Observe the ICMP ping requests and replies in Wireshark as shown above.
        
![image](https://github.com/John-Duria/Azure---Network---Protocols/assets/168502429/2051ba85-e803-4e1a-9ef4-7be1a16aa26a)

Step 5: Test ICMP Traffic with Network Security Group (NSG) Rules

    In the Azure Portal, navigate to your Ubuntu VM's networking settings.
    Open the associated "Network Security Group" (NSG).
    Disable the "Inbound ICMP" rule.
        
![image](https://github.com/John-Duria/Azure---Network---Protocols/assets/168502429/75720b34-8261-47cd-be86-2b85f95d903f)

    
    Back in the Windows 10 VM, observe Wireshark and ping activity to the Ubuntu VM. 
        ICMP packets should be dropped.
    Enable the "Inbound ICMP" rule in the NSG for the Ubuntu VM.
    Back in the Windows 10 VM, observe Wireshark and ping activity again. 
        ICMP packets should now be received successfully.

![image](https://github.com/John-Duria/Azure---Network---Protocols/assets/168502429/fb004662-2cff-4f53-97a7-a6f86b2abdc0)

    Press Ctrl+C in the Command Prompt or PowerShell to stop the continuous ping.

Analysis and Observations:
The ICMP analysis using Wireshark provided visibility into the network communication patterns and behaviors between the Windows 10 and Ubuntu VMs in an Azure environment. The observations helped validate connectivity, diagnose potential issues (such as blocked ICMP traffic), and verify the resolution of connectivity problems through network configuration adjustments.

<h3>Task 3: How to use Wireshark to capture and analyze SSH traffic steps:</h3>

Step 1: Filter for SSH Traffic Only in Wireshark

    Open Wireshark from the Start menu on your Windows 10 VM.
    Select the network interface connected to the Azure virtual network.
    Click on "Start" to begin capturing packets.
    In the Wireshark capture window, enter ssh in the display filter box and press Enter.
    This will filter and display only SSH traffic.

Step 2: SSH into Ubuntu VM from Windows 10 VM

    In the Azure Portal, go to your Ubuntu VM's overview.
    Note down the "Private IP address" listed.
    Open Command Prompt or PowerShell on Windows 10 VM:
    In Command Prompt, initiate an SSH connection using the Ubuntu VM's private IP address:
    ssh username@<Ubuntu_VM_Private_IP>
    Replace username with your Ubuntu VM's username and <Ubuntu_VM_Private_IP> with the private IP address.
    Enter your Ubuntu VM's password when prompted.
    Once connected, you should see the username and hostname of Ubuntu VM.

Observe SSH Traffic in Wireshark:

    In the Wireshark capture window, observe the SSH traffic as you interact with the Ubuntu VM over SSH.
    You should see SSH packets (e.g., SSH handshake, data transfer) in the Wireshark capture.
    To exit the SSH connection, type exit and press Enter in the Command Prompt.

![image](https://github.com/John-Duria/Azure---Network---Protocols/assets/168502429/02c84757-2d6e-403d-8433-1e9c01fd60aa)
    
<h3>Task 4: How to capture and analyze DHCP traffic using Wireshark steps:</h3>

Step 1: Filter for DHCP Traffic Only in Wireshark

    In the Wireshark capture window, enter dhcp in the display filter box and press Enter.
    This will filter and display only DHCP traffic.
    Launch Command Prompt or PowerShell with administrative privileges.
    In the Command Prompt or PowerShell, execute the following command to renew the IP address from DHCP:
      
    ipconfig /renew

    This command requests a new IP address lease from the DHCP server.

    Switch back to the Wireshark capture window.
    You should see DHCP traffic related to the IP address renewal process captured in Wireshark.
    Look for DHCP Discover, Offer, Request, and Acknowledge messages exchanged between the 
    Windows 10 VM and the DHCP server.

Analysis and Observations:

    DHCP Request: The Windows 10 VM sends a DHCP Request to request the offered IP address.
    DHCP Acknowledge: The DHCP server sends a DHCP Acknowledge message to confirm the 
    IP address lease renewal.

![image](https://github.com/John-Duria/Azure---Network---Protocols/assets/168502429/10e6af74-106c-4bb9-a086-0296036cc8de)

<h3>Task 5: How to capture and analyze DNS (Domain Name System) traffic using Wireshark steps:</h3>

Step 1: Filter for DNS Traffic Only in Wireshark

    In the Wireshark capture window, enter dns in the display filter box and press Enter.
    This will filter and display only DNS traffic.

Step 2: Use nslookup to Resolve DNS Queries

    Open Command Prompt on Windows 10 VM:
    Launch Command Prompt with administrative privileges.
    In the Command Prompt, execute the following commands to resolve the IP addresses of google.com

    nslookup google.com

    nslookup is a command-line tool used to query DNS servers and obtain DNS records, 
    such as IP addresses associated with domain names.
    Switch back to the Wireshark capture window.
    You should see DNS query and response packets related to the nslookup commands captured in Wireshark.
    Look for DNS queries for google.com as well as the corresponding DNS responses containing IP addresses.

Analysis and Observations:

    DNS Query (DNS Request): The Windows 10 VM sends DNS queries (A record requests) 
    for google.com to DNS servers.
    DNS Response: DNS servers respond with DNS response packets containing IP addresses 
    associated with google.com.

![image](https://github.com/John-Duria/Azure---Network---Protocols/assets/168502429/df4e2827-fb6a-4095-a7c2-98b449afae47)

<h3>Task 6: How to capture and analyze Remote Desktop Protocol (RDP) traffic using Wireshark steps:</h3>

Step 1: Filter for RDP Traffic (TCP Port 3389) in Wireshark

    In the Wireshark capture window, enter tcp.port == 3389 in the display filter box and press Enter.
    This will filter and display only TCP traffic on port 3389, which is used by RDP.

Step 18: Observe Continuous RDP Traffic and Analysis

    Notice that when filtering for RDP traffic (tcp.port == 3389), you will likely observe continuous
    packets being transmitted, even when no specific user activity is occurring within the RDP session.

    RDP (Remote Desktop Protocol) is designed to provide remote access and control of a computer over 
    a network.
    RDP sessions typically involve a constant stream of data between the client (local machine) and the 
    server (remote machine) to maintain the remote desktop display, respond to user inputs, and transmit
    audio/video data (if enabled).

    The non-stop traffic observed in RDP captures is attributed to the nature of the RDP protocol itself.
    RDP operates by continuously transmitting updates of the remote desktop screen, mouse movements, 
    keyboard inputs, and other interactive elements.
    Even when there is no user activity (such as mouse clicks or keyboard typing), the RDP protocol 
    remains active to maintain a live and responsive remote desktop experience.

Analysis and Observations:

    Continuous Stream of Data: RDP traffic appears as a constant stream of data due to the real-time nature 
    of remote desktop interaction.
    Protocol Behavior: RDP protocol is optimized to provide a responsive and interactive remote desktop 
    experience, leading to continuous traffic flow between the client and server.
    Difference from Activity-based Traffic: Unlike other protocols that show traffic only during specific 
    user activities (e.g., HTTP requests in web browsing), RDP traffic is persistent and reflects the 
    ongoing nature of remote desktop sessions.

![image](https://github.com/John-Duria/Azure---Network---Protocols/assets/168502429/7f459042-c224-4b1c-8c80-21ae1adb830e)

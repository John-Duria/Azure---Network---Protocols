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

Step 1: Create a Resource Group using the step-by-step tutorial on [Creating Resource Group within Azure](https://github.com/John-Duria/Azure---Resource-Group) on my repository.

Step 2: Create a Windows 10 Virtual Machine (VM)

    In the Azure Portal, search for and select "Virtual machines".
    Click "+ Create" to create a new virtual machine.
    Fill in the required details (e.g., VM name, region, image, size).
    Under "Resource group", select the resource group created in Step 1.
    Choose "Create new" for the Virtual Network and Subnet.
    Follow the prompts to complete the VM configuration.
    Click "Review + create" and then "Create" to deploy the VM.

![image](https://github.com/John-Duria/Azure---Network---Protocols/assets/168502429/bedc83aa-c92d-4a29-bfff-882ad8745839)

Step 3: Create a Linux (Ubuntu) VM

    Repeat Steps 2 from the Windows VM creation process.
    Specify a different VM name, OS disk type, and select Ubuntu Server as the image.
    Use the same resource group.
    This time, select "Use existing" for the Virtual Network and Subnet.
    Complete the configuration and deploy the Ubuntu VM.

![image](https://github.com/John-Duria/Azure---Network---Protocols/assets/168502429/60834cf6-e95b-4901-aa84-536d3e01ff82)

<h3>Task 2: Exploring Network Analysis on a Windows 10 VM: Using Remote Desktop, Wireshark, and Observing ICMP Traffic steps:</h3>

Step 1: Use Remote Desktop to Connect to Your Windows 10 VM

    In the Azure Portal, go to your Windows 10 VM's overview.
    Note down the "Public IP address" listed.
    Open Remote Desktop Connection on your local machine.
    Enter the Windows VM's public IP address.
    Click "Connect" and enter your VM credentials to establish the remote desktop session.
    
![image](https://github.com/John-Duria/Azure---Network---Protocols/assets/168502429/d007f3ed-a43b-444d-9751-c0fde346d47d)

Step 2: Install Wireshark on Windows 10 VM

    Inside the Windows 10 VM, open a web browser.
    Go to the Wireshark download page.
    Download the installer suitable for your Windows version (64-bit recommended).
    Run the downloaded Wireshark installer.
    Follow the installation prompts to complete the setup.
    Make sure to select the option to install WinPcap or Npcap (required for packet capture).

![image](https://github.com/John-Duria/Azure---Network---Protocols/assets/168502429/271cad16-a023-41b4-8c89-e6b363723106)

Step 3: Open Wireshark and Filter for ICMP Traffic

    Open Wireshark from the Start menu.
    Select the network interface connected to the Azure virtual network.
    Click on "Start" to begin capturing packets.
    In the Wireshark capture window, enter icmp in the display filter box and press Enter.
    This will filter and display only ICMP (ping) traffic.

![image](https://github.com/John-Duria/Azure---Network---Protocols/assets/168502429/d61f9d15-26b0-4552-9999-f8dba348ac9e)

Step 4: Retrieve Private IP Address and Ping the Ubuntu VM from Windows 10 VM

    In the Azure Portal, go to your Ubuntu VM's overview.
    Note down the "Private IP address" listed.
    Open Command Prompt or PowerShell on the Windows 10 VM.
    Use the command:ping <Ubuntu_VM_Private_IP>
    Observe the ICMP ping requests and replies in Wireshark as shown above.
        
![image](https://github.com/John-Duria/Azure---Network---Protocols/assets/168502429/69831d2d-29c7-4708-b59b-d53a30657d45)

![image](https://github.com/John-Duria/Azure---Network---Protocols/assets/168502429/74ab3db0-8fbe-4df1-b703-deedd3896a77)

Step 5: Test ICMP Traffic with Network Security Group (NSG) Rules

    In the Azure Portal, navigate to your Ubuntu VM's networking settings.
    Open the associated "Network Security Group" (NSG).
    Disable the "Inbound ICMP" rule.
        
![image](https://github.com/John-Duria/Azure---Network---Protocols/assets/168502429/7abbf841-1cab-4b28-8ebd-d6c4ae96d6fa)

Step 6: Observe Effects in Wiresharck and Ping Activity

    Back in the Windows 10 VM, observe Wireshark and ping activity to the Ubuntu VM. 
    ICMP packets should be dropped.

![image](https://github.com/John-Duria/Azure---Network---Protocols/assets/168502429/91c97e52-3b9d-4f82-8e3b-722773628863)

Step 7: Re-enable ICMP Traffic

    Enable the "Inbound ICMP" rule in the NSG for the Ubuntu VM.
    Back in the Windows 10 VM, observe Wireshark and ping activity again. 
    ICMP packets should now be received successfully.

![image](https://github.com/John-Duria/Azure---Network---Protocols/assets/168502429/117e4304-7f38-4973-a86f-87a4f5069c9c)

![image](https://github.com/John-Duria/Azure---Network---Protocols/assets/168502429/d598f4f8-c78d-48ba-8348-ce3f84fb047f)

Step 8: Stop the Ping Activity

    Press Ctrl+C in the Command Prompt or PowerShell to stop the continuous ping.

![image](https://github.com/John-Duria/Azure---Network---Protocols/assets/168502429/143aec8c-2936-4ad1-91c3-09ae8ae3fedc)

Analysis and Observations:

The ICMP analysis using Wireshark provided visibility into the network communication patterns and behaviors between the Windows 10 and Ubuntu VMs in an Azure environment. The observations helped validate connectivity, diagnose potential issues (such as blocked ICMP traffic), and verify the resolution of connectivity problems through network configuration adjustments.

<h3>Task 3: How to use Wireshark to capture and analyze SSH traffic steps:</h3>

Step 1: Filter for SSH Traffic Only in Wireshark

    Open Wireshark from the Start menu on your Windows 10 VM.
    Select the network interface connected to the Azure virtual network.
    Click on "Start" to begin capturing packets.
    In the Wireshark capture window, enter ssh in the display filter box and press Enter.
    This will filter and display only SSH traffic.

![image](https://github.com/John-Duria/Azure---Network---Protocols/assets/168502429/718ecab2-696e-46b4-aea1-4ae57314078d)

Step 2: SSH into Ubuntu VM from Windows 10 VM

    In the Azure Portal, go to your Ubuntu VM's overview.
    Note down the "Private IP address" listed.
    Open Command Prompt or PowerShell on Windows 10 VM:
    In Command Prompt, initiate an SSH connection using the Ubuntu VM's private IP address:
    ssh username@<Ubuntu_VM_Private_IP>
    Replace username with your Ubuntu VM's username and <Ubuntu_VM_Private_IP> with the private IP address.
    Enter your Ubuntu VM's password when prompted.
    Once connected, you should see the username and hostname of Ubuntu VM.

![image](https://github.com/John-Duria/Azure---Network---Protocols/assets/168502429/c4264637-63e0-493d-97d7-cf224f97ad76)

Step 3: Observe SSH Traffic in Wireshark and Exit SSH Session

    In the Wireshark capture window, observe the SSH traffic as you interact with the Ubuntu VM over SSH.
    Once connected via SSH, type Linux commands (e.g., pwd, ls, etc.) into the SSH session on the Windows 10 VM.
    Observe the output of these commands within the SSH connection.
    You should see SSH packets (e.g., SSH handshake, data transfer) in the Wireshark capture.
    To exit the SSH connection, type exit and press Enter in the Command Prompt.

![image](https://github.com/John-Duria/Azure---Network---Protocols/assets/168502429/0d019b8b-8925-49d7-a61f-cd3df541a37c)
    
<h3>Task 4: How to capture and analyze DHCP traffic using Wireshark steps:</h3>

Step 1: Filter for DHCP Traffic Only in Wireshark

    In the Wireshark capture window, enter dhcp in the display filter box and press Enter.
    This will filter and display only DHCP- related packets (including DHCP discover,offer, request, acknowledge) 
    in the Wireshark capture.

![image](https://github.com/John-Duria/Azure---Network---Protocols/assets/168502429/013c0b4d-8f4c-4d7a-94bc-187206928b0c)

Step 2: Attempt to Renew IP Address on Windows 10 VM

    Launch Command Prompt or PowerShell with administrative privileges.
    In the Command Prompt or PowerShell, execute the following command to renew the IP address from DHCP:
      
    ipconfig /renew

    This command requests a new IP address lease from the DHCP server.

 Step 3: Observe DHCP traffic in Wireshark
    
    Switch back to the Wireshark capture window.
    You should see DHCP traffic related to the IP address renewal process captured in Wireshark.
    Look for DHCP Discover, Offer, Request, and Acknowledge messages exchanged between the 
    Windows 10 VM and the DHCP server.

![image](https://github.com/John-Duria/Azure---Network---Protocols/assets/168502429/2441186a-d239-4338-a447-1fc48e240100)

Analysis and Observations:

    DHCP Request: The Windows 10 VM sends a DHCP Request to request the offered IP address.
    DHCP Acknowledge: The DHCP server sends a DHCP Acknowledge message to confirm the 
    IP address lease renewal.

<h3>Task 5: How to capture and analyze DNS (Domain Name System) traffic using Wireshark steps:</h3>

Step 1: Filter for DNS Traffic Only in Wireshark

    In the Wireshark capture window, enter dns in the display filter box and press Enter.
    This will filter and display only DNS traffic.

![image](https://github.com/John-Duria/Azure---Network---Protocols/assets/168502429/aefe9f57-3e5f-487e-a5af-e3a1d6c75ee5)

Step 2: Use nslookup to Resolve DNS Queries

    Open Command Prompt on Windows 10 VM:
    Launch Command Prompt with administrative privileges.
    In the Command Prompt, execute the following commands to resolve the IP addresses of google.com and disney.com
        
        To query the IP address of google.com using nslookup, run the following command:
        nslookup google.com

        Similarly, query the IP address of disney.com using nslookup:
        nslookup disney.com

    nslookup is a command-line tool used to query DNS servers and obtain DNS records, 
    such as IP addresses associated with domain names.
    Switch back to the Wireshark capture window.
    You should see DNS query and response packets related to the nslookup commands captured in Wireshark.
    Look for DNS queries for google.com as well as the corresponding DNS responses containing IP addresses.

![image](https://github.com/John-Duria/Azure---Network---Protocols/assets/168502429/ba650b00-42a3-41ff-a804-2978834f82ab)

Analysis and Observations:

    DNS Query (DNS Request): The Windows 10 VM sends DNS queries (A record requests) 
    for google.com to DNS servers.
    DNS Response: DNS servers respond with DNS response packets containing IP addresses 
    associated with google.com.

![image](https://github.com/John-Duria/Azure---Network---Protocols/assets/168502429/d0a0cb84-1f31-43e1-b0be-801a807b9c69)

<h3>Task 6: How to capture and analyze Remote Desktop Protocol (RDP) traffic using Wireshark steps:</h3>

Step 1: Filter for RDP Traffic (TCP Port 3389) in Wireshark

    In the Wireshark capture window, enter tcp.port == 3389 in the display filter box and press Enter.
    This will filter and display only TCP traffic on port 3389, which is used by RDP.

Step 2: Observe Continuous RDP Traffic and Analysis

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

![image](https://github.com/John-Duria/Azure---Network---Protocols/assets/168502429/e1dc0a83-04f7-45b1-ae5e-abef4d370632)


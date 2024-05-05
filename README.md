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

<h2>High-Level Steps</h2>

- Step 1. Create resources (Windows 10 and Ubuntu Server) 
- Step 2. Observe ICMP Traffic
- Step 3. Observe SSH Traffic
- Step 4. Observe DHCP Traffic
- Step 5. Observe DNS Traffic
- Step 6. Observe RDP Traffic

<h2>Actions and Observations</h2>

![image](https://github.com/John-Duria/Azure---Network---Protocols/assets/168502429/34390e2c-9eab-43cf-8ff2-aed08e2e276a)


Setting up an Azure virtual machines involves the following steps:

Step 1: Create a Resource Group using the step-by-step tutorial on how to use Microsoft Azure to create a Resource Group on my repository.

Step 2: Create a Windows 10 Virtual Machine (VM)

In the Azure Portal, search for and select "Virtual machines".

<p>Click "+ Create" to create a Azure virtual machine.</p>
<p>Fill in the required details (e.g., VM name, region, image, size).</p>
<p>Under "Resource group", select the resource group created in Step 1 (MyResourceGroup).</p>
<p>In Networking tab Choose "Create new" for the Virtual Network and Subnet.</p>
<p>Follow the prompts to complete the VM configuration.</p>
<p>Click "Review + create" and then "Create" to deploy the VM.</p>

Step 3: Create a Linux (Ubuntu) VM

    Repeat Steps 2-4 from the Windows VM creation process.
        Specify a different VM name, OS disk type, and select Ubuntu Server as the image.
        Use the same resource group (MyResourceGroup).
        This time, select "Use existing" for the Virtual Network and Subnet.
        Complete the configuration and deploy the Ubuntu VM.
<br />

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

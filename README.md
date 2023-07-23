
![network-security-group-interaction](https://github.com/AIweave/microsoft-azure/assets/121763338/50ba90a5-1c2b-4654-9222-2c949ee168df)

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>

In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />

**Must Know**: [Network Security Groups](https://docs.microsoft.com/en-us/azure/virtual-network/network-security-groups-overview) is a tool in Azure that contains security rules that inspect incoming and outgoing traffic in a network for the allowing or denying of packages. [Wireshark](https://www.comptia.org/content/articles/what-is-wireshark-and-how-to-use-it) is the application used to capture and observe packets being transmitted in a network. Two virtual machines (VMs) will be used in this process. [Microsoft Remote Desktop](https://www.google.com/search?q=remote+desktop+is&client=safari&rls=en&biw=1920&bih=1000&sxsrf=AB5stBiOBLLwtDq2wH81RM_KnRnqJ48yhw%3A1690078451681&ei=84y8ZMCJKbukqtsPodeCMA&ved=0ahUKEwiAz4Tu4KOAAxU7kmoFHaGrAAYQ4dUDCA8&uact=5&oq=remote+desktop+is&gs_lp=Egxnd3Mtd2l6LXNlcnAiEXJlbW90ZSBkZXNrdG9wIGlzMgUQABiABDIFEAAYgAQyBRAAGIAEMgUQABiABDIFEAAYgAQyBRAAGIAEMgUQABiABDIFEAAYgAQyBRAAGIAEMgUQABiABEiINlDdCFjUKnACeAGQAQOYAfcEoAGFGKoBCzQuOS4xLjEuMS4xuAEDyAEA-AEBqAIUwgIKEAAYRxjWBBiwA8ICBxAjGOoCGCfCAhYQLhgDGI8BGOoCGLQCGIwDGOUC2AEBwgIWEAAYAxiPARjqAhi0AhiMAxjlAtgBAcICCBAAGIoFGJECwgILEAAYgAQYsQMYgwHCAgsQLhiABBjHARjRA8ICCxAuGIAEGLEDGIMBwgIREC4YgwEYxwEYsQMY0QMYgATCAgsQLhiKBRixAxiDAcICERAuGIAEGLEDGIMBGMcBGNEDwgIEECMYJ8ICBxAjGIoFGCfCAgcQABiKBRhDwgIKEAAYigUYsQMYQ8ICCBAAGIAEGLEDwgILEAAYgAQYsQMYyQPiAwQYACBBiAYBkAYIugYGCAEQARgL&sclient=gws-wiz-serp) is a program for remotely connecting and interacting with a computer from another location. 

<h2>Video Demonstration</h2>

- ### [YouTube: Azure Virtual Machines, Wireshark, and Network Security Groups](https://www.youtube.com)

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines)
- Microsoft Remote Desktop
- Various Command-Line Tools
- Various Network Protocols (SSH, RDH, DNS, DHCP, ICMP)
- Wireshark (Protocol Analyzer)

<h2>Operating Systems Used </h2>

- Windows 10
- Ubuntu Server 20.04


<h2>Instructions</h2>

- **Part 1 (Create the Resources)**
  - In Azure, create a Resource Group.
  - Next, create the first VM, Windows 10 Virtual Machine. 
  - While creating the VM, select the previously created Resource Group.
  - Allow it to create a new Virtual Network (Vnet) and Subnet.
  - Create the second VM, Linux (Ubuntu) (VM2).
  - While creating the VM, select the previously created Resource Group and Vnet.

- **Part 2 (Observe ICMP Traffic)**
Use Remote Desktop to connect to your Windows 10 Virtual Machine
Within your Windows 10 Virtual Machine, Install Wireshark
Open Wireshark and filter for ICMP traffic only
Retrieve the private IP address of the Ubuntu VM and attempt to ping it from within the Windows 10 VM
Observe ping requests and replies within WireShark
From The Windows 10 VM, open command line or PowerShell and attempt to ping a public website (such as www.google.com) and observe the traffic in WireShark
Initiate a perpetual/non-stop ping from your Windows 10 VM to your Ubuntu VM
Open the Network Security Group your Ubuntu VM is using and disable incoming (inbound) ICMP traffic
Back in the Windows 10 VM, observe the ICMP traffic in WireShark and the command line Ping activity
Re-enable ICMP traffic for the Network Security Group your Ubuntu VM is using
Back in the Windows 10 VM, observe the ICMP traffic in WireShark and the command line Ping activity (should start working)
Stop the ping activity

Part 2 (Observe SSH Traffic)
Back in Wireshark, filter for SSH traffic only
From your Windows 10 VM, “SSH into” your Ubuntu Virtual Machine (via its private IP address)
Type commands (username, pwd, etc) into the linux SSH connection and observe SSH traffic spam in WireShark
Exit the SSH connection by typing ‘exit’ and pressing [Enter]

Part 2 (Observe DHCP Traffic)
Back in Wireshark, filter for DHCP traffic only
From your Windows 10 VM, attempt to issue your VM a new IP address from the command line (ipconfig /renew)
Observe the DHCP traffic appearing in WireShark

Part 2 (Observe DNS Traffic)
Back in Wireshark, filter for DNS traffic only
From your Windows 10 VM within a command line, use nslookup to see what google.com and disney.com’s IP addresses are
Observe the DNS traffic being show in WireShark

Part 2 (Observe RDP Traffic)
Back in Wireshark, filter for RDP traffic only (tcp.port == 3389)
Observe the on-going spam of traffic 



https://learn.microsoft.com/en-us/azure/virtual-network/network-security-groups-overview

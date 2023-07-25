
![network-security-group-interaction](https://github.com/AIweave/microsoft-azure/assets/121763338/50ba90a5-1c2b-4654-9222-2c949ee168df)

<h1>Network Security Groups (NSGs) and Inspecting Traffic Between Azure Virtual Machines</h1>

In this tutorial, we observe various network traffic to and from Azure Virtual Machines with Wireshark as well as experiment with Network Security Groups. <br />

**Must Know**: [Network Security Groups](https://docs.microsoft.com/en-us/azure/virtual-network/network-security-groups-overview) is a tool in Azure that contains security rules that inspect incoming and outgoing traffic in a network for the allowing or denying of packages. [Wireshark](https://www.comptia.org/content/articles/what-is-wireshark-and-how-to-use-it) is the application used to capture and observe packets being transmitted in a network. Two virtual machines (VMs) will be used in this process. [Microsoft Remote Desktop](https://www.google.com/search?q=remote+desktop+is&client=safari&rls=en&biw=1920&bih=1000&sxsrf=AB5stBiOBLLwtDq2wH81RM_KnRnqJ48yhw%3A1690078451681&ei=84y8ZMCJKbukqtsPodeCMA&ved=0ahUKEwiAz4Tu4KOAAxU7kmoFHaGrAAYQ4dUDCA8&uact=5&oq=remote+desktop+is&gs_lp=Egxnd3Mtd2l6LXNlcnAiEXJlbW90ZSBkZXNrdG9wIGlzMgUQABiABDIFEAAYgAQyBRAAGIAEMgUQABiABDIFEAAYgAQyBRAAGIAEMgUQABiABDIFEAAYgAQyBRAAGIAEMgUQABiABEiINlDdCFjUKnACeAGQAQOYAfcEoAGFGKoBCzQuOS4xLjEuMS4xuAEDyAEA-AEBqAIUwgIKEAAYRxjWBBiwA8ICBxAjGOoCGCfCAhYQLhgDGI8BGOoCGLQCGIwDGOUC2AEBwgIWEAAYAxiPARjqAhi0AhiMAxjlAtgBAcICCBAAGIoFGJECwgILEAAYgAQYsQMYgwHCAgsQLhiABBjHARjRA8ICCxAuGIAEGLEDGIMBwgIREC4YgwEYxwEYsQMY0QMYgATCAgsQLhiKBRixAxiDAcICERAuGIAEGLEDGIMBGMcBGNEDwgIEECMYJ8ICBxAjGIoFGCfCAgcQABiKBRhDwgIKEAAYigUYsQMYQ8ICCBAAGIAEGLEDwgILEAAYgAQYsQMYyQPiAwQYACBBiAYBkAYIugYGCAEQARgL&sclient=gws-wiz-serp) is a program for remotely connecting and interacting with a computer from another location. 

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
  - Use Microsoft Remote Desktop to connect to your Windows 10 Virtual Machine.
  - Within Windows 10, install [Wireshark](https://www.wireshark.org/download.html) from the internet.
  - Open Wireshark and filter for ICMP traffic only.
 
    ![Screen Shot 2023-07-23 at 12 19 51 AM](https://github.com/AIweave/microsoft-azure/assets/121763338/12f634d8-2fd8-4bd9-a036-3f7b08b9a372)


  - Retrieve the private IP address of the Ubuntu VM and attempt to ping it from within the Windows 10 VM command prompt.
  - Observe ping requests and replies within WireShark.
    (A "Reply" means that Windows 10 successfully communicated with Ubuntu's network.)
    
    ![Screen Shot 2023-07-23 at 12 15 09 AM](https://github.com/AIweave/microsoft-azure/assets/121763338/8b7e1a2b-a001-406f-9a2a-e63f3961d616)

- **(Observe SSH Traffic)**
  - Back in Wireshark, filter for SSH traffic only.
  - From your Windows 10 VM,“SSH into” your Ubuntu Virtual Machine (via its private IP address) by typing "ssh (Private IP)" within the command prompt.
  - Enter "yes" to continue connecting, then enter the Ubuntu's creditials (username, pwd) for access. (The username@VM name will be highighted in green to signify a successful connection.)

    ![Screen Shot 2023-07-25 at 11 03 11 AM](https://github.com/AIweave/microsoft-azure/assets/121763338/2583e876-1e80-4f7f-bb9d-e9168f644b2d)
    
    ![Screen Shot 2023-07-22 at 11 59 13 PM](https://github.com/AIweave/microsoft-azure/assets/121763338/f3dff505-93a6-4c9a-ad2d-b26099608be1)

  - Observe SSH traffic spam in WireShark.

    ![Screen Shot 2023-07-25 at 11 03 58 AM](https://github.com/AIweave/microsoft-azure/assets/121763338/9eb83e2c-2b25-4383-bce9-7e1a09b189d6)

  - Exit the SSH connection by typing ‘exit’ and pressing [Enter].

- **(Observe DHCP Traffic)**
  - Back in Wireshark, filter for DHCP traffic only.
  - From your Windows 10 VM, attempt to issue your VM a new IP address from the command line (ipconfig /renew).
 
    ![Screen Shot 2023-07-25 at 11 05 25 AM](https://github.com/AIweave/microsoft-azure/assets/121763338/805d5dc1-e27c-4403-b255-1d7efab320a0)

  - Observe the DHCP traffic appearing in WireShark.

- **(Observe DNS Traffic)**
  - Back in Wireshark, filter for DNS traffic only.
  - In Windows 10 command prompt, type "nslookup www.google.com" to see what google.com's IP addresses istpc.

    ![Screen Shot 2023-07-25 at 11 11 15 AM](https://github.com/AIweave/microsoft-azure/assets/121763338/2af23ab9-43c9-48a4-98cb-a03e3b7cadf2)

  - Observe the DNS traffic being show in WireShark.

- **(Observe RDP Traffic)**
  - Back in Wireshark, filter for RDP traffic only by entering "tcp.port == 3389"
  - Observe the on-going spam of traffic
 
    ![Screen Shot 2023-07-25 at 11 06 45 AM](https://github.com/AIweave/microsoft-azure/assets/121763338/32b8a695-4b0d-4f7a-9ab0-cd2122055c50)


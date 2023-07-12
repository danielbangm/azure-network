![image](https://github.com/danielbangm/azure-ressources/assets/22795502/074de211-4659-4e32-93b0-52a7f8eed69e)

<h1>Azure activities: Performing Activities on the Network</h1>
This tutorial dives into some compute and networking for a better understanding of firewall and really solidify our understanding of network protocols.

<h2>Environment and Technologies Used</h2>

- Microsoft Azure Virtual Machine VM1 (Windows 10)
- Microsoft Azure Virtual Machine VM2 (Linux~Ubuntu)
- Remote Desktop
- Wireshark (a Protocol Analyser)
- Bunch of Commands line tools

<h2>Operating Systems Used</h2>

- Windows 10
- Ubuntu

<h2>List of Prerequisites</h2>

- Make sure you completed the first part of this lab and have your VMs ready and running in portal.azure

<h2>Labs steps</h2>

- Step 1: Connect to Azure VM 1

<p>
To do this, we are going to use Remote Desktop Connection from our PC to remotely connect to VM1. If you're using a windows machine you can just tab Remote desktop in the search bar . If you are a Mac's user, you should download Microsoft Remote Desktop first. We are going to grab the Public IP address of VM1 in Azure to use in remote access.
</p> 

![image](https://github.com/danielbangm/azure-network/assets/22795502/2fdd6306-a9ef-44be-a910-0a6b2fcc4051)
![image](https://github.com/danielbangm/azure-network/assets/22795502/fd5e5238-0bc7-4258-a713-6cd69377aa57)

- Step 2: Install Wireshark in VM1
<p>
From VM1, we're going to install a program call wireshark and use it to inspect traffic as we interact with VM2. Choose adapter and you can capture the traffic even though we're not doing anything yet. You can also filter the traffic in wireshark for example by ICMP, TCP, etc...
</p>

![image](https://github.com/danielbangm/azure-network/assets/22795502/d4179653-4828-4126-8707-c5c2e8a60052)

- Step 3: Ping VM2 from VM2

<p>
 From VM1 let's try to ping VM2. To do that you need to go back to www.portal.azure.com to find VM2 private IP address (10.0.0.5 in this case) and then go back to the remote desktop inside VM1. Use the powershell command and tape "ping 10.0.0.5 The ping was successful because VM1 and VM2 are basically in the same network. Now we're going to initiate a perpertual ping with the command "ping 10.0.0.5 -t", Notice we have non-stop echo packets   
</p>

![image](https://github.com/danielbangm/azure-network/assets/22795502/07305e97-3744-4b00-9740-3c880d40c315)

- step 4: Configuring VM2 Firewall

<p>
We are going to block ICMP from the Firewall in VM2. In order to do that we can just go back to www.portal.azure.com and browse for Network Security Group. Then choose VM2 -- Settings -- Inbound security rules. As of now there's no rule on ICMP so we're going to create a new rule from any source to any destination, protocol is ICMP and the action is deny. After applying that rule on the Network Security Group of VM2, go back to VM1 and observe how our requests are now timed out. This is because the firewall is now denying any incoming traffic from ICMP and you can also notice there's no more reply from wireshark as well. If this is not making sense to you here's a great ressource on how <a href="https://<a href="https://learn.microsoft.com/en-us/azure/virtual-network/network-security-groups-overview">Azure Security Group</a> works.
</p>

![image](https://github.com/danielbangm/azure-network/assets/22795502/5ab70701-18b7-4343-926a-e2ff450b0f90)
![image](https://github.com/danielbangm/azure-network/assets/22795502/91a2c31d-97a6-4c2e-b392-6f5508baca75)


- Step 5: Reconfiguring VM2 Firewall
  
<p>
We are just going to reallow ICMP in our VM2's Network Security Group and observe how our requests will now have reply. To do that we just going to portal.Azure then Network Security Group and allow ICMP
</p>

![image](https://github.com/danielbangm/azure-network/assets/22795502/4f42ac31-4ca2-4a14-914a-9ed8d38c1191)
![image](https://github.com/danielbangm/azure-network/assets/22795502/7020fd26-133b-4d65-9854-00f6b409d003)

-  Step 6: Connect TO VM2 via SSH from VM1

<p>
First we are going to clear our wireshark and filter by SSH. Then in VM1 go to the powershell and type the command "ssh 10.0.0.5@labuser" in order to SSH VM2 because VM2's private IP address is 10.0.0.5. It will prompt you to enter VM2's password that you created earlier today. From now we can observe the traffic in wireshark

![image](https://github.com/danielbangm/azure-network/assets/22795502/f2258f08-af3a-49d8-bbe0-491ecb1e585b)

<p>
Now you'll notice we are in VM2 which runs Ubuntu and how powershell prompt has changed. We can now type couple of Linux commands and also see how the traffic changes in wireshark
</p>

![image](https://github.com/danielbangm/azure-network/assets/22795502/799723d9-f15a-49c6-82f8-0cc67f6117a6)

-  Step 7: Wireshark hands-on

<p>
 You can filter for example ssh traffic in wireshark by typing ssh in the filter area or you can also type "tcp.port == 22" since ssh uses tcp port 22
</p>

![image](https://github.com/danielbangm/azure-network/assets/22795502/ae6c36af-fdb7-49ff-b90e-3dc495035b3c)








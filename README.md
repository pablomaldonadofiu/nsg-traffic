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

<h2>Set up Before Starting</h2>

- Create one Windows Virtaul Machine and one Linux(ubuntu) VM. Which can be created in AZURE
- install Wireshark in Windows VM (just google Wireshark and download) 

<h2>Actions and Observations</h2>


<p>
Now that we have our 2 machines (windows and linux) and WireShark installed in windows, let’s open wireshark and pick Ethernet at the middle of the screen, now click at the blue icon at the top left of the app (as seen in the pic below)
</p>
<p>
<img src="https://i.imgur.com/X8WN67N.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
After clicking the blue icon, we will be able to see the current internet traffic of our machine. Because there are too much information being presented, let’s filter the information by typing at the top bar, for now let’s filet by icmp. 
</p>
<p>
<img src="https://i.imgur.com/tZnyXiI.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />


<p>
At the moment, we should not be able to see anything, because there is no ICMP traffic for now. To see some ICMP traffic, let’s open the command line and try pinging something for example “ping 8.8.8.8” (8.8.8.8 is google IP address), the ping should go through and you should be able to see the ICMP traffic in wireshark. Here we can see the source, destination and the protocol that is being used. 
</p>
<p>
<img src="https://i.imgur.com/pojgKAb.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />


<p>
Now let’s see what happens if we ping our second VM (linux) but then we deny traffic from ICMP in our second machine. First, ping the VM2 using VM1(windows), just like we ping 8.8.8.8, let’s ping VM2 IP address which can be found at VM2’s AZURE portal. That ping should return normally and will also be shown at wireshark.
</p> <p>To deny traffic from ICMP in VM2, let’s go to AZURE and search “Network security groups” and click on VM2 -> Inbound Security rules -> + add. Leave anything as default and under “Protocol” select IMCP then Deny. 
</p>
<p>
<img src="https://i.imgur.com/2mDxuwT.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />

<p>
If we go back to our VM1 and try to ping VM2 again, we will get “Request timed out” and if we check Wireshark, we can see that before we would get Request and Reply, but now we are only getting Requests. 
</p>
<p>
<img src="https://i.imgur.com/TsTLCQ7.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />


<p>
Checking SSH traffic:</p> 
<p>At the search bar of Wireshark, type SSH. You should see an empty page because there is no SSH traffic for now. To connect VM1 to VM2 using SSH, go to the command line and type “ssh USERNAME@X.X.X.X” (Please note that USERNAME is the username of VM2 and X.X.X.X is its IP address), then type yes and enter the password for VM2 (password is not shown but it is typing). Now we should be seeing some SSH traffic in Wireshark 
</p>
<p>
<img src="https://i.imgur.com/T8czUMD.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />


<p>
We can inspect more traffic by typing the protocol in Wireshark and then do some actions, for example, if you want to check some DHCP traffic we can type “ipconfig /renew” and see that traffic, another example is to check DNS traffic and doing nslookups and see the traffic in Wireshark. There are many types of traffics that can be inspect so go ahead and try new protocols or ports to inspect! 
</p>
<br />

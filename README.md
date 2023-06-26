# networksecuritygroups
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

<h2>Actions and Observations</h2>

</p>
</p>
  Start with creating 2 Virtual Machines under the same Resource Group
  </p>
  </p>

  
<img src="https://i.ibb.co/H75sL44/Step1.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Start with connecting too VM1 with remote desktop by clicking on VM1 on azure. Open up Remote Desktop through start tab and copy VM1's IP address 
</p>
<br />

<p>
<img src="https://i.ibb.co/HT3yK7y/Step-2.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
Enter the login and password that you've put when you first created the VM. If you can't find this option click on "More Choices"
</p>
<br />

<p>
<img src="https://i.ibb.co/1Jr3ZM6/Step-3.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<p>
This tab will pop up, click on "Yes"
</p>
<br />
<img src="https://i.ibb.co/QkXC7gj/Step-4.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />
Select the options, press "Accept" after 
</p>
<br />
<img src="https://i.ibb.co/Ns1tCxy/step-5.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />
We are now connected too the VM, you can confirm this by look at the top left corner. (It should show the VM IP address)
</p>
<br />
<img src="https://i.ibb.co/6H0mVKm/Step-6.jpg" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />
Once connected into VM1 desktop, search up "Wireshark.org" and download it. Make sure too download the appropiate file for your computer's system 
</p>
<br />
<img src="https://i.ibb.co/TYvctBS/step-7.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />
Launch the file once the download is complete. Use all default settings (don't change anything) , keep going until installation is finished
</p>
<br />
<img src="https://i.ibb.co/k1r97WC/step8.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.ibb.co/yFVdrzx/step8-5.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<img src="https://i.ibb.co/nbGxz0r/step8-6.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>
<br />
Once everything is finished installing, open up the start menu and click on the wireshark icon too open up the app
<img src="https://i.ibb.co/YcWpNr7/step9.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
Click on "Ethernet"
<img src="https://i.ibb.co/s1pn5Tk/step9-1.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
After clicking on Ethernet; click on the blue shark icon too start capturing packets
<img src="https://i.ibb.co/m8q8xd6/step9-2.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<p/>
<br />
It will start spamming traffic, you can see that 10.0.0.4 is our ip address
<img src="https://i.ibb.co/n63Ynbk/step10.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<p/>
<br />
Next step is too filter all the traffic so it stops spamming, this is done by typing in "icmp" which stands for "internet control messaging protocol". This is the protocol that ping uses 
<img src="https://i.ibb.co/MMXrzxf/step10-1.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<p/>
It should clear all the traffic and look blank like this
<p/>
<br />
<img src="https://i.ibb.co/FqQx9BW/step10-2.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<p/>
<br />
Once all the traffic cleared, the next step is too ping VM2's ip address from VM1. You can find VM2 ip address by searching up virtual machines on portal.azure and clicking virtual machines tab. Once you find VM2, click on it and the ip address should show on the side. (Note- we are pinging the PRIVATE ip address) 
<p/>
<br />
<img src="https://i.ibb.co/9hp1rxH/step10-3.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<p/>
<br />
Once you get the ip address for VM2, open VM1 back up on remote desktop. Once back on VM1, open windows powershell (you can do this by typing "windows powershell" on the start menu) 
<p/>
<br />
<img src="https://i.ibb.co/mJzQ4Cs/step10-4.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<p/>
<br />
Next step is start pinging VM2 from VM1. Type "ping 10.0.0.5" into windows powershell and it should start too send requests too VM2. You can see the reply/request go through on wireshark (10.0.0.4 is VM1, 10.0.0.5 is VM2)
<p/>
<br />
<img src="https://i.ibb.co/28dnnpW/step10-5.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<p/>
<br />
Congratulations! You have successfully performed a network action. The next type of ping we will do is called a "perpetual ping" which means a never ending ping, as well as learning how too use firewall too block incoming ping requests. First we have too start by clearing out our wireshark app, press the green "fin" button too clear it and press "Continue without saving"
<p/>
<br />
<img src="https://i.ibb.co/H7x2tFg/step11.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<p/>
<br />
Once everything is cleared, type in "ping -t 10.0.0.5" into windows powershell. This should start the perpetual ping ("-t" is the command for it)
</p>
<br />
<img src="https://i.ibb.co/vHjXKHS/step11-1.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<p/>
<br />
It should start too ping continuously like this
<p/>
<br />
<img src="https://i.ibb.co/ZJ9RfTv/step11-2.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<p/>
<br />
The next step is learning how too block incoming traffic using Network security groups (Azure's firewall) Type "Network Security Groups" on the search bar in azure too get to the page. We can see NSG for both VM1 and VM2 
<img src= "https://i.ibb.co/NxM60XT/step12.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>


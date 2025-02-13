<h1>Active Directory Homelab</h1>

 ### [Pictoral Walkthrough Demonstration]

<h2>Description</h2>
In this lab we are going to walk through how to create and active directory HomeLab envionrment using Oracle Box. Our goal 
is to help to develop your understanding of how active directory and windows networking works. If you have any questions about
what we have create do hesitate to shoot me an email.
<br />


<h2>Languages and Utilities Used</h2>

- <b>PowerShell</b> 
- <b>Oracle Virtual Box</b>

<h2>Environments Used </h2>

- <b>Windows 10</b> (21H2)
- <b>Server 2019</b>

<h2>Program walk-through:</h2>
<p align="center">
Creating our own Active Directory Lab: <br/>
<img src="https://imgur.com/vh6G4Te.png" height="80%" width="80%" "/>
<p align="center"> First we want to download our virtual box from Oracle.
                  Dont forget to also download the extension pack as well <br/>
 
<br />

<p align="center">
Next we want to Create our first Virtual Machine: <br/>
<img src="https://imgur.com/CFGit4D.png" height="80%" width="80%""/>
 <p align="center"> We want to download our Windows Server 2019 ISO and Windows 10 ISO.
                    Then we want to set up our server within our Virtual Box. Give it a name.(ie; DC)
                    Set other parameters for your VM like RAM,Number of Processors,Network Adapters(NAT,
                    Internal Network),Storage. Remember to put the ISO server in the Optical Drive  
                  <br/>


<br />
<br />
Install Windows Server:  <br/>
<img src="https://imgur.com/lsPsQiF.png" height="80%" width="80%" "/>
  <p align="center"> Here at the server log in use the same password that you gave at the default admin section.
                     Note: as a the mouse navigation may be lagging. So you can install VM Guest additions for better
                     navigation of the mouse within your VM. After that we want to do two things with the server.
                      We want to set up our IP addressing for the internal NIC and external NIC</br>
<br />
<br />

<br />
<br />
Setting Up IP Addressing:  <br/>
<img src="https://imgur.com/HlQEBHt.png" height="80%" width="80%" "/>
  <p align="center"> Here, within the desktop section of the VM go to the bottom right of the screen and click the 
                     computer icon, then click network. The click adapter options. We want to define the external and internal
                     adapters by renaming them; One internal and one external. Note that you should be able to tell the differnece 
                      between the adapters becuase the internal network will have an APIPA address.On the internal adapter we want 
                      assign this adapter with an IP address and subnet mask. </br>
<br />
<br />

<br />
<br />
Rename the PC on the VM:  <br/>
<img src="https://imgur.com/osMS8y1.png" height="80%" width="80%" "/>
  <p align="center"> Here, we want to simply right click the start button and go to system and then give the 
                     computer name of you choice. Then restart VM (ie DC)</br>
<br />
<br />

<br />
<br />
Next We want to install Active Directory Domain Services:  <br/>
<img src="https://imgur.com/SqDIap3.png" height="80%" width="80%" "/>
  <p align="center"> Here we want to to install Active Directory Domain Services and then we want to create a domain.
                     So, first click add roles and features, and choose Active Directory Domain Services. I have intentionally excluded 
                      a few steps with this installation for brevity.Note: after you have downloaded the AD DS you must do a post 
                      deployment configuration. Then add a new forest. Create the name of your domain with a password then intsall.
                      this will restart your computer. </br>

                      
<br />
<br />

<br />
<br />
   We want to now create our own Dedicated Domian Administrator Account :  <br/>
<img src="https://imgur.com/amfhSLF.png" height="80%" width="80%" "/>
  <p align="center"> When the computer restarts from the prior installation, this is what you should see the built-in administration 
                    account. However, we want to create our own dedicated domain admin account instead of using the built-in
                    Administrator Account. We can do this by going to the start button, then Administrator tools, then active directory 
                   users and computers.</br>
<br />
<br />

<br />
<br />
   Active Directory Users and Computers  <br/>
<img src="https://imgur.com/yOVIB4W.png" height="80%" width="80%" "/>
  <p align="center">Within the users and computers right click on the mydomain.com. We want to create and Organiztional Unit
                    to put our admin account in. Lets name it "ADMINS"</br>
<br />
<br />
<br />
<br />
   ADMINS-(Organization Unit)  <br/>
<img src="https://imgur.com/pRmp794.png" height="80%" width="80%" "/>
  <p align="center"> Inside here we want to create a new user and maybe give it your name. The create a user logon name,
                     as a common convention we would use something like a-cdavis, then we create a log on password.
                     Note: after you have created the account its not a domain yet. </br>
<br />
<br />

<br />
<br />
   Back into Active Directory users and computers <br/>
<img src="https://imgur.com/P7wUHVP.png" height="80%" width="80%" "/>
  <p align="center"> Go back to Users and Computers and right click on the username that you have created. Right click,
                     go to properties, member of and add the new user name to Domain admins. To verify that this works log out(sign out)
                      of the domain controller. Then sign into other account with you unser account name and password.</br>
<br />
<br />

<br />
<br />
   The Next thing We Want to Set Up A NAT(Network Address Translation) and a RAS(Remote Access Service) <br/>
<img src="https://imgur.com/G0fkVL3.png" height="80%" width="80%" "/>
  <p align="center"> The purpose of this is when we create our windows 10 Client its going to allow the client to be on a 
                      private virtual network but still be able to access the external network through the Domain Controller.So
                       we want to install NAT and RAS on the DC to allow our client to hav e the ability to do that. So go
                       to roles and feature and click remote access. We also want to also include routing and Direct access, add 
                       features and install.  
                       </br>
<br />
<br />

<br />
<br />
   Installing Remote Access <br/>
<img src="https://imgur.com/fsmo7HX.png" height="80%" width="80%" "/>
  <p align="center">  
                       </br>
<br />
<br />

<br />
<br />
   Installing NAT <br/>
<img src="https://imgur.com/SA7Mbae.png" height="80%" width="80%" "/>
  <p align="center"> After this is done go to tools and click routing and remote access. We want to install NAT to allow our internal 
                     client to connect to the internet using one public address. Use this interface to connect to the internet. </br>
<br />
<br />


<br />
<br />
   Next we want to Set Up a DHCP server on our Domain <br/>
<img src="https://imgur.com/SqDIap3.png" height="80%" width="80%" "/>
  <p align="center"> This will allow our window 10 client to get an IP address that will let them get on the internet.
                     Go to the Domain Dashboard and Click and Roles and Feature. We want to click the DCHP server and install it.
                     After the installtion to to tools. We want to set up the scope of the address. The purpose of DHCP is to allow 
                     clients on the network to automatically get ip address.</br>
<br />
<br />

<br />
<br />
   Creating the Scope of Our DHCP addresses <br/>
<img src="https://imgur.com/XbmTVl7.png" height="80%" width="80%" "/>
  <p align="center"> The scope entails you create a range of ip addresses that your client will be able to accesss to use internally then 
                     via  NAT will be able to translate into the public IP address that we have confiured for external use.</br>
<br />
<br />


<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>

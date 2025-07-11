<h1>Active Directory Home Lab</h1>

 <!--- ### [YouTube Demonstration]() --!>

<h2>Description</h2>
This project demonstrates how to set up a basic Home Lab while building and configuring a fully functional Active Directory (AD) environment using Oracle VirtualBox. The purpose of the lab is to provide hands-on experience with Windows Server networking, Active Directory, and domain management in a controlled, isolated environment. By setting up a virtual network, this project allows users to explore core concepts of AD, including domain controllers, DNS configuration, user management, group policies, and domain joining.
<br />


<h2>Languages and Utilities Used</h2>

- <b>Oracle VirtualBox</b> 
- <b>PowerShell</b>

<h2>Environments Used </h2>

- <b>Windows 10</b> ISO
- <b>Server 2019</b> ISO

<h2>Program walk-through:</h2>

<p align="center">
Set up VirtualBox Environment: <br/>
Go to virtualbox.org/wiki/Downloads. Download your preferred platform package. Also accept and download the extension.
<img src="https://i.imgur.com/sq59v90.png" width="600" alt="VMSetup Steps"/>
<br />
<br />
Download Windows 10 ISO:  <br/>
Go to www.microsoft.com/en-us/software-download/windows10. 
<img src="https://i.imgur.com/AG2jMtJ.png" width="600" alt="VMSetup Steps"/>
<br />
<br />
Download Server 2019 ISO: <br/>
Go to www.microsoft.com/en-us/evalcenter/download-windows-server-2019. Select your langauge and ISO downloads.
<img src="https://i.imgur.com/KTLPQ7p.png" width="600" alt="VMSetup Steps"/>
<br />
<br />
Creating Our Virtual Machines: <br/>
Open Oracle VirtualBox. Click "New" then name your VM DC(Domain Controller) and for version select Other Windows(64-bit). At least 2GB(2048MB) of RAM and click "Next" until finish.
<br />
<img src="https://i.imgur.com/GFqARyp.png" width="600" alt="VMSetup Steps"/>
<img src="https://i.imgur.com/peUCCcU.png" width="600" alt="VMSetup Steps"/>
<br />
Next click settings > Advanced > General change Shared Clipboard and Drag'n'Drop to bidirectional. This allow you to ctrl c and ctrl v between the virtual machine and your actual computer. Drag'n'Drop bidirectional allows user to drag files from the desktop into the virtual machine.
<br />
<img src="https://i.imgur.com/I4XvPTP.png" width="600" alt="VMSetup Steps"/>
<br />
 If you have a computer with plenty cores you can do more but if you have few do less or just keep it at one.
<br />
<img src="https://i.imgur.com/iMEFAkL.png" width="600" alt="VMSetup Steps"/>
<br />
Go to Network > Expert. Adapter 1 is attached to NAT. Remember we are creating the Domain Controller(DC) so you want to have two NIC(Network Interface Card), one that is dedicated for internet which will be running NAT and the second(Adapter 2) dedicated for the internal vmware network.
<br />
<img src="https://i.imgur.com/9yI3EfM.png" width="600" alt="VMSetup Steps"/>
<img src="https://i.imgur.com/tutqicO.png" width="600" alt="VMSetup Steps"/>
<br />
Start the DC(VM), then select the server 2019 ISO that was downloaded and click "mount" to start the virtual machine. At the Windows Setup click "Next" then Install Now
<br />
<img src="https://i.imgur.com/k5g2GsK.png" width="600" alt="VMSetup Steps"/>
<img src="https://i.imgur.com/j1STndP.png" width="600" alt="VMSetup Steps"/>
<img src="https://i.imgur.com/okGttuc.png" width="600" alt="VMSetup Steps"/>
<br />
After install, select "Windows Server 2019 Standard Evaluation (Desktop Experience) x64" click "Next" for this and license terms agreement. Select the Custom type of installation and click "Next" you will see the installing Windows, this will take some time. 
<br />
<img src="https://i.imgur.com/aotauF8.png" width="600" alt="VMSetup Steps"/>
<img src="https://i.imgur.com/Sxizs4Y.png" width="600" alt="VMSetup Steps"/>
<img src="https://i.imgur.com/4brTnVk.png" width="600" alt="VMSetup Steps"/>
<br /> 
At the Customize Setting, create a password(Bluemachina28) for your Admin account and click "Finish".
<img src="https://i.imgur.com/OR1RhX1.png" width="600" alt="VMSetup Steps"/>
<br />
At this screen, go to input > keyboard > insert CTRL-ALT-DEL then enter your password again.
<img src="https://i.imgur.com/b1qSYXl.png" width="600" alt="VMSetup Steps"/>
<br />
Active Directory: <br/> Install active directory domain services and create a domain. In Server Manager, click add roles and features. Continue clicking next until you get to "Select Destination Server", select your domain controller server. Next select "Active Directory Domain Services"> add features > continue next and finally click install
<br/>
<img src="https://i.imgur.com/SYgSlSc.png" width="600" alt="AD"/>
<img src="https://i.imgur.com/ocAd2dv.png" width="600" alt="AD"/>
<img src="https://i.imgur.com/GmXozTe.png" width="600" alt="AD"/>
<br />
After installing the Active Directory you have to create the domain. Click "Promote this server to domain controller"> click "add new forest" then name your domain(Bluemachinadomain.com) click "Next". Create a password(Bluemachina28). Continue to click "Next" and finally "install". A restart will begin automatically.
<br/>
<img src="https://i.imgur.com/LZrX0G1.png" width="600" alt="AD"/>
<img src="https://i.imgur.com/rAXzHOP.png" width="600" alt="AD"/>
<img src="https://i.imgur.com/18FXX3m.png" width="600" alt="AD"/>
<img src="https://i.imgur.com/HUH8BW5.png" width="600" alt="AD"/>
<br/>
Now we create our own dedicated domain admin account instead of the built-in administrator account. Go to Start > Windows Administrative Tools > Active Directory Users and Computers. See the Bluemachinadomain.com, that is the newly created domain.
<br/>
<img src="https://i.imgur.com/CmbqXdD.png" width="600" alt="AD"/>
<br/>
Creating an Organizational Unit to put our admin account in (its like a folder in active directory) right click your domain name > New > Organizational Unit. Which allow you to name it. I will name it _ADMINS. Inside our _ADMINS lets create a new user. Right click _ADMINS > New > User, enter info(a-jwhitehead) the "a" signify it's an admin account. Then you will be asked to create a password(Bmjwhiteh6). In this lab I checked "password never expires" > Finish
<br/>
<img src="https://i.imgur.com/suYCjZK.png" width="600" alt="AD"/>
<img src="https://i.imgur.com/TgYLfyD.png" width="600" alt="AD"/>
<br/>
Making an account into a Domain Admin Account: <br/>
Now we have an account but it's not an admin. To make this account admin, right click the user account > properties > Member Of > click Add > Type "Domain Admins" > click Check Names > click Ok > Apply > Ok. Now we have our domain admin account. Remember if you want to use this account as an domain admin account you have to sign out of the domain controller then sign in after clicking "Other User" using your domain admin account(a-jwhitehead) and password.
<br/>
<img src="https://i.imgur.com/LoNEVZO.png" width="600" alt="AD"/>
<img src="https://i.imgur.com/kaIWn26.png" width="600" alt="AD"/>
<img src="https://i.imgur.com/DzAXSiI.png" width="600" alt="AD"/>
<br/>
Install RAS/NAT(Remote Access Service/Network Address Translation): <br/>
Next, install RAS/NAT on the Domain Controller to allow the Windows 10 Client(once we create it) to remain on a private virtual network while still being able to access the internet through the Domain Controller. On Server Manager Dashboard, go to Add roles and features > click next until get to Select Server Roles > click Remote Access > Next > Next > in Select Role Service > click Routing > Add Features > then Next until install.
<br/>
<img src="https://i.imgur.com/kfyDBtZ.png" width="600" alt="AD"/>
<img src="https://i.imgur.com/pFi8V0o.png" width="600" alt="AD"/>
<img src="https://i.imgur.com/26hJR6V.png" width="600" alt="AD"/>
<br/>
After install go to Tools > Routing and Remote Access > right click DC (Local) > click Configure and Enable Routing and Remote Access > click Next > click Network Address Translation > Next > click the one we named INTERNET earlier then click Next > Then Finish
<br/>
<img src="https://i.imgur.com/Wv4uYc3.png" width="600" alt="AD"/>
<img src="https://i.imgur.com/Hj3xrxj.png" width="600" alt="AD"/>
<img src="https://i.imgur.com/Px8acYH.png" width="600" alt="AD"/>
<img src="https://i.imgur.com/9WAq1zK.png" width="600" alt="AD"/>
<br/>
Setup the DHCP(Dynamic Host Configuration Protocol) Server on our Domain Controller: <br/>
This will allow the Windows 10 Client to get an IP Address which will let it get on the internet and browse even though on private internal network. On Server Manager Dashboard, go to Add roles and features > click Next until you get to Server Roles > click DHCP Server then Add Features > Next until Install
<br/>
<img src="https://i.imgur.com/LkVCakQ.png" width="600" alt="AD"/>
<br/>
Once Install is complete, let's set up DHCP: <br/>
Go to Tools > DHCP > click dropdown on DC > click dropdown on IPv4 > left click on IPv4 > New Scope > Next > In the name section I type: 172.16.0.100-200 then click Next > Next 
<br/> 
<img src="https://i.imgur.com/Lvt12h8.png" width="600" alt="AD"/>
<img src="https://i.imgur.com/1ENxaz5.png" width="600" alt="AD"/> <br/>
In Start IP address I type: 172.16.0.100 and in End IP Address: 172.16.0.200 Length: 24 make sure the subnet mask is 255.255.255.0 then click Next <br/>
<img src="https://i.imgur.com/YHCwyTY.png" width="600" alt="AD"/> <br/>
Lease Duration I did 8 days click Next > <br/>
<img src="https://i.imgur.com/hPP9xEo.png" width="600" alt="AD"/> <br/>
Configure DHCP Options, click Yes then Next <br/>
<img src="https://i.imgur.com/exhcKpL.png" width="600" alt="AD"/> <br/>
Router (Default Gateway): in the IP Address enter the domain controller IP Address: 172.16.0.1 and click Add then Next > Next until Finish. When finish, right click the DC and click Authorize then right click it again to refresh it
<img src="https://i.imgur.com/UQ3hDpQ.png" width="600" alt="AD"/>
<br/>
Using Powershell script to create users in Active Directory: <br/>
The Purpose is to create a bunch of users so I don't have to manually create each user. Click Start > Windows PowerShell > Right click Windows PowerShell ISE > More > Run as Admin > Click the little folder that say, Open Script and I open the script on my desktop(vm) > After upload script I had to Unrestrict some things to be able to use the script > After using the script you can see a bunch of random name were generated
<img src="https://i.imgur.com/dMqixyS.png" width="600" alt="AD"/>
<img src="https://i.imgur.com/Gb589Tp.png" width="600" alt="AD"/>
<br/>
Creating the Client VM: <br/>

<br/>
<!--
<br />
Sanitization complete:  <br/>
<img src="https://i.imgur.com/K71yaM2.png" width="600" alt="VMSetup Steps"/>
<br />
<br />
Observe the wiped disk:  <br/>
<img src="https://i.imgur.com/AeZkvFQ.png" width="600" alt="VMSetup Steps"/>
</p>
--!>

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>

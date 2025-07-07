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

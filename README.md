<h1> Configuration and Deployment of Active Directory </h1>

<h2> Environment and Technology </h2>

- Microsoft Azure
- Active Directory
- Powershell

<h2> Operating Systems </h2>

- Windows Server 2022
- Windows 10 Pro

<h2> Steps to Configuration and Deployment </h2>

1. Create a Virtual Machine using Windows Server 2022 as the image. This will be our Domain Controller (DC-1).  

<p align="center">
<img src="https://i.imgur.com/vCOaCLU.png" height="50%" width="50%" alt="DC-1 Setup"/>
</p>

2. Create a Vitual Machine using Windows 10 Pro as the image. This will be a client machine (Client-1).  
<p align="center">
<img src="https://i.imgur.com/Ja7LoRM.png" height="50%" width="50%" alt="Client-1 Setup"/>
</p>

3. Set the Domain Controller's Network Interface Private IP Address to static.
<p align="center">
<img src="https://i.imgur.com/X4odscV.png" height="50%" width="50%" alt="DC-1 Networking Settings"/>
<img src="https://i.imgur.com/y7bP3Bn.png" height="50%" width="50%" alt="DC-1 IP Settings"/>
</p>

4. Log in to Client-1 using Remote Desktop. Ping the Private IP Address of DC-1. This request should time out.  
<p align="center">
<img src="https://i.imgur.com/ctgZkqB.png" height="50%" width="50%" alt="Pinging DC-1"/>
</p>

5. Log in to DC-1 using Remote Desktop. Enable ICMPv4 on the server's firewall.  
<p align="center">
<img src="https://i.imgur.com/vpwBrTJ.png" height="50%" width="50%" alt="Enabling echo requests"/>
</p>

6. Install a new Active Directory Forest on DC-1 and promote server to Domain Controller.  
<p align="center">
<img src="https://i.imgur.com/z7LoGb6.png" height="50%" width="50%" alt="Creating new active directory forest"/>
<img src="https://i.imgur.com/lDGnjhj.png" height="50%" width="50%" alt="Promote server to domain controller"/>
</p>

7. Within Active Directory Users and Computers, create a new Organizational Unit called "_EMPLOYEES".
8. Within Active Directory Users and Computers, create a new Organizational Unit called "_ADMINS".
<p align="center">
<img src="https://i.imgur.com/eABVAhC.png" height="50%" width="50%" alt="Creating new organizational unit"/>
</p>

9. Create a new employee and give that employee Admin privileges.
<p align="center">
<img src="https://i.imgur.com/T1L5w7r.png" height="50%" width="50%" alt="Creating new employee"/>
<img src="https://i.imgur.com/FXCpetf.png" height="50%" width="50%" alt="Giving new employee Admin privileges"/>
</p>

10. Log back in to DC-1 as the new employee that was created in the previous step.
11. Within the Azure portal, set Client-1's DNS settings to the Private IP of DC-1.
<p align="center">
<img src="https://i.imgur.com/qmQ1Rgc.png" height="50%" width="50%" alt="Changing Client-1 DNS settings"/>
</p>

12. Restart Client-1. On Client-1, run "ipconfig /all" to verify the new DNS settings have taken effect.
<p align="center">
<img src="https://i.imgur.com/uADK8kI.png" height="50%" width="50%" alt="Client-1 DNS Server is now DC-1"/>
</p>

13. Log in to Client-1 as the original user created with the VM and join Client-1 to DC-1's domain.
<p align="center">
<img src="https://i.imgur.com/7QuT063.png" height="50%" width="50%" alt="Joining Client-1 to mydomain.com"/>
</p>

14. Create an organizational unit called "_CLIENTS" and drag Client-1 into the new folder.
<p align="center">
<img src="https://i.imgur.com/txJ7htq.png" height="50%" width="50%" alt="Moving Client-1 machine into the _CLIENTS OU"/>
</p>

15. Using the new Admin employee credentials, log in to Client-1 and allow domain users to access Remote Desktop.
<p align="center">
<img src="https://i.imgur.com/sY8blo1.png" height="50%" width="50%" alt="Allowing all users to access DC-1 Client Machines remotely"/>
</p>

16. Use Powershell to run a script that creates additional users. Make sure to run Powershell as an Administrator.
<p align="center">
<img src="https://i.imgur.com/o26hURI.png" height="50%" width="50%" alt="Using script to create new users"/>
</p>


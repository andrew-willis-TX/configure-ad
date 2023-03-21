<h1> Configuration and Deployment of Active Directory </h1>

<h2> Environment and Technology </h2>

- Microsoft Azure
- Active Directory
- Powershell

<h2> Operating Systems </h2>

- Windows Server 2022
- Windows 10 Pro

<h2> Steps to Configuration and Deployment </h2>

- Create a Virtual Machine using Windows Server 2022 as the image. This will be our Domain Controller (DC-1).
<img src="https://i.imgur.com/vCOaCLU.png" height="50%" width="50%" alt="DC-1 Setup"/>

- Create a Vitual Machine using Windows 10 Pro as the image. This will be a client machine (Client-1).
<img src="https://i.imgur.com/Ja7LoRM.png" height="50%" width="50%" alt="Client-1 Setup"/>

- Set the Domain Controller's Network Interface Private IP Address to static.
<img src="https://i.imgur.com/X4odscV.png" height="50%" width="50%" alt="DC-1 Networking Settings"/>
<img src="https://i.imgur.com/y7bP3Bn.png" height="50%" width="50%" alt="DC-1 IP Settings"/>

- Log in to Client-1 using Remote Desktop. Ping the Private IP Address of DC-1. This request should time out. 
<img src="https://i.imgur.com/ctgZkqB.png" height="50%" width="50%" alt="Pinging DC-1"/>

- Log in to DC-1 using Remote Desktop. Enable ICMPv4 on the server's firewall.
<img src="https://i.imgur.com/vpwBrTJ.png" height="50%" width="50%" alt="Enabling echo requests"/>

- Install a new Active Directory Forest on DC-1 and promote server to Domain Controller.
<img src="https://i.imgur.com/z7LoGb6.png" height="50%" width="50%" alt="Creating new active directory forest"/>
<img src="https://i.imgur.com/lDGnjhj.png" height="50%" width="50%" alt="Promote server to domain controller"/>

- Within Active Directory Users and Computers, create a new Organizational Unit called "_EMPLOYEES".
- Within Active Directory Users and Computers, create a new Organizational Unit called "_ADMINS".
<img src="https://i.imgur.com/eABVAhC.png" height="50%" width="50%" alt="Creating new organizational unit"/>


- Create a new employee and give that employee Admin privileges.
<img src="https://i.imgur.com/T1L5w7r.png" height="50%" width="50%" alt="Creating new employee"/>
<img src="https://i.imgur.com/FXCpetf.png" height="50%" width="50%" alt="Giving new employee Admin privileges"/>

- Log back in to DC-1 as the new employee that was created in the previous step.
- Within the Azure portal, set Client-1's DNS settings to the Private IP of DC-1.
<img src="https://i.imgur.com/qmQ1Rgc.png" height="50%" width="50%" alt="Changing Client-1 DNS settings"/>

- Restart Client-1. On Client-1, run "ipconfig /all" to verify the new DNS settings have taken effect.
<img src="https://i.imgur.com/uADK8kI.png" height="50%" width="50%" alt="Client-1 DNS Server is now DC-1"

- Log in to Client-1 as the original user created with the VM and join Client-1 to DC-1's domain.
<img src="https://i.imgur.com/7QuT063.png" height="50%" width="50%" alt="Joining Client-1 to mydomain.com"/>

- Create an organizational unit called "_CLIENTS" and drag Client-1 into the new folder.
<img src="https://i.imgur.com/txJ7htq.png" height="50%" width="50%" alt="Moving Client-1 machine into the _CLIENTS OU"/>

- Using the new Admin employee credentials, log in to Client-1 and allow domain users to access Remote Desktop.
<img src="https://i.imgur.com/sY8blo1.png" height="50%" width="50%" alt="Allowing all users to access DC-1 Client Machines remotely"/>

- Use Powershell to run a script that creates additional users. Make sure to run Powershell as an Administrator.
<img src="https://i.imgur.com/o26hURI.png" height="50%" width="50%" alt="Using script to create new users"/>


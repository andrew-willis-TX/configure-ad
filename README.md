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
- Log in to DC-1 using Remote Desktop. Enable ICMPv4 on the server's firewall.
- Install a new Active Directory Forest on DC-1 and promote server to Domain Controller.
- Within Active Directory Users and Computers, create a new Organizational Unit called "_EMPLOYEES".
- Within Active Directory Users and Computers, create a new Organizational Unit called "_ADMINS".
- Create a new employee and give that employee Admin privileges. 
- Log back in to DC-1 as the new employee that was created.
- Within the Azure portal, set Client-1's DNS settings to the Private IP of DC-1.
- Restart Client-1.
- Log in to Client-1 as the original user created with the VM and join Client-1 to DC-1's domain.
- Create an organizational unit called "_CLIENTS" and drag Client-1 into the new folder.
- Using the new Admin employee credentials, log in to Client-1 and allow domain users to access Remote Desktop. 
- Use Powershell to run a script to create many additional users.


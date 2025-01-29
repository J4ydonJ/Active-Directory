<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>On-premises Active Directory Deployed in the Cloud (Azure)</h1>
This tutorial outlines the implementation of on-premises Active Directory within Azure Virtual Machines.<br />



<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- Domain Creation
- OU Creation
- Client DNS
- Remote Desktop

<h2>Deployment and Configuration Steps</h2>

<p>
  
![image](https://github.com/user-attachments/assets/fe5d9b49-7d98-42eb-b3eb-8b344c000da5)


</p>
<p>
To create the Domain for active directory, first start by using <b/>Server Manager</b> as an admin and configure a local server. Continue through the install steps and install <b/>Active Directory Domain Systems</b>, you will click the flag in the top right section of the screen and add a new forest labeled as mydomain.com. After you install everything, the domain will restart and will require you to log in again. When logging in you will have to sign in with a new domain login, since we used mydomain.com we will sign in as mydomain\<b/>username</b>. The passowrd used for the account will still be the same but the username log in will be different depending on how you want to log in. Doing this makes it so domain admins will have a different log in than the other agent users.
</p>
<br />


<p>
  
![image](https://github.com/user-attachments/assets/1976e8d4-e8f7-44a0-8d8d-75eeb6c1f5ef)

</p>
<p>
With windows start, open <b/> Active Directory Users and Computers</b> and create 2 OUs (Organizational Unit) labeled as _EMPLOYEES and _ADMINS. Create your admin username and password for log in. After this is done you must select the account properties and under <b/>Select Groups</b> add your account to <b/>domain admins</b>. This will make a new log in for the account that you made. The new account will be mydomain.com\<b/>username</b>.  
</p>
<br />

<p>
  
![image](https://github.com/user-attachments/assets/4c4955fa-acf2-4f40-a55a-9a7bf9c205d5)

</p>
<p>
Next you can add client computers to the domain within the cloud (Azure). This is done by setting the client's <b/>DNS</b> server settings as the domain controller's private ip adress. This allows any Dns questions asked sent to the domain instead of the virtual network. Doing this will make a connection to the domain conroller accsessable. 
</p>
<br />



<p> 
  
![image](https://github.com/user-attachments/assets/01cb5be8-aee0-42e4-a524-166755cdbd1d)



</p>
<p> 
You can now open powershell and attempt to ping the <b/>Domain Controller</b>, if the ping was successful you can also type ipconfig /all. This will show the location that the DNS will be sent to and it will show the primary DNS suffix. Now you should see that the DNS server should show the private ip address of the Domain Controller.  </p>

<p>
  
![image](https://github.com/user-attachments/assets/59273899-6c23-4776-99ed-95740bd8dd9c)


</p>
<p>
Now you can log in to client computer usuing the domain controller account that you previosly made. Once you log in go to computer settings and find the remote desktop settings. Once you are there, select user accounts and the domain should show up. Here you can add access to the client. You can choose who has access by selecting domain admins or domain users. This will allow accounts created inside of the domain users group to use this client for log in. This proccess can be repeated for however many clients need to be created. 
</p>
<br />

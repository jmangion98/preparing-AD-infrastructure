<p align="center">
<img src="https://i.imgur.com/pU5A58S.png" alt="Microsoft Active Directory Logo"/>
</p>

<h1>Preparing Active Directory Infrastructure in Azure </h1>
In this project, I set up two virtual machines (VMs): one running Windows Server to function as a Domain Controller, and the other running Windows 10 as a client, which will be joined to the domain.<br />



<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services


<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)


<h2>Project Walkthrough</h2>



1. Create a Resource Group:

- Start by heading to Microsoft Azure and creating a resource group.
</p>

![image](https://github.com/user-attachments/assets/ecd6b747-791a-4fab-b70a-060057ecebf0)


2. Create a Virtual Network:

- After creating the resource group, create a Virtual Network.
</p>

![image](https://github.com/user-attachments/assets/59c00f49-4853-488b-9d8c-bd7417c62aee)
<p>
3. Set Up the Domain Controller VM:

- Create and set up the virtual machine that will function as the Domain Controller (Windows Server 2022).
</p>

![image](https://github.com/user-attachments/assets/afab89dc-8e8e-45c0-9f55-3406fcd449e9)

![image](https://github.com/user-attachments/assets/fe7b7d05-701a-4ed7-92d4-15ed9293d81b)

<br />

</p>4. Configure Networking for Domain Controller:

- In the Virtual Machine's Networking tab, ensure that it is connected to the virtual network created earlier. </p>

![image](https://github.com/user-attachments/assets/0d162eb8-200f-4a5a-8f6e-d8eeb4d1de3a)

<p>5. Create the Client VM:

- Create a second virtual machine that serves as the client, selecting Windows 10 as the operating system.</p>

![image](https://github.com/user-attachments/assets/b39c7903-30b7-4064-ab6b-fe4a7abdfdbf)

![image](https://github.com/user-attachments/assets/5a6d5e06-91a0-4e76-91e6-1945abb8ff2f)

<p>6. Configure Networking for Client:

- Ensure that the client VM is also configured to connect to the same virtual network.</p>

![image](https://github.com/user-attachments/assets/b90bd423-583c-47b4-afb3-45267b1d45f6)

<p>7. Set Static IP for Domain Controller:

- Change the Domain Controller's private IP address from dynamic to static, as it will also function as a DNS server. This ensures the DNS configuration remains valid for the client.</p>

![image](https://github.com/user-attachments/assets/a21af208-ca09-411e-ae32-cb65c3c6a910)
![image](https://github.com/user-attachments/assets/3fbf5935-ac8f-488c-b848-f3010613d620)

<p>8. Remote Desktop Connection to Domain Controller:

- Use Remote Desktop with the Domain Controller's public IP address and the login credentials set during VM configuration.</p>

![image](https://github.com/user-attachments/assets/111958d5-2ce5-4da4-86f7-9a58823c977d)


After logging into the Domain Controller, you should see the Server Manager screen displayed.
</p>

![Screenshot 2024-10-02 144622](https://github.com/user-attachments/assets/c3c871a4-1500-4715-a601-126531d6d652)


9. Disable Windows Firewall:

- To disable the firewall, right-click the "Start" button and select "Run." Type wf.msc.
</p>

![image](https://github.com/user-attachments/assets/ffa1b34c-a5a0-43c4-a02a-f712fd0757e0)


Open Firewall Settings:

  - In "Windows Defender Firewall Properties," disable the firewall state under the "Domain Profile," "Private Profile," and "Public Profile" tabs.
</p>

![image](https://github.com/user-attachments/assets/a36dca60-fc80-4122-9cc5-fcefeaffb92c)
![image](https://github.com/user-attachments/assets/3c7b4f9e-f82b-4db5-acf4-f204df1f9ff8)


Next, we need to configure the client's DNS settings to point to the Domain Controller. To do this, we’ll return to Microsoft Azure to obtain the Domain Controller's private IP address</p>

![image](https://github.com/user-attachments/assets/1151fa43-c461-4e5a-978d-63b9c8036599)

<p> 10. Configure Client DNS Settings:

- Obtain the Domain Controller's private IP address from Azure. On the client machine, change the DNS settings to point to the Domain Controller by selecting "Custom" under DNS servers and entering the Domain Controller's private IP.</p>

![image](https://github.com/user-attachments/assets/7d6a1744-a68c-47dc-96b6-7f2f96ee1afa)


11. Restart the Client VM:

- After making DNS changes, restart the client virtual machine.</p>

![image](https://github.com/user-attachments/assets/c5b55841-f42f-4b06-97ad-11c08f886ffb)


12. Remote Desktop Connection to Client:

- After the restart, connect to the client machine using its public IP and the configured login credentials.
</p>

![image](https://github.com/user-attachments/assets/7f36ffe5-c802-4ea7-8f42-1f8857d51c5a)

<p>13. Ping the Domain Controller from the Client:

- Open PowerShell on the client and ping the Domain Controller using its private IP. If there’s a timeout error, ensure both machines are on the same virtual network in Azure.</p>

![image](https://github.com/user-attachments/assets/70c23a03-a89a-4705-b0fb-287d9d70d3c2)


14. Check DNS Configuration:

- Run ipconfig /all in PowerShell to verify that the "DNS Servers" section points to the Domain Controller.
</p>

![image](https://github.com/user-attachments/assets/9b7f2a23-2948-42cd-b81b-f170d76ef569)



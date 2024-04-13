![image](https://github.com/jamstylr/Building-Intuition-for-DNS/assets/159660523/b2dca626-db5d-4442-93de-8ac489e78c3e)


<h1>Building-Intuition-for-DNS</h1>
In this lab, we're going to explore how DNS (Domain Name System) works. Think of DNS as the internet's phonebook—it helps your computer find websites by translating easy-to-remember domain names (like google.com) into the unique numbers (IP addresses) that computers understand. Building on what we learned in a previous lab where I set up a network with "mydomain.com," which serves as our designated domain for this learning environment, this tutorial continues our journey. Within this network, I configured two virtual machines: one acts as the domain controller, and the other as a client. We'll be using the same administrative account, Jane Doe, for both the computer and the server, keeping things consistent as we learn about DNS.<br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- PowerShell

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (21H2)


<h2>DNS Configuration Steps</h2>

![image](https://github.com/jamstylr/Building-Intuition-for-DNS/assets/159660523/d6ae7d4a-6ad9-4361-8c51-9b87f9fd2d3e)
![image](https://github.com/jamstylr/Building-Intuition-for-DNS/assets/159660523/a22ee661-0593-4750-8e4a-e19d0c7f2051)
![image](https://github.com/jamstylr/Building-Intuition-for-DNS/assets/159660523/1df0dc13-950f-4ca5-a375-2637bf51262b)
![image](https://github.com/jamstylr/Building-Intuition-for-DNS/assets/159660523/84e9720e-c3a1-45a1-bf99-a920aa3830d8)
![image](https://github.com/jamstylr/Building-Intuition-for-DNS/assets/159660523/392622f6-11f8-4f25-88f7-5fec7e8aa126)
<p>
First, log into both Client-1 and DC-1 as administrators using the credentials mydomain.com\jane_admin. From Client-1, open Command Prompt as an administrator and attempt to ping “mainframe”. You'll notice that this ping fails. When pinging "mainframe," Client-1 checks the DNS cache, examines its local host file, and consults the DNS server. To resolve this, we need to create a DNS A-Record for mainframe on the domain controller. From DC-1, open Server Manager, navigate to Tools, then DNS. Go to DC-1 -> Forward Lookup Zone -> mydomain.com. Right-click and select New Host. Enter "mainframe" as the Name and DC-1’s IP address as the IP Address. Click Add Host and then Done. Now, when we return to Client-1 and ping mainframe again, you'll observe that it now works and receives a reply.
</p>
<br />

![image](https://github.com/jamstylr/Building-Intuition-for-DNS/assets/159660523/7445ae44-f8e0-4301-98b7-2613dcb528fa)
![image](https://github.com/jamstylr/Building-Intuition-for-DNS/assets/159660523/d6db2de5-b2bc-494c-875b-d4ee27bafb68)
<p>
Next, we'll create an A-Record for "mainframe" with the IP address 8.8.8.8 on the domain controller. However, upon returning to the client machine, it may continue to ping the previous address despite the change. This occurs because we need to clear the DNS cache using the command "ipconfig /flushdns". This command resets the DNS cache, allowing the new record address to appear when attempting to ping "mainframe" again.
</p>
<br />

![75607D3D-05C9-4E83-A351-D7944878DBC2_1_105_c](https://github.com/jamstylr/Building-Intuition-for-DNS/assets/159660523/de901359-2263-48d1-9a75-e6f21fb1d298)

<p>
Finally, we'll set up a CNAME record directing the host "search" to "www.google.com". When attempting to ping "search," the host won't be located. This is because the CNAME record for "search" doesn't exist yet. We need to return to the DNS Manager on DC-1 and establish the CNAME record for "search". Once the CNAME record is configured, we can ping "search" again, and it will resolve to www.google.com.
</p>
<br />

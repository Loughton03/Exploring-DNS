<p align="center">
<img src="https://i.imgur.com/1tzHtTS.png" alt="logo"/>
</p>

<h1>Exploring DNS in Practice</h1>
This lab focuses on the practical application of DNS, a core IT concept, by configuring DNS records and observing how DNS operates in a network environment. Building on a previous lab, I have a client machine joined to the domain "ernestotest.com" and am logged in with the administrative account "Jane Doe" on both the client and domain controller VMs. Administrative access is essential to complete this lab.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines)
- Remote Desktop Connection
- Active Directory Domain Services
- Command Prompt

<h2>Operating Systems Used</h2>

- Windows 10 Pro
- Windows Server 2022

<h2>DNS Configuration Steps</h2>

<p>
<img src="https://i.imgur.com/6U4O4x5.png" height="80%" width="80%" alt="mainframe-ping"/>
</p>

<p>
<img src="https://i.imgur.com/b3psGx7.png" height="80%" width="80%" alt="create-new-dns-host"/>
</p>

<p>
<img src="https://i.imgur.com/UoxOh10.png" height="80%" width="80%" alt="successful-mainframe-ping"/>
</p>

<p>
To test name resolution, I started on the client VM by pinging "mainframe," which returned an error since no DNS record existed. A nslookup command confirmed the absence of a DNS entry. I opened the DNS Manager on the domain controller, navigated to the Forward Lookup Zones, and within "ernestotest.com," I created a new host record for "mainframe" using the domain controller's IP address. After refreshing the DNS server, I returned to the client VM, where "ping mainframe" successfully resolved to the specified IP.
</p>

<p>
<img src="https://i.imgur.com/XPhLYUK.png" height="80%" width="80%" alt="changed-DNS-address"/>
</p>

<p>
<img src="https://i.imgur.com/pxzVer9.png" height="80%" width="80%" alt="DNS-resolves-old-address"/>
</p>

<p>
<img src="https://i.imgur.com/iTb0xG4.png" height="80%" width="80%" alt="displayDNS"/>
</p>

<p>
<img src="https://i.imgur.com/jTedkGT.png" height="80%" width="80%" alt="successful-DNS-change"/>
</p>

<p>
I changed the "mainframe" DNS record's IP address to 8.8.8.8 (Google's public DNS) on the domain controller to observe DNS caching and refreshed the server. However, the client's "ping mainframe" still returned the previous IP. Running ipconfig /displaydns showed the old IP cached in the client's DNS records. Using ipconfig /flushdns cleared the cache, and a subsequent "ping mainframe" confirmed the IP address update to 8.8.8.8.
</p>

<p>
<img src="https://i.imgur.com/dusaQcB.png" height="80%" width="80%" alt="configure-cname-record"/>
</p>

<p>
<img src="https://i.imgur.com/Rlw8Bz9.png" height="80%" width="80%" alt="cname-record-ping"/>
</p>

<p>
Next, I created a CNAME record to map "search" to Google's domain. In the DNS Manager on the domain controller, within Forward Lookup Zones, I added a CNAME record called "search" that pointed to Google. After refreshing the server, the "ping search" and nslookup search on the client VM returned Google's IP address, confirming the CNAME configuration.
</p>

<h3>Lessons Learned</h3>

<p>
This lab provided insights into the practical workings of DNS, highlighting how DNS records are managed and how caching affects network connectivity.
</p>


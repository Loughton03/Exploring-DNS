<p align="center">
<img src="" alt="place-holder"/>
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

<img src="" height="80%" width="80%" alt="place-holder"/>

<img src="" height="80%" width="80%" alt="place-holder"/>

<img src="" height="80%" width="80%" alt="place-holder"/>

<p>
To test name resolution, I started on the client VM by pinging "mainframe," which returned an error since no DNS record existed. A nslookup command confirmed the absence of a DNS entry. I opened the DNS Manager on the domain controller, navigated to the Forward Lookup Zones, and within "ernestotest.com," I created a new host record for "mainframe" using the domain controller's IP address. After refreshing the DNS server, I returned to the client VM, where "ping mainframe" successfully resolved to the specified IP.
</p>

<img src="" height="80%" width="80%" alt="place-holder"/>

<img src="" height="80%" width="80%" alt="place-holder"/>

<img src="" height="80%" width="80%" alt="place-holder"/>

<img src="" height="80%" width="80%" alt="place-holder"/>

<p>
I changed the "mainframe" DNS record's IP address to 8.8.8.8 (Google's public DNS) on the domain controller to observe DNS caching and refreshed the server. However, the client's "ping mainframe" still returned the previous IP. Running ipconfig /displaydns showed the old IP cached in the client's DNS records. Using ipconfig /flushdns cleared the cache, and a subsequent "ping mainframe" confirmed the IP address update to 8.8.8.8.
</p>

<img src="" height="80%" width="80%" alt="place-holder"/>

<img src="" height="80%" width="80%" alt="place-holder"/>

<img src="" height="80%" width="80%" alt="place-holder"/>
<p>
Next, I created a CNAME record to map "search" to Google's domain. In the DNS Manager on the domain controller, within Forward Lookup Zones, I added a CNAME record called "search" that pointed to Google. After refreshing the server, the "ping search" and nslookup search on the client VM returned Google's IP address, confirming the CNAME configuration.
</p>

<h3>Lessons Learned</h3>

<p>
This lab provided insights into the practical workings of DNS, highlighting how DNS records are managed and how caching affects network connectivity.
</p>


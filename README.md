<p align="center">
  <img src="https://imgur.com/ooUztKm.png height="80% width="80%" alt="Disk Sanitization Steps"/>
</p>

<h1>Configuring and Managing DNS using Virtual Machines in Microsoft Azure</h1>

This lab activity explores DNS record management and its impact on network connectivity by performing hands-on exercises with A-records, local DNS caching, and CNAME records.
<br />


<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Powershell

<h2>Operating Systems Used </h2>

- Windows 10 Pro (21H2)
- Ubuntu Server 20.04

<h2>High-Level Steps</h2>

- Configuring A-Records
- Managing DNS Caching
- Implementing CNAME

<h2>Configuration Steps</h2>
<br />

<h2>A-Record Exercise</h2>
<br />

<h3>Objective:</h3>
<p>Demonstrate how to create and test an A-record in a DNS server.</p>
<p>Understand how to create and test A-records in a DNS server.</p>
<br />

<h3>1. Log into the Domain Controller and "Client-1" (DC-1)</h3>
<br />

![Screenshot 2025-02-21 155210](https://github.com/user-attachments/assets/fb5457b5-e0cb-458a-a96d-46be5927a31d)
<p>- Use your domain admin account: mydomain.com\jane_admin.</p>
<br />

<h3>2. Test Name Resolution Before Creating the A-Record</h3>
<br />

![Screenshot 2025-02-21 145233](https://github.com/user-attachments/assets/2a0026d6-05fb-4849-a951-302d3019b54c)

<p>- Open Command Prompt on Client-1 and run: "ping sion"</p>
<p>- Observe that the ping request fails.</p>
<br />

<h3>3. Check DNS Records for "sion".</h3>
<br />

![Screenshot 2025-02-21 145448](https://github.com/user-attachments/assets/777558c9-1df3-47e2-bfa5-615913f6df79)

<p>- Run: "nslookup sion".</p>
<p>- Observe that no DNS record exists.</p>
<br />

<h3>4. Create an A-Record on DC-1</h3>
<br />

![Screenshot 2025-02-21 145610](https://github.com/user-attachments/assets/a84230d6-78f4-422e-9751-f3824261bbc4)

<p>- On DC-1, open DNS Manager.</p>
<br />

![Screenshot 2025-02-21 145905](https://github.com/user-attachments/assets/026d9eab-10ee-4911-977d-30961eeabf96)
![Screenshot 2025-02-21 145956](https://github.com/user-attachments/assets/162475d6-a349-4067-a47c-9f104584586b)

<p>- Navigate to Forward Lookup Zones > mydomain.com.</p>
<p>- Right-click and select New Host (A or AAAA).</p>
<p>- Enter "sion" as the hostname.</p>
<p>- Assign it DC-1’s Private IP address.</p>
<p>- Click Add Host and confirm.</p>
<br />

<h3>5. Test Name Resolution After Adding the A-Record</h3>
<br />

![Screenshot 2025-02-21 150410](https://github.com/user-attachments/assets/daa3e7f1-e761-43ed-a06d-7a70e7941f3f)

<p>- On Client-1, run: "ping sion".</p>
<p>- Observe that the ping request now succeeds.</p>
<br />

<h2>Local DNS Cache</h2>
<br />

<h3>Objective:</h3>
<p>Understand how DNS caching works and how to flush the cache.</p>
<br />

<h3>1. Modify the Existing A-Record on DC-1</h3>
<br />

![Screenshot 2025-02-21 150528](https://github.com/user-attachments/assets/6921af53-3dc5-4b02-a2b2-138fb2c9ae28)

<p>- On DC-1, change "sion"’s record IP address to 8.8.8.8.</p>
<br />

<h3>2. Check Name Resolution on Client-1</h3>
<br />

![Screenshot 2025-02-21 150650](https://github.com/user-attachments/assets/059ce80c-acc3-4d93-ad8c-a3d3550a9065)

<p>- On Client-1, ping "sion":</p>
<p>- Observe that it still resolves to the old address.</p>
<br />

<h3>3. Check the Local DNS Cache</h3>
<br />

![Screenshot 2025-02-21 150845](https://github.com/user-attachments/assets/7507c1da-073e-4d08-add2-a00268894bd8)

<p>- Run: "ping mainframe".</p>
<p>- Observe that it still resolves to the old address.</p>
<br />

<h3>4. Flush the DNS Cache</h3>
<br />

![Screenshot 2025-02-21 151437](https://github.com/user-attachments/assets/18e9c743-b352-4f38-baed-0d9d60960a2b)

<p>- Run: "ipconfig /flushdns".</p>
<p>- This clears the local cache.</p>
<br />

![Screenshot 2025-02-21 151437](https://github.com/user-attachments/assets/0f447793-7e17-4e54-92c8-73a906b6e385)

<h3>5. Verify Cache is Cleared</h3>
<br />

![Screenshot 2025-02-21 165140](https://github.com/user-attachments/assets/2e8973db-c003-4fa9-93b6-fcfee72f740c)

<p>- Run: "ipconfig /displaydns".</p>
<p>- Observe that the cache is now empty.</p>
<br />

<h3>6. Test Resolution Again</h3>
<br />

![Screenshot 2025-02-21 151514](https://github.com/user-attachments/assets/5991603f-af3b-4a90-a7e5-afbfc8f05079)

<p>- Ping "sion": "ping sion".</p>
<p>- Observe that it now resolves to "8.8.8.8".</p>
<br />

<h2>CNAME Record Exercise</h2>
<br />

<h3>Objective:</h3>
<p>Create and verify a CNAME record that maps a hostname to another domain.</p>
<p>Configure and test a CNAME record to alias a hostname.</p>
<br />

<h3>1. Create a CNAME Record on DC-1</h3>
<br />

![Screenshot 2025-02-21 151702](https://github.com/user-attachments/assets/b1c0ca57-ab3a-41da-9b1b-0615c83a749f)

<p>- On DC-1, open DNS Manager.</p>
<p>- Navigate to Forward Lookup Zones > mydomain.com.</p>
<p>- Right-click and select New Alias (CNAME).</p>
<br />

![Screenshot 2025-02-21 151856](https://github.com/user-attachments/assets/45c04300-038b-447a-9f6c-96fe2afc781c)

<p>- Enter "matcha" as the alias.</p>
<p>- In the Fully Qualified Domain Name (FQDN) field, enter www.google.com.</p>
<p>- Click OK to save.</p>
<br />

<h3>2. Test the CNAME Record on Client-1</h3>
<br />

![Screenshot 2025-02-21 152004](https://github.com/user-attachments/assets/fdfbae4a-83e2-4174-91b5-e8d484325d87)

<p>- On Client-1, run: "ping matcha".</p>
<p>- Observe the results, which should resolve to Google's IP address.</p>
<br />

<h3>3. Verify CNAME Resolution with nslookup</h3>
<br />

![Screenshot 2025-02-21 152137](https://github.com/user-attachments/assets/0c9f2f63-18a2-4694-b7ee-5947bbb98839)

<p>- Run: "nslookup matcha".</p>
<p>- Observe that "search" correctly resolves to www.google.com.</p>
<br />



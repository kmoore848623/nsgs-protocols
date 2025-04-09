![ChatGPT Image Apr 9, 2025, 01_57_38 PM](https://github.com/user-attachments/assets/e7686537-3164-41b9-9b72-06aba88fb62c)


# Network Security Groups (NSGs) and Traffic Analysis with Wireshark in Azure

This project demonstrates how to inspect and control network traffic between Azure Virtual Machines using Network Security Groups (NSGs) and Wireshark. You'll capture various types of traffic such as ICMP, SSH, DNS, and HTTP/S, and apply NSG rules to observe how they affect traffic flow.

---

## 🧰 Tools & Technologies Used

- Microsoft Azure (Virtual Machines, NSGs)
- Windows 10 and Ubuntu Server 20.04
- Remote Desktop & SSH
- Wireshark (for protocol analysis)
- Command Line Tools: `ping`, `ipconfig`, `nslookup`, `ssh`

---

## 🖥️ Operating Systems

- Windows 10 (21H2)
- Ubuntu Server 20.04

---



## 🔬 Summary of Actions & Observations

### Step 1: Initial VM Setup & ICMP Capture

- Create one Windows VM and one Linux VM in the same VNet and Resource Group.
- Install Wireshark on the Windows VM.
- Filter for `icmp` traffic and initiated ping tests to both the Linux VM and external site (www.google.com).
- Observe echo requests and replies in real time.

![ICMP Ping](images/icmp-ping.png)

---

### Step 2: NSG Rule to Block ICMP

- Initiate continuous ping to the Linux VM.
- Create a rule in the NSG attached to the Linux VM to deny inbound ICMP.
- Verify via Wireshark that echo replies stopped arriving.
- Delete the rule and confirmed ICMP traffic resumed as expected.

![ICMP Blocked](images/icmp-blocked.png)
![ICMP Restored](images/icmp-restored.png)

---

### Step 3: SSH and Dynamic IP

- Use PowerShell to SSH into the Linux VM.
- Observe SSH traffic in Wireshark.
- Run `ipconfig /renew` from an admin PowerShell prompt to request a new IP.
- Capture the DHCP and ARP traffic during the lease renewal.

![SSH Traffic](images/ssh-traffic.png)
![IP Renew](images/ip-renew.png)

---

### Step 4: DNS Queries with nslookup

- Use `nslookup` to resolve IPs for www.google.com and www.disney.com.
- Observe DNS traffic and resolution patterns in Wireshark.

![nslookup Traffic](images/nslookup-traffic.png)

---

## 💡 Notes

- NSGs offer fine-grained control over VM traffic and are crucial for Azure security.
- Wireshark is an invaluable tool for validating traffic flow and protocol-level behavior.
- Combine Azure's built-in monitoring tools with packet analysis for deeper insights.

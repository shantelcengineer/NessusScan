Watch Me Build The Lab HERE

https://www.loom.com/share/baa5bfd0914d46f1a2f7be6a486bb71b

**Tenable Nessus Vulnerability Scan**

Hands on lab demonstrating launching an EC2 instances, downloading Tenable Nessus and running a Scan

**Overview**

This document records the steps for performing a Nessus vulnerability scan against a Windows EC2 instance. It covers instance creation, remote access, installing Nessus, creating a Nessus account (using a temporary email), discovering the instance IP address, running the scan, and capturing results.

**Lab Objective**

Launch a Windows EC2 instance
Connect via RDP
Install Tenable Nessus scanner (local/remote) or use Nessus-hosted scanner
Create a Nessus account using a temporary email
Discover the instance IP address from within the instance
Configure and run a scan against the instance IP
Capture and summarize the scan findings

---

## Steps — Instance Creation & RDP Access

1. **Launch EC2 instance**
   - AMI: Windows (select appropriate Windows Server AMI)  
   - Instance type: `tm.3.2xlarge`  
   - Configure network & security:
     - Ensure RDP (TCP 3389) is allowed in the security group for your IP (or restrict to a bastion)
   - Key pair: create or use existing (to decrypt Administrator password)

2. **Retrieve Administrator password**
   - EC2 Console → Instances → Actions → Get Windows Password  
   - Decrypt using your private key file (`.pem`)

3. **RDP into Windows instance**
   - Remote Desktop Client
   - Server: `<public-ip-or-dns>` (replace with actual)
   - Username: `Administrator`
   - Password: (decrypted password from step 2)

---

## Steps — Install Nessus & Account Registration

1. **Download Nessus**
   - Open a browser inside the Windows instance
   - Navigate to Tenable's download page and download the Windows installer (`Nessus-<version>-x64.msi`)

2. **Create a Nessus account using temporary email**
   - Open a temp mail website (e.g., temp-mail.org or similar)
   - Register on Tenable/Nessus site using the temporary email
   - Retrieve confirmation link or code from the temp mail inbox and complete registration

3. **Install Nessus**
   - Run the `.msi` installer and follow prompts
   - Start Nessus service after installation
   - Open Nessus web UI: `https://localhost:8834` (in the instance browser)
   - Complete initial setup (trial or activation, create admin user)

---

## Steps — Retrieve IP Address from Windows Command Shell

Open PowerShell or Command Prompt and run one of these:

- Get local IPv4:
```powershell
ipconfig /all

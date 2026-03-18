📘 README — Azure Bastion VM Setup (Day 8)
🚀 Project Overview

This project demonstrates how to securely deploy and access both Windows and Linux Virtual Machines on Microsoft Azure using Azure Bastion, without exposing RDP (3389) or SSH (22) ports to the internet.

🛠️ What I Built

✅ Windows Virtual Machine (IIS Hosting)

✅ Linux Virtual Machine (Nginx Hosting)

✅ Azure Bastion for secure access

✅ Virtual Network with subnet configuration

✅ No public exposure of RDP/SSH ports

🔐 Key Concept

Instead of opening:

❌ RDP (3389)

❌ SSH (22)

We used:
👉 Azure Bastion (secure browser-based connection)

🌐 Architecture
Virtual Network
│
├── Azure Bastion (Subnet: AzureBastionSubnet)
│
├── Windows VM (IIS Website)
│
└── Linux VM (Nginx Website)
⚙️ Steps Performed
🪟 Windows VM Setup

Connected via Bastion (Browser-based RDP)

Opened PowerShell

Installed IIS:

Install-WindowsFeature -name Web-Server -IncludeManagementTools

Hosted a static website:

Path: C:\inetpub\wwwroot

Replaced index.html

🐧 Linux VM Setup

Connected via Bastion (SSH in browser)

Updated system:

sudo apt update && sudo apt upgrade -y

Installed Nginx:

sudo apt install nginx -y

Hosted a static website:

cd /var/www/html
sudo nano index.html
🌍 Output

Windows VM → IIS hosted webpage

Linux VM → Nginx hosted webpage

📌 Learning Highlights

Secure VM access using Bastion

No need for public IP exposure for SSH/RDP

Hosting websites on both Windows & Linux servers

Hands-on with IIS & Nginx

🔗 Repository Contents

Terraform / Setup files (if applicable)

Website code (HTML)

Documentation

🧠 Use Case

This setup is useful for:

Secure enterprise environments

Production-grade architectures

Learning cloud networking & security

🧭 Azure Portal Steps (Step-by-Step Guide)
1️⃣ Create Virtual Network

Go to Virtual Networks

Click Create

Add:

Address space: 10.0.0.0/16

➕ Add Subnets:

default → 10.0.1.0/24

AzureBastionSubnet → 10.0.2.0/27 (IMPORTANT: name must be exact)

2️⃣ Create Azure Bastion

Search Bastion

Click Create

Select:

Same VNet

AzureBastionSubnet

Create new Public IP

👉 Wait for deployment (~5–10 mins)

3️⃣ Create Windows VM

Go to Virtual Machines → Create

Choose:

Image: Windows Server 2019/2022

Size: Standard_B2s (or similar)

⚠️ Important:

NO inbound ports (RDP disabled)

Networking:

Select same VNet

Select default subnet

No Public IP (optional but recommended)

4️⃣ Create Linux VM

Same process:

Image: Ubuntu 22.04

Authentication: SSH or password

⚠️ Important:

NO inbound ports (SSH disabled)

5️⃣ Connect via Bastion

Go to VM → Click Connect → Bastion

Enter credentials

👉 Opens:

Windows → RDP in browser

Linux → SSH in browser

6️⃣ Configure Servers
🪟 Windows (IIS)
Install-WindowsFeature -name Web-Server -IncludeManagementTools

Edit:

C:\inetpub\wwwroot\index.html
🐧 Linux (Nginx)
sudo apt update
sudo apt install nginx -y

Edit:

/var/www/html/index.html
🎯 Final Result

Secure access via Bastion

Websites hosted on both VMs

No open ports exposed to internet 🔐

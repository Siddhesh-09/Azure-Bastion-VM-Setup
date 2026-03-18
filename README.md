# 🚀 Azure Bastion VM Setup (Day 8)

## 📌 Overview
This project demonstrates how to deploy and securely access **Windows and Linux Virtual Machines** on Microsoft Azure using **Azure Bastion**, without exposing RDP (3389) or SSH (22) ports to the internet.

Both VMs are configured to host static websites:
- 🪟 Windows VM → IIS Web Server
- 🐧 Linux VM → Nginx Web Server

---

## 🏗️ Architecture


Virtual Network
│

├── AzureBastionSubnet (Azure Bastion)

│

├── Default Subnet

│ ├── Windows VM (IIS)

│ └── Linux VM (Nginx)


---

## 🛠️ Resources Created

- Virtual Network (VNet)
- Subnets:
  - Default Subnet
  - AzureBastionSubnet
- Azure Bastion Host
- Windows Virtual Machine
- Linux Virtual Machine

---

## 🔐 Security Approach

Instead of exposing:
- ❌ RDP (3389)
- ❌ SSH (22)

We used:
- ✅ Azure Bastion (secure browser-based access)

---

## ⚙️ Implementation Steps (Azure Portal)

### 1. Create Virtual Network

- Address Space: `10.0.0.0/16`

Create Subnets:
- Default Subnet → `10.0.1.0/24`
- AzureBastionSubnet → `10.0.2.0/27` *(Name must be exact)*

---

### 2. Create Azure Bastion

- Go to **Bastion → Create**
- Select:
  - Same Virtual Network
  - AzureBastionSubnet
- Create a Public IP

---

### 3. Create Windows Virtual Machine

- Image: Windows Server (2019/2022)
- Size: Standard_B2s (or similar)
- Authentication: Username & Password

⚠️ Important:
- Do NOT open RDP (3389)
- Use same VNet and subnet

---

### 4. Create Linux Virtual Machine

- Image: Ubuntu 22.04 LTS
- Authentication: SSH or Password

⚠️ Important:
- Do NOT open SSH (22)
- Use same VNet and subnet

---

### 5. Connect via Azure Bastion

- Go to VM → Connect → Bastion
- Enter credentials

✔ Windows → Browser-based RDP  
✔ Linux → Browser-based SSH  

---

## 🌐 Server Configuration

### 🪟 Windows VM (IIS Setup)

Run in PowerShell:

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools


# Active Directory: Setting Up a Domain Controller in Azure

## Overview
This guide outlines the step-by-step process of setting up **Active Directory** in a **Microsoft Azure environment**. It includes the creation of a **Domain Controller (DC-1)** and a **client machine (Client-1)** that will be connected to the domain.

## 🔹 Step 1: Setup Domain Controller in Azure

### **1. Create a Resource Group**

- Open **Azure Portal** → Navigate to **Resource Groups** → Click **Create**.

![Screenshot 2025-03-19 145515](https://github.com/user-attachments/assets/a807c683-c330-49be-98c7-4be1bbf783a6)


### **2. Create a Virtual Network and Subnet**

- Go to **Azure Portal** → **Virtual Networks** → **Create a Virtual Network**.

![Screenshot 2025-03-19 145920](https://github.com/user-attachments/assets/72747e47-8e31-46fb-9c39-5ebb2f24a55b)


- Define the **Subnet** where both the Domain Controller and Client machine will reside.



### **3. Create the Domain Controller VM**
- In **Azure Portal**, create a **Windows Server 2022 VM**.
- **Name:** `DC-1`
- **Username:** `labuser`
- **Password:** `Cyberlab123!`
- Assign the VM to the **Virtual Network** created in Step 2.

![Screenshot 2025-03-19 150316](https://github.com/user-attachments/assets/51827e7b-edac-4f4d-b167-9b72cd6e5270)


### **4. Configure Network Settings for DC-1**
- After the VM is created, go to **Networking settings**.
- Set **NIC Private IP address** to **Static**.

![Screenshot 2025-03-19 151507](https://github.com/user-attachments/assets/9d684350-4e8c-4ab4-8ed8-6144998f5669)


### **5. Log into DC-1 and Configure Firewall**
- Use **Remote Desktop (RDP)** to log in to `DC-1`.

![Screenshot 2025-03-19 153109](https://github.com/user-attachments/assets/5ee62e69-fe7b-4370-9b8a-5cb92cfe438c)

- Open **Windows Defender Firewall** → Disable the firewall (for testing connectivity).

![Screenshot 2025-03-19 155323](https://github.com/user-attachments/assets/f9fb3c88-cdbb-4ca3-afdb-1a17d13d3475)

![Screenshot 2025-03-19 155407](https://github.com/user-attachments/assets/c3ca0b04-19a6-4b36-8cc2-0256fef45333)


## 🔹 Step 2: Setup Client-1 in Azure

### **1. Create the Client VM**
- In **Azure Portal**, create a **Windows 10 VM**.
- **Name:** `Client-1`
- **Username:** `labuser`
- **Password:** `Cyberlab123!`
- Attach `Client-1` to the **same region** and **Virtual Network** as `DC-1`.

![Screenshot 2025-03-19 152638](https://github.com/user-attachments/assets/ead805e6-d7b8-4e82-b4b2-abfda18f0b2a)


### **2. Configure Client-1's DNS Settings**
- After the VM is created, **set Client-1’s DNS settings** to `DC-1`'s **Private IP Address**.

![Screenshot 2025-03-19 160737](https://github.com/user-attachments/assets/0e65f073-4da1-4ea8-95a0-e1c241e6646b)

![Screenshot 2025-03-19 160920](https://github.com/user-attachments/assets/144fb599-5ad1-4d06-a8d5-ea1afa8014c1)


### **3. Restart Client-1**
- From **Azure Portal**, restart `Client-1` to apply DNS settings.

![Screenshot 2025-03-19 161457](https://github.com/user-attachments/assets/2ae778d0-bbff-442d-a4f5-c164b2f88c65)


### **4. Test Connectivity Between Client-1 and DC-1**
- **Login to Client-1** via **RDP**.

![Screenshot 2025-03-19 162807](https://github.com/user-attachments/assets/94ac5363-fe45-4733-850e-090dfcce483a)

- Open **Command Prompt (cmd)** and run:
  ```powershell
  ping <DC-1 Private IP>
  ```
  - ✅ If successful, the machines can communicate.
  - ❌ If failed, check firewall and network settings.

![Screenshot 2025-03-19 165454](https://github.com/user-attachments/assets/e910316b-ec0e-49ae-8750-f3c2469b8244)

Communication was at first unsuccessful due to dc-1's firewall settings not being completely turned off. 
After ensuring the firewall settings were off, client-1 and dc-1 were able to communicate.

### **5. Verify DNS Configuration on Client-1**
- Open **PowerShell** and run:
  ```powershell
  ipconfig /all
  ```
- Ensure the **DNS Server** field shows `DC-1`'s **Private IP Address**.

![Screenshot 2025-03-19 165756](https://github.com/user-attachments/assets/9a947e37-6391-4edb-99ab-d501c4d15a3d)


---

## ✅ Conclusion
You have successfully set up a **Domain Controller (DC-1)** and a **Windows 10 client (Client-1)** in **Azure**. This setup forms the foundation for an **Active Directory environment**, allowing further configuration of **user management, group policies, and authentication services**.

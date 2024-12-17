# Creating a Custom Linux-Based Operating System with .NET Support

## Table of Contents
1. **Overview**
2. **Requirements**
3. **Setup Base OS in VirtualBox or VMware**
4. **Install .NET Runtime and SDK**
5. **Customizing the OS**
6. **Remastering the ISO**
7. **Testing and Deployment**
8. **Adding and Running a New .NET Project**

---

## 1. Overview
This guide walks you through creating a custom operating system based on **Ubuntu** (Linux) that supports **.NET technology**. You will:
- Use Ubuntu as the base OS.
- Install the .NET SDK and runtime.
- Customize the OS to suit your needs.
- Remaster the ISO for deployment on other systems.

---

## 2. Requirements
Ensure you have the following tools and resources:

- **Base System**: A physical or virtual machine to install Ubuntu.
- **Operating System**: Ubuntu 22.04 LTS (or any recent version).
- **Virtualization Software**:
  - **VirtualBox** or **VMware** for creating virtual machines.
- **Software Tools**:
  - `Cubic` for remastering the ISO.
  - `.NET SDK` and `Runtime`.
  - ISO burning tools like **Rufus** (Windows) or `dd` (Linux).
- **Storage**: At least 20 GB of free disk space.
- **Internet Connection**.

---

## 3. Setup Base OS in VirtualBox or VMware

### Step 1: Download Ubuntu ISO
1. Visit [Ubuntu's official site](https://ubuntu.com/download/desktop).
2. Download the latest **Desktop** ISO.

### Step 2: Set Up a Virtual Machine
Use **VirtualBox** or **VMware** to set up a virtual machine:

#### VirtualBox
1. Install VirtualBox from [VirtualBox.org](https://www.virtualbox.org/).
2. Create a new virtual machine:
   - **Name**: Custom Ubuntu
   - **RAM**: Allocate at least 4 GB.
   - **Storage**: Create a 20+ GB virtual hard disk.
3. Attach the Ubuntu ISO as the boot disk.
4. Start the VM and install Ubuntu.

#### VMware
1. Install VMware Workstation or VMware Player.
2. Create a new virtual machine:
   - **Name**: Custom Ubuntu
   - **RAM**: Allocate at least 4 GB.
   - **Storage**: Create a 20+ GB virtual hard disk.
3. Attach the Ubuntu ISO as the boot disk.
4. Start the VM and install Ubuntu.

---

## 4. Install .NET Runtime and SDK

### Step 1: Update the System
Inside the virtual machine, run the following commands:
```bash
sudo apt update && sudo apt upgrade -y
```

### Step 2: Install .NET SDK
Install the **.NET 6** SDK (or any version you require):
```bash
wget https://dotnet.microsoft.com/download/dotnet/scripts/v1/dotnet-install.sh
chmod +x dotnet-install.sh
./dotnet-install.sh --version 6.0.100
```

### Step 3: Verify Installation
```bash
~/.dotnet/dotnet --version
```

### Step 4: Set Up PATH
Add .NET to the system path:
```bash
echo 'export DOTNET_ROOT=$HOME/.dotnet' >> ~/.bashrc
echo 'export PATH=$PATH:$DOTNET_ROOT:$DOTNET_ROOT/tools' >> ~/.bashrc
source ~/.bashrc
```
Verify again:
```bash
dotnet --info
```

---

## 5. Customizing the OS

### Step 1: Install Additional Software
Install any additional packages you need:
```bash
sudo apt install -y git curl build-essential vim
```

### Step 2: Pre-configure .NET Projects
Copy pre-built .NET applications or custom scripts into the virtual machine:
```bash
mkdir ~/CustomApps
cp /path/to/your/project ~/CustomApps/
```

### Step 3: Modify Default Settings
Customize Ubuntu to suit your preferences:
- Update themes, wallpapers, and startup applications.
- Add aliases or startup scripts.

---

## 6. Remastering the ISO

### Step 1: Install Cubic
Install Cubic for remastering the ISO inside the virtual machine:
```bash
sudo apt install cubic
```

### Step 2: Launch Cubic and Customize
1. Open Cubic from the applications menu.
2. Select the default Ubuntu ISO as the base.
3. Follow the on-screen steps:
   - **Install .NET SDK and runtime**.
   - Include any custom software or files.
4. Finalize the remastering process and export the new ISO.

### Step 3: Extract the ISO from the Virtual Machine
To transfer the new ISO outside the VM:
1. Use file-sharing tools in **VirtualBox** or **VMware**.
   - In VirtualBox, enable shared folders.
   - In VMware, use shared folders or drag-and-drop functionality.
2. Copy the remastered ISO to the host machine.

---

## 7. Testing and Deployment

### Step 1: Boot and Verify
1. Create a bootable USB drive with the new ISO:
   ```bash
   sudo dd if=custom-ubuntu.iso of=/dev/sdX bs=4M status=progress && sync
   ```
   Replace `/dev/sdX` with your USB drive.
2. Boot the ISO on a physical or virtual machine.
3. Verify `.NET` is pre-installed:
   ```bash
   dotnet --info
   ```

### Step 2: Final Deployment
Distribute the ISO for installation on other systems.

---

## 8. Adding and Running a New .NET Project

### Step 1: Create a New .NET Project
Inside the Ubuntu environment, create a new .NET project:
```bash
mkdir ~/NewProject
cd ~/NewProject
~/.dotnet/dotnet new console -o MyApp
```
This creates a new .NET **console application** in the `MyApp` folder.

### Step 2: Build and Run the Project
Navigate to the project directory and run the application:
```bash
cd MyApp
~/.dotnet/dotnet run
```

### Step 3: Edit and Update
- Open the `Program.cs` file in a text editor (e.g., Vim, Nano, or VS Code):
  ```bash
  nano Program.cs
  ```
- Make changes to the code, save the file, and re-run the project:
  ```bash
  ~/.dotnet/dotnet run
  ```

---

## Conclusion
By following this guide, you have:
- Set up Ubuntu in a virtual environment.
- Installed and configured .NET.
- Added and run a new .NET project.
- Remastered the ISO with all required packages.
- Exported the new ISO for deployment.

Your custom OS is now ready for use!

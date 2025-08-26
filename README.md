# Setting Up Kali Linux and Metasploitable for Penetration Testing

![Metasploit Logo](https://media.licdn.com/dms/image/v2/D4D12AQEa_J0dinoDtA/article-cover_image-shrink_720_1280/article-cover_image-shrink_720_1280/0/1721187455024?e=1761782400&v=beta&t=-fWGHQHAQg8do_m7uYqShhL2ZfH_fRGmCWEvZYV1-5g)

## Introduction

This guide walks you through the process of setting up Kali Linux and Metasploitable virtual machines in VirtualBox for penetration testing. Kali Linux is a specialized Linux distribution for security researchers and penetration testers, while Metasploitable is a deliberately vulnerable virtual machine designed for practicing ethical hacking techniques. By following this guide, you'll configure both machines on the same network, enabling you to test security exploits in a controlled environment.

**Note**: This guide is for educational purposes only. Unauthorized testing on live systems is illegal. Always obtain explicit permission before performing security testing.

## Prerequisites

- **VirtualBox**: Installed on your system (download from [virtualbox.org](https://www.virtualbox.org/)).
- **Kali Linux VM Image**: Available from the official Kali Linux website.
- **Metasploitable VM Image**: Available from the Metasploit project website.
- **Extraction Tool**: WinRAR or a similar tool to extract downloaded files.
- **Web Browser**: For downloading the VM images (e.g., Brave, Firefox, or Chrome).
- **Basic Knowledge**: Familiarity with virtual machines and basic networking concepts.

## Step-by-Step Setup Guide

This guide follows the structure of a YouTube tutorial, providing a clear, step-by-step process to set up Kali Linux and Metasploitable.

### Step 1: Downloading the Virtual Machine Images

1. **Download Metasploitable**:
   - Visit the Metasploit project website ([sourceforge.net/projects/metasploitable](https://sourceforge.net/projects/metasploitable/)).
   - Click the **Download** button to get the Metasploitable VM image (typically a `.zip` file).

2. **Download Kali Linux**:
   - Go to the official Kali Linux website ([kali.org](https://www.kali.org/get-kali/)).
   - Select the **VirtualBox** image under the virtual machine section and download it (e.g., `.ova` or `.vbox` format).

3. **Monitor Downloads**:
   - Use your browser’s download manager to track the progress of both files. Ensure sufficient disk space (approximately 10-20 GB for both).

### Step 2: Extracting the Downloaded Files

1. **Extract Files**:
   - Use an extraction tool like WinRAR to unzip the downloaded files:
     ```bash
     # Example using WinRAR (Windows)
     winrar x metasploitable-linux-2.0.0.zip
     winrar x kali-linux-2023.4-vbox-amd64.ova
     ```
   - Extract both files to separate folders (e.g., `Metasploitable` and `Kali-Linux`).

### Step 3: Importing Kali Linux into VirtualBox

1. **Open VirtualBox**:
   - Launch Oracle VM VirtualBox.

2. **Add Kali Linux VM**:
   - Click **File > Import Appliance** (or **Add** in older versions).
   - Select the extracted Kali Linux file (e.g., `kali-linux-2023.4-vbox-amd64.ova` or `.vbox`).
   - Click **Open** and then **Import** (or **Start** for `.vbox` files).

3. **Log In to Kali Linux**:
   - Start the Kali Linux VM.
   - Use the default credentials: **Username**: `kali`, **Password**: `kali`.

4. **Check IP Address**:
   - Open a terminal in Kali Linux and run:
     ```bash
     ip a
     ```
   - Note the IP address (e.g., `10.0.2.x`) for later use.

5. **Power Off Kali Linux**:
   - Shut down the VM to prepare for network configuration.

### Step 4: Importing Metasploitable into VirtualBox

1. **Add Metasploitable VM**:
   - In VirtualBox, click **New**.
   - Name the machine `Metasploitable`, set **Type** to `Linux`, and **Version** to `Ubuntu (64-bit)` or similar.
   - Choose **Use an existing virtual hard disk file**.
   - Navigate to the extracted Metasploitable file (e.g., `metasploitable.vmdk`), select it, and click **Open** > **Create**.

2. **Start Metasploitable**:
   - Start the Metasploitable VM.
   - Log in with the default credentials: **Username**: `msfadmin`, **Password**: `msfadmin`.

3. **Check IP Address**:
   - In the Metasploitable terminal, run:
     ```bash
     ip a
     ```
   - Note the IP address (e.g., `10.0.2.x`).

4. **Power Off Metasploitable**:
   - Shut down the VM to configure networking.

### Step 5: Configuring the Network

1. **Create a NAT Network**:
   - In VirtualBox, go to **File > Preferences > Network**.
   - Click the **+** icon to create a new NAT network.
   - Name it `network-tuto` and set the network address to `10.0.2.0/24`.

2. **Assign NAT Network to Kali Linux**:
   - Open the **Settings** for the Kali Linux VM.
   - Go to the **Network** tab, set **Adapter 1** to:
     - **Attached to**: `NAT Network`.
     - **Name**: `network-tuto`.
   - Save the settings.

3. **Assign NAT Network to Metasploitable**:
   - Repeat the process for the Metasploitable VM, assigning the same `network-tuto` NAT network.

### Step 6: Verifying Connectivity

1. **Start Both VMs**:
   - Launch Kali Linux and Metasploitable.

2. **Log In**:
   - Log in to Kali Linux (`kali`/`kali`).
   - Log in to Metasploitable (`msfadmin`/`msfadmin`).

3. **Check IP Addresses**:
   - In Kali Linux, run:
     ```bash
     ip a
     ```
   - In Metasploitable, run:
     ```bash
     ip a
     ```
   - Confirm both VMs are on the same subnet (e.g., `10.0.2.x`).

4. **Test Connectivity**:
   - From Kali Linux, ping the Metasploitable VM’s IP address (e.g., `10.0.2.4`):
     ```bash
     ping 10.0.2.4
     ```
   - Successful ping responses confirm network connectivity.

### Step 7: Next Steps
With Kali Linux and Metasploitable set up on the same network, you’re ready to explore penetration testing techniques, such as:
- Running Metasploit Framework on Kali Linux (`msfconsole`).
- Scanning Metasploitable for vulnerabilities using tools like Nmap.
- Exploiting known vulnerabilities in Metasploitable for practice.

## Best Practices
- **Use Snapshots**: Create VirtualBox snapshots before testing exploits to revert changes easily.
- **Isolate the Environment**: Ensure the NAT network is isolated from your host network to prevent accidental exposure.
- **Update Kali Linux**: Run `sudo apt update && sudo apt upgrade` to keep tools current.
- **Ethical Hacking**: Only test on systems you own or have explicit permission to test.

## Conclusion
This guide demonstrated how to set up Kali Linux and Metasploitable virtual machines in VirtualBox, configure them on a shared NAT network, and verify connectivity. This setup provides a safe environment for learning penetration testing and ethical hacking.

For a video walkthrough of this process, check out the tutorial linked in the repository. Star and contribute to support the community!

**Resources**:
- [Kali Linux Downloads](https://www.kali.org/get-kali/)
- [Metasploitable Download](https://sourceforge.net/projects/metasploitable/)
- [VirtualBox](https://www.virtualbox.org/)
- [Metasploit Framework Documentation](https://docs.metasploit.com/)

**Disclaimer**: This guide is for educational purposes only. Unauthorized testing is illegal and unethical. Always obtain explicit permission before performing security testing.

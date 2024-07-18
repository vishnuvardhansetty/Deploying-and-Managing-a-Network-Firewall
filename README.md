# pfSense Firewall Setup and Configuration

## Project Overview
This project involves setting up and configuring a pfSense firewall in a virtual environment. The objective is to control network traffic, monitor logs, and generate reports on traffic patterns and potential threats.

## Prerequisites
- Basic knowledge of networking concepts.
- A computer with virtualization software (VirtualBox, VMware).
- ISO image of pfSense.

## Step-by-Step Setup Guide

### Step 1: Setting Up the Virtual Environment
1. **Download and Install Virtualization Software**
   - [Download VirtualBox](https://www.virtualbox.org/)
   - Install the software following the on-screen instructions.
   - ![Download virtualbox](https://github.com/user-attachments/assets/f3bf4194-710b-4923-9f64-7c2a83288e8c)

2. **Download pfSense ISO**
   - [Download pfSense ISO](https://www.pfsense.org/download/) for the desired architecture (usually amd64).
   - ![Screenshot (2)](https://github.com/user-attachments/assets/d742bcf1-1519-4e3f-b052-4b39a1133805)

### Step 2: Creating a Virtual Machine for pfSense
1. **Open VirtualBox**
   - Launch your chosen virtualization software.

2. **Create a New Virtual Machine**
   - **VirtualBox**:
     - Click "New".
     - Name the VM (e.g., "pfSense").
     - Set the type to "BSD" and version to "FreeBSD (64-bit)".
     - Click "Next".
  ![Screenshot (3)](https://github.com/user-attachments/assets/dccce8df-c0b8-4c3b-a313-39eb04a543ad)

3. **Allocate Resources**
   - **Memory**:
     - Assign at least 1 GB of memory (1024 MB).
     - Click "Next".
   - **Hard Disk**:
     - Create a new virtual hard disk.
     - Set the disk size to at least 10 GB.
     - Use the default options for disk type and storage allocation.
     - Click "Create".
     - ![Screenshot (4)](https://github.com/user-attachments/assets/4b3f77ae-7b37-4efe-8af5-4ee1132aaa12)


4. **Attach the pfSense ISO**
   - **VirtualBox**:
     - Select the VM and click "Settings".
     - Go to "Storage" and click on the empty CD/DVD drive.
     - Click the disk icon next to "Optical Drive" and choose "Choose a disk file".
     - Browse to the pfSense ISO file and select it.

### Step 3: Installing pfSense
1. **Start the VM**
   - **VirtualBox**: Select the VM and click "Start".
2. **Follow Installation Prompts**
   - Select the default options for language and keymap.
   - Choose "Install" from the pfSense installer menu.
   - Select the appropriate partition scheme (usually the default).
   - Wait for the installation to complete.
   - ![Screenshot (5)](https://github.com/user-attachments/assets/55d9cb10-2440-485a-9b0c-554001794d41)

3. **Complete the Installation**
   - Once the installation is complete, remove the ISO from the virtual drive.
     - **VirtualBox**: Go to "Devices" > "Optical Drives" > "Remove disk from virtual drive".
     - **VMware**: Go to "VM" > "Removable Devices" > "CD/DVD" > "Disconnect".
   - Reboot the VM.

### Step 4: Initial Configuration of pfSense
1. **Initial Console Setup**
   - After reboot, follow the console prompts to set up the initial configuration.
   - Assign network interfaces (WAN and LAN). The first interface will typically be assigned to the WAN, and the second to the LAN.
     - The interface assignment prompt will look like:
       ```
       Valid interfaces are:
       em0 0000:00:01.0
       em1 0000:00:02.0
       Which interface do you want to configure as WAN? (em0)
       Which interface do you want to configure as LAN? (em1)
       ```
       ![Screenshot (6)](https://github.com/user-attachments/assets/d2e8c5d6-d108-447a-aa65-cabd31974834)


2. **Access pfSense Web Interface**
   - Connect a device to the LAN interface.
   - Set the device's network settings to DHCP or manually assign an IP address in the same subnet as the pfSense LAN IP.
   - Open a web browser and navigate to the LAN IP address (default is usually `192.168.1.1`).
   - Log in with default credentials (username: `admin`, password: `pfsense`).
   - ![Screenshot (7)](https://github.com/user-attachments/assets/39ae5aca-c900-4797-8458-defaeffff561)

3. **Wizard Setup**
   - Follow the initial setup wizard in the web interface to configure basic settings such as hostname, domain, DNS servers, and password.
     - **Step 1**: Welcome to pfSense Setup Wizard.
     - **Step 2**: General Information (hostname, domain, DNS servers).
     - ![Screenshot (10)](https://github.com/user-attachments/assets/923d0c24-25fb-4dad-8b79-9432739e2467)
     - **Step 3**: Time Server Information (set NTP server if needed).
     - **Step 4**: WAN Configuration (set IP address type, usually DHCP for home networks).
     - **Step 5**: LAN Configuration (confirm or change LAN IP address).
     - **Step 6**: Set Admin WebGUI Password.
     - ![Screenshot (11)](https://github.com/user-attachments/assets/651203e7-348f-4c7c-9a55-60716ac95aa9)
     - **Step 7**: Reload configuration and complete setup.

### Step 5: Configuring Firewall Rules
1. **Navigate to Firewall Rules**
   - In the pfSense web interface, go to "Firewall" > "Rules".

2. **Default Rules**
   - Review the default rules. By default, pfSense blocks all incoming traffic on the WAN and allows all outgoing traffic on the LAN.

3. **Create a New Rule**
   - Click on "Add" to create a new firewall rule.
   - Example Rule: Allow HTTP/HTTPS traffic from LAN to WAN.
     - **Action**: Pass
     - **Interface**: LAN
     - **Address Family**: IPv4
     - **Protocol**: TCP
     - **Source**: LAN net
     - **Destination**: Any
     - **Destination Port Range**: HTTP (80) and HTTPS (443)
     - **Description**: Allow HTTP/HTTPS traffic from LAN to WAN
   - Save and apply changes.
   - ![Screenshot (12)](https://github.com/user-attachments/assets/217d0aa2-b5bc-4775-9564-58319e15bb32)


4. **Testing Firewall Rules**
   - On a device connected to the LAN, try accessing the internet to ensure rules are working.
   - Adjust rules as necessary for different types of traffic (e.g., SSH, FTP).

### Step 6: Monitoring and Logging
1. **View Logs**
   - Go to "Status" > "System Logs" in the pfSense web interface.
   - Review logs to see traffic allowed and blocked by the firewall.
     - Logs are categorized by type (e.g., Firewall, DHCP, System).
     - ![Screenshot (13)](https://github.com/user-attachments/assets/270c933d-1d5b-4a6b-ae52-27208230229a)

2. **Enable Additional Logging**
   - Configure logging options in "Status" > "System Logs" > "Settings".
   - Enable logging for specific rules if needed by editing the rule and checking the "Log packets that are handled by this rule" option.

### Step 7: Reporting and Analysis
1. **Generate Reports**
   - Use pfSense's built-in reporting tools to generate traffic reports.
   - Go to "Diagnostics" > "Traffic Graph" to see real-time traffic data.

2. **Analyze Traffic Patterns**
   - Review logs and reports to identify any unusual traffic patterns or potential threats.
   - Document findings and any actions taken to mitigate threats.

## Summary Report
Include a brief summary report here on traffic patterns, potential threats identified, and any actions taken to mitigate these threats.

---

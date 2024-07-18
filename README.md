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

2. **Download pfSense ISO**
   - [Download pfSense ISO](https://www.pfsense.org/download/) for the desired architecture (usually amd64).

### Step 2: Creating a Virtual Machine for pfSense
1. **Open VirtualBox/VMware**
   - Launch your chosen virtualization software.

2. **Create a New Virtual Machine**
   - **VirtualBox**:
     - Click "New".
     - Name the VM (e.g., "pfSense Firewall").
     - Set the type to "BSD" and version to "FreeBSD (64-bit)".
     - Click "Next".
   - **VMware**:
     - Click "Create a New Virtual Machine".
     - Select "Installer disc image file (iso)" and browse to the pfSense ISO file.
     - Click "Next".

3. **Allocate Resources**
   - **Memory**:
     - Assign at least 1 GB of memory (1024 MB).
     - Click "Next".
   - **Hard Disk**:
     - Create a new virtual hard disk.
     - Set the disk size to at least 10 GB.
     - Use the default options for disk type and storage allocation.
     - Click "Create".

4. **Attach the pfSense ISO**
   - **VirtualBox**:
     - Select the VM and click "Settings".
     - Go to "Storage" and click on the empty CD/DVD drive.
     - Click the disk icon next to "Optical Drive" and choose "Choose a disk file".
     - Browse to the pfSense ISO file and select it.
   - **VMware**:
     - Select the VM and click "Edit virtual machine settings".
     - Select "CD/DVD (SATA)" and choose "Use ISO image file".
     - Browse to the pfSense ISO file and select it.

### Step 3: Installing pfSense
1. **Start the VM**
   - **VirtualBox**: Select the VM and click "Start".
   - **VMware**: Select the VM and click "Power on this virtual machine".

2. **Follow Installation Prompts**
   - Select the default options for language and keymap.
   - Choose "Install" from the pfSense installer menu.
   - Select the appropriate partition scheme (usually the default).
   - Wait for the installation to complete.

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

2. **Access pfSense Web Interface**
   - Connect a device to the LAN interface.
   - Set the device's network settings to DHCP or manually assign an IP address in the same subnet as the pfSense LAN IP.
   - Open a web browser and navigate to the LAN IP address (default is usually `192.168.1.1`).
   - Log in with default credentials (username: `admin`, password: `pfsense`).

3. **Wizard Setup**
   - Follow the initial setup wizard in the web interface to configure basic settings such as hostname, domain, DNS servers, and password.
     - **Step 1**: Welcome to pfSense Setup Wizard.
     - **Step 2**: General Information (hostname, domain, DNS servers).
     - **Step 3**: Time Server Information (set NTP server if needed).
     - **Step 4**: WAN Configuration (set IP address type, usually DHCP for home networks).
     - **Step 5**: LAN Configuration (confirm or change LAN IP address).
     - **Step 6**: Set Admin WebGUI Password.
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

4. **Testing Firewall Rules**
   - On a device connected to the LAN, try accessing the internet to ensure rules are working.
   - Adjust rules as necessary for different types of traffic (e.g., SSH, FTP).

### Step 6: Monitoring and Logging
1. **View Logs**
   - Go to "Status" > "System Logs" in the pfSense web interface.
   - Review logs to see traffic allowed and blocked by the firewall.
     - Logs are categorized by type (e.g., Firewall, DHCP, System).

2. **Enable Additional Logging**
   - Configure logging options in "Status" > "System Logs" > "Settings".
   - Enable logging for specific rules if needed by editing the rule and checking the "Log packets that are handled by this rule" option.

### Step 7: Reporting and Analysis
1. **Generate Reports**
   - Use pfSense's built-in reporting tools to generate traffic reports.
   - Go to "Diagnostics" > "Traffic Graph" to see real-time traffic data.

2. **Analyze Traffic Patterns**
   - Review logs and reports to identify any unusual traffic patterns or potential threats.
   - Document your findings and any actions taken to mitigate threats.

### Step 8: Documentation and Presentation
1. **Document the Setup Process**
   - Write detailed documentation of each step, including screenshots.
   - Explain the rationale behind each configuration decision.

2. **Create a Presentation**
   - Prepare a presentation summarizing your project.
   - Highlight key configurations, rules created, and any significant findings from your analysis.

## Deliverables
- Detailed documentation of the setup process.
- Screenshots of configurations and logs.
- A summary report of traffic patterns and potential threats.
- A presentation highlighting key aspects of the project.

---

## Screenshots
![VirtualBox New VM](path/to/your/screenshot1.png)
![pfSense Installation](path/to/your/screenshot2.png)
![pfSense Web Interface](path/to/your/screenshot3.png)

---

## Summary Report
Include a brief summary report here on traffic patterns, potential threats identified, and any actions taken to mitigate these threats.

---

## Presentation
Link to the presentation file (e.g., PDF, PowerPoint) here.

[Presentation](path/to/your/presentation.pdf)


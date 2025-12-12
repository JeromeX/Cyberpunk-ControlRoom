# 🌐 CYBER CONTROL ROOM

> **A Cyberpunk-themed Network Monitoring & Management System.**
> Visualize your network infrastructure with style. Detect rogue devices, monitor server health, and get alerted when systems go dark.

## ⚡ Features

### 👁️ Network Overwatch

  * **Auto-Scanning:** Periodically scans defined network segments (CIDR) to detect active hosts.
  * **Live Status:** Real-time online/offline status checking via ICMP (Ping).
  * **Vendor Recognition:** Automatic MAC address resolution and Vendor lookup using a robust OUI downloader (IEEE & Wireshark mirrors).
  * **Rogue Device Detection:** New devices must be explicitly "approved" by an administrator before being fully tracked.

### 🛡️ Security & Alerts

  * **Offline Alerts:** Automatically sends an email notification if a critical device is offline for more than 1 hour.
  * **Daily Reports:** Sends a summary of network health and server traffic every morning at 08:00.
  * **Secure Architecture:**
      * Hybrid Database: MySQL for core data, SQLite for high-speed logging.
      * Encrypted Configuration: Sensitive DB credentials are encrypted using Fernet (symmetric encryption).
      * Role-Based Access Control (RBAC): Administrator and Poweruser roles.

### 💻 The Dashboard (UI)

  * **Cyberpunk Aesthetic:** High-contrast, neon-styled interface using Bootstrap 5 and custom CSS.
  * **Real-time Feedback:** Devices glow red when online and fade to grey with a skull icon when offline.
  * **System Monitor:** Displays server CPU, RAM, Disk usage, and Temperature in real-time.
  * **Integrated Log Terminal:** View system events directly in the browser (backed by a crash-resistant file-first logging system).

-----

## 🛠️ Tech Stack

  * **Backend:** Python (Flask)
  * **Database:** MySQL (Primary), SQLite (Logs & OUI Cache)
  * **Frontend:** HTML5, CSS3 (Neon variables), JavaScript (Fetch API), Bootstrap 5
  * **Libraries:** `ping3`, `psutil`, `cryptography`, `requests`

-----

## 🚀 Installation & Setup

### Prerequisites

  * Python 3.8 or higher
  * MySQL Server (local or remote)
  * Linux/Windows/MacOS (Root/Admin privileges required for raw socket pings on some OS)

### 1\. Clone the Repository

```bash
git clone https://github.com/yourusername/cyber-control-room.git
cd cyber-control-room
```

### 2\. Install Dependencies

Create a virtual environment (recommended) and install requirements:

```bash
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
pip install flask flask-login mysql-connector-python ping3 psutil cryptography requests
# Optional for better ARP detection:
pip install scapy
```

### 3\. Database Setup

Ensure your MySQL server is running. You need to create an empty database (or let the setup script do it if the user has permissions):

```sql
CREATE DATABASE controlroom;
```

### 4\. Run the Application

Start the server. On the first run, it will generate a `secret.key` for encryption.

```bash
python app.py
```

*Note: On Linux, you might need `sudo python app.py` to allow ICMP pings.*

### 5\. Initial Configuration

1.  Open your browser and navigate to `http://localhost:5000`.
2.  You will be redirected to the **/setup** page.
3.  Enter your MySQL credentials and define an **Admin User**.
4.  Once initialized, log in with your new credentials.

-----

## 📖 Usage Guide

### Managing Instances (Networks)

Go to the **Menu** -\> **+ Instance**.

  * **Name:** e.g., "Home LAN"
  * **Network IP:** e.g., "192.168.1.0"
  * **CIDR:** e.g., 24 (for /24 subnet)

### Adding Devices

  * **Auto-Scan:** Click the **SCAN** button. New devices will appear as "Waiting Approval".
  * **Manual Add:** Go to **Menu** -\> **+ Device**. Enter IP and Name. The system immediately checks if it's online.

### Background Tasks

The system runs several threads in the background:

  * `scan_worker`: Cycles through instances based on the set interval.
  * `daily_report_worker`: Sends emails at 08:00.
  * `log_sync_worker`: Syncs the high-speed `system.log` file to the encrypted SQLite database.

-----

## 📂 Project Structure

```
/
├── app.py                 # Main Flask application & Logic
├── templates/
│   ├── index.html         # Main Dashboard
│   ├── login.html         # Auth Page
│   └── setup.html         # First-time Setup
├── static/
│   └── Cyberpunk_JX.png   # Background Image
├── system.log             # Raw plain-text logs (File-First logging)
├── controlroom_log.db     # Encrypted SQLite Log Storage
├── oui_encrypted.db       # Vendor Database (Auto-downloaded)
└── secret.key             # Encryption Key (DO NOT SHARE!)
```

-----

## ⚠️ Troubleshooting

  * **Pings not working:** Ensure the script has root/admin privileges (`sudo`). `ping3` requires raw sockets.
  * **Database Locked:** The system uses a `log_lock` and a file-first logging approach to prevent SQLite locks. If issues persist, check file permissions.
  * **OUI Download Failed:** The system tries 3 different mirrors (IEEE, LinuxNet, Wireshark). If all fail, a fallback emergency dataset is used.

-----

## 📜 License

This project is licensed under the MIT License - see the [LICENSE]([https://www.google.com/search?q=LICENSE](https://github.com/JeromeX/Cyberpunk-ControlRoom?tab=MIT-1-ov-file)) file for details.

-----

## 👨‍💻 Author

**Malte Speck** *Concept & Development*

-----

*System initialized. Happy Hunting.* 🕵️‍♂️

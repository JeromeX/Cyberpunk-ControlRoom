# CYBER CONTROL ROOM
<img width="1920" height="1080" alt="2025-12-13 09_12_31-SYSTEM INITIALIZATION und 1 weitere Seite - Maltex – Microsoft​ Edge" src="https://github.com/user-attachments/assets/bd3a4999-0c9e-4463-adee-e7c74cddef06" />
<img width="1920" height="1080" alt="2025-12-13 09_13_07-ACCESS CONTROL und 1 weitere Seite - Maltex – Microsoft​ Edge" src="https://github.com/user-attachments/assets/25a11a5a-365f-4729-b9c1-c20e96c008ce" />
<img width="1920" height="1080" alt="2025-12-13 09_14_31-CONTROL ROOM und 1 weitere Seite - Maltex – Microsoft​ Edge" src="https://github.com/user-attachments/assets/fe504b70-2e78-4115-9185-77c73cbcc4d4" />

> **Secure Network Monitoring & Management System**

This repository contains the loader logic for the Cyber Control Room. The core application logic is protected and encrypted. This system provides real-time network scanning, device management, and visual monitoring in a cyberpunk aesthetic.

## 📦 Deliverables

The system consists of two critical files:
1.  `boot.py` - The secure bootloader and execution environment.
2.  `controlroom.enc` - The encrypted core payload containing the application logic.

## 🚀 Prerequisites

To run the Cyber Control Room, you need a Linux Server (Ubuntu/Debian recommended) with the following components:

* **OS:** Ubuntu 20.04 LTS or newer / Debian 11+
* **Python:** Version 3.8 or newer
* **Database:** MySQL or MariaDB
* **Access:** Root privileges (required for network scanning)

## 🛠️ Quick Start

1.  **Prepare Directory:**
    Place `boot.py` and `controlroom.enc` in `/var/www/html/controlroom`.

2.  **Install Dependencies:**
    ```bash
    apt update && apt install python3-pip python3-venv mariadb-server
    ```

3.  **Setup Virtual Environment & Libraries:**
    ```bash
    python3 -m venv venv
    source venv/bin/activate
    pip install flask flask-login cryptography mysql-connector-python psutil ping3 dnspython
    ```

4.  **Run:**
    ```bash
    python boot.py
    ```

5.  **Access:**
    Open `http://<YOUR_SERVER_IP>:5000` in your browser.

## 🔒 Security Note

The application runs purely in memory. The source code is decrypted on-the-fly and never written to the disk.

## 📄 License

Proprietary software. Unauthorized distribution or reverse engineering of the `.enc` file is strictly prohibited.

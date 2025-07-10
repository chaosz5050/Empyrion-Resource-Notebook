# 🚀 Empyrion Resource Location Tracker

A web-based resource tracking tool for Empyrion - Galactic Survival. Track mining locations, danger levels, and distances across sectors, planets, and moons. Perfect for server admins and players who want to share resource information with their community.

![Empyrion Resource Tracker](https://img.shields.io/badge/Empyrion-Resource%20Tracker-blue?style=for-the-badge&logo=spacex)

## ✨ Features

- 🌐 **Web-based interface** - Access from any device with a browser
- 📱 **Mobile-friendly** - Responsive design perfect for phones and tablets
- 🌙 **Dark theme** - Easy on the eyes during long gaming sessions
- ⚡ **Real-time editing** - Click to edit any field, auto-saves instantly
- 🏷️ **Resource tagging** - Visual tags for multiple resources per location
- 🔍 **Advanced filtering** - Filter by name, type, danger level, or resources
- 📊 **CSV export** - Share data with your community
- 🌐 **Network sharing** - Multiple users can access simultaneously
- 💾 **SQLite database** - Lightweight, no external database required

## 🎮 Perfect for Gaming

- Access resource locations on your phone while playing Empyrion
- Share with server members - no installation required for them
- Track dangerous areas and safe mining spots
- Calculate distances from your starting location
- Never Alt+Tab out of the game again!

## 📋 Requirements

- Python 3.7+
- Flask web framework

## 🚀 Quick Start

### 1. Installation

```bash
# Install Flask
pip install flask

# Download the application
# Save the empyrion_tracker.py file to your desired directory
```

### 2. Run the Application

```bash
python empyrion_tracker.py
```

### 3. Access the Tracker

The application will show you the access URLs:

```
🚀 Empyrion Resource Location Tracker
==================================================
🖥️  Local access:   http://localhost:5000
📱 Network access:  http://192.168.1.100:5000
==================================================
```

- **Local access:** Use `localhost:5000` on the same machine
- **Network access:** Use the IP address from other devices on your network

## 🔥 Opening Firewall Port 5000

To allow other devices (phones, tablets, other computers) to access your tracker, you need to open port 5000 in your firewall.

### Linux (CachyOS/Arch/Most Distributions)

#### Using UFW (Ubuntu/Debian-based):
```bash
# Enable UFW if not already enabled
sudo ufw enable

# Allow port 5000
sudo ufw allow 5000

# Check status
sudo ufw status
```

#### Using firewalld (Fedora/RHEL/CentOS):
```bash
# Allow port 5000
sudo firewall-cmd --permanent --add-port=5000/tcp
sudo firewall-cmd --reload

# Check status
sudo firewall-cmd --list-ports
```

#### Using iptables (Advanced users):
```bash
# Allow incoming connections on port 5000
sudo iptables -I INPUT -p tcp --dport 5000 -j ACCEPT

# Save rules (method varies by distribution)
# Debian/Ubuntu:
sudo iptables-save > /etc/iptables/rules.v4

# RHEL/CentOS:
sudo service iptables save
```

### Windows

#### Method 1: Windows Defender Firewall (GUI)
1. Open **Windows Security** → **Firewall & network protection**
2. Click **Advanced settings**
3. Click **Inbound Rules** → **New Rule**
4. Select **Port** → **Next**
5. Select **TCP** and enter **5000** in specific ports
6. Select **Allow the connection** → **Next**
7. Apply to all profiles (Domain, Private, Public) → **Next**
8. Name it "Empyrion Resource Tracker" → **Finish**

#### Method 2: Command Line (PowerShell as Administrator)
```powershell
# Allow inbound traffic on port 5000
New-NetFirewallRule -DisplayName "Empyrion Resource Tracker" -Direction Inbound -Protocol TCP -LocalPort 5000 -Action Allow

# Verify the rule was created
Get-NetFirewallRule -DisplayName "Empyrion Resource Tracker"
```

#### Method 3: Command Prompt (as Administrator)
```cmd
# Allow inbound traffic on port 5000
netsh advfirewall firewall add rule name="Empyrion Resource Tracker" dir=in action=allow protocol=TCP localport=5000

# List all rules to verify
netsh advfirewall firewall show rule name="Empyrion Resource Tracker"
```

## 📱 Mobile Access

After opening the firewall port:

1. **Find your computer's IP address:**
   - Linux: `ip addr show` or `hostname -I`
   - Windows: `ipconfig` (look for IPv4 Address)

2. **Access from phone/tablet:**
   - Connect to the same WiFi network
   - Open browser and go to `http://YOUR_IP_ADDRESS:5000`
   - Example: `http://192.168.1.100:5000`

## 🎯 Usage Guide

### Adding Locations

1. Click **"+ Add Location"** to create a new entry
2. Click on any field to edit directly
3. Use dropdowns for Type (Sector/Planet/Moon) and Danger Level
4. Add resources by clicking **"+ Add"** in the Resources column
5. Changes are saved automatically

### Resource Management

- **Add resources:** Click the **"+ Add"** button in any Resources cell
- **Remove resources:** Click the **"×"** on any resource tag
- **Multiple resources:** Each location can have unlimited resources

### Filtering

Use the filter controls at the top to find specific locations:

- **Name:** Search system or sector names
- **Type:** Filter by Sector, Planet, or Moon
- **Danger:** Filter by Low, Medium, or High danger levels
- **Resource:** Find all locations containing specific resources

### Distance Tracking

- Set your reference point in **"Distance from"** field
- Enter distances manually in the Distance column
- All distances are relative to your chosen reference point

### Exporting Data

- Click **"📥 Export CSV"** to download all locations
- Share the CSV file with your server community
- Import the CSV data into other tools if needed

## 🗃️ Database

- Uses SQLite database (`empyrion_resources.db`)
- Created automatically in the same directory as the script
- Lightweight and portable
- No external database server required

### Backup Your Data

```bash
# Simply copy the database file
cp empyrion_resources.db empyrion_resources_backup.db
```

## 🔧 Troubleshooting

### Can't Access from Other Devices

1. **Check firewall:** Ensure port 5000 is open (see instructions above)
2. **Check IP address:** Make sure you're using the correct IP
3. **Same network:** Ensure all devices are on the same WiFi/network
4. **Antivirus:** Some antivirus software may block the connection

### Application Won't Start

1. **Check Python version:** Requires Python 3.7+
   ```bash
   python --version
   ```

2. **Install Flask:**
   ```bash
   pip install flask
   ```

3. **Check port availability:**
   ```bash
   # Linux/Mac
   netstat -tuln | grep 5000
   
   # Windows
   netstat -an | findstr 5000
   ```

### Database Issues

If you encounter database errors:

```bash
# Delete the database file to start fresh
rm empyrion_resources.db

# Restart the application
python empyrion_tracker.py
```

## 🚀 Advanced Usage

### Custom Port

To run on a different port, modify the last line in `empyrion_tracker.py`:

```python
app.run(host='0.0.0.0', port=8080, debug=False)  # Change 5000 to 8080
```

### Running as a Service

For permanent deployment, consider running as a system service:

#### Linux (systemd)

Create `/etc/systemd/system/empyrion-tracker.service`:

```ini
[Unit]
Description=Empyrion Resource Tracker
After=network.target

[Service]
Type=simple
User=your-username
WorkingDirectory=/path/to/your/tracker
ExecStart=/usr/bin/python3 empyrion_tracker.py
Restart=always

[Install]
WantedBy=multi-user.target
```

```bash
sudo systemctl enable empyrion-tracker
sudo systemctl start empyrion-tracker
```

## 🤝 Contributing

Found a bug or want to suggest a feature? Please create an issue or submit a pull request!

## 📄 License

This project is open source and available under the [MIT License](LICENSE).

## 🎮 About Empyrion

[Empyrion - Galactic Survival](https://empyriongame.com/) is a 3D open world space sandbox survival adventure that combines space and planet exploration, building, crafting, combat and survival.

---

**Happy Mining! 🛠️⛏️**

*Track your resources, share with your community, and never lose a good mining spot again!*
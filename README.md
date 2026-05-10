# AiQ Phoenix Tech - Resilient IT Management Suite

A comprehensive, multi-tabbed IT management application built with the Phoenix vision: never backs down, self-healing, and resilient. Built using Windows-native tools to maintain a zero-dollar budget while being powerful enough for enterprises yet simple enough for novice users.

## 🔥 Phoenix Vision

The Phoenix doesn't back down and doesn't take no lightly. If a path is missing, it builds it. If a file is missing, it replaces it. It has backup processes for backup processes. This application embodies that spirit with:

- **Self-healing capabilities** - Automatic recovery and resilience
- **Zero-budget approach** - Uses built-in Windows tools (robocopy, sfc, DISM, chkdsk, etc.)
- **Enterprise-grade power** - Robust enough for corporate environments
- **Novice-friendly UX** - Simple, intuitive interface with dropdown selections

## 🎨 Design Theme

**Phoenix Command**: Dark blue background with fiery reds, oranges, and yellows
- Professional, high-contrast, resilient aesthetic
- Tactical command center feel
- White tab navigation that turns black when active

## ✨ Features

### 1. **Dashboard**
- Real-time system health monitoring
- CPU, Memory, and Disk usage metrics
- Recent backup and maintenance job history
- Network device overview
- Quick status indicators
- **Quick Actions Widget** - One-click maintenance shortcuts:
  - System File Check (SFC)
  - Network Scan
  - DISM Health Check

### 2. **Backup & Recovery**
- Robocopy-based backup with safety flags
- Incremental and full backup modes
- Encryption support for sensitive data
- External drive support with auto-mount/unmount (GUID-based)
- Source size vs. destination size checking
- Automatic deletion of oldest backups when space is limited
- Email notifications for backup completion
- Task scheduler integration for automated backups
- Terminal-style log viewer

### 3. **System Maintenance & Repair**
Automated maintenance tasks including:
- **SFC (System File Checker)** - Scan and repair Windows system files
- **DISM Commands** - Check, scan, and restore Windows image health
- **CHKDSK** - Check and repair disk errors
- **Defrag/TRIM** - Smart logic to detect HDD vs SSD and run appropriate commands
- **Windows Updates** - Automated update checking and installation
- **Device Manager Conflict Resolution** - Detect and resolve driver conflicts
- **Antivirus Detection** - Smart detection of installed antivirus (Windows Defender or third-party)
- **Memory Checks** - System memory diagnostics
- **Safe Stop Feature** - Gracefully stop maintenance tasks (lets current scan finish before stopping safely)
- **Running Task Indicator** - Visual alerts showing active maintenance operations
- Email summaries of PC health after scans

### 4. **Remote Access Management**
- RDP-based host and agent setup
- Configuration guides for Windows Remote Desktop
- Session management
- Host and agent installer generation

### 5. **Network Dashboard**
- Active remote session monitoring
- Geo-location tracking of connections (using free IP-API)
- Unauthorized access detection
- Real-time session status
- Security alerts

### 6. **Network Mapping**
- Network device discovery
- IP address scanning (ARP-based on Windows)
- Device information collection (hostname, MAC address, type)
- Geographic location data for devices
- Visual device grid layout

### 7. **Settings**
- **Email Configuration** with 20+ provider support:
  - Gmail, Outlook, Yahoo, AOL, iCloud, Zoho, GMX, Mail.com, FastMail
  - ProtonMail, Yandex, Tutanota, Mailgun, SendGrid, Mailchimp
  - Amazon SES, SparkPost, Mailjet, Postmark
  - Custom SMTP server option
- **App Password Support** - Works with both regular passwords and app passwords
- **Notification Toggles** - Email alerts for each tool
- **Config Export/Import** - Settings saved to config.json
- **Task Scheduler Integration** - Schedule all automated tasks

## 🛠️ Technology Stack

### Backend
- **FastAPI** - High-performance Python API framework
- **MongoDB** - Document database for storing configurations and logs
- **Motor** - Async MongoDB driver
- **aiosmtplib** - Async email sending
- **psutil** - System information and monitoring
- **subprocess** - Windows command execution

### Frontend
- **React 19** - Modern UI library
- **Framer Motion** - Smooth animations and transitions
- **Tailwind CSS** - Utility-first styling with custom Phoenix theme
- **Shadcn/UI** - Beautiful, accessible components
- **Lucide React** - Icon library
- **Sonner** - Toast notifications
- **Axios** - HTTP client

### Design System
- **Typography**: Rajdhani (headings), Manrope (body), JetBrains Mono (code/logs)
- **Colors**: Deep space backgrounds (#020617, #0f172a) with orange-to-red gradients
- **Components**: Pill-shaped buttons, glassmorphism effects, terminal-style log viewers

## 🚀 Installation & Setup

### Prerequisites
- Node.js 16+ and Yarn
- Python 3.11+
- MongoDB
- Windows OS (for full Windows-specific features)

### Backend Setup
```bash
cd /app/backend
pip install -r requirements.txt

# Configure environment variables in .env
MONGO_URL="mongodb://localhost:27017"
DB_NAME="phoenix_tech"
CORS_ORIGINS="*"
```

### Frontend Setup
```bash
cd /app/frontend
yarn install

# Environment is pre-configured in .env
REACT_APP_BACKEND_URL=https://phoenix-it-hub.preview.emergentagent.com
```

### Running the Application
```bash
# Start backend (runs on port 8001)
cd /app/backend
uvicorn server:app --host 0.0.0.0 --port 8001

# Start frontend (runs on port 3000)
cd /app/frontend
yarn start
```

## 📋 Configuration

### Email Setup
1. Navigate to **Settings** tab
2. Select your email provider from the dropdown (or choose "Custom SMTP Server")
3. Enter your email address
4. For Gmail users:
   - Go to Google Account → Security → 2-Step Verification → App Passwords
   - Generate an app password and use it in the password field
5. Toggle notification preferences for each tool
6. Click "Save All Settings"

### Backup Configuration
1. Go to **Backup & Recovery** tab
2. Fill in:
   - Backup name
   - Source path (e.g., `C:\Important Data`)
   - Destination path (e.g., `D:\Backups`)
   - Backup type (Incremental or Full)
   - Enable encryption (optional)
   - Enable email notifications (optional)
3. Click "Save Configuration"
4. Use "Run" button to execute backup manually
5. Configure scheduling in Task Scheduler integration

### Remote Access Setup
1. **On Host Machine** (machine you want to access):
   - Open System Properties → Remote tab
   - Enable "Allow remote connections to this computer"
   - Add users to "Remote Desktop Users" group
   - Ensure firewall port 3389 is open

2. **On Client Machine** (machine you're accessing from):
   - Use Windows built-in Remote Desktop Connection (mstsc.exe)
   - Or download the Phoenix Tech agent
   - Enter host IP address or hostname
   - Authenticate with user credentials

## 🎯 Windows Commands Reference

### Backup Commands
```bash
# Incremental backup
robocopy "C:\Source" "D:\Backup" /E /XO /XJ /R:3 /W:5 /MT:8

# Full backup (mirror)
robocopy "C:\Source" "D:\Backup" /MIR /XJ /R:3 /W:5 /MT:8
```

### Maintenance Commands
```bash
# System File Checker
sfc /scannow

# DISM commands
DISM /Online /Cleanup-Image /CheckHealth
DISM /Online /Cleanup-Image /ScanHealth
DISM /Online /Cleanup-Image /RestoreHealth

# Disk check
chkdsk C: /F

# Defrag (HDD)
defrag C: /O

# TRIM (SSD)
defrag C: /L

# Windows Update
powershell -Command "Get-WindowsUpdate -Install -AcceptAll"
```

### Network Commands
```bash
# List network devices
arp -a

# Active sessions
query session

# Network statistics
netstat -an
```

## 📊 API Endpoints

### System
- `GET /api/` - API status
- `GET /api/system/info` - System information (CPU, memory, disk, platform)

### Settings
- `GET /api/settings` - Get current settings
- `POST /api/settings` - Save settings

### Backup
- `POST /api/backup/config` - Create backup configuration
- `GET /api/backup/config` - Get all backup configurations
- `POST /api/backup/run/{config_id}` - Run backup job
- `GET /api/backup/jobs` - Get backup job history

### Maintenance
- `POST /api/maintenance/run/{job_type}` - Run maintenance task
- `POST /api/maintenance/stop/{job_id}` - Safely stop running maintenance task
- `GET /api/maintenance/jobs` - Get maintenance job history
- `GET /api/maintenance/running` - Get currently running maintenance tasks

### Network
- `GET /api/network/scan` - Scan network for devices
- `GET /api/network/devices` - Get discovered devices
- `GET /api/remote/sessions` - Get active remote sessions

## 🔒 Security Features

- **Encryption Support** - Optional encryption for sensitive backups
- **App Password Support** - Secure email authentication
- **Geo-location Monitoring** - Track connection origins
- **Unauthorized Access Detection** - Alert on suspicious sessions
- **Secure RDP Configuration** - Best practices for remote access
- **Environment Variables** - No hardcoded credentials

## 🐛 Troubleshooting

### Windows Commands Not Available
If you see "simulated" status for jobs, the application is running on a non-Windows system. The commands will work properly when deployed on Windows.

### Email Not Sending
1. Verify email credentials are correct
2. For Gmail: Use App Password, not regular password
3. Check SMTP port (usually 587 for TLS)
4. Ensure firewall allows outbound SMTP connections

### Backup Fails
1. Verify source and destination paths exist
2. Ensure you have write permissions
3. Check disk space on destination
4. Run the application with administrator privileges

### Network Scan Returns No Devices
1. Ensure ARP cache is populated (ping devices first)
2. Run with administrator privileges
3. Check network connectivity
4. Verify firewall isn't blocking network discovery

## 📝 Notes

- **Windows-Specific Features**: Full functionality requires Windows OS with administrator privileges
- **Task Scheduler**: Automated scheduling requires Windows Task Scheduler integration
- **Drive Mounting**: External drive GUID mounting requires Windows diskpart
- **Antivirus Detection**: Smart logic detects Windows Defender or third-party antivirus
- **HDD vs SSD Detection**: Automatically runs appropriate optimization commands

## 🎨 Design Credits

- **Fonts**: Google Fonts (Rajdhani, Manrope, JetBrains Mono)
- **Icons**: Lucide React
- **UI Components**: Shadcn/UI
- **Animations**: Framer Motion

## 📄 License

Built for AiQ - Phoenix Tech. All rights reserved.

---

**Remember**: The Phoenix never backs down. This application embodies resilience, self-healing, and determination. Built strong for enterprises, simple for everyone.

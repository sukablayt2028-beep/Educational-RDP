  # 🖥️ GitHub Actions RDP via Tailscale

> **⚠️ IMPORTANT WARNING:** This project uses GitHub Actions runners in ways not intended by GitHub. Use at your own risk. Your account may be suspended or banned.

![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-2088FF?style=for-the-badge&logo=github-actions&logoColor=white)
![Ubuntu](https://img.shields.io/badge/Ubuntu-E95420?style=for-the-badge&logo=ubuntu&logoColor=white)
![Tailscale](https://img.shields.io/badge/Tailscale-000000?style=for-the-badge&logo=tailscale&logoColor=white)

A workflow that creates a temporary Ubuntu desktop environment with RDP access via Tailscale VPN.

---

## 📋 Table of Contents

- [⚠️ Warnings & Disclaimers](#️-warnings--disclaimers)
- [✨ Features](#-features)
- [🚀 Quick Start](#-quick-start)
- [📱 Device Setup Guides](#-device-setup-guides)
- [⚙️ Configuration Options](#️-configuration-options)
- [🐛 Troubleshooting](#-troubleshooting)
- [✅ Alternatives (Recommended)](#-alternatives-recommended)

---

## ⚠️ Warnings & Disclaimers

### **🚨 THIS VIOLATES GITHUB'S TERMS OF SERVICE**

Using GitHub Actions runners as personal VMs is **prohibited** and can result in:

- ❌ **Account suspension**
- ❌ **Permanent ban from GitHub**
- ❌ **Loss of access to all repositories**
- ❌ **No refunds for paid plans**

### **What to AVOID:**

| ❌ DON'T | ✅ DO INSTEAD |
|---------|--------------|
| Use for cryptocurrency mining | Use proper cloud VMs |
| Host websites/services | Use GitHub Pages, Vercel, Netlify |
| Run 24/7 long-term | Use Oracle Cloud Free Tier |
| Store important data | Use GitHub Repositories |
| Use for production work | Use AWS/Azure/GCP |

### **Limitations:**

- ⏱️ **6-hour maximum runtime** (then auto-terminated)
- 💾 **No data persistence** (everything deleted after workflow ends)
- 🐌 **Limited resources** (2 CPU cores, 7GB RAM)
- 🌐 **Shared network** (slower performance)
- 👁️ **Actively monitored** (GitHub detects abuse patterns)

---

## ✨ Features

- 🖥️ **Ubuntu Desktop Environment** (LXDE - lightweight)
- 🔐 **Secure RDP Access** via Tailscale VPN
- 📱 **Cross-platform** (Windows, macOS, Linux, iOS, Android)
- ⚡ **Performance optimized** for low-resource usage
- 🔄 **On-demand deployment** (manual workflow trigger)

---

## 🚀 Quick Start

### **Prerequisites:**

1. GitHub account
2. Tailscale account (free at [tailscale.com](https://tailscale.com))
3. RDP client on your device

### **Step 1: Fork This Repository**

Click the "Fork" button at the top right of this page.

### **Step 2: Get Tailscale Auth Key**

1. Go to https://login.tailscale.com/admin/settings/keys
2. Click **"Generate auth key"**
3. Settings:
   - ✅ **Reusable** (optional - allows multiple uses)
   - ✅ **Ephemeral** (recommended - auto-removes device when offline)
   - Expiration: 90 days (or custom)
4. Copy the key (starts with `tskey-auth-...`)

### **Step 3: Add Secret to GitHub**

1. In your forked repository, go to **Settings** → **Secrets and variables** → **Actions**
2. Click **"New repository secret"**
3. Name: `TAILSCALE_AUTH_KEY`
4. Value: Paste your Tailscale auth key
5. Click **"Add secret"**

### **Step 4: Run the Workflow**

1. Go to **Actions** tab
2. Click **"Fast RDP Setup"** workflow
3. Click **"Run workflow"** button
4. Select branch: `main`
5. Click green **"Run workflow"** button

### **Step 5: Get Connection Details**

1. Wait ~2-3 minutes for setup
2. Click on the running workflow
3. Click **"setup-rdp"** job
4. Expand **"Display Info"** step
5. Copy the **Tailscale IP address** (format: `100.x.x.x`)

### **Step 6: Connect**

See [Device Setup Guides](#-device-setup-guides) below for your device.

---

## 📱 Device Setup Guides

### 🪟 **Windows**

#### **Method 1: Built-in Remote Desktop**

1. Press `Win + R`
2. Type: `mstsc` and press Enter
3. Computer: `100.x.x.x` (your Tailscale IP)
4. Click **"Connect"**
5. Login:
   - Username: `runner`
   - Password: `Pass123`

#### **Method 2: Tailscale App (Easier)**

1. Download Tailscale: https://tailscale.com/download/windows
2. Install and sign in
3. Follow Method 1 above

---

### 🍎 **macOS**

1. **Install Tailscale:**
   - Download: https://tailscale.com/download/mac
   - Install and sign in

2. **Install Microsoft Remote Desktop:**
   - App Store: https://apps.apple.com/app/microsoft-remote-desktop/id1295203466
   - Or download directly from Microsoft

3. **Connect:**
   - Open Microsoft Remote Desktop
   - Click **"+ Add PC"**
   - PC name: `100.x.x.x` (Tailscale IP)
   - User account:
     - Username: `runner`
     - Password: `Pass123`
   - Click **"Add"**
   - Double-click to connect

---

### 🐧 **Linux**

#### **Ubuntu/Debian:**

```bash
# Install Tailscale
curl -fsSL https://tailscale.com/install.sh | sh
sudo tailscale up

# Install RDP client
sudo apt install remmina

# Connect
remmina
# Server: 100.x.x.x
# Username: runner
# Password: Pass123
```

#### **Fedora/RHEL:**

```bash
# Install Tailscale
sudo dnf install -y tailscale
sudo systemctl enable --now tailscaled
sudo tailscale up

# Install RDP client
sudo dnf install remmina

# Connect via Remmina GUI
```

#### **Command-line (any distro):**

```bash
xfreerdp /v:100.x.x.x /u:runner /p:Pass123 /w:1920 /h:1080
```

---

### 📱 **iOS (iPhone/iPad)**

1. **Install Tailscale:**
   - App Store: https://apps.apple.com/app/tailscale/id1470499037
   - Open and sign in

2. **Install Microsoft Remote Desktop:**
   - App Store: https://apps.apple.com/app/microsoft-remote-desktop/id714464092

3. **Setup Connection:**
   ```
   Open Microsoft Remote Desktop
   → Tap "+" (top right)
   → "Add PC"
   → PC name: 100.x.x.x
   → User account: "Add User Account"
      Username: runner
      Password: Pass123
   → Friendly name: GitHub Ubuntu (optional)
   → Save
   ```

4. **Connect:**
   - Tap the saved connection
   - Accept certificate warning

#### **Performance Settings (iOS):**

1. Tap **"..."** on connection → **Edit**
2. **Display:**
   - Resolution: `1280x720` (faster) or `1920x1080` (sharper)
   - Color depth: `High Color (16-bit)` for speed
3. **Session:**
   - Disable **"Play sound on remote PC"**
4. **Save**

---

### 🤖 **Android**

1. **Install Tailscale:**
   - Google Play: https://play.google.com/store/apps/details?id=com.tailscale.ipn
   - Sign in and connect

2. **Install Microsoft Remote Desktop:**
   - Google Play: https://play.google.com/store/apps/details?id=com.microsoft.rdc.androidx

3. **Setup:**
   ```
   Open Microsoft Remote Desktop
   → Tap "+"
   → Desktop
   → PC name: 100.x.x.x
   → User name: runner
   → Password: Pass123
   → Friendly name: GitHub Ubuntu
   → Save
   ```

4. **Connect:**
   - Tap the connection
   - Accept certificate

---

### 🌐 **Web Browser (Any Device)**

**Note:** Requires NoMachine variant (see Configuration Options)

1. Install Tailscale on your device
2. Access via browser: `http://100.x.x.x:4000`
3. Login with credentials

---

## ⚙️ Configuration Options

### **Change Desktop Environment**

Edit `.github/workflows/rdp-setup.yml`:

```yaml
# Ultra-lightweight (recommended)
sudo apt install -y lxde-core xrdp

# Balanced (moderate resources)
sudo apt install -y xfce4 xfce4-terminal xrdp

# Feature-rich (heavy)
sudo apt install -y ubuntu-desktop xrdp
```

### **Change Password**

```yaml
- name: Configure RDP
  run: |
    echo "runner:YourNewPassword" | sudo chpasswd
```

### **Increase Runtime**

```yaml
jobs:
  setup-rdp:
    timeout-minutes: 360  # Change to 60-360 (max 6 hours)
```

### **Use NoMachine (Better Performance)**

Replace RDP setup with:

```yaml
- name: Install NoMachine
  run: |
    wget https://download.nomachine.com/download/8.11/Linux/nomachine_8.11.3_4_amd64.deb
    sudo dpkg -i nomachine_8.11.3_4_amd64.deb
```

Download NoMachine client:
- iOS: https://apps.apple.com/app/nomachine/id668068562
- Android: https://play.google.com/store/apps/details?id=com.nomachine.nxandroid
- Windows/Mac/Linux: https://www.nomachine.com/download

---

## 🐛 Troubleshooting

### **Problem: "Cannot connect to PC"**

**Solution:**
1. Verify Tailscale is running on both devices:
   ```bash
   tailscale status
   ```
2. Check the IP is correct in workflow logs
3. Ensure workflow is still running (< 6 hours)

---

### **Problem: "Connection refused"**

**Solution:**
```bash
# In GitHub Actions logs, check:
sudo systemctl status xrdp

# Manually restart (add to workflow):
sudo systemctl restart xrdp
```

---

### **Problem: Black screen after login**

**Solution:**

Add to workflow before starting xrdp:

```yaml
- name: Fix black screen
  run: |
    echo "startlxde" > ~/.xsession
    sudo systemctl restart xrdp
```

---

### **Problem: Very slow performance**

**Solutions:**

1. **Lower resolution** in RDP client (1280x720)
2. **Use LXDE** instead of XFCE/GNOME
3. **Switch to NoMachine** instead of RDP
4. **Check Tailscale connection type:**
   ```bash
   tailscale status
   # Look for "direct" instead of "relay"
   ```

---

### **Problem: Workflow stops after 6 hours**

**Solution:**

This is GitHub's hard limit. Options:
- Re-run the workflow manually
- Use a proper VPS (see Alternatives below)

---

### **Problem: Account suspended**

**Solution:**

None. GitHub bans are typically permanent for Terms of Service violations.

**Prevention:** Use legal alternatives from the start.

---

## ✅ Alternatives (Recommended)

### **🏆 Oracle Cloud (Best Free Option)**

**What you get:**
- ✅ 4 ARM cores or 2 AMD cores
- ✅ 24GB RAM
- ✅ 200GB storage
- ✅ 10TB bandwidth/month
- ✅ **FREE FOREVER**
- ✅ No time limits
- ✅ Root access

**Setup:**

1. **Sign up:** https://oracle.com/cloud/free
2. **Create VM:** 
   - Compute → Instances → Create Instance
   - Image: Ubuntu 22.04
   - Shape: Ampere (ARM) - 4 cores, 24GB RAM
3. **SSH in:**
   ```bash
   ssh ubuntu@<instance-ip>
   ```
4. **Install desktop:**
   ```bash
   sudo apt update
   sudo apt install -y lxde-core xrdp
   sudo systemctl enable xrdp
   echo "ubuntu:yourpassword" | sudo chpasswd
   ```
5. **Install Tailscale:**
   ```bash
   curl -fsSL https://tailscale.com/install.sh | sh
   sudo tailscale up
   ```
6. **Connect via RDP** using Tailscale IP

---

### **☁️ Other Cloud Providers**

| Provider | Free Tier | Best For |
|----------|-----------|----------|
| **AWS EC2** | 12 months | Enterprise/Learning |
| **Azure VM** | $200 credit | Windows apps |
| **Google Cloud** | $300 credit | Big data/ML |
| **DigitalOcean** | $200 credit | Simplicity |
| **Linode** | $100 credit | Performance |

---

### **🏠 Self-Hosted GitHub Runner**

**Legal way to use GitHub Actions with your own VM:**

1. Create a VPS (Oracle, AWS, etc.)
2. Install GitHub self-hosted runner:
   ```bash
   # On your VPS:
   mkdir actions-runner && cd actions-runner
   curl -o actions-runner-linux-x64-2.311.0.tar.gz -L \
     https://github.com/actions/runner/releases/download/v2.311.0/actions-runner-linux-x64-2.311.0.tar.gz
   tar xzf ./actions-runner-linux-x64-2.311.0.tar.gz
   ./config.sh --url https://github.com/YOUR_USERNAME/YOUR_REPO --token YOUR_TOKEN
   sudo ./svc.sh install
   sudo ./svc.sh start
   ```
3. Install RDP + Tailscale on the same VPS
4. Use workflows to control your own machine

---

### **💻 GitHub Codespaces (For Development)**

**What it is:**
- Cloud-based VS Code environment
- 60 hours/month free
- 2-4 cores, 8-16GB RAM

**When to use:**
- Software development
- Learning to code
- Testing applications
- Short-term projects

**Setup:**
1. Go to your repository
2. Click **"Code"** → **"Codespaces"** → **"New codespace"**
3. Use browser-based VS Code

---

## 📊 Comparison Table

| Solution | Cost | Performance | Persistence | Legal | Time Limit |
|----------|------|-------------|-------------|-------|------------|
| **GitHub Actions** | Free | ⭐⭐ | ❌ | ❌ | 6 hours |
| **Oracle Cloud** | Free | ⭐⭐⭐⭐⭐ | ✅ | ✅ | None |
| **AWS Free Tier** | Free (12mo) | ⭐⭐⭐⭐ | ✅ | ✅ | None |
| **DigitalOcean** | $4/mo | ⭐⭐⭐⭐ | ✅ | ✅ | None |
| **Codespaces** | Free (60h) | ⭐⭐⭐⭐ | ✅ | ✅ | 60h/mo |

---

## 📚 Additional Resources

### **Tailscale Documentation:**
- Getting Started: https://tailscale.com/kb/1017/install/
- iOS Setup: https://tailscale.com/kb/1020/install-ios/
- Android Setup: https://tailscale.com/kb/1021/install-android/

### **RDP Clients:**
- Microsoft Remote Desktop (iOS): https://apps.apple.com/app/microsoft-remote-desktop/id714464092
- Microsoft Remote Desktop (Android): https://play.google.com/store/apps/details?id=com.microsoft.rdc.androidx
- Remmina (Linux): https://remmina.org/
- NoMachine: https://www.nomachine.com/

### **Desktop Environments:**
- LXDE: https://www.lxde.org/
- XFCE: https://www.xfce.org/
- Ubuntu Desktop: https://ubuntu.com/desktop

---

## 🤝 Contributing

This is an educational project. Contributions welcome:

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Submit a pull request

---

## 📜 License

MIT License - see [LICENSE](LICENSE) file for details.

---

## ⚖️ Legal Disclaimer

This project is provided for **educational purposes only**. 

- The maintainers are not responsible for any account suspensions, bans, or other consequences resulting from use of this software
- Users are solely responsible for compliance with GitHub's Terms of Service
- We strongly recommend using legitimate cloud VPS providers instead

**USE AT YOUR OWN RISK.**

---

## 💬 Support

- **Issues:** Open an issue in this repository
- **Discussions:** Use GitHub Discussions tab
- **Not for:** Getting unbanned from GitHub (we can't help with that)

---

## 🙏 Acknowledgments

- [GitHub Actions](https://github.com/features/actions)
- [Tailscale](https://tailscale.com/)
- [LXDE Team](https://www.lxde.org/)
- [xrdp Project](http://xrdp.org/)

---

<div align="center">

### ⚠️ Remember: Use legitimate cloud providers for real work ⚠️

**Recommended:** [Oracle Cloud Free Tier](https://oracle.com/cloud/free) | [AWS](https://aws.amazon.com/free/) | [Azure](https://azure.microsoft.com/free/)

---

**Made with ⚡ and ⚠️ warnings**

</div>

---

## 📝 Quick Reference Card

```
┌─────────────────────────────────────────┐
│  CONNECTION DETAILS                     │
├─────────────────────────────────────────┤
│  IP Address: 100.x.x.x (from workflow) │
│  Username:   runner                     │
│  Password:   Pass123                    │
│  Protocol:   RDP (port 3389)            │
│  Desktop:    LXDE                       │
│  Max Time:   6 hours                    │
└─────────────────────────────────────────┘

┌─────────────────────────────────────────┐
│  QUICK COMMANDS                         │
├─────────────────────────────────────────┤
│  Windows:    mstsc                      │
│  macOS:      Microsoft Remote Desktop   │
│  Linux:      remmina                    │
│  iOS:        MS Remote Desktop App      │
│  Android:    MS Remote Desktop App      │
└─────────────────────────────────────────┘
```

# 🔧 Troubleshooting Guide

Solutions to common problems.

## Table of Contents

1. [Connection Issues](#connection-issues)
2. [Performance Issues](#performance-issues)
3. [Control Issues](#control-issues)
4. [Windows/Security Issues](#windows-security-issues)
5. [Build Issues](#build-issues)

---

## Connection Issues

### Desktop Client Won't Connect

**Symptoms:**
- "Connection failed" error
- Can't reach server
- Timeout errors

**Solutions:**

1. **Check Internet Connection**

Test connection
ping google.com

2. **Verify Server URL**
- Open `desktop_client.py`
- Check `SERVER_URL` is correct
- Should be `https://your-app.up.railway.app`

3. **Check Railway Server**
- Visit server URL in browser
- Should show landing page
- If not, check Railway dashboard for errors

4. **Firewall/Antivirus**
- Temporarily disable to test
- Add exception for `system32.exe`
- Allow outbound connections on port 443

5. **Try Different Network**
- Test on mobile hotspot
- Some corporate networks block WebSocket

---

### Viewer Can't Connect

**Symptoms:**
- "Waiting for screen share..." forever
- Connection timeout
- Blank screen

**Solutions:**

1. **Check Link**
- Link should be complete (not truncated)
- Format: `https://server.com/view/1234567890`

2. **Check Room Still Active**
- Host must be connected first
- Host must click "Start Sharing"
- Room expires when host disconnects

3. **Browser Issues**
- Try different browser (Chrome recommended)
- Clear cache and cookies
- Disable browser extensions
- Allow JavaScript

4. **Network Issues**
- Check firewall settings
- Try incognito/private mode
- Test on different network

---

### Connection Keeps Dropping

**Symptoms:**
- Frequent disconnects
- "Reconnecting..." messages
- Choppy experience

**Solutions:**

1. **Increase Timeout Values**
Edit `app.py`:

ping_timeout=180, # Increase from 120
ping_interval=20, # Decrease from 25

2. **Check Network Stability**
Test for packet loss
ping -t railway-server.com

3. **Reduce Bandwidth Usage**
- Lower FPS
- Reduce resolution
- Lower JPEG quality

4. **Use Wired Connection**
- WiFi can be unstable
- Ethernet is more reliable

---

## Performance Issues

### Laggy/Slow Screen Updates

**Symptoms:**
- Delayed screen updates
- Low FPS
- Stuttering

**Solutions:**

1. **Reduce Quality Settings**

SCREEN_WIDTH = 854
SCREEN_HEIGHT = 480
JPEG_QUALITY = 35
FPS = 30


2. **Check CPU Usage**
- Close unnecessary programs
- Check Task Manager
- Should be < 60% CPU

3. **Network Speed**
- Test: https://speedtest.net
- Need 5+ Mbps both upload/download
- Reduce quality if slower

4. **Close Background Apps**
- Discord, Zoom, etc. use bandwidth
- Cloud sync (Dropbox, OneDrive)
- Windows Update

---

### High CPU Usage

**Symptoms:**
- Computer slows down
- Fan spinning loudly
- >80% CPU usage

**Solutions:**

1. **Lower FPS**
FPS = 24 # Instead of 45 or 60

2. **Reduce Resolution**
SCREEN_WIDTH = 640
SCREEN_HEIGHT = 360


3. **Lower JPEG Quality**
JPEG_QUALITY = 30


4. **Check for Other Issues**
- Malware scan
- Windows Update running?
- Other heavy programs?

---

### Blurry/Low Quality Screen

**Symptoms:**
- Can't read text
- Images look pixelated
- Poor quality

**Solutions:**

1. **Increase Quality**
SCREEN_WIDTH = 1280
SCREEN_HEIGHT = 720
JPEG_QUALITY = 70

2. **Check Network Speed**
- Quality auto-adjusts to bandwidth
- Need 5+ Mbps for HD quality

3. **Viewer Screen Size**
- View in fullscreen
- Use larger monitor
- Zoom browser (Ctrl + Plus)

---

## Control Issues

### Mouse Not Moving

**Symptoms:**
- Mouse clicks work but movement doesn't
- Cursor doesn't follow viewer's mouse

**Solutions:**

1. **Run as Administrator**
- Right-click `system32.exe`
- "Run as administrator"
- Required for mouse control

2. **Check UAC Settings**
- Lower UAC level in Control Panel
- Or run as admin (see above)

3. **Check Event Handlers**
- Events should show in console (if enabled)
- If not, server not forwarding correctly

---

### Keyboard Not Working

**Symptoms:**
- Can't type
- Keys don't register
- Some keys work, others don't

**Solutions:**

1. **Run as Administrator**
- Required for keyboard control
- Right-click → Run as admin

2. **Check Blocked Keys**
- Ctrl, Alt, Win are blocked by default
- This is intentional (security)

3. **Special Characters**
- Some special chars may not work
- Use on-screen keyboard as workaround

---

### Click Not Registering

**Symptoms:**
- Clicks don't work
- Have to click multiple times

**Solutions:**

1. **Network Delay**
- Wait for screen to update
- Don't spam click
- Reduce FPS if severe

2. **Run as Administrator**
- Required for full control

3. **Double-Click Timing**
- System double-click speed setting
- Adjust in Windows mouse settings

---

## Windows/Security Issues

### Windows Defender Flags Executable

**Symptoms:**
- "Virus detected" warning
- File deleted automatically
- Can't run exe

**Solutions:**

1. **Add Exception**
- Windows Security → Virus & threat protection
- Manage settings → Exclusions
- Add `system32.exe` folder

2. **False Positive**
- This is normal for PyInstaller exes
- Submit to Microsoft for review
- Or build from source yourself

3. **Disable Real-time Protection** (temporary)
- Only while running app
- Re-enable after

---

### "Windows protected your PC" Message

**Symptoms:**
- SmartScreen warning
- "Don't run" recommendation

**Solutions:**

1. **Click "More info"**
2. **Click "Run anyway"**
3. **Or**: Add code signing certificate (for distribution)

---

### Permission Denied Errors

**Symptoms:**
- Can't run executable
- Access denied messages

**Solutions:**

1. **Run as Administrator**
2. **Check File Permissions**
- Right-click → Properties
- Security tab
- Give full control

3. **Antivirus Blocking**
- Add exception
- Temporarily disable

---

## Build Issues

### PyInstaller Fails

**Symptoms:**
- Build errors
- Missing modules
- Import errors

**Solutions:**

1. **Update PyInstaller**
pip install --upgrade pyinstaller

2. **Install Missing Packages**
pip install -r requirements.txt

3. **Clear Cache**
pyinstaller --clean --onefile desktop_client.py


4. **Check Python Version**
python --version # Should be 3.11+

---

### "Module not found" Error

**Symptoms:**
- ImportError when running
- Missing dependencies

**Solutions:**

1. **Install Requirements**
pip install flask python-socketio mss pillow pyautogui websocket-client


2. **Hidden Imports**
Add to PyInstaller command:

---

### Large EXE Size

**Symptoms:**
- Executable is 50+ MB
- Takes long to build

**Solutions:**

1. **This is Normal**
- PyInstaller bundles Python + libraries
- 40-60 MB is expected

2. **Optimize (Advanced)**
pip install pyinstaller[encryption]
pyinstaller --onefile --strip desktop_client.py

---

## Railway Server Issues

### Deployment Failed

**Symptoms:**
- Build errors in Railway
- Deployment not working

**Solutions:**

1. **Check Logs**
- Railway dashboard → Deployments
- Click failed deployment
- Read error messages

2. **Common Fixes**
- Check `requirements.txt` is correct
- Verify `Procfile` syntax
- Check `runtime.txt` for correct Python version

3. **Redeploy**
- Settings → Restart
- Or push empty commit:
git commit --allow-empty -m "Trigger redeploy"
git push
---

### Server Not Responding

**Symptoms:**
- 503 errors
- Server timeout
- Can't access landing page

**Solutions:**

1. **Check Railway Status**
- Railway dashboard
- Should show "Active"

2. **Check Logs**
- Look for errors
- Python crashes?

3. **Restart Service**
- Settings → Restart

---

## Getting Help

If none of these solutions work:

1. **Check Documentation**
- Re-read [Installation Guide](INSTALLATION.md)
- Review [Configuration Guide](CONFIGURATION.md)

2. **Create GitHub Issue**
- Describe problem clearly
- Include error messages
- Mention your configuration
- Steps to reproduce

3. **Provide Information**
- OS version
- Python version
- Network type (WiFi/Wired)
- Error logs

---

## Useful Commands

### Check Versions

python --version
pip --version
pyinstaller --version

### Check Network

Windows
ping railway-server.com
tracert railway-server.com
ipconfig /all

Check open ports
netstat -an | find "5000"

### Clear Python Cache

Delete pycache
find . -type d -name pycache -exec rm -r {} +

Or manually delete:
- pycache folders
- *.pyc files
- build/ folder
- dist/ folder


---

**Still having issues?** Create an issue on GitHub with detailed information.

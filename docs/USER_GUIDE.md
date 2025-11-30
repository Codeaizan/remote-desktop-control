# 📖 User Guide

Learn how to use Remote Desktop Control effectively.

## Table of Contents

1. [Getting Started](#getting-started)
2. [Host (Sharing Your Screen)](#host-sharing-your-screen)
3. [Viewer (Controlling Remote Screen)](#viewer-controlling-remote-screen)
4. [Features](#features)
5. [Best Practices](#best-practices)

---

## Getting Started

### System Requirements

**Host (Desktop Client)**
- Windows 10/11
- 4GB RAM minimum
- Stable internet connection (2+ Mbps upload)

**Viewer**
- Any device with a web browser
- Stable internet connection (5+ Mbps download recommended)

---

## Host (Sharing Your Screen)

### Starting a Session

1. **Run the Application**
   - Double-click `system32.exe`
   - Or right-click → "Run as administrator" (for better performance)
   - Browser opens automatically with control panel

2. **Start Sharing**
   - Click the green "Start Sharing" button
   - Wait 2-3 seconds for connection
   - Status changes to "🟢 Sharing Active"

3. **Copy the Link**
   - Click "Copy Link" button
   - Share via email, chat, or any messaging app

4. **Share Your Screen**
   - Send the link to viewers
   - They can connect immediately
   - Multiple viewers can join simultaneously

### Stopping a Session

1. Click the red "Stop Sharing" button
2. All viewers will be disconnected
3. Screen sharing stops immediately

### What's Being Shared

- ✅ Primary monitor screen
- ✅ Mouse cursor position
- ✅ All visible windows and applications
- ❌ Audio is NOT shared
- ❌ Other monitors are NOT shared (single monitor only)

---

## Viewer (Controlling Remote Screen)

### Connecting

1. **Open the Link**
   - Click the link shared by the host
   - Opens in your default browser
   - Works on any device (PC, tablet, phone)

2. **Wait for Connection**
   - Status shows "🟢 Connected"
   - Screen appears within 1-2 seconds
   - You'll see the host's screen in real-time

### Controls

#### Mouse Control

- **Move**: Move your mouse over the screen
- **Click**: Left-click anywhere
- **Right-click**: Right-click for context menu
- **Double-click**: Double-click to open items
- **Scroll**: Use mouse wheel to scroll

#### Keyboard Control

- **Type**: Any character keys work normally
- **Special Keys**:
  - Enter, Backspace, Tab
  - Arrow keys (↑ ↓ ← →)
  - Delete, Home, End
  - Page Up, Page Down
  - Escape

#### Blocked Keys (Security)

These keys are **blocked** for security:
- ❌ Ctrl key combinations
- ❌ Alt key combinations
- ❌ Windows key
- ❌ System shortcuts

### Screen Quality

The screen updates in real-time:
- **Fast mode**: 30-60 FPS, lower quality
- **Quality mode**: 24-30 FPS, higher quality
- Automatic adjustment based on connection speed

---

## Features

### Real-time Streaming

- Low latency (< 100ms typically)
- Smooth mouse movement
- Instant keyboard input
- Adaptive quality based on network

### Auto-reconnect

- Automatically reconnects if connection drops
- Resumes where you left off
- No need to restart

### Security

- Unique room IDs per session
- Encrypted connection (HTTPS)
- No data stored after session ends
- System keys blocked for safety

---

## Best Practices

### For Hosts

1. **Network**
   - Use wired connection if possible
   - Minimum 2 Mbps upload speed
   - Close bandwidth-heavy apps

2. **Privacy**
   - Close sensitive documents before sharing
   - Be aware viewers see everything on your screen
   - Only share links with trusted people

3. **Performance**
   - Close unnecessary programs
   - Don't run heavy applications during sharing
   - Monitor CPU usage

### For Viewers

1. **Network**
   - Stable 5+ Mbps connection recommended
   - WiFi is fine for viewing
   - Close other bandwidth-heavy apps

2. **Browser**
   - Use latest Chrome, Firefox, or Edge
   - Enable JavaScript
   - Allow pop-ups if needed

3. **Controls**
   - Be gentle with clicks (avoid spam clicking)
   - Wait for screen updates before clicking again
   - Use keyboard shortcuts when possible

---

## Common Workflows

### Remote Tech Support

1. Host shares screen
2. Viewer diagnoses issue
3. Viewer takes control to fix
4. Host observes the fix
5. Session ends when complete

### Remote Presentation

1. Host shares presentation screen
2. Viewers watch in real-time
3. Host maintains control
4. Viewers can ask to control if needed

### Remote Work

1. Access work computer from home
2. Work normally through viewer
3. Save work on remote computer
4. Disconnect when done

---

## Keyboard Shortcuts

### Host (Control Panel)

- No special shortcuts (use buttons)

### Viewer

- **Esc**: Attempt to close dialogs on host
- **Tab**: Navigate between fields
- **Enter**: Confirm/Submit on host
- **Backspace**: Delete text on host

---

## Tips & Tricks

1. **Faster Performance**
   - Lower resolution in config
   - Reduce FPS if lagging
   - Use wired internet

2. **Better Quality**
   - Increase resolution in config
   - Increase JPEG quality
   - Ensure good internet speed

3. **Multiple Viewers**
   - All viewers see same screen
   - All can control simultaneously
   - Last input wins (be careful!)

4. **Mobile Viewing**
   - Works on phones/tablets
   - Use landscape mode for better view
   - Touch = mouse click
   - Two-finger scroll = scroll

---

## Limitations

- Single monitor only (primary display)
- No audio streaming
- No file transfer (yet)
- Windows host only (viewer = any OS)
- Maximum 4-5 simultaneous viewers recommended

---

## FAQ

**Q: Can I share specific windows only?**  
A: No, entire primary monitor is shared.

**Q: Can viewers hear audio?**  
A: No, audio is not transmitted.

**Q: How many viewers can join?**  
A: Unlimited technically, but 4-5 recommended for performance.

**Q: Is my data stored?**  
A: No, everything is real-time. Nothing is recorded or stored.

**Q: Can I use on Mac?**  
A: Desktop client is Windows-only. Viewers can use any OS.

---

**Need help?** See [Troubleshooting Guide](TROUBLESHOOTING.md)

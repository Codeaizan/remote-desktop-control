# ⚙️ Configuration Guide

Customize Remote Desktop Control for your specific needs.

## Configuration Options

### Performance Tuning

Edit `desktop_client.py` lines 18-28:

==================== SCREEN SHARING SETTINGS ====================
Resolution - Smaller = Faster, Larger = Better Quality
SCREEN_WIDTH = 854 # Width in pixels
SCREEN_HEIGHT = 480 # Height in pixels

JPEG Quality - Lower = Faster, Higher = Better Quality
JPEG_QUALITY = 35 # Range: 20-95

Frames Per Second - Higher = Smoother
FPS = 45 # Options: 15, 24, 30, 45, 60


---

## Preset Configurations

### 🚀 Maximum Speed (Best for slow internet)

SCREEN_WIDTH = 640
SCREEN_HEIGHT = 360
JPEG_QUALITY = 30
FPS = 60


**Characteristics:**
- Very smooth (60 FPS)
- Lower quality image
- Minimal bandwidth usage
- Good for text/coding

---

### ⚡ Fast & Balanced (Recommended)

SCREEN_WIDTH = 854
SCREEN_HEIGHT = 480
JPEG_QUALITY = 35
FPS = 45


**Characteristics:**
- Smooth performance (45 FPS)
- Decent quality
- Good for most use cases
- Balanced bandwidth usage

---

### 📊 Standard (Default balanced)

SCREEN_WIDTH = 1280
SCREEN_HEIGHT = 720
JPEG_QUALITY = 50
FPS = 30


**Characteristics:**
- HD quality (720p)
- Smooth enough (30 FPS)
- Good for presentations
- Moderate bandwidth

---

### 🎨 High Quality (Best for design work)

SCREEN_WIDTH = 1920
SCREEN_HEIGHT = 1080
JPEG_QUALITY = 80
FPS = 24


**Characteristics:**
- Full HD (1080p)
- Highest quality
- Cinematic framerate (24 FPS)
- High bandwidth required

---

## Advanced Settings

### Scroll Speed

Edit line 264 in `desktop_client.py`:

Current: 3x multiplier
pyautogui.scroll(delta * 3)

Options:
pyautogui.scroll(delta * 1) # Slow, precise
pyautogui.scroll(delta * 3) # Balanced
pyautogui.scroll(delta * 5) # Fast
pyautogui.scroll(delta * 10) # Very fast


---

### Mouse Movement Throttle

Edit `viewer.html` line 90:

// Current: 16ms delay (60 updates/sec)
if (now - lastMouseMove < 16) return;

// Options:
if (now - lastMouseMove < 8) return; // 120 updates/sec (very responsive)
if (now - lastMouseMove < 16) return; // 60 updates/sec (balanced)
if (now - lastMouseMove < 33) return; // 30 updates/sec (saves bandwidth)


---

### Connection Timeouts

Edit `app.py` lines 17-18:

ping_timeout=120, # Time before disconnecting idle client
ping_interval=25, # How often to send keep-alive ping

For unstable connections:
ping_timeout=180, # 3 minutes
ping_interval=20, # Every 20 seconds

For stable connections:
ping_timeout=60, # 1 minute
ping_interval=30, # Every 30 seconds


---

### Buffer Size

Edit `app.py` line 19:

max_http_buffer_size=10000000 # 10MB (default)

For high quality/resolution:
max_http_buffer_size=20000000 # 20MB

For lower quality:
max_http_buffer_size=5000000 # 5MB


---

## Bandwidth Requirements

| Configuration | Upload (Host) | Download (Viewer) |
|---------------|---------------|-------------------|
| Maximum Speed | 1-2 Mbps | 1-2 Mbps |
| Fast & Balanced | 2-3 Mbps | 2-3 Mbps |
| Standard | 3-5 Mbps | 3-5 Mbps |
| High Quality | 8-12 Mbps | 8-12 Mbps |

---

## Security Settings

### Block Additional Keys

Edit `desktop_client.py` line 243:

### Add more blocked keys

blocked_keys = ['Control', 'Alt', 'Meta', 'OS', 'Win', 'F1', 'F4']


### Disable Specific Features

Disable keyboard control (mouse only)
@sio.on('control_key_press')
def on_key_press(data):
return # Ignore all keyboard input

Disable mouse clicks (view only)
@sio.on('control_mouse_click')
def on_mouse_click(data):
return # Ignore all clicks


---

## Server Configuration

### Environment Variables (Railway)

Add in Railway dashboard → Variables:

SECRET_KEY=your-random-secret-key-here
PORT=5000
PYTHON_VERSION=3.11.9


### Custom Domain (Railway Pro)

1. Go to Settings → Networking
2. Add custom domain
3. Update DNS records as shown
4. Update `SERVER_URL` in `desktop_client.py`

---

## Rebuilding After Changes

### After changing client code:

cd client
pyinstaller --onefile --noconsole --name=system32 desktop_client.py


### After changing server code:

cd server
git add .
git commit -m "Updated configuration"
git push origin main


Railway auto-deploys in 1-2 minutes.

---

## Performance Troubleshooting

### If lagging:
1. Reduce FPS
2. Lower resolution
3. Decrease JPEG quality
4. Check network speed

### If blurry:
1. Increase resolution
2. Increase JPEG quality
3. May need better internet

### If choppy:
1. Increase FPS
2. Check CPU usage
3. Close other programs
4. Use wired connection

---

## Monitoring Performance

### Check FPS in browser console:

Add to `viewer.html`:

setInterval(() => {
console.log(FPS: ${frameCount / 30});
frameCount = 0;
}, 30000);

### Check bandwidth usage:

Use browser DevTools → Network tab to see data transfer rates.

---

## Testing Configurations

1. Make changes to settings
2. Rebuild executable
3. Test with local viewer first
4. Test with remote viewer
5. Monitor performance
6. Adjust as needed

---

**Recommended testing order:**
1. Start with "Fast & Balanced"
2. Adjust based on your internet speed
3. Fine-tune for your specific use case

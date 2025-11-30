# 🛡️ Security Guide

Security considerations and best practices.

## Security Features

### Built-in Protection

1. **Blocked System Keys**
   - Ctrl combinations blocked
   - Alt combinations blocked
   - Windows key blocked
   - Prevents dangerous shortcuts

2. **HTTPS Encryption**
   - All data encrypted in transit
   - Provided by Railway platform
   - TLS 1.2+ encryption

3. **Unique Room IDs**
   - Random timestamp-based IDs
   - Hard to guess
   - Expire on disconnect

4. **No Data Persistence**
   - No screen recordings
   - No logs stored
   - Sessions cleared on disconnect

5. **Client-side Control**
   - Host maintains full control
   - Can stop session anytime
   - No forced access

---

## Security Risks

### Potential Threats

1. **Link Sharing**
   - Anyone with link can access
   - No password protection by default
   - Share only with trusted people

2. **Screen Content**
   - Viewers see everything on screen
   - Personal data, passwords, etc.
   - Be careful what you show

3. **Remote Control**
   - Viewers can control your computer
   - Can access files, run programs
   - Only share with authorized users

4. **Network Attacks**
   - Man-in-the-middle (mitigated by HTTPS)
   - DDoS (Railway handles this)
   - Session hijacking (room ID protection)

---

## Best Practices

### For Hosts

1. **Before Sharing**
   - Close sensitive documents
   - Clear browser history if needed
   - Log out of sensitive websites
   - Close password managers

2. **During Session**
   - Monitor what viewers are doing
   - Don't leave session unattended
   - Stop sharing when done

3. **After Session**
   - Click "Stop Sharing"
   - Close the application
   - Clear sensitive data if any was shown

4. **Link Management**
   - Only share with trusted people
   - Use secure channels (encrypted chat)
   - Don't post publicly
   - Generate new link for each session

---

### For Viewers

1. **Respect Privacy**
   - Don't access personal files
   - Don't share screenshots
   - Ask before controlling

2. **Secure Connection**
   - Use secure network (not public WiFi)
   - Use VPN if possible
   - Don't save links in browser history

---

## Adding Password Protection

### Option 1: Simple Password Check

Edit `server/app.py`:

Add after room creation
ROOM_PASSWORDS = {}

@socketio.on('create_room')
def handle_create_room(data):
room_id = data.get('room_id')
password = data.get('password', '') # Get password

ROOM_PASSWORDS[room_id] = password  # Store password
# ... rest of code
@socketio.on('join_room')
def handle_join_room(data):
room_id = data.get('room_id')
password = data.get('password', '')
# Check password
if ROOM_PASSWORDS.get(room_id) != password:
    emit('error', {'message': 'Wrong password'})
    return

# ... rest of code


### Option 2: Token-based Access

Generate secure tokens for each session:

import secrets

def generate_secure_token():
return secrets.token_urlsafe(32)

Use token in URL instead of timestamp
room_id = generate_secure_token()

---

## Firewall Configuration

### Windows Firewall

Allow the application:

1. Windows Security → Firewall & network protection
2. Allow an app through firewall
3. Add `system32.exe`
4. Allow both Private and Public networks

### Router Firewall

- No port forwarding needed
- Outbound connections only
- HTTPS (443) should be allowed by default

---

## Compliance Considerations

### GDPR (Europe)

- No personal data stored
- No cookies used
- Real-time only, no recording
- Users control their data

### HIPAA (Healthcare)

- **NOT compliant** for medical data
- No encryption at rest
- No audit logs
- Don't use for patient information

### Corporate Use

- Check with IT department
- May violate corporate policies
- Some networks block WebSocket
- Consider corporate VPN

---

## Vulnerability Reporting

If you discover a security vulnerability:

1. **Don't** create public GitHub issue
2. Email: security@yourproject.com
3. Include:
   - Description
   - Steps to reproduce
   - Potential impact
   - Suggested fix (if any)

4. Allow time for fix before disclosure
5. Credit will be given

---

## Security Checklist

### Before Using

- [ ] Read this security guide
- [ ] Understand risks
- [ ] Have host authorization
- [ ] Use secure network
- [ ] Close sensitive apps

### During Session

- [ ] Monitor viewer actions
- [ ] Don't show passwords
- [ ] Don't access sensitive data
- [ ] Stay at computer
- [ ] Watch for suspicious activity

### After Session

- [ ] Stop sharing properly
- [ ] Close application
- [ ] Change passwords if shown
- [ ] Clear any sensitive data
- [ ] Log out of accounts

---

## Known Limitations

1. **No Authentication**
   - Anyone with link can access
   - No username/password login
   - Add if needed (see above)

2. **No Audit Trail**
   - Can't see who accessed what
   - No session logs
   - Add logging if needed

3. **No Rate Limiting**
   - Could be abused for DDoS
   - Railway provides some protection
   - Add if needed for production

4. **No Access Control**
   - Can't restrict specific actions
   - All-or-nothing control
   - Modify code to add restrictions

---

## Hardening Tips

### 1. Add Authentication

Require API key
API_KEYS = {'key1', 'key2', 'key3'}

@socketio.on('connect')
def handle_connect():
auth = request.args.get('auth')
if auth not in API_KEYS:
return False # Reject connection

### 2. Add Rate Limiting

from collections import defaultdict
import time

connections = defaultdict(list)

@socketio.on('connect')
def handle_connect():
ip = request.remote_addr
now = time.time()

# Remove old connections
connections[ip] = [t for t in connections[ip] if now - t < 60]

# Check limit (5 connections per minute)
if len(connections[ip]) >= 5:
    return False

connections[ip].append(now)


### 3. Add Logging

import logging

logging.basicConfig(
filename='connections.log',
level=logging.INFO,
format='%(asctime)s - %(message)s'
)

@socketio.on('connect')
def handle_connect():
logging.info(f'Connection from {request.remote_addr}')


### 4. Restrict Actions

Disable keyboard, allow mouse only
@sio.on('control_key_press')
def on_key_press(data):
return # Ignore all keyboard input


---

## Security Updates

Keep software updated:

Update dependencies
pip install --upgrade flask flask-socketio flask-cors

Check for vulnerabilities
pip install safety
safety check


---

## Disclaimer

This software is provided "as-is" without warranty. Users are responsible for:

- Ensuring authorized access
- Protecting sensitive data
- Complying with laws and regulations
- Using responsibly and ethically

Not recommended for:
- Medical/healthcare data (HIPAA)
- Financial systems
- Critical infrastructure
- Unattended production systems

---

**Use responsibly and secure your deployments!**

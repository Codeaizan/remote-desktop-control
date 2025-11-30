# 📥 Installation Guide

Complete instructions for setting up the Remote Desktop Control application.

## Table of Contents

1. [Server Setup (Railway)](#server-setup)
2. [Desktop Client Setup](#desktop-client-setup)
3. [Building from Source](#building-from-source)
4. [Deployment](#deployment)

---

## Server Setup (Railway)

### Prerequisites

- GitHub account
- Railway account (sign up at https://railway.app)

### Step 1: Fork the Repository

1. Go to the project repository
2. Click "Fork" button (top-right)
3. Wait for fork to complete

### Step 2: Deploy to Railway

1. Visit https://railway.app
2. Click "Start New Project"
3. Select "Deploy from GitHub repo"
4. Authorize Railway to access your GitHub
5. Select your forked repository
6. Click "Deploy"
7. Wait for deployment (2-3 minutes)

### Step 3: Get Your Server URL

1. Click on your deployed service
2. Go to "Settings" tab
3. Scroll to "Networking"
4. Click "Generate Domain"
5. Copy the URL (e.g., `https://your-app.up.railway.app`)

### Step 4: Configure Environment Variables (Optional)

1. Go to "Variables" tab
2. Add these variables:
   - `SECRET_KEY`: Any random string (for security)
   - `PORT`: 5000 (default, don't change unless needed)

---

## Desktop Client Setup

### Option A: Download Pre-built Executable (Easiest)

1. Go to [Releases](https://github.com/YOUR_USERNAME/remote-desktop-server/releases)
2. Download `system32.exe`
3. Save to a folder (e.g., `C:\RemoteDesktop\`)
4. **First time only**: Right-click → Properties → Unblock (if present)
5. Run the executable

### Option B: Build from Source

See [Building from Source](#building-from-source) section below.

---

## Building from Source

### Prerequisites

- Python 3.11 or higher
- Git
- pip (Python package manager)

### Step 1: Clone Repository

git clone (https://github.com/Codeaizan/remote-desktop-server.git)

cd remote-desktop-server


### Step 2: Install Dependencies

#### Server Dependencies

cd server
pip install -r requirements.txt


#### Client Dependencies

cd ../client
pip install -r requirements.txt


### Step 3: Configure Server URL

Edit `client/desktop_client.py`:

Line 10: Replace with your Railway URL
SERVER_URL = "https://your-app.up.railway.app"


### Step 4: Build Executable

cd client
pyinstaller --onefile --noconsole --name=system32 desktop_client.py


The executable will be in `client/dist/system32.exe`

---

## Deployment

### Deploy Server Updates

cd server
git add .
git commit -m "Your commit message"
git push origin main


Railway will automatically redeploy (takes 1-2 minutes).

### Distribute Desktop Client

1. Build the executable as shown above
2. Share `system32.exe` with users
3. Optionally, create an installer using NSIS or Inno Setup

---

## File Structure

remote-desktop-server/
├── server/
│ ├── app.py # Main server application
│ ├── requirements.txt # Python dependencies
│ ├── Procfile # Railway deployment config
│ ├── runtime.txt # Python version
│ └── templates/
│ ├── index.html # Landing page
│ └── viewer.html # Viewer interface
├── client/
│ ├── desktop_client.py # Desktop client source
│ ├── requirements.txt # Client dependencies
│ └── dist/
│ └── system32.exe # Built executable
├── docs/ # Documentation
├── README.md # Main readme
└── LICENSE # License file


---

## Verification

### Test Server

Visit your Railway URL in a browser. You should see the landing page.

### Test Desktop Client

1. Run `system32.exe`
2. Browser should open automatically
3. Click "Start Sharing"
4. You should see a viewer link generated
5. Open link in another browser/device
6. You should see your screen

---

## Troubleshooting

See [Troubleshooting Guide](TROUBLESHOOTING.md) for common issues.

---

## Next Steps

- Read [User Guide](USER_GUIDE.md) to learn how to use the application
- Review [Configuration Guide](CONFIGURATION.md) for performance tuning
- Check [Security Guide](SECURITY.md) for security best practices

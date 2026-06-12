# 🤖 Odysseus — Local AI on Your Mac
> Run a private, self-hosted AI chat interface on your MacBook. No subscriptions. No cloud. No data leaving your machine.

![macOS](https://img.shields.io/badge/macOS-only-black?style=flat-square&logo=apple) ![Docker](https://img.shields.io/badge/Docker-required-2496ED?style=flat-square&logo=docker) ![Ollama](https://img.shields.io/badge/Ollama-required-black?style=flat-square) ![Model](https://img.shields.io/badge/model-llama3.2-green?style=flat-square)

---

## 📋 Table of Contents

- [What is this?](#-what-is-this)
- [Requirements](#-requirements)
- [Step 1 — Install Docker](#-step-1--install-docker)
- [Step 2 — Install Ollama](#-step-2--install-ollama)
- [Step 3 — Pull the AI Model](#-step-3--pull-the-ai-model)
- [Step 4 — Install Odysseus](#-step-4--install-odysseus)
- [Step 5 — Open in Browser](#-step-5--open-in-browser)
- [Step 6 — Log In](#-step-6--log-in)
- [Step 7 — Personalize](#-step-7--personalize)
- [Step 8 — Make it a Desktop App](#-step-8--make-it-a-desktop-app)
- [Step 9 — Access from iPhone](#-step-9--access-from-iphone)
- [Troubleshooting](#-troubleshooting)

---

## 💡 What is this?

**Odysseus** is an open-source AI chat app — like ChatGPT, but running 100% locally on your Mac.

- ✅ Completely private
- ✅ Works offline
- ✅ Free forever
- ✅ Uses [Ollama](https://ollama.com) to run AI models locally

> Built by [pewdiepie-archdaemon](https://github.com/pewdiepie-archdaemon/odysseus). This guide is a beginner-friendly walkthrough.

---

## ⚙️ Requirements

| Requirement | Minimum |
|---|---|
| macOS | Monterey or later |
| RAM | **8GB minimum — 16GB recommended** |
| Free Disk Space | ~5GB |
| Docker Desktop | Latest version |
| Ollama | Latest version |

> ⚠️ **RAM Warning:** Running a local AI model is memory-intensive. If your Mac has 8GB RAM, close other apps while using Odysseus. 16GB gives a much smoother experience.

---

## 🐳 Step 1 — Install Docker

Docker is the environment that Odysseus runs inside. Think of it as a ready-made room with everything pre-installed.

1. Go to [docker.com/products/docker-desktop](https://www.docker.com/products/docker-desktop)
2. Download **Docker Desktop for Mac**
3. Open the `.dmg` file and drag Docker to Applications
4. Launch Docker from Applications — wait for the whale icon to appear in your menu bar
5. Confirm it's running:

```bash
docker --version
```

You should see something like `Docker version 24.x.x`

---

## 🦙 Step 2 — Install Ollama

Ollama is the tool that downloads and runs AI models locally on your Mac.

1. Go to [ollama.com](https://ollama.com)
2. Click **Download for Mac**
3. Open and install it
4. Confirm it's working:

```bash
ollama --version
```

---

## 🧠 Step 3 — Pull the AI Model

This downloads the AI brain (llama3.2) to your Mac. ~2GB download — do this on WiFi.

```bash
# Download the model
ollama pull llama3.2

# Confirm it's there
ollama list
```

You should see `llama3.2` listed. That's your local AI model, ready to go.

---

## 🚀 Step 4 — Install Odysseus

Open Terminal (`Cmd + Space` → type Terminal → Enter) and run these commands one by one:

```bash
# Clone the Odysseus repo
git clone https://github.com/pewdiepie-archdaemon/odysseus.git && cd odysseus

# Create your config file
cp .env.example .env

# Build and start Odysseus
docker compose up -d --build

# Check everything is running
docker compose ps
```

> ⏳ The first build takes 2–5 minutes. Docker is setting up the full environment. Subsequent starts are instant.

When you see containers listed as **Up** — you're done.

---

## 🌐 Step 5 — Open in Browser

```
http://localhost:7000
```

Or if that doesn't work:

```
http://127.0.0.1:7000
```

You should see the Odysseus login screen.

---

## 🔐 Step 6 — Log In

**Default credentials:**
- Username: `admin`
- Password: check your logs

```bash
docker compose logs odysseus | grep -i password
```

Look for a line that shows your auto-generated password and copy it.

---

## 🎨 Step 7 — Personalize

If it doesnt launch/ throws error run this:

docker compose logs odysseus 2>&1 | grep -i "pass\|admin\|creat\|account 

(Copy and paste this in terminal)


Once logged in, go to **Settings** to:

- Change your username
- Set a personal password
- Pick your default model (llama3.2)

**To set custom credentials before first launch**, edit your `.env` file:

```bash
# Add these lines to ~/odysseus/.env
ODYSSEUS_ADMIN_PASSWORD=yourpassword
ODYSSEUS_ADMIN_USER=yourusername
```


Then restart:

```bash
docker compose up -d
```

---

## 🖥️ Step 8 — Make it a Desktop App (Mac only)

Turn Odysseus into a proper Mac app that lives in your Dock.

1. Open **Automator** (`Cmd + Space` → Automator)
2. Click **New Document**
3. Choose **Web Application**
4. Paste this URL: `http://127.0.0.1:7000`
5. `File → Save` → name it **Odysseus** → save to **Applications**
6. Open Launchpad — Odysseus is now an app

**Optional — Add a custom icon:**
1. Find an icon image you like (PNG works best)
2. Open it in **Preview** → `Cmd + A` → `Cmd + C`
3. Right-click Odysseus in Applications → **Get Info**
4. Click the icon in the top-left of the Info window → `Cmd + V`

---

## 📱 Step 9 — Access from iPhone

As long as your iPhone is on the **same WiFi network**:

```bash
# Find your Mac's local IP
ipconfig getifaddr en0
```

Then on your iPhone, open Safari and go to:

```
http://YOUR_IP_HERE:7000
```

Example: `http://192.168.1.5:7000`

---

## 🛠️ Troubleshooting

**Localhost not loading?**

Try these URLs in order:
```
http://localhost:7000
http://localhost:7000/setup
http://127.0.0.1:7000
http://127.0.0.1:7000/setup
```

**Forgot your password?**
```bash
docker compose logs odysseus | grep -i password
```

**Need a full reset?**
```bash
docker compose down
rm -rf data
docker compose up -d
```
> ⚠️ This wipes all your data and chat history. Only use if nothing else works.

**Docker not starting?**
- Make sure Docker Desktop app is open and the whale icon is in your menu bar
- Try restarting Docker Desktop

**Model feels slow?**
- Close other apps to free up RAM
- llama3.2 runs best with 16GB RAM

---

## 📎 Quick Command Reference

```bash
# Start Odysseus
docker compose up -d

# Stop Odysseus
docker compose down

# Check status
docker compose ps

# View logs
docker compose logs odysseus

# Full reset (deletes data)
docker compose down && rm -rf data && docker compose up -d
```

---

<div align="center">

Made with ❤️ for the local AI community

⭐ Star the [original repo](https://github.com/pewdiepie-archdaemon/odysseus) if this helped you

</div>

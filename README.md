🚀 Fai Free VPS Deploy Bot

<p align="center">
  <b>⚡ Free VPS Deployment | 🤖 Discord Bot | 🔥 24/7 Hosting</b>
</p>Welcome to Fai Free VPS Deploy Bot! 🎉

A Python-powered Discord VPS deployment bot. Follow this guide to install all dependencies, configure your environment variables directly from the terminal, and keep your bot running 24/7 using Systemd.

---

✨ Features

- 🤖 Discord Bot Integration
- 🐍 Python-powered
- 🔐 Secure Environment Variable Setup
- ⚡ Automatic Bot Restart
- 🔄 Automatic Startup After VPS Reboot
- 🖥️ Systemd Service Support
- 📡 Live Console Logs

📋 Requirements

- 🐧 Ubuntu / Debian VPS
- 🐍 Python 3
- 🔑 Root or Sudo Access
- 🤖 Discord Bot Token

---

1️⃣ Update VPS Packages

Run this command:

apt update && apt upgrade -y

Install Python and pip:

apt install python3 python3-pip -y

2️⃣ Install Required Python Libraries

Copy and execute all commands:

pip install davey --break-system-packages --ignore-installed

pip install discord --break-system-packages --ignore-installed

pip install python-dotenv --break-system-packages --ignore-installed

pip install PyNaCl --break-system-packages --ignore-installed

pip install paramiko --break-system-packages --ignore-installed

pip install flask --break-system-packages --ignore-installed

pip install flask_cors --break-system-packages --ignore-installed

pip install argon2-cffi --break-system-packages --ignore-installed

3️⃣ Create Environment File

Create your ".env" file from "test.env":

cp test.env .env

4️⃣ ⚙️ Automatic .env Configuration

🔥 No Nano, no manual editing!

This Python script automatically detects variables from your "test.env" configuration and asks you to enter their values directly in the terminal.

python3 - <<'PY'
import getpass
from pathlib import Path

env_file = Path(".env")

if not env_file.exists():
    print("❌ ERROR: .env file not found!")
    raise SystemExit(1)

lines = env_file.read_text().splitlines()
updated = []

print("\n🚀 FAI VPS ENVIRONMENT SETUP")
print("=" * 40)

for line in lines:
    stripped = line.strip()

    if not stripped or stripped.startswith("#") or "=" not in stripped:
        updated.append(line)
        continue

    key, old_value = line.split("=", 1)
    key = key.strip()

    if not key:
        updated.append(line)
        continue

    print(f"\n⚙️ Setting up: {key}=")
    value = getpass.getpass(f"🔑 Enter {key}: ")

    if value:
        updated.append(f"{key}={value}")
        print(f"✅ {key}= [CONFIGURED]")
    else:
        updated.append(line)
        print(f"⏭️ {key}= [UNCHANGED]")

env_file.write_text("\n".join(updated) + "\n")

print("\n" + "=" * 40)
print("🎉 ENVIRONMENT CONFIGURATION COMPLETED!")
print("🚀 Your .env file is ready!")
PY

📝 Example Environment Variables

Your "test.env" may contain:

DISCORD_BOT_TOKEN=

The script will automatically detect the variable and request its value.

🔒 Security: Never upload ".env" to GitHub or share your Discord Bot Token.

5️⃣ 🖥️ Create Systemd Service

Create the service file:

sudo nano /etc/systemd/system/bot.service

Paste this complete configuration:

[Unit]
Description=Fai Free VPS Deploy Bot
After=network.target

[Service]
User=root
WorkingDirectory=/root
ExecStart=/usr/bin/python3 /root/bot.py
Restart=always
RestartSec=5
Environment=PYTHONUNBUFFERED=1

[Install]
WantedBy=multi-user.target

Save the file and exit Nano.

6️⃣ 🚀 Start Your Bot 24/7

Execute all commands:

sudo systemctl daemon-reload

sudo systemctl restart bot

sudo systemctl enable bot

🎉 Your bot is now configured to start automatically and restart if it crashes.

7️⃣ 📊 Bot Management Commands

🟢 Check Bot Status

systemctl status bot

📡 View Live Console Logs

journalctl -u bot -f

🔄 Restart Bot

systemctl restart bot

▶️ Start Bot

systemctl start bot

⛔ Stop Bot

systemctl stop bot

❌ Disable Automatic Startup

systemctl disable bot

---

🛡️ Security

- 🔐 Keep your Discord token private.
- 🚫 Never upload ".env" to GitHub.
- 📁 Add ".env" to ".gitignore".
- ⚠️ Only run scripts you trust.

🎉 Installation Completed!

Congratulations! Your Fai Free VPS Deploy Bot is configured for 24/7 operation using Systemd.

---

<p align="center">
  🚀 <b>Fai Free VPS Deploy Bot</b>
  <br>
  💙 Developed by <b>FaiLive2</b>
  <br>
  🌐 GitHub: https://github.com/FaiLive2
</p>

🚀 VPS Deploy Bot

A Python-based Discord VPS Deploy Bot. Follow this guide to install dependencies, configure environment variables, and run the bot continuously using Systemd.

📋 Requirements

- Ubuntu/Debian VPS
- Python 3
- Root or sudo access
- Discord Bot Token

1. Update Packages

apt update && apt upgrade -y
apt install python3 python3-pip -y

2. Install Python Dependencies

pip install davey --break-system-packages --ignore-installed
pip install discord --break-system-packages --ignore-installed
pip install python-dotenv --break-system-packages --ignore-installed
pip install PyNaCl --break-system-packages --ignore-installed
pip install paramiko --break-system-packages --ignore-installed
pip install flask --break-system-packages --ignore-installed
pip install flask_cors --break-system-packages --ignore-installed
pip install argon2-cffi --break-system-packages --ignore-installed

3. Configure Environment Variables

First, create your ".env" file:

cp test.env .env

You don't need Nano or any other text editor to configure your environment variables.

Run this command to configure them directly through the terminal:

python3 - <<'PY'
import getpass
from pathlib import Path

env_file = Path(".env")

if not env_file.exists():
    print("ERROR: .env file not found!")
    raise SystemExit(1)

lines = env_file.read_text().splitlines()
updated = []

print("\n========== ENVIRONMENT SETUP ==========\n")

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

    print(f"Setting up: {key}=")
    value = getpass.getpass(f"Enter {key}: ")

    if value:
        updated.append(f"{key}={value}")
        print(f"{key}= [CONFIGURED]\n")
    else:
        updated.append(line)
        print(f"{key}= [UNCHANGED]\n")

env_file.write_text("\n".join(updated) + "\n")

print("======================================")
print("Environment configuration completed!")
PY

The script automatically detects variables inside "test.env", asks you to enter their values, and saves everything into ".env".

Example:

DISCORD_BOT_TOKEN=your_discord_bot_token

Important: Never share your ".env" file or Discord Bot Token publicly. Add ".env" to ".gitignore".

4. Create Systemd Service

Create the service file:

sudo nano /etc/systemd/system/bot.service

Paste the following configuration:

[Unit]
Description=Vps Deploy Bot
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

Save and exit.

5. Enable and Start the Bot

Run these commands:

sudo systemctl daemon-reload
sudo systemctl enable bot
sudo systemctl restart bot

Your bot will now automatically restart if it crashes and start again when your VPS reboots.

6. Check Bot Status

Check whether your bot is running:

systemctl status bot

View live bot logs:

journalctl -u bot -f

Restart:

systemctl restart bot

Stop:

systemctl stop bot

Start:

systemctl start bot

🎉 Installation Completed!

Your VPS Deploy Bot is now configured to run continuously using Systemd.

---

Developed by FaiLive2

GitHub: https://github.com/FaiLive2# Fai-advance-free-d-vps

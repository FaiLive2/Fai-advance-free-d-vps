🚀 Fai Free VPS Deploy Bot

<p align="center">
  <b>⚡ Free VPS Deployment | 🤖 Discord Bot | 🔥 24/7 Hosting</b>
</p>Welcome to Fai Free VPS Deploy Bot! 🎉

A Python-powered Discord VPS deployment bot. Follow this guide to install all dependencies, configure your environment variables directly from the terminal, and keep your bot running 24/7 using Systemd.

---
apt install python3-pip -y

pip install davey --break-system-packages --ignore-installed
pip install discord --break-system-packages --ignore-installed
pip install dotenv --break-system-packages --ignore-installed
pip install PyNaCl --break-system-packages --ignore-installed
pip install paramiko --break-system-packages --ignore-installed
pip install flask --break-system-packages --ignore-installed
pip install flask_cors --break-system-packages --ignore-installed
pip install argon2-cffi --break-system-packages --ignore-installed

cp test.env .env

# SETUP THE .env FILE

# INSIDE THE .env FILE CAN PUT THE VIRABLES WITHOUT USE nano OR OTHERS CAN SETUP BY TERMINAL AND ALSO SHOWING WHICH VIRABLES IS SETUPING LIKE SHOWING DISCORD_BOT_TOKEN= LIKE THIS OK

sudo nano /etc/systemd/system/bot.service

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


sudo systemctl daemon-reload
sudo systemctl restart bot
sudo systemctl enable bot

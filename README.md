# Cobm
sudo apt update
	sudo apt install apache2 mysql-server php php-mysql php-xml php-curl php-zip php-gd php-mbstring php-intl unzip -y



curl -fsSL https://deb.nodesource.com/setup_14.x | sudo -E bash -
sudo apt install nodejs -y


wget https://releases.rocket.chat/latest/download -O rocket.chat.tgz
tar -xzf rocket.chat.tgz
cd bundle/programs/server
npm install
cd ../../..


sudo useradd -m -s /bin/bash rocketchat
sudo mv bundle /opt/Rocket.Chat
sudo chown -R rocketchat:rocketchat /opt/Rocket.Chat

sudo useradd -m -s /bin/bash rocketchat
sudo mv bundle /opt/Rocket.Chat
sudo chown -R rocketchat:rocketchat /opt/Rocket.Chat


sudo nano /etc/systemd/system/rocketchat.service 

[Unit]
Description=Rocket.Chat
After=network.target

[Service]
ExecStart=/usr/bin/node /opt/Rocket.Chat/main.js
Restart=always
User=rocketchat
Environment=MONGO_URL=mongodb://localhost:27017/rocketchat
Environment=ROOT_URL=https://tuservidor.com/chat
Environment=PORT=3000

[Install]
WantedBy=multi-user.target
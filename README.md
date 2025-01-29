# Research paper about Plex, Plex with Tdarr and Jellyfin cpu usage

There are 3 seperate docker compose files for each tests that I am running. Alongside those is a monitoring docker-compose which I have deployed on every machine for detailed monitoring. I am using prometheus to scrape the data and grafana to visualize all the data.
Every machine is a default Ubtuntu server (24.04.1 LTS) setup using cloud-init on proxmox.

These are the commands I used to set up each machine. I have another repository with ansible scripts that does it automatically but to keep it easily reproducable I have used just these commands by hand.
```
# Qemu guest agent install
sudo apt update && sudo apt -y install qemu-guest-agent
sudo systemctl start qemu-guest-agent

# Docker install
sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin -y
sudo usermod -aG docker $USER

mkdir monitoring
cd monitoring
wget https://raw.githubusercontent.com/DaandeJong100/Research-paper-31-01-25/refs/heads/main/Monitoring/docker-compose.yml
sudo docker compose up -d
```

## 1. Plex
```
wget https://raw.githubusercontent.com/DaandeJong100/Research-paper-31-01-25/refs/heads/main/Plex/docker-compose.yml
wget https://raw.githubusercontent.com/DaandeJong100/Research-paper-31-01-25/refs/heads/main/Plex/.env
# nano .env to adjust values
sudo docker compose up -d
```
## 2. Plex + Tdarr
```
wget https://raw.githubusercontent.com/DaandeJong100/Research-paper-31-01-25/refs/heads/main/Plex%2BTdarr/docker-compose.yml
wget https://raw.githubusercontent.com/DaandeJong100/Research-paper-31-01-25/refs/heads/main/Plex%2BTdarr/.env
# nano .env to adjust values
sudo docker compose up -d
```
## 3. Jellyfin
```
wget https://raw.githubusercontent.com/DaandeJong100/Research-paper-31-01-25/refs/heads/main/Jellyfin/docker-compose.yml
wget https://raw.githubusercontent.com/DaandeJong100/Research-paper-31-01-25/refs/heads/main/Jellyfin/.env
# nano .env to adjust values
sudo docker compose up -d
```

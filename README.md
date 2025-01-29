# Research paper about Plex, Plex with Tdarr and Jellyfin cpu usage

There are 3 seperate docker compose files for each tests that I am running. Alongside those is a monitoring docker-compose which I have deployed on every machine for detailed monitoring. I am using prometheus to scrape the data and grafana to visualize all the data.
Every machine is a default Ubtuntu server (24.04.1 LTS) setup using cloud-init on proxmox.

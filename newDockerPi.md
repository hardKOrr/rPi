# ***newDockerPi.txt***

# ***Micro SD Preparations***
## ***Create these files before first boot***
`boot\ssh`

`boot\wpa_supplicant.conf`
```
country=us
update_config=1
ctrl_interface=/var/run/wpa_supplicant
network={
  scan_ssid=1
  ssid="WiFi Network Name"
  psk="WiFi Network Password"
}
```

# ***Pi configuration***
`sudo raspi-config`
- System Options
  - Password
  - Hostname
- Display Options
  - Resolution
- Interface Options  
  - VNC
- Localisation
  - Timezone

# ***Stay Up-to-date***
```
sudo apt-get -y update
sudo apt-get -y upgrade
```

# ***Editor***
`sudo apt install code`

# ***Docker***
## ***Docker-Compose***
### ***Install***
```
curl -sSL https://get.docker.com | sh
sudo usermod -aG docker ${USER}
sudo apt-get install libffi-dev libssl-dev
sudo apt install python3-dev
sudo apt-get install -y python3 python3-pip
sudo pip3 install docker-compose
sudo systemctl enable docker
```
### ***Yml config***
`nano ~/docker-compose.yml`
```
#docker-compose.yml
```

`sudo chmod a+w ~/docker-compose.yml`

## ***Docker Containers***
- cbcrowe/pihole-unbound:latest
- homeassistant/raspberrypi4-homeassistant:stable
- karsten13/magicmirror:latest
- linuxserver/qbittorrent

## ***ToDo***
- Need a better way to manage VPN, ideally so qbittorrent can see it and bind to it
- Something doesn't like to auto connect smb, might be windows sharing
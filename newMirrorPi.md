# ***newMirrorPi.md***

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

# ***Correct QoS issues***
I had to do this locally, ssh wouldn't stay connected

`sudo nano /etc/ssh/sshd_config`
```
IPQoS cs0 cs0
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

# ***Create service to disable wifi power management (all users)***
## ***Service Script***
`sudo nano ~/WiFiPowerMgmt.sh`
```
#!/bin/sh -
iwconfig wlan0 power off
```

## ***Service Configuration File***

`sudo nano /lib/systemd/system/WiFiPowerMgmt.service`
```
Description=Disables WifI Power Management
After=multi-user.target
[Service]
Type=idle
ExecStart=/home/pi/WiFiPowerMgmt.sh

[Install]
WantedBy=multi-user.target
```

## ***Service Install***
`sudo chmod 644 /lib/systemd/system/WiFiPowerMgmt.service`

`sudo systemctl daemon-reload`

`sudo systemctl enable WiFiPowerMgmt.service`

# ***Stay Up-to-date***
`sudo apt-get -y update`

`sudo apt-get -y dist-upgrade`

`sudo apt-get -y upgrade`


# ***Chromium install and autostart***

## ***Install***
`sudo apt-get install -y --no-install-recommends xserver-xorg x11-xserver-utils xinit openbox`

`sudo apt-get install -y --no-install-recommends chromium-browser`

`sudo apt-get install -y rpi-chromium-mods`

`sudo apt-get install -y python-sense-emu python3-sense-emu`

`sudo apt-get install ttf-mscorefonts-installer`

## ***Auto-Start***
`sudo nano /etc/xdg/openbox/autostart`
```
xset s off
xset s noblank
xset -dpms
setxkbmap -optionn terminate:ctr_alt_bksp
sed -i 's/"exited_cleanly":false/"exited_cleanly":true/' ~/.config/chromium/'Local State'
sed -i 's/"exited_cleanly":false/"exited_cleanly":true/; s/"exit_type":"[^"]\+"/"exit_type":"Normal"/' ~/.config/chromium/Default/Preferences
chromium-browser --disable-infobars --noerrdialogs --incofnito --check-for-update-interval=1 
--simulate-critical-update --kiosk 'http://`MagicMirrorHost/IP`:8080'
```

# ***Boot behavior***

`sudo nano ~/.bash_profile`
```
[[ -z $DISPLAY && $XDG_VTNR -eq 1 ]] && startx -- -nocursor
```

`sudo nano /boot/config.txt`
```
overscan_left/right/top/bottom
display_rotate=3
```

# ***crontab to execute reboots and manage display power***

`sudo crontab -e`
```
# reboot daily at 6:30
30 6 * * *  /sbin/shutdown -r now

# monitor on daily at 7:00
0 7 * * * vcgencmd display_power 1

# monitor off daily at 16:00
0 16 * * * vcgencmd display_power 0
0 17 * * * vcgencmd display_power 0

# reboot daily at 17:30
30 17 * * * /sbin/shutdown -r now

# monitor on daily at 18:00
0 18 * * * vcgencmd display_power 1

# monitor off daily at 20:00
0 20 * * * vcgencmd display_power 0
0 21 * * * vcgencmd display_power 0
0 22 * * * vcgencmd display_power 0
0 23 * * * vcgencmd display_power 0
0 0 * * * vcgencmd display_power 0
0 1 * * * vcgencmd display_power 0
0 2 * * * vcgencmd display_power 0
0 3 * * * vcgencmd display_power 0
0 4 * * * vcgencmd display_power 0
0 5 * * * vcgencmd display_power 0
0 6 * * * vcgencmd display_power 0
```

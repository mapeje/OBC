Modifications from instructions per https://flows.nodered.org/node/node-red-contrib-flic-buttons to work with Openplotter

1. Download the flic daemon as instructed:
```git clone https://github.com/50ButtonsEach/fliclib-linux-hci.git```

2. Start the dameon manually by using: ```sudo /home/pi/fliclib-linux-hci/bin/armv6l/./flicd -f /home/pi/fliclib-linux-hci/bin/armv6l/flic.sqlite3```

3. Scan for bluetooth device using:
 ```cd /home/pi/.signalk/red/node_modules/node-red-contrib-flic-buttons/lib```
```node scanwizard.js```
  
4. To autostart flic daemon:
```mkdir /home/pi/.flic```
```sudo nano /etc/systemd/system/flicd.service```

Add below, save and exit:
```
[Unit]
Description=flicd Service
After=bluetooth.service
Requires=bluetooth.service

[Service]
TimeoutStartSec=0
ExecStart=/home/pi/fliclib-linux-hci/bin/armv6l/./flicd -f /home/pi/fliclib-linux-hci/bin/armv6l/flic.sqlite3 -s 0.0.0.0 -l /var/log/flicd.log -w
Restart=always
RestartSec=3

[Install]
WantedBy=multi-user.target
```
5. Enable start at boot 
```sudo systemctl enable /etc/systemd/system/flicd.service```

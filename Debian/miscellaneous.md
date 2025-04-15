# Small things that don't fit anywhere else

## Installing qbittorrent

1. Read [LinuxCapable Guide](https://linuxcapable.com/install-qbittorrent-on-debian-linux/).  Make sure to install qbittorrent-nox.
2. Create home directory for qbittorrent user.
3. Create/edit qbittorrent service in systemd.
4. Set qbittorrent to start at boot.

qbittorrent-nox.service configuration
```
[Unit]
Description=qBittorrent Command Line Client
After=local-fs.target network-online.target nss-lookup.target
Wants=network-online.target
RequiresMountsFor=/mnt/download1 /mnt/download2

[Service]
Type=forking
User=qbittorrent
Group=qbittorrent
UMask=007
ExecStart=/usr/bin/qbittorrent-nox -d --webui-port=8080
Restart=on-failure

[Install]
WantedBy=multi-user.target
```

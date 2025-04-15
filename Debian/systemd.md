## Useful systemd commands.

# Graphical or multi-user display.
```
systemctl set-default multi-user.target -> set CLI.
systemctl set-default graphical.target -> set GUI.
```

# To check NFS mount paths
Run command `systemctl list-units -t mount --all`

# Run qbittorrent with NFS shares - need to wait for NFS shares to be available.
1. Edit /etc/systemd/system/qbittorrent-nox.service.
2. Add/edit the following lines:
```
[Unit]
Description=qBittorrent Command Line Client
Requires=mnt-<NFS path 1>.mount <NFS path 2>.mount
Wants=network-online.target
After=local-fs.target network-online.target nss-lookup.target
```

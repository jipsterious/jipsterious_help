# Podman Information - what I learned

## Podman initial setup
1. Get busybox image to test network.
2. Network/Subnet configuration is in /usr/share/containers/containers.conf (see https://github.com/containers/common/blob/main/docs/containers.conf.5.md).
3. When the Podman package is installed, a default network configuration is commonly installed into /etc/cni/net.d as 87-podman-bridge.conflist.  In addition, the default network name is defined in /usr/share/containers/libpod.conf with the key cni_default_network.

See https://www.redhat.com/en/blog/container-networking-podman.


## Getting, running images
Get/download image - podman pull "image name"

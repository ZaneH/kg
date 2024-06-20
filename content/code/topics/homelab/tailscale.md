---
title: Tailscale
---

To get this running in LXC Container, I needed these lines in the `/etc/pve/lxc/102.conf` file.

```
lxc.cgroup.devices.allow: c 10:200 rwm
lxc.mount.entry: /dev/net/tun dev/net/tun none bind,create=file
```
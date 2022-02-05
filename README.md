# config_preseed_di
This repo contains my Debian preseed work.

# Project Goal
To capture my fully automated deployment configurations as code.

The deployments SHOULD align to the following, in general;
* PRIVATE
* SECURE
* SIMPLE
* UNOPINIONATED

# Password Is Plain Text
As above, we consider SECURE as a requirement. In this case; we do not include
any ways to login to the host without bare-metal access.

We will look to tweak this, by leveraging a variable passed to/via GRUB.
Ideally; that will also include an encrypted luks deployment with the same.

# Prerequisites
A functional deploy/init system that includes an `auto` and `preseed` pointer.

In my case; I leverage PXE. isc-dhcp-server, tftpd-hpa

I use the grub config exposed via tftpd-hpa to customise my deployments;
```
auto=true url=tftp://${net_efinet0_next_server}/debian-installer/preseed/${net_default_mac}.cfg interface=auto priority=critical noshell console=ttyS0
```

Where a host does not expose a serial port, you shoudl remove `console=ttyS0`.

# Usage
Considering the above; point to, via an include or symlink, to src/default.cfg.


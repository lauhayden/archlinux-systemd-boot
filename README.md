# Arch Installation Disk as systemd-boot Entry

Tired of carrying USB with the Arch installation disk for system rescue? This simple package
installs the Arch Linux installation media as a boot option for `systemd-boot`. **Caveat: the
installation disk is quite large, so an EFI System Partition of >1GiB is recommended.**

## Installation

1. In order for the installation disk to find the squashfs image, the EFI System Partition has to
be labled `ESP`. Label it by using the `fatlabel` tool. The label that the initramfs looks for can
be changed by modifying the `archisolabel` argument in `arch-installmedia.conf`.

2. Standard Arch `makepkg` and `pacman -U` installation.

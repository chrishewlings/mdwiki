# Arch Linux

##Install from scratch

1. Check network connectivity. `ping google.com`
2. Ensure time and date are valid : `timedatectl set-ntp true`
3. Partition disks with `parted`, `gdisk`, or `fdisk`
4. Run `set /dev/sdaX boot on` to flag partition containing `/boot` as bootable
5. after partitioning, format partition(s) to desired format (`mkfs.ext4`, `mkfs.btrfs`, etc.)
6. Create and enable swap:
	+ `mkswap /dev/sdaY`
	+ `swapon /dev/sdaY`
7. Mount your new root filesystem: `mount /dev/sdaX /mnt`
8. Use `pacstrap` to build your new install: `pacstrap -i /mnt base base-devel`
9. Generate an `fstab` file: `genfstab -U /mnt > /mnt/etc/fstab` (the `-U` means UUIDs will be used instead of regular disklabels. It's a good thing.)
10. Finally, chroot into the new system. `arch-chroot /mnt /bin/bash`

## Building up from barebones system (still in chroot)

### Basic systems admin/firstinstall

1. Set up your locale:
	+ uncomment `en_US.UTF-8` from `/etc/locale.gen` & run `locale-gen`
	+ add desired locale to `/etc/locale.conf` : `echo "LANG=en.US.UTF-8" > /etc/locale.conf`
2. Set up time zone: `ln -sf /usr/share/zoneinfo/America/FuckYeah /etc/localtime`
3. Set hwclock to UTC `hwclock --systohc --utc`
4. Set hostname `echo "balls" > /etc/hostname`
5. Install a bootloader, FFS!
	+ BIOS:
		+ `pacman -S grub os-prober`
		+ `grub-install --recheck /dev/sda`
		+ `grub-mkconfig -o /boot/grub/grub.cfg`
	+ EFI: 
		+ `pacman -S dosfstools` # for EFI partition manipulation
		+ `bootctl --path=$(ESP) install`, replacing the variable with your own ESP
		+ Create `$ESP/loader/entries/arch.conf`, with contents:

		```
title	Arch Linux
linux	/vmlinuz-linux
initrd	/initramfs-linux.img
options	root=/dev/sdaX rw
```
- Add any additional packages you may need.
	+ `dialog wifi-menu iw wpa_supplicant` # if using wireless

- You should now be able to reboot into the system proper!

### Generally good ideas
- Change root password : `passwd`

 
### Package Management
- Get all GPG keys for arch repos (fixes sig errors)
	- `pacman-key --init`
	- `pacman-key --populate archlinux`

- Disable crappy/slow mirrors
	+ `mv /etc/pacman.d/mirrorlist /etc/pacman.d/mirrorlist.bak`
	+ `rankmirrors -n6 /etc/pacman.d/mirrorlist.bak > /etc/pacman.d/mirrorlist`

#### Installs

Repos to add to `/etc/pacman.conf`:
```
[xyne-any] # or {i686, x86_64}
SigLevel = Required
Server = ttp://xyne.archlinux.ca/repos/xyne
 ```

#### Packages to install 
- `powerpill` - faster downloading from pacman
- `pacaur` - best AUR manager i've found
	+ configure pacaur to use `powerpill`
		+ 

- Disable root login in /etc/sshd/

### Passwords + Users

- Add new admin user
	+ `useradd -m -G wheel -s /bin/bash $USERNAME`
- Disable root login entirely (_MAKE SURE YOU CAN SUDO FIRST!_)
	- `sudo passwd -l root`


## Networking
### Wireless
- arch ISO has `netctl` and `wifi-menu` (as well as many wireless firmwares) installed on the live image. This is expressly _NOT_ true of a pacstrapped system, so if using wifi, make sure you install drivers for it!

### Wired
- DHCP enabled by default on live image.
- to enable DHCP over wired network on install, run `systemctl enable dhcpcd@eth0.service`

#### Set up static IP
- via `systemd-networkd`, create `/etc/systemd/network/name.network`:

```
[Match]
Name=eth0

[Network]
DNS=8.8.8.8

[Address]
Address=192.168.0.2/24

[Route]
Gateway=192.168.0.1
```
- Don't forget to `systemctl disable dhcpcd@eth0.service` afterwards.

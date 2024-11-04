# Project 1 - "Arch Linux Installation"
## System Administration
#### Talha Choudhury


# Part 1: Installation

- VMWare:
-- I used VMWare workstation for the Arch Linux installation


- Acquiring an ISO
-- For this portion I went to Arch Linux
-- On the website with the ISOs, I went to the ISOs in the United States and used the one provided by MIT. [MIT ISO](https://mirrors.mit.edu/archlinux/iso/2024.10.01/)
-- The download link I then selected was the ``archlinux-2024.10.01-x86_64.iso``
-- After downloading the ISO, I loaded up VMWare and made a new VM, and selected `Linux Other`


# Part 2: Setup

- The first thing I did was use the command to get internet. Because I was in a VMWare, it would be as if I was using Ethernet. `ip link` was the command I used

- To set the computer time, I ran the command `timedatacl` But this did not set the time accoring to the proper time zone

- After was making the paritions for the VM in which I used the following commands:
-- `gdisk /dev/sda`
-- `n`
-- `+1M`
-- `ef02`
-- `n`
-- `w`
-- `mkfs.ext4 /dev/sda2`

- After making the needed partions, I the used the following command to add needed Linux firmware and some essential applications.
-- `pacstap -K /mnt base linux linux-headers dhcpcd nano grub vim`

- Generating an FSTAB file:
-- `genfstab -U /mnt >> /mnt/etc/fstab`

- Chroot 
-- Next command I did to get to the root was `arch-chroot /mnt`

- Setting Time
-- `ln -sf /usr/share/zoneinfo/America/Chicago /etc/localtime`
-- `locale-gen`

- Enable DHCP
--`systemctl enable dhcpcd`

- Setting Hostname and password
-- Here comes the more interesting part where now the root name and password can finally be set. To do this:
-- `/etc/hostname` - with desired hostname
-- `mkinitcpio -P`
-- `passwd` - to set the password of the root.

- Getting a desktop environment
-- `grub-install --target=i386-pc /dev/sda`
-- `grub-mkconfig -o /boot/grub/grub.cfg`

-- I decided on using gnome

-- `pacman -S gnome-shell mutter`
-- `systemctl enable --now gdm`






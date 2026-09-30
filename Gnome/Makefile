# Makefile for arch Linux ISO Build Let me be honest I no idea how the heck this works but I got the command anyway
#I thought it definitely doesn't need to be like this big I try to make the command smaller and it definitely breaks it so if it works it works i'm not going to touch it

.PHONY: all clean fix-config build

# Default target: fixes package lists/configs, cleans old builds, and builds the ISO
all: fix-config clean build

# Step 1: Apply all pacman, network, and package list fixes
fix-config:
	@echo "==> Applying configuration fixes..."
	@sed -i 's/^#DisableDownloadTimeout/DisableDownloadTimeout/' /etc/pacman.conf /root/Linux/Gnome/pacman.conf 2>/dev/null || true
	@sed -i 's/^#ParallelDownloads = 5/ParallelDownloads = 5/' /etc/pacman.conf /root/Linux/Gnome/pacman.conf 2>/dev/null || true
	@sed -i 's/Include = \/etc\/pacman.d\/chaotic-mirrorlist/#Include = \/etc\/pacman.d\/chaotic-mirrorlist/g' /root/Linux/Gnome/pacman.conf 2>/dev/null || true
	@sed -i 's/\[chaotic-aur\]/#\[chaotic-aur\]/g' /root/Linux/Gnome/pacman.conf 2>/dev/null || true
	@sed -i "s/bootmodes=(.*)/bootmodes=('bios.syslinux' 'uefi.grub')/g" /root/Linux/Gnome/profiledef.sh 2>/dev/null || true
	@sed -i 's/gearlever//g' /root/Linux/Gnome/packages.x86_64 2>/dev/null || true
	@sed -i 's/gnome-terminal-transparency//g' /root/Linux/Gnome/packages.x86_64 2>/dev/null || true

# Step 2: Clean working directories
clean:
	@echo "==> Cleaning work and out directories..."
	@rm -rf work/ out/

# Step 3: Run mkarchiso build
build:
	@echo "==> Building ISO with mkarchiso..."
	mkarchiso -v -w ./work -o ./out .

## 1. Remove X11VNC and Gnome-Connections

On Debian, your user, by default, is not on the sudoers file, so you will need to run these commands as root

```bash
apt purge x11vnc
```

```bash
apt purge gnome-connections
```

```bash
apt autoremove
```

## 2. Configure APT sources

```bash
mv /etc/apt/sources.list /etc/apt/sources.list.bkp
```

```bash
nano /etc/apt/sources.list
```

```text
deb https://deb.debian.org/debian/ trixie main contrib non-free non-free-firmware
#deb-src https://deb.debian.org/debian/ trixie main contrib non-free non-free-firmware

deb https://security.debian.org/debian-security trixie-security main contrib non-free non-free-firmware
#deb-src https://security.debian.org/debian-security trixie-security main contrib non-free non-free-firmware

deb https://deb.debian.org/debian trixie-updates main contrib non-free non-free-firmware
#deb-src https://deb.debian.org/debian trixie-updates main contrib non-free non-free-firmware

## Debian Trixie Backports
#deb https://deb.debian.org/debian trixie-backports main contrib non-free non-free-firmware
#deb-src https://deb.debian.org/debian trixie-backports main contrib non-free non-free-firmware
```

```bash
apt update && apt full-upgrade -y
```

## 3. Install firewall tools

```bash
apt install ufw gufw
```

## 4. Configure kernel swappiness values

```bash
nano /etc/sysctl.d/99-swappiness.conf
```

```text
# Controls the kernel tendency to move processes to swap space
# Lower value = more RAM usage and less disk usage (default: 60)
vm.swappiness=10

# Controls how aggressively the kernel reclaims inode/dentry cache
# Lower value = more cache kept = better disk performance (default: 100)
vm.vfs_cache_pressure=50
```

## 5. Create a Swap File

Check if a swap file or partition already exists

```bash
swapon --show
```

```bash
free -h
```

Create a swap file

```bash
fallocate -l 8G /swapfile
```

Set permissions so only root can read and write

```bash
chmod 600 /swapfile
```

Format the swap file

```bash
mkswap /swapfile
```

Activate the swap file

```bash
swapon /swapfile
```

Make the changes permanent

```bash
echo '/swapfile none swap sw 0 0' >> /etc/fstab
```

## 6. Install Kernel Headers

```bash
apt install linux-headers-amd64 linux-headers-$(uname -r)
```

## 7. Install Linux Firmware

```bash
apt install firmware-linux firmware-linux-nonfree
```

## 8. Install Applications

```bash
apt install curl
```

```bash
apt install git
```

- Postman
- Node.js
- PyCharm
- Visual Studio Code

## 9. Configure Git and GitHub

```bash
ssh-keygen -t ed25519 -C "user@example.com"
```

```bash
git config --global user.name "User"
```

```bash
git config --global user.email "user@example.com"
```

## 10. Configure Postman

```bash
tar -xzf postman.tar.gz -C /opt
```

```bash
ln -s /opt/Postman/Postman /usr/local/bin/postman
```

```bash
nano /usr/share/applications/postman.desktop
```

```text
[Desktop Entry]
Version=1.0
Type=Application
Name=Postman
GenericName=API Client
Comment=API Development Environment
Exec=/usr/local/bin/postman
Icon=/opt/Postman/app/resources/app/assets/icon.png
Terminal=false
Categories=Development;
StartupNotify=true
```

## 11. Add a Directory to the User's $PATH

Edit the file ~/.bashrc:

```bash
nano ~/.bashrc
```

Add the following line at the end of the file:

```text
export PATH="$PATH:/your/path"
```

Apply the changes:

```bash
source ~/.bashrc
```

## 12. Add a Directory to the System-Wide $PATH

Create a script in /etc/profile.d/:

```bash
nano /etc/profile.d/my-path.sh
```

Add the following line:

```text
export PATH="$PATH:/your/path"
```

Apply the changes:

```bash
source /etc/profile.d/my-path.sh
```

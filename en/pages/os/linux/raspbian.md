Raspbian Configuration
======================

# /etc/network/interfaces

change dhcp to static

address 192.168.0.6
netmask 255.255.255.0
network 192.168.0.0
broadcast 192.168.0.255
gateway 192.168.0.1


# change user

adduser <name>
usermod -a -G adm,dialout,cdrom,sudo,audio,video,plugdev,games,users,netdev,input,spi,gpio <name>

#Remove motd

echo " " | sudo tee /etc/motd

# Set up fsck on every boot
sudo tune2fs -c 1 /dev/mmcblk0p2

#Remove software you don't use

Sudo apt-get remove --purge wolfram* sonic-pi lxde* scratch*

#Add sources you will use

sudo echo "deb http://archive.raspbian.org/mate wheezy main" >> /etc/apt/sources.list #mate

sudo echo "deb http://repo.ajenti.org/debian main main debian" >> /etc/apt/sources.list.d/ajenti.list #ajenti
wget http://repo.ajenti.org/debian/key -O- | sudo apt-key add - #ajenti

## nzbget

gpg --recv-keys --keyserver keyserver.ubuntu.com 0E50BF67
gpg -a --export 0E50BF67 | sudo apt-key add -
echo "deb http://packages.unusedbytes.ca wheezy main" | sudo tee -a /etc/apt/sources.list

## xbmc

echo "deb http://archive.mene.za.net/raspbian wheezy contrib" | sudo tee -a /etc/apt/sources.list
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-key 5243CDED


#Add software you will use

## install unrar-nonfree

wget http://sourceforge.net/projects/bananapi/files/unrar_5.2.6-1.arm6_armhf.deb

sudo dpkg -i ./unrar_5.2.6-1.arm6_armhf.deb


sudo apt-get install ruby samba netatalk avahi-daemon avahi-discover libnss-mdns mate-core mate-desktop-environment ajenti python-pip python-dev libevent-dev nzbget tmux transmission-daemon git-core python-cheetah git dialog

pip install -U gevent
pip install greenlet==dev

git clone git://github.com/midgetspy/Sick-Beard.git

git clone git://github.com/petrockblog/RetroPie-Setup.git



## configure nzbget with defaults

sudo cp /usr/share/nzbget/nzbget.conf ~/.nzbget
sudo chown chrishewlings:root ~/.nzbget


## configure transmission

http://www.robertsetiadi.net/installing-transmission-in-raspberry-pi/


## set up avahi services

sudo cp ssh.service sftp.service /etc/avahi/services

## americanize that shit

- `sudo dpkg-reconfigure locales` and disable en_GB, enable en_US
- `sudo dpkg-reconfigure keyboard-configuration`
- `sudo dpkg-reconfigure tzdata`
- `sudo setupcon`
#### modify packages list
- replace `.uk` with `.us` in `/etc/apt/sources.list`

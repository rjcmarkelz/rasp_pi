# Raspberry Pi Install Commands and Tricks
## Use direct network connection

ip=10.0.1.10



# had a WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED! 
# this fixed the problem
http://blog.tinned-software.net/ssh-remote-host-identification-has-changed/http://pihw.wordpress.com/guides/direct-network-connection/


#2016-04-2
Downloaded fresh version of Raspbian
mv to clean /Desktop/
unzip to see .img file

##format drive
plug in sdhc card (anything over 32 GB is sdxc)-learned the hardway
diskutil list
view disks- mine was located at disk3
/dev/disk3  
You need to unmount these before preceding or it will not work!
capital D to unmount whole disk
diskutil unmountDisk /dev/disk3

[needs to be formatted as FAT32](http://superuser.com/questions/527657/how-do-you-format-a-2-gb-sd-card-to-fat32-preferably-with-disk-utility) 
sudo diskutil eraseDisk FAT32 RASPBIAN MBRFormat /dev/disk3

###load OS onto sd card
sudo dd bs=1m if=2016-03-18-raspbian-jessie.img of=/dev/rdisk3

sudo diskutil eject /dev/disk3

ip=169.254.1.2 in boot/cmdline.txt

## Set up Pi
Plug the SD card into the pi, along with a network cable directly into the router, and a 5V 1.5 Amp power supply. 

### Mac Terminal
See network, plug in Pi, wait 90 seconds to boot and then:
arp -a 
Will give you IP address of Pi
ssh pi@<ip address> 
password raspberry

[instructions here](https://www.raspberrypi.org/forums/viewtopic.php?t=74176)

### Once in the pi
pi@raspberrypi 
sudo raspi-config
Expand filesystem
Change Rootpassword
Finish and reboot

ssh back into the pi
sudo apt-get update
sudo apt-get upgrade

# VNC on Pi
[instructions](https://www.raspberrypi.org/documentation/remote-access/vnc/)
sudo apt-get install tightvncserver

make a server to connect to
vncserver :1 -geometry 1920x1080 -depth 24
set up passwords (8 characters)

# VNC on Mac
Already had this installed
Open VNC and vnc://<raspi ip address>:1
Works great!

#### all documentation that i looked up saved in chrome webbrowser

### update- ssh not working on 64 GB drive- host failure



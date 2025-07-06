## after install install ubuntu

update packages
обновить инфу о репоизитриях с пакетами

```
sudo apt update
```

обновит пакеты

```
sudo apt upgrade -y
```
#### nextcloud
Если nextcloud установлен в стоке, то перейди в папку /var/snap/nextcloud/45728/nextcloud/config и укажи в config.php в trusted_domains ip адрес роутера

## After extend the disk space in ProxMox

df -h
or
vgdisplay
info about the hard drives

For extend the disk with space what you add in ProxMox

1. type this command

   ```
   cf - disk
   ```

2. Point your main disk(sda3 or just the biggest one) and choose **resize** punct on botton panel
3. Point the extended disk and choose **write** punct on botton panel
4. type this command but for disk what ws extended(don't change it if you extend sda3). This command is made for extend the partition

   ```
   pvresize /dev/sda3
   ```

5) type this command for extend the volume
   ```
   lvextend -l +100%FREE /dev/ubuntu-vg/ubuntu-lv
   ```
6) type this for resize Root File System
   ```
   resize2fs /dev/mapper/ubuntu--vg-ubuntu--lv
   ```
7) Confirm Changes
   ```
   df-h
   ```

# USB(cool way)
//TODO Need to be extended and retested

For dawload it use
```
opkg install usbutils
```

For device status us 
```
lsusb
```
It shows Raw USB device list, Bus/Device numbers, Vendor:Product IDs (e.g., 13d3:3273) Device names
If you want to see USB port physical hierarchy by tree structure use
```
lsusb -t
```
it shows driver and in use(like rt2800usb), connection speeds (like 480M/5000M) and interface classes (like Class=Wireless)
# Just usefull commands

#### Show usb devices

install

```
sudo apt install usbview
```

open app in gui

```
sudo usbview
```

Make user access for folder in admin directory.($USER — reference of user)

```
sudo chown -R $USER:$USER /var/www/your_domain
```
For check is app active
```
sudo systemctl is-active 'service name'
```

For check app status

```
sudo systemctl status 'service name'
```

For start the stopped app

```
sudo systemctl start 'service name'
```

Change user

```
su - username
```

Delete user

```
sudo deluser --remove-home username
```
NextCloudAccess from web

Зайди в  ```/var/snap/nextcloud/45728/nextcloud/config``` и укажи в config.php в trusted_domains ip адрес роутера




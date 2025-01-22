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

For check app status

```
sudo systemctl status 'service name'
```

For start the stopped app

```
sudo systemctl start 'service name'
```

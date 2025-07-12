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

# Интересные факты

``$`` - обычный пользователь
``#`` - супер пользователь

## Команды и опции
При работе в командной строке, мы используем командный интерпретатор(Самый популярный - Bash), который интрепретирует команды в действия системы и действия системы в ответ.

Синтаксис команд в bash: команда -> опции -> аргументы.
Иногда для уменьшения вводимого текста используются длинные ключи (команда --слово) или короткие опции (команда -c). Например ``ls -l``. Список всех доступный опций команды можно получить, если ввести ключ ``команда --help``. Команды бывают обычными в встроенными в оболочку(их невозможно найти как программы на диске, но зато они доступны сразу после загрузки оболочки)
p.s. Длинные опции не могут содержать пробелов.

## Аргументы
Бывают аргументы команцы ``команда аргумент1 аргумент2)`` и аргументы опций/ключей ``команда --опция аргумент --опция аргумент``

## Документация
Вместе с пакетами программного обеспечения часто устонавливается документация, которая находится в каталоге ``/usr/share/doc``
**man** - это справочная система. Синтаксис выглядит так: ``man команда``. 
Вывод состоит из нескольких секций как:
``man [N] команда`` где 0 - файлы заголовков, 1 - команды оболочки, 2 - системные вызовы, 3 - библиотечные вызовы, 4 - специальные файлы, 5 - конфигурационные файлы, 6 - игры, 7 - соглашения, 8 - команды системного администрирования, 9 - ядро;
``Synopsis (Синтаксис)`` - показывает все доступные опции и маркирует обязательные(без скобок) и необязательные(в [])
``Description`` - полное описание команды.
``Options`` - список всех опций и описаний к ним.
``Files`` - список файлов, связанных с командой.(не всегда есть)
``See also`` - список связанных команд.
``Author`` - автор команды
## Работа с файлами
У команы ``ls`` есть опции ``d`` - информация о самом каталоге, ``-l`` - информация о байтах, ``-a`` - показать все файлы, ``-S`` - сортировка по размеру.

FHS (Filesystem Hierarchy Standard)
![resources/]()



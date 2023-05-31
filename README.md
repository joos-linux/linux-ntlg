# linux-ntlg
Linux command

### Основы
- man command
- command --help
- echo "text"
- cat file
- head file
- tail file
- grep
- less file
- pwd
- cd path
- mkdir dir
- ls (-l -a -h)
- ln (-s - symlink) - hard link
- cp file/dir (to) file/dir (-R -v)
- mv file/dir (to) file/dir (-v)
- rm file (-R -v)
- rmdir dir (-v)
- apt (update, upgrade, serch, install, remove, purge, autoremove)
- $PATH

### Процессы
- ps (-a)
- top
- pidstat (sudo apt install sysstat) - process monitoring - pidstat -p 1583(id) 1
- /proc - cataloge with sys statistic, processes, kernel parametr 
- cat /proc/cpuinfo
- cat /proc/version
- cat /proc/stat
- strace
- nice - sudo nice -n 13 nano
- renice - sudo renice 5 13111
- ls > file - output to file
- ls >> file - output add to file
- ls 1>file 2>error - ok to file, error to error
- ls 1>file 2>&1 > all to file
- | - pipe - ps aux | grep root
- kill -l
- sudo kill -pid- / sudo killall nano / sudo pkill -u user1
 
### Память
- lscpu
- dmidecode -t memory / dmidecode -t baseboard - hardware info
- cat /proc/meminfo
- top
- htop
- free -h
- sysctl -a | grep dirty - cache
- sync - write all cache to hdd
- swapon -s; grep Swap /proc/meminfo; free -h - show swap file
- mkswap /swapfile - make /swapfile swap
- swapoff\swapon /swapfile
- cat /etc/fstab - mounted device

### Дисковые системы
- cat /proc/devices - devices list
- ls -la /dev
- lsblk - list block devices
- lshw -short -C disk, hdparm -I /dev/sda, smartctl --all /dev/nvme0 - show info about hardware
- dmsetup ls - show device mapper devices
- lsblk
- blkid
- fdisk
- gdisk
- parted
- cat /proc/partitions
- RAID
```
sudo yum (apt-get) install mdadm
sudo mdadm --create /dev/md0 -l 1 -n 2 /dev/sd{b,c}
```
- cat /proc/mdstat - status
- /etc/mdadm.conf - config file
- LVM
- - pvcreate, vgcreate, lvcreate - create volume, volume group, logic volume
- - pvs, vgs, lvs - show volume, volume group, logic volume
- top
- iostat - disk monitoring
- iotop - process with disk
- vmstat 5 5 - show cpu, memory, disk

### Файловые системы
- cat /proc/filesystems - show filessytem
- fsck - errors check
- file -s /dev/sda1 - show filesystem type
- df -T - show filesystem type
- FAT (create FAT)
- - apt install dosfstools
- - fdisk /dev/sd*
- - mkfs.vfat -F 32 -n MyDrive /dev/sd*
- - fatresize -s /dev/sd*
- NTFS
- - apt install ntfs-3g
- - mount -t ntfs-3g /dev/sdb1 /mnt - mount ntfs
- Ext4
- - mkfs -t ext4 /dev/hdb1 - create ext4 in /dev/hdb1
- XFS
- - mkfs.xfs /dev/sda1
- - xfs_growfs / -d
- - xfs_info /dev/sda1
- - xfs_check /dev/sdb1, xfs_repair /dev/sdb1
- Btrfs
- - mkfs.btrfs /dev/sdc -L single_drive - create only 1 hdd
- - mkfs.btrfs /dev/sdc /dev/sdd -L double_drive - create with 2 hdd
- - sudo mkfs.btrfs /dev/sdc /dev/sdd -d raid1 -m raid1 -L raid1_drive - raid with btrfs
- - btrfs filesystem df / - info
- - btrfs filesystem resize -2g /mnt - change size
- /etc/fstab - how to mount - what (UUID) where (path) type(ext4) option(defaults) backup(0) check(1)
-  systemctl list-units -t mount --all - show all mounted
-  systemctl edit --full boot.mount - write to file
-  mount - show all mounted
-  - mount -t ext4 -o noexec /dev/sdb6 /mnt
-  - mount --uuid="b386d319-05c2-42c8-8364-8d37280b69e0" /mnt
-  - mount --label="home" /mnt/
-  - umount /mnt
-  stat file - info about file
- df -i
- ls -i
- file -s /dev/sda3

### Ядро
- /lib/modules/
- lsmod - info about all modules
- insmod - /lib/modules/modulename.ko - load with insmod
- modprobe module-name - load module
- modinfo module-name - info about module
- rmmod module-name
- strace command
- DKMS (Dynamic Kernel Module Support) - add my module to kernel
- - dkms add -m module-name
- - dkms status
- - dkms build -m module-name -v module-version
- - dkms install -m module-name -v module-version
- - dkms autoinstall
- /etc/modules - ubuntu file for modules


### Загрузка
- /boot/grub/grub.cfg — Debian, Ubuntu
- /boot/grub2/grub.cfg — Red Hat, CentOS
- update-grub/grub2-mkconfig
- sudo nano /etc/default/grub - for change
- sudo update-grub
- shutdown -r now
- cat /proc/cmdline - shov info about system
- sysctl -a - kerner param
- cat /etc/sysctl.conf | more - config file
- cat /etc/sysctl.conf | grep ipv4 - ipv4
- sudo sysctl net.ipv4.ip_forward=1 - make gateway
- /sbin/init - process/daemon manage all
- systemd - modern process manage all
- systemctl get-default
- systemd module
- - /usr/lib/systemd/system/ – модули из пакетов (Nginx, Apache,MySQL)
- - /run/systemd/system/ — модули, созданные во время работы ОС
- - /etc/systemd/system/ — модули, созданные пользователем
- systemd-analyze plot > test.svg
- sudo systemctl list-dependencies
- systemctl list-units — список модулей
- systemctl list-units --type=service — список модулей-служб
- systemctl status module — состояние выбранного модуля
- systemctl enable\disable module — разрешить/запретить модуль
- systemctl start\stop\restart module — запустить/остановить/модуль
- systemctl daemon-reload — перезапуск конфигурации systemd
- journalctl
- nano /etc/systemd/journald.conf
- journalctl --since=yesterday --until=now

### Управление пакетами
- apt install
- apt update
- apt upgrade
- apt search -pattern-
- apt show -packet_name-
- apt list -
--installed
--upgradeable
--all-versions
- apt remove <packet_name>
- apt purge <packet_name> 
- apt reinstall <packet_name>
- apt autoremove 
- apt -f install 
- yum update
- yum update <packet_name>
- yum downgrade <packet_name>
- yum search <pattern>
- yum list
 -- installed
 -- available 
 -- all 
 - yum install <packet_name>
 - yum remove <packet_name>
 - yum reinstall <packet_name>
 - yum autoremove
 - yum clean packages
 

# linux-ntlg
Linux command

### Основы
- bin - исполняемые файлы
- lib - библиотеки
- etc - конфигурационные файлы
- home - домашний каталог
- dev - представление устройств (нет на диске)
- proc - представление процессов (нет на диске)
- sys - представление системных параметров и состояний (нет на диске)
- tmp - временные файлы и директории (доступ есть у всех)
- usr - допольнительная иерархия
- var - различные изменяющиеся файлы (логи, кэш)
- opt - самостоятельные иерархии каталогов
- . - текущая директория (есть во всех директориях)
- .. - директория уровнем выше (есть во всех директориях)
- ~ - домашняя директория
- man команда - описание команды
- команда -h - описание команды
- echo "text" - вывести  текст в консоль
- cat file - выводиь содержимое файла
- head file - показать первые 10 строк файла
- tail file - показать последние 10 строк файла
- grep условие [цель] — вывести строки, содержащие условие
- less file - интерактивный просмотр текста
- hostnamectl - информация о системе
- Поток номер 0 (STDIN)
- Поток номер 1 (STDOUT)
- Поток номер 2 (STDERR)
- pwd -  вывести рабочую директорию
- cd путь - перейти в каталог
- mkdir dir -  создать каталог
- ls (-l -a -h) - просмотр содержимого каталога
- ln (-s - symlink) - hard link
- cp file/dir (to) file/dir (-R -v) - копирует источник в цель
- mv file/dir (to) file/dir (-v) - перемещает исходный файл в целевой
- rm file (-R -v) - удалить файл
- rmdir dir (-v) - удалить пустую директорию
- apt (update, upgrade, serch, install, remove, purge, autoremove)
- $PATH - путь содержит все директории, где интерпретатор командной строки ищет команды.
- **dmesg** - процесс загрузки системы
- .bashrc - настройки баш - можно дописать синоним


### Процессы
**Процесс** - Программа во время выполнения или Сущность, представляющая понятие активности/работы с точки зрения операционной системы
- ps aux (PID - идентификатор, TTY - устройство на котором запущен, STAT - статус, TIME - время CPU использованное процессом, COMMAND - команда запуска, START - время запуска)
- STAT (R — выполняется, D — uninterruptable sleep (ожидает ввод-вывод), S — interruptable sleep, I — idle (бездействует > 20 секунд), T — приостановлен, Z — зомби, W — выгружен на диск (swap file), < — имеет повышенный приоритет, N — имеет пониженный приоритет, L — страницы заблокированы в ядре, s — лидер сеанса (например, консоль))
- top
- **pidstat (sudo apt install sysstat) - pidstat -p 1583(id) 1** - показывает через 1 секунду процесс
- /proc - cataloge with sys statistic, processes, kernel parametr 
- cat /proc/cpuinfo - информация о CPU
- cat /proc/version — версия Linux
- cat /proc/stat - cистемная статистика
- **strace** - нужен для отладки - отображает каждый системный вызов, выполненный процессом и каждый полученный сигнал - подключается по PID и показывает в реальном времени (если без параметров)
- strace echo 1 - системный вызов echo 1
- PID / PPID - уникальный идентификатор процесса / идентификатор родительского процесса
- UID / EUID - дентификатор пользователя, создавшего данный процесс / текущий идентификатор пользователя процесса
- nice (-20 ... 19) - число, показывающее, какая часть процессорного времени может быть выделена (ядром) для процесса. Т.е. это пользовательский приоритет, который отличается от приоритета планировщика. По умолчанию, наследуется от родительского процесса
- nice - sudo nice -n 13 nano
- [command] & - фоновый процесс (отображается но не блокирует консоль) - pidstat -p 1 -t 1 &
- fg - возвращает фоновый процесс в нормельное состояние, после чего его можно завершить
- renice - sudo renice 5 13111
- ls > file - вывод в новый файл
- ls >> file - дополнение к существующему файлу
- ls 1>file 2>error - запись потоков вывода и ошибок в разные файлы
- ls 1>file 2>&1 > запись потоков вывода и ошибок в один и тот же файл
- | - pipe - ps aux | grep root
- Сигнал (signal) — уведомление процесса о каком-либо событии
- kill -l - набор сигналов
- dd - копировать побайтово
- dd if=/dev/urandom of=/dev/null bs=100M count=5  - bs - размер куска, count - сколько раз
- pgrep - грепаем id процесса можно регуляркой - pgrep "^dd$"
- kill (-10) -SIGUSR1 3830239(PID) - вернят прогресс по процессу
- kill (-2) -SIGINT 3830239(PID) - запрос на завершение текущей операции (CTRL-C)
- kill -9 (-KILL) PID - завершает процесс на уровне ядра. Не блокируется
- kill -15 (-TERM) PID - запрос на завершение программы
- sudo kill -pid- / sudo killall nano / sudo pkill -u user1
- Потоки (нити, threads) — программно выделенные части одного процесса, использующие его ресурсы совместно
- **ps m** - просмотр потоков
- **ps -eLf** - просмотр потоков


### Память
**RAM** (Random Access Memory, память с произвольным доступом) или ОЗУ (Оперативное Запоминающее Устройство) — энергозависимая память с произвольным доступом к ячейкам RAM, ОЗУ — энергозависимое запоминающее устройство, в котором во время работы компьютера хранится исполняемый код и входные/выходные данные.

**ROM** (Read Only Memory, память только для чтения) или ПЗУ (постоянное запоминающее устройство) — энергонезависимая память для хранения массива неизменяемых данных

**SRAM**(Static RAM) — cтатическая память с произвольным доступом

**DRAM** (Dynamic RAM) — динамическая память с произвольным доступом

**UMA** (Uniform Memory Access, равномерный доступ к памяти): все процессоры имеют доступ к совместно используемой памяти через общую шину;

**NUMA**(Non-Uniform Memory Access, неравномерный доступ к памяти): для каждого процессора существует отдельный локальный модуль памяти, к которому он может обращаться напрямую.

- **lscpu** - позволяет отобразить информация о процессоре
- **dmidecode** -t memory / dmidecode -t baseboard - позволяет получить информацию о комплектующих ПК
- cat /proc/meminfo - позволяет в режиме чтения узнать большинство текущих настроек операционной системы (x86)

**Виртуальная память** - Абстракция, которая позволяет выполнять программы, требующие больше оперативной памяти, чем имеется в компьютере, путём автоматического перемещения частей программы между основной памятью и другими хранилищами.

**Организация виртуальной памяти**
- Страничная — адресное пространство делится на части одинакового фиксированного размера, называемые виртуальными страницами. Адрес задается номером страницы в виртуальной памяти и смещением внутри страницы
- Сегментная — адресное пространство делится на части, называемые сегментами, размер которых определяется смысловым значением содержащейся в них информации. Виртуальный адрес задается номером сегмента и смещением внутри сегмента

- top - отображает потребление ресурсов процессами в реальном времени (и другую информацию)
- htop - та же утилита с псевдографическим интерфейсом
- free -h - утилита для отображения состояния памяти
- cat /proc/meminfo - раздел файловой системы /proc с текущей информацией о состоянии памяти в операционной системе.

**Cache** — промежуточный буфер с быстрым доступом для хранения информации, которая с большой вероятностью будет запрошена.

**TLB** — это специальный кэш, который хранит соответствие страниц в виртуальной и физической памяти, которые с наибольшей вероятностью будут запрошена.

**MMU** — компонент аппаратного обеспечения компьютера,отвечающий за управление доступом к памяти

**Кэш-память** — сверхбыстрая память используемая процессором, для временного хранения данных, которые наиболее часто используются.

- **sysctl -a | grep dirty** - найти в настройках Linux параметры, которые используются при кэшировании (“грязные” страницы).
- sync - команда заставляет Linux записать все кэшированные данные на диск
- echo 2 > /proc/sys/vm/drop_caches — очистка inode и dentrie
- **swapon -s**; grep Swap /proc/meminfo; free -h - команды показывают использование файла подкачки
- mkswap /swapfile - размечает файл /swapfile как файловую систему swap
- swapoff\swapon /swapfile - отключение/подключение файла подкачки в систему
- cat /etc/fstab - выводит список устройств для монтирования. Можно приписать swap раздел
- /proc/sys/vm/vfs_cache_pressure — размер дискового кэша
- /proc/sys/vm/swappiness — процент переноса данных в swap


### Планировщик задач
**Планировщик** (шедулер, англ. scheduler) — часть операционной системы, ответственная за распределение ресурсов компьютера между рабочими юнитами (процессами, потоками, пользователями и т. д.)
- невозможно узнать, когда завершится программа;
- программа может зависнут, а процессор не знает о времени;
- используем аппаратные прерывания.

Программно невозможно понять, что прошло какое-то время. Остаётся использовать аппаратные прерывания. Используем аппаратные прерывания от контроллера прерываний периферии, в частности — timer.
- Многозадачность
- нужно делить время работы на процессоре (Процент времени процесса = Приоритет ÷ Сумма приоритетов)
- как справедливо поделить время на процессоре? (Чтобы никто не забирал больше, чем надо, но получал достаточно.)
- сама система распределения не должна быть дорогой
- Кооперативная многозадачность - Процессы сами по доброй воле (вызовом специальной команды) отдают управление (простота, скорость, низкая отзывчивость, зависания)
- Вытесняющая многозадачность - Планировщик (по таймеру) останавливает текущий процесс и передаёт управление другому (прогнозируемая отзывчивость, независимость процессов, схожая скорость число-дробилок, дороже)
- С помощью утилиты **taskset** можно задавать, на каких процессорах будет исполняться программа или менять по PID
```
$ time taskset 1 ./a.out
real 0m1,372s - реальное время
user 0m1,368s - сумма времени с каждого процессора (тут 1)
sys 0m0,005s - системное время
$ time ./a.out
real 0m5,007s - реальное
user 0m39,886s - все процессоры (теряемя время на записи кэша в RAM)
sys 0m0,004s
```
- **vmstat 5 1** - предоставляет краткую информацию о различных ресурсах системы и связанных с ними неполадках, приводящих к снижению производительности

**Procs**(vmstat)
- r: количество запущенных процессов (работающих или ожидающих выполнения).
- b: количество спящих процессов.

**Memory**(vmstat)
- swpd: объем используемой виртуальной памяти.
- free: объем свободной памяти.
- buff: количество памяти, используемой в качестве буферов.
- cache: объем памяти, используемой в качестве кеша.
- inact: количество неактивной памяти (опция -a).
- active: количество активной памяти. (опция -a)

**Swap**(vmstat)
- si: объем памяти, выгруженный с диска (/s).
- so: объем памяти, перенесенный на диск (/s).

**IO**(vmstat)
- bi: блоки, полученные от блочного устройства (blocks/s).
- bo: блоки, отправленные на блочное устройство (blocks/s).

**System**(vmstat)
- in: количество прерываний в секунду, включая часы.
- cs: количество переключений контекста в секунду.

**CPU**(vmstat) Здесь проценты от общего времени процессора.
- us: время, потраченное на запуск кода, не относящегося к ядру (время пользователя).
- sy: время, потраченное на выполнение кода ядра (системное время).
- id: время бездействия. До версии Linux 2.5.41 это включает время ожидания ввода-вывода.
- wa: время, проведенное в ожидании ввода/вывода. До Linux 2.5.41, включено в idle.
- st: время, украденное из виртуальной машины. До Linux 2.6.11 неизвестно.
   
- nice -n {приоритет} {программа} {аргументы}
- sudo nice -n — если приоритет меньше 0
- renice -n {приоритет} PID — для уже запущенного процесса
- renice -n -g -u — для запущенной группы процессов, для пользователя
- **ps ax -o pid,ni,cmd** — чтобы посмотреть nice запущенных процессов

**CFS планировщик**
- храним не процессы, а sched_entity — планировщик может рассчитывать время, например, для пользователей;
- все sched_entity лежат в бинарном сбалансированном дереве, отсортированном по оставшемуся времени исполнения и имеет сложность O(logN);
- CFS планировщик более справедлив — при равном приоритете задачи будут получать более равные кванты, чем в O(1);
- Работает сразу на все процессоры — нет проблемы с локальными spinlock-ами.


### Дисковые системы
- **SCSI** (Small Computer System Interface) – это интерфейс, предназначенный для объединения на одной шине устройств различных классов: жестких дисков, CD-ROM, приводов CD, DVD, стримеров, сканеров, принтеров и т. д.
- **PATA** (Parallel Advanced Technology Attachment) или IDE (Integrated Drive Electronics) – параллельный интерфейс подключения накопителей (гибких дисков, жёстких дисков и оптических дисководов) к компьютеру
- **SATA** (Serial ATA) – последовательный интерфейс обмена данными с накопителями информации. SATA является развитием параллельного интерфейса ATA (IDE)
- **Serial Attached SCSI** (SAS) – последовательный компьютерный интерфейс, разработанный для подключения различных устройств хранения данных, например, жёстких дисков и ленточных накопителей. SAS разработан для замены параллельного интерфейса SCSI и основывается во многом на терминологии и наборах команд SCSI. SAS обратно совместим с интерфейсом SATA: устройства 3 Гбит/с и 6 Гбит/с SATA могут быть подключены к контроллеру SAS, но не наоборот
- **Peripheral Component Interconnect Express** (PCI Express, PCIe) — последовательный высокопроизводительный интерфейс для передачи данных. Имеет несколько видов разъемов для подключения различного оборудования, в том числе разъем M2 для подключения запоминающих устройств
- **Fibre channel** (волоконный канал) — семейство протоколов для высокоскоростной передачи данных.
- **Fibre Channel Protocol** (FCP) — транспортный протокол (как TCP в IP- сетях), инкапсулирующий протокол SCSI по сетям Fibre Channel. Является основой построения сетей хранения данных.
- **DAS** – блочное устройство с диска, который физически, напрямую, подключен к хост-машине. Необходимо поместить на нее файловую систему, прежде чем ее можно будет использовать. Технологии для этого включают IDE, SCSI, SATA и т.д.
- **SAN** – блочное устройство, которое доставляется по сети. Как и DAS, вы все равно должны разместить на нем файловую систему, прежде чем она сможет использоваться. Технологии для этого включают FibreChannel, iSCSI, FoE и т. Д.
- **NAS** – файловая система, доставляемая по сети. Технологии для этого включают NFS, CIFS, AFS и т.д.
- **СХД** (сеть хранения данных, SAN, storage area network) – архитектурное решение для подключения внешних устройств хранения данных (дисковые массивы, ленточные библиотеки) к серверам таким образом, чтобы операционная система распознала подключённые ресурсы как локальные
- cat /proc/devices - отображает список устройств, опознанных ядром
- ls -la /dev - каталог специального назначения, который содержит файлы устройств
- lsblk - list block devices
- **lshw -short** -C disk, hdparm -I /dev/sda, smartctl --all /dev/nvme0 - утилиты, которые отображают информацию об имеющихся дисках с точки зрения железа
- **stat /dev/sda** - информация о устройстве

**Виртуальная файловая система** (англ. virtual file system — VFS) - это абстрактный уровень поверх конкретной реализации файловой системы. Она используется для доступа к локальным файловым системам(ФС) (fat32, ext4, ntfs), сетевым ФС(nfs), а также к устройствам, не предназначенным для хранения данных (procfs). VFS предоставляет единообразный доступ клиентских приложений к различным типам файловых систем. VFS декларирует программный интерфейс между ядром и конкретной файловой системой, таким образом, для добавления поддержки новой файловой системы не требуется вносить изменений в ядро операционной системы

**Device mapper** - Подсистема ядра Linux, которая позволяет мэппить одно блочное устройство на другое или несколько других. Это позволяет реализовать объединение нескольких реальных устройств в одно виртуальное, создавать snapshot’ы, организовывать балансировку между устройствами, делать шифрованные тома и т.д. Через device-mapper, в качестве низкоуровнего API, работают LVM, cryptsetup, dm-multipath и другие утилиты

- dmsetup ls - отображает список устройств, созданных с помощью device mapper
- /dev/mapper/vgdata-lvdata – ссылки на устройства, созданные device mapper
- dev/dm-0, /dev/dm-1 – устройства которые создаются device mapper

**Раздел** — часть долговременной памяти жёсткого диска или флеш- накопителя, выделенная для удобства работы, и состоящая из смежных блоков. На одном устройстве хранения может быть несколько разделов

**Использование разделов дает возможность:**
- хранить информацию в разных файловых системах, или в одинаковых файловых системах, но с разным размером кластера;
- на одном жёстком диске можно установить несколько операционных систем

**MBR** (Master Boot Record, главная загрузочная запись) содержит сведения о структуре жесткого диска и код для запуска операционной системы

![mbr](https://github.com/joos-linux/linux-ntlg/blob/main/mbr.png)

**GUID** (Globally Unique Identifier) Partition Table (GPT) — стандарт формата размещения таблиц разделов на физическом жестком диске. Является частью расширяемого микропрограммного интерфейса, Extensible Firmware Interface, EFI.

![gpt](https://github.com/joos-linux/linux-ntlg/blob/main/gpt.png)

- **lsblk** – утилита выводит список блочных устройств с информацией о них
- **blkid** – утилита отображает информацию об уникальных идентификаторах блочных устройств
- **fdisk** – утилита позволяет управлять разделами с разметкой MBR
- fdisk /dev/sdb  | o - DOS, g - gpt,  n - add partition, d - delete
- gdisk – утилита позволяет управлять разделами с разметкой GPT
- parted – утилита позволяет управлять разделами с разметкой MBR и GPT. В отличие от gdisk и fdisk изменения применяются сразу, не требуя подтверждения
- cat /proc/partitions – вывести список разделов
- **RAID** (Redundant Array of Independent Disks, избыточный массив независимых дисков) — технология виртуализации данных, которая объединяет несколько дисков в логический элемент для повышения производительности и отказоустойчивости
- **RAID 0** (striping, чередование) — дисковый массив из двух или более жёстких дисков без резервирования. Информация разбивается на одинаковые по длине блоки, а затем записывается поочерёдно на каждый диск в структуре. Основное предназначение такой системы — увеличение производительности, при этом вам будет доступен полный объем всех дисков. Если один диск выходит из строя, все данные становятся недоступными
- **RAID 1** (mirroring, зеркалирование) — массив из двух или более дисков, являющихся полными копиями друг друга. Обеспечивается бесперебойность работы, даже если один из дисков выйдет из строя. Производительность остается на прежнем уровне, объем равен меньшему из дисков в массиве
- **RAID 5** - Данные записываются на все диски в томе и в блок четности
для каждого блока данных. Если один физический диск выходит из строя, данные из неисправного диска можно восстановить на запасной диск. Данные сохраняются при выходе из строя одного диска, но в случае выхода из строя второго диска до того, как данные смогли быть восстановлены на запасной диск, все данные будут утеряны. Для создания тома RAID 5 требуется минимум три диска
- **RAID 10** - В режиме RAID 10 сочетаются защита режима RAID 1 и
производительность режима RAID 0. При использовании четырех дисков в режиме RAID 10 создается два сегмента RAID 1, которые объединяются в страйп RAID 0. При использовании восьми дисков в страйпе RAID 0 будет уже четыре сегмента RAID 1. В режиме RAID 10 могут выйти из строя до 2х дисков в двух сегментах RAID 1
```
sudo yum (apt-get) install mdadm — установка утилиты
sudo mdadm --create /dev/md0 -l 1 -n 2 /dev/sd{b,c} — создание нового массива
```
- cat /proc/mdstat - текущее состояние
- /etc/mdadm.conf - файл конфигурации

**LVM** - (Logical Volume Manager, Менеджер логических томов) — это дополнительный слой абстракции между «железом» и файловой системой, позволяющий использовать разные области одного жёсткого диска и/или области с разных жёстких дисков как один логический том

**Преимущества LVM**
- легко изменять размер логических томов,
- можно объединять несколько физических устройств в один логический пул,
- возможное количество логических томов намного превышает возможности традиционного деления диска на разделы,
- с помощью снэпшотов можно делать бэкапы логических томов.
- **pvcreate, vgcreate, lvcreate** - create volume, volume group, logic volume
- **pvs, vgs, lvs** - show volume, volume group, logic volume
- top — выводит информацию о работающих в системе процессах и информацию о них
- **iostat** - мониторинг использования дисковых разделов
- **iotop** - аналогична утилите top, но вместо использования процесами CPU и памяти показывает работу процессов с дисками
- **vmstat 5 5** - утилита отображает информацию об использовании CPU, памяти, дисков
- **sar -p -d 5 3** - утилита для отображения различных параметров
(статистики) работы системы


### Файловые системы
- Часть операционной системы,которая устанавливает физическую и логическую структуру файлов на разделе или диске, управляет созданием и изменением файлов и сопутствующих данных. В Linux на каждый раздел можно установить свою ФС, которая отвечает за порядок и способ организации информации.
- **Функции файловых систем** - размещение и упорядочивание на носителе данных в виде файлов; - создание, чтение и удаление файлов; - назначение и изменение атрибутов файлов; - защита файлов при системном сбое; - защита файлов от несанкционированного доступа; - поиск файлов
- **cat /proc/filesystems** - вывести список файловых систем, которые поддерживаются ядром
- fsck - утилита, с помощью которой можно проверить ФС на ошибки
- **file -s /dev/sda1** - выводит тип файловой системы
- **df -T** - выводит тип файловой системы
- 
**Журналирование** - в том или ином виде применяется практически во всех современных файловых системах. При использовании журналирования файл сначала записывается в журнал («лог»). После этого файл записывается на жесткий диск, а потом удаляется из журнала, после чего операция записи считается завершённой. Если во время записи выключилось питание, то после включения системы файловая система может проверить журнал и найти незавершённые операции.

**Extent** - В традиционных файловых системах заголовки(inode) указывают на отдельные блоки . В файловых системах с поддержкой экстентов используются указатели не на блоки, а на экстенты - непрерывные области носителя информации.

**COW(Copy-On-Write - копирование при записи)** - механизм для оптимизации различных процессов в операционных системах. Идея подхода copy-on-write заключается в том, что при чтении области данных используется общая копия, в случае изменения данных — создается новая копия.

**FAT** (File Allocation Table, таблица размещения файлов) – файловая система, которая использовалась в операционной системе DOS. В файловой системе FAT дисковое пространство логического
раздела делится на три области: зарезервированная, системная и область данных
- Команды для создания FAT
```
apt install dosfstools
fdisk /dev/sd*
mkfs.vfat -F 32 -n MyDrive /dev/sd*
fatresize -s /dev/sd*
```
**NTFS** (new technology file system, «файловая система новой технологии») — стандартная файловая система для семейства операционных систем Windows NT.
- - apt install ntfs-3g
- - mount -t ntfs-3g /dev/sdb1 /mnt - mount ntfs

**Ext4** — является развитием Ext2 и Ext3. Самая популярная, “файловая система по умолчанию” в Linux. В отличие от Ext3 введен механизм пространственной (extent) записи файлов, уменьшающего фрагментацию и повышающего производительность.
- - mkfs -t ext4 /dev/hdb1 - создания ext4 на разделе /dev/hdb1

**XFS** - высокопроизводительная 64-битная журналируемая файловая система.
- - **mkfs.xfs /dev/sda1** - содание файловой системы
- - xfs_growfs / -d - увеличивает файловую систему на все доступное пространство
- - xfs_info /dev/sda1 -  - выводит информацию про метаданные файловой системы
- - xfs_check /dev/sdb1, xfs_repair /dev/sdb1 -  - проверяет файловую систему на ошибки

**Btrfs** - (B-tree FS) — файловая система для Linux, основанная на структурах B-деревьев и работающая по принципу «копирование при записи» (copy-on-write)
- - mkfs.btrfs /dev/sdc -L single_drive - создание ФС на одном диске
- - mkfs.btrfs /dev/sdc /dev/sdd -L double_drive - оздание ФС на двух дисках
- - sudo mkfs.btrfs /dev/sdc /dev/sdd -d raid1 -m raid1 -L raid1_drive - создать рейд средствами btrfs
- - btrfs filesystem df / - получить информацию о ФС
- - btrfs filesystem resize -2g /mnt - изменить размер тома в реальном времени

**NFS (Network File System, сетевая файловая система)** — протокол сетевого доступа к файловым системам. Позволяет пользователям подключать удаленные сетевые каталоги к своей системе и передавать файлы между серверами.
- **/etc/fstab** - конфигурационный файл, содержащий инструкции по монтированию блочных устройств, NFS-ресурсов и псевдо-файловых систем в пространство файловых имен и областей подкачки страниц - что монтируем (UUID) куда монтируем (path) тип(ext4) опции(defaults) индикатор необходимости делать резервную копию(0) порядок проверки раздела(1)
- **mount -a** - проверка корректности /etc/fstab
- Автоматическое монтирование autofs - Может быть реализовано с помощью пакета autofs и позволяет автоматически подключать различные ресурсы (сетевые устройства, жесткие диски) в начале их использования и отключать при прекращении использования
- apt-get install autofs – установка пакета
- man auto.master –получение справки по пакету
- systemctl list-units -t mount --all - вывести состояние всех описаных в systemd точек монтирования
- systemctl edit --full boot.mount - открыть на редактирование unit- файл
- mount - show all mounted
- - mount -t ext4 -o noexec /dev/sdb6 /mnt
- - mount --uuid="b386d319-05c2-42c8-8364-8d37280b69e0" /mnt
- - mount --label="home" /mnt/
- - umount /mnt

**Типы файлов в линукс**
- Обычные файлы ( - ) (регулярные) – любые текстовые, исполняемые, библиотечные, графические файлы
- Каталоги ( d ) – хранят именованные ссылки (только ссылки, но не сами файлы) на другие файлы
- Символьные ссылки ( l ) – файл с текстовой строкой, которая представляет собой путь к самому файлу
- Сокеты ( s ) и каналы ( p ) – файлы, которые используются для взаимодействия между различными процессами
- Файлы блочных ( b ) и символьных ( c ) устройств – используются для взаимодействия с внешними устройствами
- mkfifo mypipe - создает pipe - канал - можно в него отправлять и из него брать информацию
- Жесткие ссылки - Не является отдельным типом файла, Существует в рамках одной ФС, Представляет собой второе имя файла, Не может указывать на каталог, При удалении уменьшается счетчик жестких ссылок(если 0 - то сам файл)
- Символические ссылки - Является отдельным типом файла, Может ссылаться на другие разделы и ФС, Представляет собой ссылку или ярлык на файл, Может указывать на каталог, При удалении - удаляется файл-ярлык
- Inode (index-node, индекс-узел, индексный дескриптор) — структура данных в ФС, в которой хранится метаинформация о файлах каталогах и т.д
- информации в inodes: - размер файла; - идентификатор (ID) устройства, содержащего файл; - ID пользователя-владельца файл; - указатели на блоки (кластеры) диска, в которых размещён файл; - количество блоков, занимаемых файлом
- В ext2,3,4 - заканчиваются, в xfs, btrfs - они inods динамические
- stat file - информация о файле
- **df -i** - все inods в разделах - сколько используется и сколько осталось
- **ls -i** - inods текущего каталога
- file -s /dev/sda3 - покажет файловую систему раздели и другую информацию о разделе


### Ядро
**Монолитные ядра** – все функции операционной системы загружены в единый файл и выполняются в качестве одного процесса в одном адресном пространстве.

**Микроядра** – все функции ядра разделяются на несколько процессов, которые обычно называют серверами. Все серверы поддерживаются независимыми друг от друга и выполняются каждый в своем адресном пространстве.

**Гибридные ядра** – различные комбинации, совмещающие оба вышеуказанных подхода.

- На сегодняшний день Linux — монолитное ядро с поддержкой загружаемых модулей.
- Драйверы устройств и расширения ядра обычно запускаются в нулевом кольце защиты, с полным доступом к оборудованию.
- Все драйверы и подсистемы работают в своем адресном пространстве, отделенном от пользовательского.
- В отличие от обычных монолитных ядер, драйверы устройств легко собираются в виде модулей и загружаются или выгружаются во время работы системы.
- /lib/modules/
- **lsmod** - info about all modules
- insmod - /lib/modules/modulename.ko - load with insmod
- modprobe module-name - load module
- modinfo module-name - info about module
- rmmod module-name

**Подсистемы ядра:**
- Process Scheduler (SCHED) — планировщик процессов, отвечает законтроль над доступом процессов к CPU;
- Memory Manager (MM) — менеджер памяти, обеспечивает различным процессам безопасный доступ к основной памяти системы;
- Virtual File System (VFS) — виртуальная файловая система, создает абстрактный слой, скрывая детали оборудования, предоставляя общий файловый интерфейс для всех устройств
- Network Interface (NET) — сетевые интерфейсы, обеспечивает работу с различными сетевыми стандартами и сетевым оборудованием;
- Inter-Process Communication (IPC) — межпроцессная подсистема, поддерживающая несколько механизмов для process-to-process связей в единой Linux-системе.

**Планировщик процессов** — основная подсистема. Все остальные зависят от нее, так как всем им необходимо приостанавливать и возобновлять выполнение процессов.
- Выполнение в режиме ядра - Передача ядру контроля над процессом для выполнения необходимой задачи. Например, открытие файла или передачи данных по сети. Существует 2 события, при которых выполнение переходит в режим ядра:
- системные вызовы - Поступают от пользовательских программ и касаются работы с устройствами, памятью и т.п. Системный вызов — обращение прикладной программы к ядру операционной системы для выполнения какой-либо операции
- аппаратные прерывания - Сигнализируют об окончании какого-либо действия со стороны устройства или о возникшей на устройстве ошибке. - Когда CPU получает прерывание, он останавливает любые процессы - Если это не более приоритетное прерывание, тогда обработка пришедшего прерывания произойдет только тогда, когда более приоритетное будет завершено. - Сохраняет некоторые параметры в стеке. - Вызывает обработчик прерывания
- strace command

**Dynamic Kernel Module Support (DKMS)** — это фреймворк, который используется для генерации тех модулей ядра Linux, которые в общем случае не включены в дерево исходного кода.
- DKMS позволяет драйверам устройств автоматически пересобираться, когда ядро уже установлено. Пользователь может не ждать, пока какая-то компания, проект или сопроводитель пакета выпустит новую версию модуля. Значительное число модулей, не включенных в ядро, имеют DKMS вариант; некоторые из них размещаются в официальных репозиториях.
- - dkms add -m module-name
- - dkms status
- - dkms build -m module-name -v module-version
- - dkms install -m module-name -v module-version
- - dkms autoinstall
- Автозагрузка модулей - Для автоматической загрузки модулей в разных дистрибутивах предусмотрены разные механизмы.
- Ubuntu: файл /etc/modules
- CentOS: /etc/modules-load.d/*.conf
- В этих файлах преимущественно перечисляются альтернативные имена модулей, их параметры, применяемые при их загрузке, а также черные списки, запрещенные для загрузки.


### Загрузка
**Загрузка (boot, booting)** — процесс запуска устройства и загрузки ОС. В этот момент происходит обнаружение и (само)настройка всех компонентов системы

**Этапы загрузки**
- Загрузка BIOS/UEFI (MBR/GPT).
- Поиск, загрузка в память и запуск загрузчика (GRUB).
- Поиск, загрузка в память и запуск ядра ОС.
- Запуск системных служб.
- Запуск пользовательских служб.

**BIOS (Basic Input/Output System)** — набор системных программ (firmware), используемых для процесса проверки и инициализации аппаратного обеспечения с последующим запуском загрузчика ОС.

**POST (power-on self-test)** — процесс первоначальной проверки оборудования сразу после его включения

**Процесс загрузки BIOS**
- Инициализация видеокарты (как option BIOS);
- Запуск и выполнение POST;
- Поиск загрузчика ОС на доступных устройствах (проверка сигнатуры загрузочного диска);
- Передача управления на найденный загрузочный сектор.

**UEFI, Unified Extensible Firmware Interface (интерфейс расширяемой прошивки)** — спецификация интерфейса между ОС и аппаратными прошивками (firmware), UEFI, в отличии от BIOS, содержит свой собственный загрузчик — UEFI Boot Manager
- SEC (Security) — проверяет цифровые подписи и передает управление доверенному коду.
- PEI (Pre EFI Initialization) — инициализация устройств.
- DXE (Driver eXecution Environment) — загрузка сервисов UEFI.
- BDS (Boot Device Select) — поиск устройств загрузки.
- RT (Run Time) — GRUB.

**GRand Unified Boot (GRUB)** — стандарт де-факто для загрузчиков Linux. Основное назначение: загрузка ядра ОС и выбор параметров загрузки.
- Настройка GRUB - grub.cfg - Внесение изменений в конфигурацию GRUB - /etc/default/grub - подтверждение - update-grub/grub2-mkconfig
- cat /proc/cmdline - Параметры ядра
- BOOT_IMAGE — образ ядра, которое загружено в данный момент
- root — корневая ФС
- vt.handoff — параметр специфичный для Ubuntu, нужен для сокрытия вывода загрузчика
- sysctl -a - Просмотр параметров ядра
- cat /etc/sysctl.conf | more - config file - Просмотр конфигурационного файла

**Initrd (Initial RAM Disk)** — образ, содержащий модули для инициализации ядра. GRUB передает ядру данный образ как параметр загрузки, поэтому, следует обратить внимание на то, что файл initrd должен соответствовать загружаемому ядру. Если ядро содержит все необходимые модули, то файл initrd не нужен.

**init** — специальный процесс (демон) управления системой и службами - Режимы работы init - однопользовательский (службы не запускаются), многопользовательский (режим запуска по умолчанию), сервер (аналогичен многопользовательскому, но без GUI)
- /sbin/init - Расположение init
**Варианты init**
- - System V - Все службы запускаются последовательно
- - BSD init - FreeBSD, NetBSD, OpenBSD
- - systemd - упрощенный процесс загрузки, параллельный запуск служб, запись событий в системный журнал.

**Процесс запуска Init-V**
- GRUB загружает и запускает ядро;
- ядро запускает /sbin/init;
- init разбирает /etc/inittab и выполняет сценарий для инициализации системы;
- init выполняет скрипт /etc/rc.d/rc или /etc/init.d/rc;
- скрипты из /etc/rcn.d или /etc/init.d/rcn.d запускают различные службы.

**systemd** — современный менеджер управления службами Linux. Позволяет выполнять следующие действия со службами: запускать/останавливать; добавлять/удалять; редактировать; собирать логи.
- Цель (target) — нужное состояние системы; ссылка на файл, содержащий зависимости (службы) Systemd запускает все зависимости из соответствующего target файла. Когда все зависимости будут запущены, то система будет работать на соответствующем target-уровне
- systemctl get-default - проверка target - (graphical.target)
- Модуль (unit) — описывает запускаемую службу, устройство и т.п. - Каждый модуль описан в своем файле (unit file): /usr/lib/systemd/system/ – модули из пакетов (Nginx, Apache, MySQL); /run/systemd/system/ — модули, созданные во время работы ОС; /etc/systemd/system/ — модули, созданные пользователем.
- Типы модулей - модули служб — обычные службы ОС, модули монтирования — монтируют ФС, целевый модули/цели — группируют другие модули
- systemctl list-units — список модулей
- systemctl list-units --type=service — список модулей-служб
- systemctl status module — состояние выбранного модуля
- systemctl enable\disable module — разрешить/запретить модуль
- systemctl start\stop\restart module — запустить/остановить/модуль
- systemctl daemon-reload — перезапуск конфигурации systemd
- journalctl - Журнал — база данных, в которой хранятся сообщения ядра и служб, начиная с загрузки и заканчивая завершением работы
- nano /etc/systemd/journald.conf - Настройки журнала
- jurnalctl -u=sshd — сообщения для модуля ssh
- journalctl --since=yesterday --until=now - временной период

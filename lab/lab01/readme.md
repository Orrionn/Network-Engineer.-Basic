# Лабораторная работа. Базовая настройка коммутатора
## Задачи
### Часть 1. Проверка конфигурации коммутатора по умолчанию
### Часть 2. Создание сети и настройка основных параметров устройства
-	Настройте базовые параметры коммутатора.
-	Настройте IP-адрес для ПК.
### Часть 3. Проверка сетевых подключений
-	Отобразите конфигурацию устройства.
-	Протестируйте сквозное соединение, отправив эхо-запрос.
-	Протестируйте возможности удаленного управления с помощью Telnet.

## Часть 1. Создание сети и проверка настроек коммутатора по умолчанию
### Шаг 1. Создайте сеть согласно топологии.
#### Подсоедините консольный кабель, как показано в топологии. На данном этапе не подключайте кабель Ethernet компьютера PC-A.
![](https://github.com/ValeriyaKudasheva/Network-Engineer.-Basic/blob/main/lab/lab01/img/console%20cable.jpg?raw=true)

#### Установите консольное подключение к коммутатору с компьютера PC-A с помощью Tera Term или другой программы эмуляции терминала.
![](https://github.com/ValeriyaKudasheva/Network-Engineer.-Basic/blob/main/lab/lab01/img/terminal_PC-A.jpg?raw=true)

>#### Почему нужно использовать консольное подключение для первоначальной настройки коммутатора? 
>Консольное подключение производится из соображений безопасности, т.к. ус-во еще не подключено к нашей локальной сети, но позволяет сделать первоначальные настройки (установка имени хоста, настройка ip и шлюза по умолчанию, включение интерфейса, настройка vlan и др).

>#### Почему нельзя подключиться к коммутатору через Telnet или SSH?
>Т.к. по умолчанию доступ к виртуальным терминальным линиям закрыт, а на данном этапе такие настройки не проводились.

### Шаг 2. Проверьте настройки коммутатора по умолчанию.
Переходим в привилегированный режим командой *enable*

![](https://github.com/ValeriyaKudasheva/Network-Engineer.-Basic/blob/main/lab/lab01/img/enable.jpg?raw=true)

Проверяем конфигурацию командой *show running-config*

![](https://github.com/ValeriyaKudasheva/Network-Engineer.-Basic/blob/main/lab/lab01/img/running-configuration.jpg?raw=true)

>#### Сколько интерфейсов FastEthernet имеется на коммутаторе 2960?
>24 интерфейса FastEthernet

![](https://github.com/ValeriyaKudasheva/Network-Engineer.-Basic/blob/main/lab/lab01/img/FastEthernet.jpg?raw=true)

>#### Сколько интерфейсов Gigabit Ethernet имеется на коммутаторе 2960?
>2 интерфейса Gigabit Ethernet

![](https://github.com/ValeriyaKudasheva/Network-Engineer.-Basic/blob/main/lab/lab01/img/Gigabit_Ethernet.jpg?raw=true)

>#### Каков диапазон значений, отображаемых в vty-линиях?
>2 диапазона: 0-4 и 5-15

![](https://github.com/ValeriyaKudasheva/Network-Engineer.-Basic/blob/main/lab/lab01/img/vty_line.jpg?raw=true)

#### Изучите файл загрузочной конфигурации (startup configuration), который содержится в энергонезависимом ОЗУ (NVRAM).

![](https://github.com/ValeriyaKudasheva/Network-Engineer.-Basic/blob/main/lab/lab01/img/startup_config.jpg?raw=true)

>#### Почему появляется это сообщение?
>Данное сообщение означает что конфигурация энергонезависимой оперативной памяти еще не была записана в файл.

#### Изучите характеристики SVI для VLAN 1.
>#### Назначен ли IP-адрес сети VLAN 1?
>IP-адрес не назначен

![](https://github.com/ValeriyaKudasheva/Network-Engineer.-Basic/blob/main/lab/lab01/img/no_ip_address.jpg?raw=true)

>#### Какой MAC-адрес имеет SVI? 
>Mac-адрес можно посмотреть командой show version или show interface vlan1

![](https://github.com/ValeriyaKudasheva/Network-Engineer.-Basic/blob/main/lab/lab01/img/show_version.jpg?raw=true)

![](https://github.com/ValeriyaKudasheva/Network-Engineer.-Basic/blob/main/lab/lab01/img/MAC-address.jpg?raw=true)

>#### Данный интерфейс включен?
>Интерфейс выключен

![](https://github.com/ValeriyaKudasheva/Network-Engineer.-Basic/blob/main/lab/lab01/img/vlan_shutdown.jpg?raw=true)

####  Изучите IP-свойства интерфейса SVI сети VLAN 1.
>#### Какие выходные данные вы видите?
>Vlan административно выключен, как и протокол линии

![](https://github.com/ValeriyaKudasheva/Network-Engineer.-Basic/blob/main/lab/lab01/img/Vlan1.jpg?raw=true)

#### Подсоедините кабель Ethernet компьютера PC-A к порту 6 на коммутаторе и изучите IP-свойства интерфейса SVI сети VLAN 1. 
![](https://github.com/ValeriyaKudasheva/Network-Engineer.-Basic/blob/main/lab/lab01/img/FastEthernet_06.jpg?raw=true)

![](https://github.com/ValeriyaKudasheva/Network-Engineer.-Basic/blob/main/lab/lab01/img/FastEthernet_06_up.jpg?raw=true)

![](https://github.com/ValeriyaKudasheva/Network-Engineer.-Basic/blob/main/lab/lab01/img/interface_FE_06.jpg?raw=true)


>#### Какие выходные данные вы видите?
>Статус интерфейса FastEthernet0/6 изменился, теперь он поднят.
>Протокол линии также поднялся. 

#### Изучите сведения о версии ОС Cisco IOS на коммутаторе.
>#### Под управлением какой версии ОС Cisco IOS работает коммутатор?
>Коммутатор работает под управлением версии 15.0(2)SE4

![](https://github.com/ValeriyaKudasheva/Network-Engineer.-Basic/blob/main/lab/lab01/img/Cisco_version.jpg?raw=true)

>#### Как называется файл образа системы?
>Файл образа системы называется c2960-lanbasek9-mz.150-2.SE4.bin

![](https://github.com/ValeriyaKudasheva/Network-Engineer.-Basic/blob/main/lab/lab01/img/system_file.jpg?raw=true)

#### Изучите свойства по умолчанию интерфейса FastEthernet, который используется компьютером PC-A.
>#### Интерфейс включен или выключен?
>Интерфейс включен

![](https://github.com/ValeriyaKudasheva/Network-Engineer.-Basic/blob/main/lab/lab01/img/show_FE_06.jpg?raw=true)

>#### Что нужно сделать, чтобы включить интерфейс?
>Включить интерфейс можно командой no shutdown

>#### Какой MAC-адрес у интерфейса?
>Mac-адрес 00d0.bac0.de06

>#### Какие настройки скорости и дуплекса заданы в интерфейсе?
>В интерфейсе задан Full-duplex (метод передачи данных в котором информация передается в обе стороны), который составляет 100Mб/c

#### Изучите флеш-память.
>#### Какое имя присвоено образу Cisco IOS?

![](https://github.com/ValeriyaKudasheva/Network-Engineer.-Basic/blob/main/lab/lab01/img/show_flash.jpg?raw=true)

## Часть 2. Настройка базовых параметров сетевых устройств

### Шаг 1. Настройте базовые параметры коммутатора.

#### В режиме глобальной конфигурации скопируйте следующие базовые параметры конфигурации и вставьте их в файл на коммутаторе S1. 
*no ip domain-lookup*

*hostname S1*

*service password-encryption*

*enable secret class*

*banner motd #*

*Unauthorized access is strictly prohibited. #*

![](https://github.com/ValeriyaKudasheva/Network-Engineer.-Basic/blob/main/lab/lab01/img/global_config.jpg?raw=true)

#### Назначьте IP-адрес интерфейсу SVI на коммутаторе. Благодаря этому вы получите возможность удаленного управления коммутатором.
Прописываем ip-адрес коммутатору 192.168.1.2 /24

![](https://github.com/ValeriyaKudasheva/Network-Engineer.-Basic/blob/main/lab/lab01/img/no_shutdown.jpg?raw=true)

![](https://github.com/ValeriyaKudasheva/Network-Engineer.-Basic/blob/main/lab/lab01/img/ip_address.jpg?raw=true)

![](https://github.com/ValeriyaKudasheva/Network-Engineer.-Basic/blob/main/lab/lab01/img/show_interface_vlan.jpg?raw=true)

#### Доступ через порт консоли также следует ограничить  с помощью пароля. Используйте cisco в качестве пароля для входа в консоль в этом задании. Конфигурация по умолчанию разрешает все консольные подключения без пароля. Чтобы консольные сообщения не прерывали выполнение команд, используйте параметр logging synchronous.

![](https://github.com/ValeriyaKudasheva/Network-Engineer.-Basic/blob/main/lab/lab01/img/passwd_fo_line_console.jpg?raw=true)

После перезагрузки проверим работу баннера, пароль на консольную линию и domain-lookup

![](https://github.com/ValeriyaKudasheva/Network-Engineer.-Basic/blob/main/lab/lab01/img/reload.jpg?raw=true)

####	Настройте каналы виртуального соединения для удаленного управления (vty), чтобы коммутатор разрешил доступ через Telnet. Если не настроить пароль VTY, будет невозможно подключиться к коммутатору по протоколу Telnet.
>#### Для чего нужна команда login?
>Используется для запроса пароля при входе через консольный порт

### Шаг 2. Настройте IP-адрес на компьютере PC-A.
#### Назначьте компьютеру IP-адрес и маску подсети в соответствии с таблицей адресации.
![](https://github.com/ValeriyaKudasheva/Network-Engineer.-Basic/blob/main/lab/lab01/img/configuration_PC-A.jpg?raw=true)

## Часть 3 Проверка сетевых подключений
### Шаг 1. Отобразите конфигурацию коммутатора.
#### Команда show run позволяет постранично отобразить всю текущую конфигурацию.

```
S1#show run
Building configuration...

Current configuration : 1338 bytes
!
version 15.0
no service timestamps log datetime msec
no service timestamps debug datetime msec
service password-encryption
!
hostname S1
!
enable secret 5 $1$mERr$9cTjUIEqNGurQiFU.ZeCi1
!
!
!
no ip domain-lookup
!
!
!
spanning-tree mode pvst
spanning-tree extend system-id
!
interface FastEthernet0/1
!
interface Vlan1
ip address 192.168.1.2 255.255.255.0
!
banner motd ^C
Unauthorized access is strictly prohibited. ^C
!
!
!
line con 0
password 7 0822455D0A16
logging synchronous
login
!
line vty 0 4
password 7 0822455D0A16
login
transport input telnet
line vty 5 15
password 7 0822455D0A16
login
!
end


```

#### Проверьте параметры VLAN 1.

![](https://github.com/ValeriyaKudasheva/Network-Engineer.-Basic/blob/main/lab/lab01/img/show_vlan.jpg?raw=true)

>#### Какова полоса пропускания этого интерфейса?
>Пропускная способность 100000 Кбит/с или 100 Мб/c

### Шаг 2. Протестируйте сквозное соединение, отправив эхо-запрос.
#### В командной строке компьютера PC-A с помощью утилиты ping проверьте связь сначала с адресом PC-A.

![](https://github.com/ValeriyaKudasheva/Network-Engineer.-Basic/blob/main/lab/lab01/img/ping_PC-A.jpg?raw=true)

#### Из командной строки компьютера PC-A отправьте эхо-запрос на административный адрес интерфейса SVI коммутатора S1.

![](https://github.com/ValeriyaKudasheva/Network-Engineer.-Basic/blob/main/lab/lab01/img/ping_switch.jpg?raw=true)

### Шаг 3. Проверьте удаленное управление коммутатором S1.
#### Используйте удаленный доступ к устройству с помощью Telnet. 
a.	Откройте Tera Term или другую программу эмуляции терминала с возможностью Telnet. 

b.	Выберите сервер Telnet и укажите адрес управления SVI для подключения к S1.  Пароль: cisco.

c.	После ввода пароля cisco вы окажетесь в командной строке пользовательского режима. Для перехода в исполнительский режим EXEC введите команду enable и используйте секретный пароль class

![](https://github.com/ValeriyaKudasheva/Network-Engineer.-Basic/blob/main/lab/lab01/img/telnet.jpg?raw=true)

d.	Сохраните конфигурацию.

e.	Чтобы завершить сеанс Telnet, введите exit.

![](https://github.com/ValeriyaKudasheva/Network-Engineer.-Basic/blob/main/lab/lab01/img/copy_running_config.jpg?raw=true)

##	Вопросы для повторения
>#### 1.	Зачем необходимо настраивать пароль VTY для коммутатора?
>Чтобы обеспечить удалённое подключение по протоколу Telnet

>#### 2.	Что нужно сделать, чтобы пароли не отправлялись в незашифрованном виде?
>Использовать более защищенный протокол, ssh

## Приложение А. Инициализация и перезагрузка коммутатора
a.	Подключитесь к коммутатору с помощью консоли и войдите в привилегированный режим EXEC.
Откройте окно конфигурации

b.	Воспользуйтесь командой *show flash*, чтобы определить, были ли созданы сети VLAN на коммутаторе.

![](https://github.com/ValeriyaKudasheva/Network-Engineer.-Basic/blob/main/lab/lab01/img/show_flash_on_switch.jpg?raw=true)

c.	Если во флеш-памяти обнаружен файл vlan.dat, удалите его.
>Файла vlan.dat нет в директории

d.	Введите команду erase startup-config, чтобы удалить файл загрузочной конфигурации из NVRAM. 

![](https://github.com/ValeriyaKudasheva/Network-Engineer.-Basic/blob/main/lab/lab01/img/erase%20startup-config.jpg?raw=true)

e.	Перезагрузите коммутатор, чтобы удалить устаревшую информацию о конфигурации из памяти. Затем появится запрос на подтверждение перезагрузки коммутатора. Нажмите клавишу Enter, чтобы продолжить.

![](https://github.com/ValeriyaKudasheva/Network-Engineer.-Basic/blob/main/lab/lab01/img/reload_no_save.jpg?raw=true)

f.	После перезагрузки коммутатора появится запрос о входе в диалоговое окно начальной конфигурации. Чтобы ответить, введите no и нажмите клавишу Enter.

```
C2960 Boot Loader (C2960-HBOOT-M) Version 12.2(25r)FX, RELEASE SOFTWARE (fc4)
Cisco WS-C2960-24TT (RC32300) processor (revision C0) with 21039K bytes of memory.
2960-24TT starting...
Base ethernet MAC Address: 0060.2FE4.B147
Xmodem file system is available.
Initializing Flash...
flashfs[0]: 1 files, 0 directories
flashfs[0]: 0 orphaned files, 0 orphaned directories
flashfs[0]: Total bytes: 64016384
flashfs[0]: Bytes used: 4670455
flashfs[0]: Bytes available: 59345929
flashfs[0]: flashfs fsck took 1 seconds.
...done Initializing Flash.

Boot Sector Filesystem (bs:) installed, fsid: 3
Parameter Block Filesystem (pb:) installed, fsid: 4


Loading "flash:/2960-lanbasek9-mz.150-2.SE4.bin"...
######################### [OK]
Smart Init is enabled
smart init is sizing iomem
                  TYPE      MEMORY_REQ
                TOTAL:      0x00000000
Rounded IOMEM up to: 0Mb.
Using 6 percent iomem. [0Mb/512Mb]

              Restricted Rights Legend
Use, duplication, or disclosure by the Government is
subject to restrictions as set forth in subparagraph
(c) of the Commercial Computer Software - Restricted
Rights clause at FAR sec. 52.227-19 and subparagraph
(c) (1) (ii) of the Rights in Technical Data and Computer
Software clause at DFARS sec. 252.227-7013.
           cisco Systems, Inc.
           170 West Tasman Drive
           San Jose, California 95134-1706
Cisco IOS Software, C2960 Software (C2960-LANBASEK9-M), Version 15.0(2)SE4, RELEASE SOFTWARE (fc1)
Technical Support: http://www.cisco.com/techsupport
Copyright (c) 1986-2013 by Cisco Systems, Inc.
Compiled Wed 26-Jun-13 02:49 by mnguyen
Initializing flashfs...
fsck: Disable shadow buffering due to heap fragmentation.
flashfs[2]: 2 files, 1 directories
flashfs[2]: 0 orphaned files, 0 orphaned directories
flashfs[2]: Total bytes: 32514048
flashfs[2]: Bytes used: 11952128
flashfs[2]: Bytes available: 20561920
flashfs[2]: flashfs fsck took 2 seconds.
flashfs[2]: Initialization complete....done Initializing flashfs.
Checking for Bootloader upgrade..
Boot Loader upgrade not required (Stage 2)
POST: CPU MIC register Tests : Begin
POST: CPU MIC register Tests : End, Status Passed
POST: PortASIC Memory Tests : Begin
POST: PortASIC Memory Tests : End, Status Passed
POST: CPU MIC interface Loopback Tests : Begin
POST: CPU MIC interface Loopback Tests : End, Status Passed
POST: PortASIC RingLoopback Tests : Begin
POST: PortASIC RingLoopback Tests : End, Status Passed
POST: PortASIC CAM Subsystem Tests : Begin
POST: PortASIC CAM Subsystem Tests : End, Status Passed
POST: PortASIC Port Loopback Tests : Begin
POST: PortASIC Port Loopback Tests : End, Status Passed
Waiting for Port download...Complete

This product contains cryptographic features and is subject to United
States and local country laws governing import, export, transfer and
use. Delivery of Cisco cryptographic products does not imply
third-party authority to import, export, distribute or use encryption.
Importers, exporters, distributors and users are responsible for
compliance with U.S. and local country laws. By using this product you
agree to comply with applicable laws and regulations. If you are unable
to comply with U.S. and local laws, return this product immediately.
A summary of U.S. laws governing Cisco cryptographic products may be found at:
http://www.cisco.com/wwl/export/crypto/tool/stqrg.html
If you require further assistance please contact us by sending email to
export@cisco.com.
cisco WS-C2960-24TT-L (PowerPC405) processor (revision B0) with 65536K bytes of memory.
Processor board ID FOC1010X104
Last reset from power-on
1 Virtual Ethernet interface
24 FastEthernet interfaces
2 Gigabit Ethernet interfaces
The password-recovery mechanism is enabled.
64K bytes of flash-simulated non-volatile configuration memory.
Base ethernet MAC Address       : 00:60:2F:E4:B1:47
Motherboard assembly number     : 73-10390-03
Power supply part number        : 341-0097-02
Motherboard serial number       : FOC10093R12
Power supply serial number      : AZS1007032H
Model revision number           : B0
Motherboard revision number     : B0
Model number                    : WS-C2960-24TT-L
System serial number            : FOC1010X104
Top Assembly Part Number        : 800-27221-02
Top Assembly Revision Number    : A0
Version ID                      : V02
CLEI Code Number                : COM3L00BRA
Hardware Board Revision Number  : 0x01

Switch Ports Model              SW Version            SW Image
------ ----- -----              ----------            ----------
*    1 26    WS-C2960-24TT-L    15.0(2)SE4            C2960-LANBASEK9-M

Cisco IOS Software, C2960 Software (C2960-LANBASEK9-M), Version 15.0(2)SE4, RELEASE SOFTWARE (fc1)
Technical Support: http://www.cisco.com/techsupport
Copyright (c) 1986-2013 by Cisco Systems, Inc.
Compiled Wed 26-Jun-13 02:49 by mnguyen



Press RETURN to get started!


%LINK-5-CHANGED: Interface FastEthernet0/6, changed state to up

%LINEPROTO-5-UPDOWN: Line protocol on Interface FastEthernet0/6, changed state to up
```

>#### Проверим конфигурацию.

```
Switch>
Switch>en
Switch#sh
Switch#show r
Switch#show run
Building configuration...

Current configuration : 1080 bytes
!
version 15.0
no service timestamps log datetime msec
no service timestamps debug datetime msec
no service password-encryption
!
hostname Switch
!
!
!
!
!
!
spanning-tree mode pvst
spanning-tree extend system-id
!
interface FastEthernet0/1
!
interface FastEthernet0/2
!
interface FastEthernet0/3
!
interface FastEthernet0/4
!
interface FastEthernet0/5
!
interface FastEthernet0/6
!
interface FastEthernet0/7
!
interface FastEthernet0/8
!
interface FastEthernet0/9
!
interface FastEthernet0/10
!
interface FastEthernet0/11
!
interface FastEthernet0/12
!
interface FastEthernet0/13
!
interface FastEthernet0/14
!
interface FastEthernet0/15
!
interface FastEthernet0/16
!
interface FastEthernet0/17
!
interface FastEthernet0/18
!
interface FastEthernet0/19
!
interface FastEthernet0/20
!
interface FastEthernet0/21
!
interface FastEthernet0/22
!
interface FastEthernet0/23
!
interface FastEthernet0/24
!
interface GigabitEthernet0/1
!
interface GigabitEthernet0/2
!
interface Vlan1
 no ip address
 shutdown
!
!
!
!
line con 0
!
line vty 0 4
 login
line vty 5 15
 login
!

end
Switch# 
```













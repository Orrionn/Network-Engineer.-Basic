# Лабораторная работа. Настройка IPv6-адресов на сетевых устройствах 
## Задачи
### Часть 1. Настройка топологии и конфигурация основных параметров маршрутизатора и коммутатора
### Часть 2. Ручная настройка IPv6-адресов
### Часть 3. Проверка сквозного соединения

## Часть 1. Настройка топологии и конфигурация основных параметров маршрутизатора и коммутатора
### Шаг 1. Настройте маршрутизатор.
#### Назначьте имя хоста и настройте основные параметры устройства.
![](https://github.com/Orrionn/Network-Engineer.-Basic/blob/main/lab/lab4/pic/topologi.png?raw=true)

![](https://github.com/Orrionn/Network-Engineer.-Basic/blob/main/lab/lab4/pic/1.png?raw=true)

![](https://github.com/Orrionn/Network-Engineer.-Basic/blob/main/lab/lab4/pic/2.png?raw=true)

![](https://github.com/Orrionn/Network-Engineer.-Basic/blob/main/lab/lab4/pic/3.png?raw=true)

```
S1#show run
Building configuration...

Current configuration : 1246 bytes
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
interface FastEthernet0/2
!
interface FastEthernet0/3
!
interface FastEthernet0/4
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
banner motd ^C!!!!STOP!!!^C
!
!
!
line con 0
password 7 0822404F1A0A
logging synchronous
login
!
line vty 0 4
login
line vty 5 15
password 7 0822455D0A16
login
```
### Шаг 2. Настройте коммутатор.
#### Назначьте имя хоста и настройте основные параметры устройства
```
Router>
Router>en
Router#
Router#conf t
Enter configuration commands, one per line. End with CNTL/Z.
Router(config)#
Router(config)#ser
Router(config)#service pas
Router(config)#service password-encryption 
Router(config)#ena
Router(config)#enable sec
Router(config)#enable secret cisco
Router(config)#
Router(config)#ban
Router(config)#banner mo
Router(config)#banner motd #!!!!!Go away!!!!#
Router(config)#
Router(config)#no ip
Router(config)#no ip d
Router(config)#no ip domain-l
Router(config)#no ip domain-lookup 
Router(config)#
Router(config)#line co
Router(config)#line console 0
Router(config-line)#
Router(config-line)#pas
Router(config-line)#password cisco
Router(config-line)#
Router(config-line)#logg
Router(config-line)#logging syn
Router(config-line)#logging synchronous 
Router(config-line)#
Router(config-line)#login
Router(config-line)#
Router(config-line)#exit
Router(config)#
Router(config)#line
Router(config)#line vt
Router(config)#line vty 5 15
Router(config-line)#
Router#
Router#CONF T
Enter configuration commands, one per line. End with CNTL/Z.
Router(config)#
Router(config)#host
Router(config)#hostname R1
R1(config)#
```
## Часть 2. Ручная настройка IPv6-адресов
### Шаг 1. Назначьте IPv6-адреса интерфейсам Ethernet на R1.
#### a.	Назначьте глобальные индивидуальные IPv6-адреса, указанные в таблице адресации обоим интерфейсам Ethernet на R1
![](https://github.com/Orrionn/Network-Engineer.-Basic/blob/main/lab/lab4/pic/IPv6_fo_G00.png?raw=true)


![](https://github.com/Orrionn/Network-Engineer.-Basic/blob/main/lab/lab4/pic/IPv6_fo_G01.png?raw=true)

#### b.	Введите команду show ipv6 interface brief, чтобы проверить, назначен ли каждому интерфейсу корректный индивидуальный IPv6-адрес.
![](https://github.com/Orrionn/Network-Engineer.-Basic/blob/main/lab/lab4/pic/show_int_brief.png?raw=true)
>#### Примечание. Отображаемый локальный адрес канала основан на адресации EUI-64, которая автоматически использует MAC-адрес интерфейса для создания 128-битного локального IPv6-адреса канала.

#### c.	Чтобы обеспечить соответствие локальных адресов канала индивидуальному адресу, вручную введите локальные адреса канала на каждом интерфейсе Ethernet на R1.
![](https://github.com/Orrionn/Network-Engineer.-Basic/blob/main/lab/lab4/pic/LLA_G00.png?raw=true)

![](https://github.com/Orrionn/Network-Engineer.-Basic/blob/main/lab/lab4/pic/LLA_G01.png?raw=true)
>#### Примечание. Каждый интерфейс маршрутизатора относится к отдельной сети. Пакеты с локальным адресом канала никогда не выходят за пределы локальной сети, а значит, для обоих интерфейсов можно указывать один и тот же локальный адрес канала.

#### d.	Используйте выбранную команду, чтобы убедиться, что локальный адрес связи изменен на fe80::1.  
![](https://github.com/Orrionn/Network-Engineer.-Basic/blob/main/lab/lab4/pic/show_int_brief.png?raw=true)

>#### Какие группы многоадресной рассылки назначены интерфейсу G0/0?
>![](https://github.com/Orrionn/Network-Engineer.-Basic/blob/main/lab/lab4/pic/groups.png?raw=true)
>
> На интерфейс G0/0 назначены 2 многоадрессные рассылки.
>
>FF02::1 и FF02::1:FF00:1.
>
>Адрес мультикастовой рассылки FF02::1 работает как broadcast в IPv4, т.е. при отправке запроса на данный адрес, его примут все устройства в локальной сети.
>
>FF02::1:FF – это мультикастоый адрес, на который автоматически подписываются все узлы. После неизменной части
>FF02::1:FF оставшиеся 24 бита берутся с ip которые настроены на интерфейсе.
>В данном случае, оставшиеся биты взяты со следующего ip:
>
>2001:DB8:ACAD:A::1. Полный адрес: 2001:DB80:ACAD:A000:0000:0000:0000:1000
>
>Последние 24 бит 00:1000
>
>К адресу FF02::1:FF добавляются эти биты, получаем полный адрес: FF02:0000:0000:0000:0000:1000:FF00:1000.
>
>Представляем его в коротком виде и получаем нашу группу: FF02::1:FF00:1

### Шаг 2. Активируйте IPv6-маршрутизацию на R1.
#### a.	В командной строке на PC-B введите команду ipconfig, чтобы получить данные IPv6-адреса, назначенного интерфейсу ПК.
>![](https://github.com/Orrionn/Network-Engineer.-Basic/blob/main/lab/lab4/pic/ipconfig_PC-B(1).png?raw=true)

>#### Назначен ли индивидуальный IPv6-адрес сетевой интерфейсной карте (NIC) на PC-B?
> Нет, назначен только LLA адрес, который назначается автоматически, как только на устройстве включается протокол IPv6.

#### b.	Активируйте IPv6-маршрутизацию на R1 с помощью команды IPv6 unicast-routing.
![](https://github.com/Orrionn/Network-Engineer.-Basic/blob/main/lab/lab4/pic/IPv6_unicast-routing.png?raw=true)
>#### Примечание. Это позволит компьютерам получать IP-адреса и данные шлюза по умолчанию с помощью функции SLAAC (Stateless Address Autoconfiguration (Автоконфигурация без сохранения состояния адреса)).

#### c.	Теперь, когда R1 входит в группу многоадресной рассылки всех маршрутизаторов, еще раз введите команду ipconfig на PC-B. Проверьте данные IPv6-адреса.
#### Сначала необходимо включить автоматическое получение IPv6 адресов. И т.к. ранее был настроен LLA, то шлюз по умолчанию определился автоматически.

![](https://github.com/Orrionn/Network-Engineer.-Basic/blob/main/lab/lab4/pic/Automatic_IPv6.png?raw=true)

![](https://github.com/Orrionn/Network-Engineer.-Basic/blob/main/lab/lab4/pic/ipconfig_B.png?raw=true)

>#### Почему PC-B получил глобальный префикс маршрутизации и идентификатор подсети, которые вы настроили на R1?
>По умолчанию на маршрутизаторах IPv6-маршрутизация не включена и после включения командой ipv6 unicast-routing, маршрутизатор стал отправлять сообщения (Router Advertisement, RA) всем устройствам, находящимся в сети. PC-B получил данное сообщение, определил идентификатор сети(4 хекстет), далее при помощи EUI-64 определелил оставшиеся 24 бита (идентификатор интерфейса).

### Шаг 3. Назначьте IPv6-адреса интерфейсу управления (SVI) на S1.
#### a.	Назначьте адрес IPv6 для S1. Также назначьте этому интерфейсу локальный адрес канала fe80::b.

![](https://github.com/Orrionn/Network-Engineer.-Basic/blob/main/lab/lab4/pic/S1.png?raw=true)

![](https://github.com/Orrionn/Network-Engineer.-Basic/blob/main/lab/lab4/pic/IPv6_S1.png?raw=true)

#### b.	Проверьте правильность назначения IPv6-адресов интерфейсу управления с помощью команды show ipv6 interface vlan1.
![](https://github.com/Orrionn/Network-Engineer.-Basic/blob/main/lab/lab4/pic/show_vlan1.png?raw=true)

### Шаг 4. Назначьте компьютерам статические IPv6-адреса.
#### a.	Откройте окно Свойства Ethernet для каждого ПК и назначьте адресацию IPv6.

#### Автоматически получены IPv6 адреса на обеих машинах:
![](https://github.com/Orrionn/Network-Engineer.-Basic/blob/main/lab/lab4/pic/IPv6_PC-A.png?raw=true)

![](https://github.com/Orrionn/Network-Engineer.-Basic/blob/main/lab/lab4/pic/IPv6_PC-B.png?raw=true)

#### b.	Убедитесь, что оба компьютера имеют правильную информацию адреса IPv6. Каждый компьютер должен иметь два глобальных адреса IPv6: один статический и один SLACC.
>#### Примечание. При выполнении работы в среде Cisco Packet Tracer установите статический и SLACC адреса на компьютеры последовательно, отразив результаты в отчете

#### Проставляем статические IPv6 адреса на обеих машинах:
![](https://github.com/Orrionn/Network-Engineer.-Basic/blob/main/lab/lab4/pic/IPv6_PC-A_static.png?raw=true)

![](https://github.com/Orrionn/Network-Engineer.-Basic/blob/main/lab/lab4/pic/IPv6_PC-B_static.png?raw=true)

## Часть 3. Проверка сквозного подключения
#### С PC-A отправьте эхо-запрос на FE80::1. Это локальный адрес канала, назначенный G0/1 на R1.

![](https://github.com/Orrionn/Network-Engineer.-Basic/blob/main/lab/lab4/pic/echo_reply_PC-A.png?raw=true)

#### Отправьте эхо-запрос на интерфейс управления S1 с PC-A.

![](https://github.com/Orrionn/Network-Engineer.-Basic/blob/main/lab/lab4/pic/echo_reply_S1.png?raw=true)

#### Введите команду tracert на PC-A, чтобы проверить наличие сквозного подключения к PC-B.

![](https://github.com/Orrionn/Network-Engineer.-Basic/blob/main/lab/lab4/pic/tracert.png?raw=true)

#### С PC-B отправьте эхо-запрос на PC-A.

![](https://github.com/Orrionn/Network-Engineer.-Basic/blob/main/lab/lab4/pic/echo_reply_PC-B.png?raw=true)

#### С PC-B отправьте эхо-запрос на локальный адрес канала G0/0 на R1.

![](https://github.com/Orrionn/Network-Engineer.-Basic/blob/main/lab/lab4/pic/echo_reply_S1+G00.png?raw=true)

## Вопросы для повторения

>#### 1.	Почему обоим интерфейсам Ethernet на R1 можно назначить один и тот же локальный адрес канала — FE80::1?
>Локальный адреса канала, используется для взаимодействия IPv6- устройств между собой, но только внутри локальной сети. А т.к. оба интерфейса находятся в разных сегментах сети, то узлы этих сетей не будут пересекаться. И будут обращены конкретному интерфейсу, либо к G0/0, либо к G0/1.

>#### Какой идентификатор подсети в индивидуальном IPv6-адресе 2001:db8:acad::aaaa:1234/64?
>Полный ip-адрес будет выглядеть так: 2001:db8:acad:0000:0000:0000:aaaa:1234/64
Первые три хекстета занимает Prefix (префикс глобальной маршрутизации). Четвертый хекстет – идентификатор сети, в данном случае это 0000 или, согласно правилу представления ip-адресов, 0.
























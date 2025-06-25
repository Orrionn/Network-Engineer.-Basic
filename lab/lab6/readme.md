# Лабораторная работа - Внедрение маршрутизации между виртуальными локальными сетями 
## Задачи

### Часть 1. Создание сети и настройка основных параметров устройства
### Часть 2. Создание сетей VLAN и назначение портов коммутатора
### Часть 3. Настройка транка 802.1Q между коммутаторами.
### Часть 4. Настройка маршрутизации между сетями VLAN
### Часть 5. Проверка, что маршрутизация между VLAN работает


## Часть 1. Создание сети и настройка основных параметров устройства
В первой части лабораторной работы вам предстоит создать топологию сети и настроить базовые параметры для узлов ПК и коммутаторов.

### Шаг 1. Создайте сеть согласно топологии.
Подключите устройства, как показано в топологии, и подсоедините необходимые кабели.

![](https://github.com/Orrionn/Network-Engineer.-Basic/blob/main/lab/lab6/img/topology.png?raw=true)

### Шаг 2. Настройте базовые параметры для маршрутизатора.
#### a.	Подключитесь к маршрутизатору с помощью консоли и активируйте привилегированный режим EXEC.
Откройте окно конфигурации
#### b.	Войдите в режим конфигурации.
#### c.	Назначьте маршрутизатору имя устройства.
#### d.	Отключите поиск DNS, чтобы предотвратить попытки маршрутизатора неверно преобразовывать введенные команды таким образом, как будто они являются именами узлов.

#### e.	Назначьте class в качестве зашифрованного пароля привилегированного режима EXEC.
#### f.	Назначьте cisco в качестве пароля консоли и включите вход в систему по паролю.
#### g.	Установите cisco в качестве пароля виртуального терминала и активируйте вход.
#### h.	Зашифруйте открытые пароли.
#### i.	Создайте баннер с предупреждением о запрете несанкционированного доступа к устройству.
#### j.	Сохраните текущую конфигурацию в файл загрузочной конфигурации.
#### k.	Настройте на маршрутизаторе время.
```
Router>
Router>en
Router#
Router#conf t
Enter configuration commands, one per line. End with CNTL/Z.
Router(config)#hos
Router(config)#hostname R1
R1(config)#ser
R1(config)#service pas
R1(config)#service password-encryption 
R1(config)#ena
R1(config)#enable se
R1(config)#enable secret class
R1(config)#banner m
R1(config)#banner motd #NOOO STOP#
R1(config)#lin
R1(config)#line con
R1(config)#line console 0
R1(config-line)#pas
R1(config-line)#password cisco
R1(config-line)#login
R1(config-line)#logg
R1(config-line)#logging sy
R1(config-line)#logging synchronous 
R1(config-line)#exit
R1(config)#no i
R1(config)#no ip domain-l
R1(config)#no ip domain-lookup 
R1(config)#li
R1(config)#line
R1(config)#line vt
R1(config)#line vty 0 4
R1(config-line)#
R1(config-line)#pas
R1(config-line)#password cisco
R1(config-line)#^Z
R1#
%SYS-5-CONFIG_I: Configured from console by console

R1#cop
R1#copy r
R1#copy running-config st
R1#copy running-config startup-config 
Destination filename [startup-config]? 
Building configuration...
[OK]
R1#
```

### Шаг 3. Настройте базовые параметры каждого коммутатора.

#### a.	Присвойте коммутатору имя устройства.
#### b.	Отключите поиск DNS, чтобы предотвратить попытки маршрутизатора неверно преобразовывать введенные команды таким образом, как будто они являются именами узлов.
#### c.	Назначьте class в качестве зашифрованного пароля привилегированного режима EXEC.
#### d.	Назначьте cisco в качестве пароля консоли и включите вход в систему по паролю.
#### e.	Установите cisco в качестве пароля виртуального терминала и активируйте вход.
#### f.	Зашифруйте открытые пароли.
#### g.	Создайте баннер с предупреждением о запрете несанкционированного доступа к устройству.
#### h.	Настройте на коммутаторах время.
#### i.	Сохранение текущей конфигурации в качестве начальной.

>#### Коммутатор S1
```
Switch>en
Switch#
Switch#conf t
Enter configuration commands, one per line. End with CNTL/Z.
Switch(config)#hos
Switch(config)#hostname S1
S1(config)#ser
S1(config)#service pa
S1(config)#service password-encryption 
S1(config)#enab
S1(config)#enable sec
S1(config)#enable secret class
S1(config)#ban
S1(config)#banner mo
S1(config)#banner motd #NOO STOP#
S1(config)#li
S1(config)#line co
S1(config)#line console 0
S1(config-line)#pas
S1(config-line)#password cisco
S1(config-line)#logi
S1(config-line)#login 
S1(config-line)#logging sy
S1(config-line)#logging synchronous 
S1(config-line)#
S1(config-line)#exit
S1(config)#no ip domain-l
S1(config)#no ip domain-lookup 
S1(config)#
S1(config)#lin
S1(config)#line vt
S1(config)#line vty 0 4
S1(config-line)#pas
S1(config-line)#password cisco
S1(config-line)#^Z
S1#
%SYS-5-CONFIG_I: Configured from console by console

S1#clo
S1#clock se
S1#clock set 13:32:00 16 june 2025
S1#sh
S1#show clock 
13:32:6.404 UTC Mon Jun 16 2025
S1#cop
S1#copy r
S1#copy running-config st
S1#copy running-config startup-config 
Destination filename [startup-config]? 
Building configuration...
[OK]
S1#
```
>#### Коммутатор S2
```
Switch>en
Switch#
Switch#conf t
Enter configuration commands, one per line. End with CNTL/Z.
Switch(config)#ho
Switch(config)#hostname S2
S2(config)#sec
S2(config)#ser
S2(config)#service pas
S2(config)#service password-encryption 
S2(config)#en
S2(config)#ena
S2(config)#enable se
S2(config)#enable secret class
S2(config)#ban
S2(config)#banner mo
S2(config)#banner motd #NOO STOP#
S2(config)#
S2(config)#lin
S2(config)#line co
S2(config)#line console 0
S2(config-line)#
S2(config-line)#pas
S2(config-line)#password cisco
S2(config-line)#
S2(config-line)#logi
S2(config-line)#login 
S2(config-line)#logg
S2(config-line)#logging sy
S2(config-line)#logging synchronous 
S2(config-line)#exit
S2(config)#lin
S2(config)#line vt
S2(config)#line vty 0 4
S2(config-line)#pas
S2(config-line)#password cisco
S2(config-line)#exit
S2(config)#no ip domain-l
S2(config)#no ip domain-lookup 
S2(config)#
S2(config)#^Z
S2#
%SYS-5-CONFIG_I: Configured from console by console

S2#cl
S2#clo
S2#clock se
S2#clock set 13:39:00 16 june 2025
S2#clo
S2#sh
S2#show cl
S2#show clock 
13:39:8.615 UTC Mon Jun 16 2025
S2#cop
S2#copy ru
S2#copy running-config st
S2#copy running-config startup-config 
Destination filename [startup-config]? 
Building configuration...
[OK]
```

### Шаг 4. Настройте узлы ПК.
Адреса ПК можно посмотреть в таблице адресации.

>#### Настройка PC-A

![](https://github.com/Orrionn/Network-Engineer.-Basic/blob/main/lab/lab6/img/PC-A.png?raw=true)

>#### Настройка PC-B

![](https://github.com/Orrionn/Network-Engineer.-Basic/blob/main/lab/lab6/img/PC-B.png?raw=true)

## Часть 2. Создание сетей VLAN и назначение портов коммутатора
Во второй части вы создадите VLAN, как указано в таблице выше, на обоих коммутаторах. Затем вы назначите VLAN соответствующему интерфейсу и проверите настройки конфигурации. Выполните следующие задачи на каждом коммутаторе.

### Шаг 1. Создайте сети VLAN на коммутаторах.
#### a.	Создайте и назовите необходимые VLAN на каждом коммутаторе из таблицы выше.

```
S1#conf t
Enter configuration commands, one per line. End with CNTL/Z.
S1(config)#vlan 10
S1(config-vlan)#nam
S1(config-vlan)#name Control
S1(config-vlan)#exit
S1(config)#vlan 20
S1(config-vlan)#na
S1(config-vlan)#name Sales
S1(config-vlan)#exit
S1(config)#vlan 30
S1(config-vlan)#na
S1(config-vlan)#name Operations
S1(config-vlan)#exit
S1(config)#vlan 999
S1(config-vlan)#na
S1(config-vlan)#name Parking_Lot
S1(config-vlan)#exit
S1(config)#vlan 1000
S1(config-vlan)#na
S1(config-vlan)#name Native
S1(config-vlan)#
S1(config-vlan)#exit
S1(config)#
```

```
S2#conf t
Enter configuration commands, one per line. End with CNTL/Z.
S2(config)#vl
S2(config)#vlan 10
S2(config-vlan)#na
S2(config-vlan)#name Control 
S2(config-vlan)#vlan 20
S2(config-vlan)#na
S2(config-vlan)#name Sales
S2(config-vlan)#exit
S2(config)#vlan 30
S2(config-vlan)#na
S2(config-vlan)#name 
S2(config-vlan)#name Operations
S2(config-vlan)#exit
S2(config)#vlan 999
S2(config-vlan)#na
S2(config-vlan)#name Parking_Lot
S2(config-vlan)#exit
S2(config)#vlan 1000
S2(config-vlan)#na
S2(config-vlan)#name Native
S2(config-vlan)#exit
```
#### b.	Настройте интерфейс управления и шлюз по умолчанию на каждом коммутаторе, используя информацию об IP-адресе в таблице адресации. 
>#### Настройка первого коммутатора
```
S1(config-if)#ip ad
S1(config-if)#ip address 192.168.10.11 255.255.255.0
S1(config-if)#ip de
S1(config-if)#exit
S1(config)#ip de
S1(config)#ip default-gateway 192.168.10.1
S1(config)#
```
>#### Настройка второго коммутатора
```
S2(config-if)#ip ad
S2(config-if)#ip address 192.168.10.12 255.255.255.0
S2(config-if)#exit
S2(config)#ip de
S2(config)#ip default-gateway 192.168.10.1
S2(config)#
```

#### c.	Назначьте все неиспользуемые порты коммутатора VLAN Parking_Lot, настройте их для статического режима доступа и административно деактивируйте их.

>#### Назначаем неиспользуемые порты VLAN Parking_Lot на коммутаторе S1 
```
S1(config)#in
S1(config)#interface ra
S1(config)#interface range fa
S1(config)#interface range fastEthernet 0/2-4,f
S1(config)#interface range fastEthernet 0/2-4,f0/7-24, g
S1(config)#interface range fastEthernet 0/2-4,f0/7-24, gigabitEthernet 0/1-2
S1(config-if-range)#sw
S1(config-if-range)#switchport m
S1(config-if-range)#switchport mode ac
S1(config-if-range)#switchport mode access 
S1(config-if-range)#sw
S1(config-if-range)#switchport ac
S1(config-if-range)#switchport access vl
S1(config-if-range)#switchport access vlan 999
S1(config-if-range)#sh
S1(config-if-range)#shutdown
```
>#### Проверка настроек на S1
```
S1#show vlan 

VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
1    default                          active    Fa0/1, Fa0/5, Fa0/6
10   Control                          active    
20   Sales                            active    
30   Operations                       active    
999  Parking_Lot                      active    Fa0/2, Fa0/3, Fa0/4, Fa0/7
                                                Fa0/8, Fa0/9, Fa0/10, Fa0/11
                                                Fa0/12, Fa0/13, Fa0/14, Fa0/15
                                                Fa0/16, Fa0/17, Fa0/18, Fa0/19
                                                Fa0/20, Fa0/21, Fa0/22, Fa0/23
                                                Fa0/24, Gig0/1, Gig0/2
1000 Native                           active    
1002 fddi-default                     active    
1003 token-ring-default               active    
1004 fddinet-default                  active    
1005 trnet-default                    active    
```
>#### Тоже самое для S2
```
S2(config-if)#
S2(config-if)#interface range f
S2(config-if)#interface range f0/2-17, f0/19-24, g
S2(config-if)#interface range f0/2-17, f0/19-24, g0/1-2
S2(config-if-range)#sw
S2(config-if-range)#switchport mo
S2(config-if-range)#switchport mode ac
S2(config-if-range)#switchport mode access 
S2(config-if-range)#sw
S2(config-if-range)#switchport ac
S2(config-if-range)#switchport access vl
S2(config-if-range)#switchport access vlan 999
S2(config-if-range)#sh
S2(config-if-range)#shutdown 
```
>#### Проверка на S2
```
S2#show vl
S2#show vlan 

VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
1    default                          active    Fa0/1, Fa0/18
10   Control                          active    
20   Sales                            active    
30   Operations                       active    
999  Parking_Lot                      active    Fa0/2, Fa0/3, Fa0/4, Fa0/5
                                                Fa0/6, Fa0/7, Fa0/8, Fa0/9
                                                Fa0/10, Fa0/11, Fa0/12, Fa0/13
                                                Fa0/14, Fa0/15, Fa0/16, Fa0/17
                                                Fa0/19, Fa0/20, Fa0/21, Fa0/22
                                                Fa0/23, Fa0/24, Gig0/1, Gig0/2
1000 Native                           active    
1002 fddi-default                     active    
1003 token-ring-default               active    
1004 fddinet-default                  active    
1005 trnet-default                    active    
```

### Шаг 2. Назначьте сети VLAN соответствующим интерфейсам коммутатора.

a.	Назначьте используемые порты соответствующей VLAN (указанной в таблице VLAN выше) и настройте их для режима статического доступа.
>#### Назначим для S1
```
S1# conf t
Enter configuration commands, one per line.  End with CNTL/Z.
S1(config)#in
S1(config)#interface f
S1(config)#interface fastEthernet 0/6
S1(config-if)#sw
S1(config-if)#switchport m
S1(config-if)#switchport mode ac
S1(config-if)#switchport mode access 
S1(config-if)#sw
S1(config-if)#switchport ac
S1(config-if)#switchport access vlan 20
S1(config-if)#^Z
S1#
%SYS-5-CONFIG_I: Configured from console by console
```
>#### Назначим для S2
```
S2#conf t
Enter configuration commands, one per line. End with CNTL/Z.
S2(config)#int
S2(config)#interface f
S2(config)#interface fastEthernet 0/18
S2(config-if)#sw
S2(config-if)#switchport m
S2(config-if)#switchport mode a
S2(config-if)#switchport mode access 
S2(config-if)#sw
S2(config-if)#switchport a
S2(config-if)#switchport access v
S2(config-if)#switchport access vlan 30
```

#### b. Убедитесь, что VLAN назначены на правильные интерфейсы.
>#### Сделаем проверку командой show vlan для S1 
```
S1#sh vl

VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
1    default                          active    Fa0/1, Fa0/5
10   Control                          active    
20   Sales                            active    Fa0/6
```
>#### Проверим для S2
```
S2#shvl

VLAN Name                             Status    Ports
---- -------------------------------- --------- -------------------------------
1    default                          active    Fa0/1
10   Control                          active    
20   Sales                            active    
30   Operations                       active    Fa0/18
```

## Часть 3. Конфигурация магистрального канала стандарта 802.1Q между коммутаторами

В части 3 вы вручную настроите интерфейс F0/1 как транк.

### Шаг 1. Вручную настройте магистральный интерфейс F0/1 на коммутаторах S1 и S2.

#### a.	Настройка статического транкинга на интерфейсе F0/1 для обоих коммутаторов.

>#### Настроим транк на S1
```
S1(config)#int
S1(config)#interface f0/1
S1(config-if)#sw
S1(config-if)#switchport mo
S1(config-if)#switchport mode tr
S1(config-if)#switchport mode trunk
```
>#### Настроим на S2
```
S2(config)#in
S2(config)#interface f0/1
S2(config-if)#sw
S2(config-if)#switchport m
S2(config-if)#switchport mode tr
S2(config-if)#switchport mode trunk
```
#### b.	Установите native VLAN 1000 на обоих коммутаторах.
>#### Настраиваем нативный VLAN для S1
```
S1(config-if)#sw
S1(config-if)#switchport tr
S1(config-if)#switchport trunk n
S1(config-if)#switchport trunk native v
S1(config-if)#switchport trunk native vlan 1000
S1(config-if)#%SPANTREE-2-UNBLOCK_CONSIST_PORT: Unblocking FastEthernet0/1 on VLAN1000. Port consistency restored.

%SPANTREE-2-UNBLOCK_CONSIST_PORT: Unblocking FastEthernet0/1 on VLAN0001. Port consistency restored.

S1(config-if)#
```
>#### Нативный VLAN для S2
```
S2(config-if)#sw
S2(config-if)#switchport tr
S2(config-if)#switchport trunk n
S2(config-if)#switchport trunk native vlan 1000
S2(config-if)#
%CDP-4-NATIVE_VLAN_MISMATCH: Native VLAN mismatch discovered on FastEthernet0/1 (1000), with S1 FastEthernet0/1 (1).

S2(config-if)#
```

#### c.	Укажите, что VLAN 10, 20, 30 и 1000 могут проходить по транку.
>#### Указываем для S1
```
S1(config-if)#sw
S1(config-if)#switchport tr
S1(config-if)#switchport trunk al
S1(config-if)#switchport trunk allowed vl
S1(config-if)#switchport trunk allowed vlan 10,20,30,1000
S1(config-if)#
```
>#### Указываем для S2
```
S2(config-if)#sw
S2(config-if)#switchport tr
S2(config-if)#switchport trunk al
S2(config-if)#switchport trunk allowed vl
S2(config-if)#switchport trunk allowed vlan 10,20,30,1000
S2(config-if)#
```

#### d.	Проверьте транки, native VLAN и разрешенные VLAN через транк.
>#### Для S1
```
S1#sh interfaces tr
S1#sh interfaces trunk 
Port        Mode         Encapsulation  Status        Native vlan
Fa0/1       on           802.1q         trunking      1000

Port        Vlans allowed on trunk
Fa0/1       10,20,30,1000

Port        Vlans allowed and active in management domain
Fa0/1       10,20,30,1000

Port        Vlans in spanning tree forwarding state and not pruned
Fa0/1       10,20,30,1000
```
>#### Для S2
```
S2#sh in
S2#sh interfaces tr
S2#sh interfaces trunk 
Port        Mode         Encapsulation  Status        Native vlan
Fa0/1       on           802.1q         trunking      1000

Port        Vlans allowed on trunk
Fa0/1       10,20,30,1000

Port        Vlans allowed and active in management domain
Fa0/1       10,20,30,1000

Port        Vlans in spanning tree forwarding state and not pruned
Fa0/1       10,20,30,1000
```

### Шаг 2. Вручную настройте магистральный интерфейс F0/5 на коммутаторе S1.

#### a.	Настройте интерфейс S1 F0/5 с теми же параметрами транка, что и F0/1. Это транк до маршрутизатора.
```
S1(config)#interface f0/5
S1(config-if)#sw
S1(config-if)#switchport m
S1(config-if)#switchport mode tr
S1(config-if)#switchport mode trunk 
S1(config-if)#sw
S1(config-if)#switchport tr
S1(config-if)#switchport trunk na
S1(config-if)#switchport trunk native vl
S1(config-if)#switchport trunk native vlan 1000
S1(config-if)#sw
S1(config-if)#switchport tr al v
S1(config-if)#switchport tr al vlan 10,20,30,1000
S1(config-if)#
```

#### b.	Сохраните текущую конфигурацию в файл загрузочной конфигурации.
```
S1#copy ru
S1#copy running-config st
S1#copy running-config startup-config 
Destination filename [startup-config]? 
Building configuration...
[OK]
```

#### c.	Проверка транкинга.
```
S1#
%SYS-5-CONFIG_I: Configured from console by console

S1#sh in tr
Port        Mode         Encapsulation  Status        Native vlan
Fa0/1       on           802.1q         trunking      1000

Port        Vlans allowed on trunk
Fa0/1       10,20,30,1000

Port        Vlans allowed and active in management domain
Fa0/1       10,20,30,1000

Port        Vlans in spanning tree forwarding state and not pruned
Fa0/1       10,20,30,1000
```
>#### После долгих мучений, я поняла, что интерфейс на роутере был выключен и коммутатор не смог поднять транк на FastEthernet0/5
>#### После назначила повторно и транк поднялся
```
S1#sh in tr
Port        Mode         Encapsulation  Status        Native vlan
Fa0/1       on           802.1q         trunking      1000
Fa0/5       on           802.1q         trunking      1000

Port        Vlans allowed on trunk
Fa0/1       10,20,30,1000
Fa0/5       10,20,30,1000

Port        Vlans allowed and active in management domain
Fa0/1       10,20,30,1000
Fa0/5       10,20,30,1000

Port        Vlans in spanning tree forwarding state and not pruned
Fa0/1       10,20,30,1000
Fa0/5       10,20,30,1000
```

>#### Что произойдет, если G0/0/1 на R1 будет отключен?
> Транк до маршрутизатора не поднимется


## Часть 4. Настройка маршрутизации между сетями VLAN

### Шаг 1. Настройте маршрутизатор.

#### a.	При необходимости активируйте интерфейс G0/0/1 на маршрутизаторе.
>#### Настраиваем интерфейсы для VLAN 10, 20, 30 и для нативного VLAN
```
R1(config)#interface g
R1(config)#interface gigabitEthernet 0/1
R1(config-if)#no sh
R1(config-if)#no shutdown 
```
#### b.	Настройте подинтерфейсы для каждой VLAN, как указано в таблице IP-адресации. Все подинтерфейсы используют инкапсуляцию 802.1Q. Убедитесь, что подинтерфейсу для native VLAN не назначен IP-адрес. Включите описание для каждого подинтерфейса.
```
R1#conf t
Enter configuration commands, one per line. End with CNTL/Z.
R1(config)#interface gigabitEthernet 0/1.10
R1(config-subif)#
%LINK-5-CHANGED: Interface GigabitEthernet0/1.10, changed state to up

%LINEPROTO-5-UPDOWN: Line protocol on Interface GigabitEthernet0/1.10, changed state to up

R1(config-subif)#en
R1(config-subif)#encapsulation do
R1(config-subif)#encapsulation dot1Q 10
R1(config-subif)#ip ad
R1(config-subif)#ip address 192.168.10.1 255.255.255.0
R1(config-subif)#exit
R1(config)#interface gigabitEthernet 0/1.20
R1(config-subif)#
%LINK-5-CHANGED: Interface GigabitEthernet0/1.20, changed state to up

%LINEPROTO-5-UPDOWN: Line protocol on Interface GigabitEthernet0/1.20, changed state to up

R1(config-subif)#en
R1(config-subif)#encapsulation do
R1(config-subif)#encapsulation dot1Q 20
R1(config-subif)#ip ad
R1(config-subif)#ip address 192.168.20.1 255.255.255.0
R1(config-subif)#interface gigabitEthernet 0/1.30
R1(config-subif)#
%LINK-5-CHANGED: Interface GigabitEthernet0/1.30, changed state to up

%LINEPROTO-5-UPDOWN: Line protocol on Interface GigabitEthernet0/1.30, changed state to up

R1(config-subif)#en
R1(config-subif)#encapsulation do
R1(config-subif)#encapsulation dot1Q 30
R1(config-subif)#ip ad
R1(config-subif)#ip ad 192.168.30.1 255.255.255.0
R1(config-subif)#exit
R1(config)#int
R1(config)#interface g
R1(config)#interface gigabitEthernet 0/1.1000
R1(config-subif)#
%LINK-5-CHANGED: Interface GigabitEthernet0/1.1000, changed state to up

%LINEPROTO-5-UPDOWN: Line protocol on Interface GigabitEthernet0/1.1000, changed state to up

R1(config-subif)#en
R1(config-subif)#encapsulation do
R1(config-subif)#encapsulation dot1Q 1000 na
R1(config-subif)#encapsulation dot1Q 1000 native
```

#### c.	Убедитесь, что вспомогательные интерфейсы работают
```
R1#show ip interface brief 
Interface              IP-Address      OK? Method Status                Protocol 
GigabitEthernet0/0     unassigned      YES unset  administratively down down 
GigabitEthernet0/1     unassigned      YES unset  up                    up 
GigabitEthernet0/1.10  192.168.10.1    YES manual up                    up 
GigabitEthernet0/1.20  192.168.20.1    YES manual up                    up 
GigabitEthernet0/1.30  192.168.30.1    YES manual up                    up 
GigabitEthernet0/1.1000 unassigned      YES unset  up                    up 
GigabitEthernet0/2     unassigned      YES unset  administratively down down 
Vlan1                  unassigned      YES unset  administratively down down
```

## Часть 5. Проверьте, работает ли маршрутизация между VLAN

### Шаг 1. Выполните следующие тесты с PC-A. Все должно быть успешно.

Примечание. Возможно, вам придется отключить брандмауэр ПК для работы ping

#### a.	Отправьте эхо-запрос с PC-A на шлюз по умолчанию.
```
C:\>ping 192.168.20.1

Pinging 192.168.20.1 with 32 bytes of data:

Reply from 192.168.20.1: bytes=32 time<1ms TTL=255
Reply from 192.168.20.1: bytes=32 time=1ms TTL=255
Reply from 192.168.20.1: bytes=32 time<1ms TTL=255
Reply from 192.168.20.1: bytes=32 time<1ms TTL=255

Ping statistics for 192.168.20.1:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 0ms, Maximum = 1ms, Average = 0ms
```

#### b.	Отправьте эхо-запрос с PC-A на PC-B.
```
C:\>ping 192.168.30.3

Pinging 192.168.30.3 with 32 bytes of data:

Reply from 192.168.30.3: bytes=32 time<1ms TTL=127
Reply from 192.168.30.3: bytes=32 time<1ms TTL=127
Reply from 192.168.30.3: bytes=32 time<1ms TTL=127
Reply from 192.168.30.3: bytes=32 time<1ms TTL=127

Ping statistics for 192.168.30.3:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 0ms, Maximum = 0ms, Average = 0ms
```


#### c.	Отправьте команду ping с компьютера PC-A на коммутатор S2.
```
C:\>ping 192.168.10.12

Pinging 192.168.10.12 with 32 bytes of data:

Reply from 192.168.10.12: bytes=32 time<1ms TTL=254
Reply from 192.168.10.12: bytes=32 time<1ms TTL=254
Reply from 192.168.10.12: bytes=32 time<1ms TTL=254
Reply from 192.168.10.12: bytes=32 time<1ms TTL=254

Ping statistics for 192.168.10.12:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 0ms, Maximum = 0ms, Average = 0ms
```

## Шаг 2. Пройдите следующий тест с PC-B

В окне командной строки на PC-B выполните команду tracert на адрес PC-A.
>#### Какие промежуточные IP-адреса отображаются в результатах?
>
```
C:\>tracert 192.168.20.3

Tracing route to 192.168.20.3 over a maximum of 30 hops: 

  1   7 ms      0 ms      0 ms      192.168.30.1
  2   0 ms      0 ms      1 ms      192.168.20.3

Trace complete.
```
> Мы видим шлюз по умолчанию PC-B и он же ip-адрес подинтерфейса G0/0/1.30 маршрутизатора R1.

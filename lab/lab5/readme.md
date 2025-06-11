# Лабораторная работа. Доступ к сетевым устройствам по протоколу SSH
## Задачи
### Часть 1. Настройка основных параметров устройства
### Часть 2. Настройка маршрутизатора для доступа по протоколу SSH
### Часть 3. Настройка коммутатора для доступа по протоколу SSH
### Часть 4. SSH через интерфейс командной строки (CLI) коммутатора


## Часть 1. Настройка основных параметров устройств
В части 1 потребуется настроить топологию сети и основные параметры, такие как IP-адреса интерфейсов, доступ к устройствам и пароли на маршрутизаторе
### Шаг 1. Создайте сеть согласно топологии.
### Шаг 2. Выполните инициализацию и перезагрузку маршрутизатора и коммутатора.
### Шаг 3. Настройте маршрутизатор.
#### a.	Подключитесь к маршрутизатору с помощью консоли и активируйте привилегированный режим EXEC.
#### b.	Войдите в режим конфигурации.
#### c.	Отключите поиск DNS, чтобы предотвратить попытки маршрутизатора неверно преобразовывать введенные команды таким образом, как будто они являются именами узлов.
#### d.	Назначьте class в качестве зашифрованного пароля привилегированного режима EXEC.
#### e.	Назначьте cisco в качестве пароля консоли и включите вход в систему по паролю.
#### f.	Назначьте cisco в качестве пароля VTY и включите вход в систему по паролю.
#### g.	Зашифруйте открытые пароли.
#### h.	Создайте баннер, который предупреждает о запрете несанкционированного доступа.
#### i.	Настройте и активируйте на маршрутизаторе интерфейс G0/0/1, используя информацию, приведенную в таблице адресации.
#### j.	Сохраните текущую конфигурацию в файл загрузочной конфигурации.

>#### Немного забежала вперед, задала имя коммутатору - S1
```
Router>
Router>en
Router#
Router#conf t
Enter configuration commands, one per line.  End with CNTL/Z.
Router(config)#
Router(config)#host
Router(config)#hostname R1
R1(config)#
R1(config)#int
R1(config)#interface gi
R1(config)#interface gigabitEthernet 0/1
R1(config-if)#
R1(config-if)#ip ad
R1(config-if)#ip address 192.168.1.1 255.255.255.0
R1(config-if)#
R1(config-if)#no sh
R1(config-if)#no shutdown 

R1(config-if)#
%LINK-5-CHANGED: Interface GigabitEthernet0/1, changed state to up

%LINEPROTO-5-UPDOWN: Line protocol on Interface GigabitEthernet0/1, changed state to up

R1(config-if)#
R1(config-if)#serv
R1(config-if)#exit
R1(config)#serv
R1(config)#service pas
R1(config)#service password-encryption
R1(config)#
R1(config)#ena
R1(config)#enable sec
R1(config)#enable secret class
R1(config)#
R1(config)#bann
R1(config)#banner mo
R1(config)#banner motd #STOP!!!#
R1(config)#
R1(config)#lin
R1(config)#line con
R1(config)#line console 0
R1(config-line)#
R1(config-line)#pas
R1(config-line)#password cisco
R1(config-line)#
R1(config-line)#logi
R1(config-line)#login 
R1(config-line)#
R1(config-line)#logg
R1(config-line)#logging sy
R1(config-line)#logging synchronous 
R1(config-line)#
R1(config-line)#exit
R1(config)#
R1(config)#li
R1(config)#lin
R1(config)#line vt
R1(config)#line vty 0 4
R1(config-line)#
R1(config-line)#pas
R1(config-line)#password cisco
R1(config-line)#
R1(config-line)#exit
R1(config)#cop
R1(config)#^Z
R1#
%SYS-5-CONFIG_I: Configured from console by console

R1#
R1#
R1#cop
R1#copy ru
R1#copy running-config st
R1#copy running-config startup-config 
Destination filename [startup-config]? 
Building configuration...
[OK]
R1#

```

### Шаг 4. Настройте компьютер PC-A.

#### a.	Настройте для PC-A IP-адрес и маску подсети.
#### b.	Настройте для PC-A шлюз по умолчанию.

![](

### Шаг 5. Проверьте подключение к сети.
Пошлите с PC-A команду Ping на маршрутизатор R1. Если эхо-запрос с помощью команды ping не проходит, найдите и устраните неполадки подключения.

![](
>#### Эхо-запрос прошел без проблем

## Часть 2. Настройка маршрутизатора для доступа по протоколу SSH

### Шаг 1. Настройте аутентификацию устройств.

При генерации ключа шифрования в качестве его части используются имя устройства и домен. Поэтому эти имена необходимо указать перед вводом команды crypto key.

#### a.	Задайте имя устройства.
>#### Выполнила в первой части
#### b.	Задайте домен для устройства.
```
R1(config)#
R1(config)#ip dom
R1(config)#ip domain-
R1(config)#ip domain-na
R1(config)#ip domain-name WORK
```

### Шаг 2. Создайте ключ шифрования с указанием его длины.
```
R1(config)#
R1(config)#cry
R1(config)#crypto k
R1(config)#crypto key ge
R1(config)#crypto key generate rs
R1(config)#crypto key generate rsa g
R1(config)#crypto key generate rsa general-keys mod
R1(config)#crypto key generate rsa general-keys modulus 2048
The name for the keys will be: R1.WORK

% The key modulus size is 2048 bits
% Generating 2048 bit RSA keys, keys will be non-exportable...[OK]
*Mar 1 1:1:16.125: %SSH-5-ENABLED: SSH 1.99 has been enabled
R1(config)#ip ss
R1(config)#ip ssh v
R1(config)#ip ssh version 2
R1(config)#
```
### Шаг 3. Создайте имя пользователя в локальной базе учетных записей.
Настройте имя пользователя, используя admin в качестве имени пользователя и Adm1nP@55 в качестве пароля.
```
R1(config)#no username admin
R1(config)#
R1(config)#user
R1(config)#username admin pri
R1(config)#username admin privilege 15 se
R1(config)#username admin privilege 15 secret Adm1nP@55
R1(config)#
```
### Шаг 4. Активируйте протокол SSH на линиях VTY.

#### a.	Активируйте протоколы Telnet и SSH на входящих линиях VTY с помощью команды transport input.
#### b.	Измените способ входа в систему таким образом, чтобы использовалась проверка пользователей по локальной базе учетных записей.

```
R1(config)#lin
R1(config)#line vt
R1(config)#line vty 0 4
R1(config-line)#
R1(config-line)#tra
R1(config-line)#transport in
R1(config-line)#transport input al
R1(config-line)#transport input all 
R1(config-line)#
R1(config-line)#logi
R1(config-line)#login lo
R1(config-line)#login local 
R1(config-line)#
```
### Шаг 5. Сохраните текущую конфигурацию в файл загрузочной конфигурации.
```
R1(config-line)#^Z
R1#
%SYS-5-CONFIG_I: Configured from console by console

R1#
R1#cop
R1#copy st
R1#copy startup-config ru
R1#copy startup-config running-config 
Destination filename [running-config]? 

844 bytes copied in 0.416 secs (2028 bytes/sec)
R1#
%SYS-5-CONFIG_I: Configured from console by console

R1#
```
### Шаг 6. Установите соединение с маршрутизатором по протоколу SSH.

#### a.	Запустите Tera Term с PC-A.
#### b.	Установите SSH-подключение к R1. Use the username admin and password Adm1nP@55. У вас должно получиться установить SSH-подключение к R1.

![](

## Часть 3. Настройка коммутатора для доступа по протоколу SSH

### Шаг 1. Настройте основные параметры коммутатора.

#### a.	Подключитесь к коммутатору с помощью консольного подключения и активируйте привилегированный режим EXEC.
#### b.	Войдите в режим конфигурации.
#### c.	Отключите поиск DNS, чтобы предотвратить попытки маршрутизатора неверно преобразовывать введенные команды таким образом, как будто они являются именами узлов.
#### d.	Назначьте class в качестве зашифрованного пароля привилегированного режима EXEC.
#### e.	Назначьте cisco в качестве пароля консоли и включите вход в систему по паролю.
#### f.	Назначьте cisco в качестве пароля VTY и включите вход в систему по паролю.
#### g.	Зашифруйте открытые пароли.
#### h.	Создайте баннер, который предупреждает о запрете несанкционированного доступа.

```
Switch>en
Switch#
Switch#conf t
Enter configuration commands, one per line.  End with CNTL/Z.
Switch(config)#
Switch(config)#host
Switch(config)#hostname S1
S1(config)#
S1(config)#serv
S1(config)#service pas
S1(config)#service password-encryption
S1(config)#
S1(config)#ena
S1(config)#enable se
S1(config)#enable secret class
S1(config)#
S1(config)#lin
S1(config)#line co
S1(config)#line console 0
S1(config-line)#
S1(config-line)#pas
S1(config-line)#password cisco
S1(config-line)#
S1(config-line)#logg
S1(config-line)#logging sy
S1(config-line)#logging synchronous 
S1(config-line)#
S1(config-line)#log
S1(config-line)#logi
S1(config-line)#login 
S1(config-line)#
S1(config-line)#exit
S1(config)#ba
S1(config)#banner mo
S1(config)#banner motd #STOP!!!#
S1(config)#
S1(config)#line vty 0 4
S1(config-line)#pas
S1(config-line)#password cisco
S1(config-line)#
S1(config-line)#log
S1(config-line)#logi
S1(config-line)#login 
S1(config-line)#
```
#### i.	Настройте и активируйте на коммутаторе интерфейс VLAN 1, используя информацию, приведенную в таблице адресации.
#### j.	Сохраните текущую конфигурацию в файл загрузочной конфигурации.
```
S1(config-line)#exit
S1(config)#int
S1(config)#interface vla
S1(config)#interface vlan 1
S1(config-if)#
S1(config-if)#ip
S1(config-if)#ip ad
S1(config-if)#ip address 192.168.1.11 255.255.255.0
S1(config-if)#no sh
S1(config-if)#no shutdown 

S1(config-if)#
%LINK-5-CHANGED: Interface Vlan1, changed state to up

%LINEPROTO-5-UPDOWN: Line protocol on Interface Vlan1, changed state to up

S1(config-if)#
S1(config-if)#
S1(config-if)#exit
S1(config)#ip de
S1(config)#ip default-gateway 192.168.1.1
S1(config)#^Z
S1#
%SYS-5-CONFIG_I: Configured from console by console

S1#
S1#cop
S1#copy ru
S1#copy running-config st
S1#copy running-config startup-config 
Destination filename [startup-config]? 
Building configuration...
[OK]
S1#
```
### Шаг 2. Настройте коммутатор для соединения по протоколу SSH.

Для настройки протокола SSH на коммутаторе используйте те же команды, которые применялись для аналогичной настройки маршрутизатора в части 2.

#### a.	Настройте имя устройства, как указано в таблице адресации.
>#### Задала имя на шаге 1)

#### b.	Задайте домен для устройства.
#### c.	Создайте ключ шифрования с указанием его длины.
#### d.	Создайте имя пользователя в локальной базе учетных записей.
#### e.	Активируйте протоколы Telnet и SSH на линиях VTY.
#### f.	Измените способ входа в систему таким образом, чтобы использовалась проверка пользователей по локальной базе учетных записей.

```
S1(config)#
S1(config)#ip do
S1(config)#ip doma
S1(config)#ip domain-
S1(config)#ip domain-na
S1(config)#ip domain-name WORK
S1(config)#
S1(config)#cry
S1(config)#crypto ke
S1(config)#crypto key gen
S1(config)#crypto key generate rsa
S1(config)#crypto key generate rsa ge
S1(config)#crypto key generate rsa general-keys mod
S1(config)#crypto key generate rsa general-keys modulus 2048
The name for the keys will be: S1.WORK

% The key modulus size is 2048 bits
% Generating 2048 bit RSA keys, keys will be non-exportable...[OK]
*Mar 1 0:29:23.248: %SSH-5-ENABLED: SSH 1.99 has been enabled
S1(config)#ip ss
S1(config)#ip ssh ver
S1(config)#ip ssh version 2
S1(config)#user
S1(config)#username admin pri
S1(config)#username admin privilege 15 ce
S1(config)#username admin privilege 15 secr
S1(config)#username admin privilege 15 secret password
S1(config)#
S1(config)#lin
S1(config)#line vt
S1(config)#line vty 0 4
S1(config-line)#
S1(config-line)#tran
S1(config-line)#transport in
S1(config-line)#transport input ?
  all     All protocols
  none    No protocols
  ssh     TCP/IP SSH protocol
  telnet  TCP/IP Telnet protocol
S1(config-line)#transport input al
S1(config-line)#transport input all 
S1(config-line)#
S1(config-line)#logi
S1(config-line)#login local
S1(config-line)#
```
### Шаг 3. Установите соединение с коммутатором по протоколу SSH.

Запустите программу Tera Term на PC-A, затем установите подключение по протоколу SSH к интерфейсу SVI коммутатора S1.
Т.к. Tera Term не обеспечивает шифрование данных, воспользуюсь 
>#### Удалось ли вам установить SSH-соединение с коммутатором?
>Да, соединение по ssh установлено

## Часть 4. Настройка протокола SSH с использованием интерфейса командной строки (CLI) коммутатора
Клиент SSH встроен в операционную систему Cisco IOS и может запускаться из интерфейса командной строки. В части 4 вам предстоит установить соединение с маршрутизатором по протоколу SSH, используя интерфейс командной строки коммутатора.

### Шаг 1. Посмотрите доступные параметры для клиента SSH в Cisco IOS.
Используйте вопросительный знак (?), чтобы отобразить варианты параметров для команды ssh. 
S1# ssh? 

>Вариантов команды не так много(
```
S1#
S1#ssh ?
  -l  Log in using this user name
  -v  Specify SSH Protocol Version
S1#ssh
```
### Шаг 2. Установите с коммутатора S1 соединение с маршрутизатором R1 по протоколу SSH.
#### a.	Чтобы подключиться к маршрутизатору R1 по протоколу SSH, введите команду –l admin. Это позволит вам войти в систему под именем admin. При появлении приглашения введите в качестве пароля Adm1nP@55
```
S1#
S1#
S1#ssh -l admin 192.168.1.1

Password: 

STOP!!!

R1#
```
#### b.	Чтобы вернуться к коммутатору S1, не закрывая сеанс SSH с маршрутизатором R1, нажмите комбинацию клавиш Ctrl+Shift+6. Отпустите клавиши Ctrl+Shift+6 и нажмите x. Отображается приглашение привилегированного режима EXEC коммутатора.
```
R1#
S1#
```
#### c.	Чтобы вернуться к сеансу SSH на R1, нажмите клавишу Enter в пустой строке интерфейса командной строки. Чтобы увидеть окно командной строки маршрутизатора, нажмите клавишу Enter еще раз.
```
S1#
[Resuming connection 1 to 192.168.1.1 ... ]

R1#
```
#### d.	Чтобы завершить сеанс SSH на маршрутизаторе R1, введите в командной строке маршрутизатора команду exit.
```
R1#exit

[Connection to 192.168.1.1 closed by foreign host]
S1#
S1#
```

## 	Вопрос для повторения
>#### Как предоставить доступ к сетевому устройству нескольким пользователям, у каждого из которых есть собственное имя пользователя?
>Необходимо для каждого пользователя создать учетную запись с необходимыми правами. Доступно 16 уровней: 0-15, где 15 - привилегированный режим, 0 - самый низкий уровень.
>Для наглядности создам пользователя с минимальными правами и посморю какие команды ему доступны:
```
S1#conf t
Enter configuration commands, one per line.  End with CNTL/Z.
S1(config)#
S1(config)#user
S1(config)#username user
S1(config)#username user1 pr
S1(config)#username user1 privilege ?
  <0-15>  User privilege level
S1(config)#username user1 privilege 0 sec
S1(config)#username user1 privilege 0 secret qwerty
S1(config)#^Z
S1#
%SYS-5-CONFIG_I: Configured from console by console

S1#ssh -l user1 192.168.1.1

Password: 

STOP!!!

R1>?
Exec commands:
  disable     Turn off privileged commands
  enable      Turn on privileged commands
  exit        Exit from the EXEC
  logout      Exit from the EXEC
R1>
```
>Доступны только 4 команды
>И для сравнения посмотрию что доступно ранее созданному пользователю, у которого максимально возможные права:
```
S1#ssh -l admin 192.168.1.1
Password: 

STOP!!!

R1#?
Exec commands:
  <1-99>      Session number to resume
  auto        Exec level Automation
  clear       Reset functions
  clock       Manage the system clock
  configure   Enter configuration mode
  connect     Open a terminal connection
  copy        Copy from one file to another
  debug       Debugging functions (see also 'undebug')
  delete      Delete a file
  dir         List files on a filesystem
  disable     Turn off privileged commands
  disconnect  Disconnect an existing network connection
  enable      Turn on privileged commands
  erase       Erase a filesystem
  exit        Exit from the EXEC
  logout      Exit from the EXEC
  mkdir       Create new directory
  more        Display the contents of a file
  no          Disable debugging informations
  ping        Send echo messages
  reload      Halt and perform a cold restart
  resume      Resume an active network connection
  rmdir       Remove existing directory
  send        Send a message to other tty lines
  setup       Run the SETUP command facility
  show        Show running system information
  ssh         Open a secure shell client connection
  telnet      Open a telnet connection
  terminal    Set terminal line parameters
  traceroute  Trace route to destination
  undebug     Disable debugging functions (see also 'debug')
  vlan        Configure VLAN parameters
  write       Write running configuration to memory, network, or terminal
R1#
```
>С привилегированными правами доступны все возможные команды











































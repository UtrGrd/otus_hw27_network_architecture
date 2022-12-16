# OTUS ДЗ№27 Архитектура сетей

# Домашнее задание

### Дано
Vagrantfile с начальным  построением сети
inetRouter
centralRouter
centralServer

тестировалось на virtualbox

### Планируемая архитектура
построить следующую архитектуру

Сеть office1
- 192.168.2.0/26      - dev
- 192.168.2.64/26    - test servers
- 192.168.2.128/26  - managers
- 192.168.2.192/26  - office hardware

Сеть office2
- 192.168.1.0/25      - dev
- 192.168.1.128/26  - test servers
- 192.168.1.192/26  - office hardware


Сеть central
- 192.168.0.0/28    - directors
- 192.168.0.32/28  - office hardware
- 192.168.0.64/26  - wifi

```
Office1 ---\
      -----> Central --IRouter --> internet
Office2----/
```
Итого должны получится следующие сервера
- inetRouter
- centralRouter
- office1Router
- office2Router
- centralServer
- office1Server
- office2Server

### Теоретическая часть
- Найти свободные подсети
- Посчитать сколько узлов в каждой подсети, включая свободные
- Указать broadcast адрес для каждой подсети
- проверить нет ли ошибок при разбиении

### Практическая часть
- Соединить офисы в сеть согласно схеме и настроить роутинг
- Все сервера и роутеры должны ходить в инет черз inetRouter
- Все сервера должны видеть друг друга
- у всех новых серверов отключить дефолт на нат (eth0), который вагрант поднимает для связи
- при нехватке сетевых интервейсов добавить по несколько адресов на интерфейс

# Результат

### =================ТЕОРЕТИЧЕСКАЯ ЧАСТЬ=================

### >Сеть Central - свободные подсети есть.

#### 192.168.0.0/28 - directors
- Network:   192.168.0.0/28 (Class C)
- Broadcast: 192.168.0.15
- HostMin:   192.168.0.1
- HostMax:   192.168.0.14
- Hosts/Net: 14 (Private Internet)

#### 192.168.0.16/28 - Free
- Network:   192.168.0.16/28 (Class C)
- Broadcast: 192.168.0.31
- HostMin:   192.168.0.17
- HostMax:   192.168.0.30
- Hosts/Net: 14 (Private Internet)

#### 192.168.0.32/28 - office hardware
- Network:   192.168.0.32/28 (Class C)
- Broadcast: 192.168.0.47
- HostMin:   192.168.0.33
- HostMax:   192.168.0.46
- Hosts/Net: 14 (Private Internet)

#### 192.168.0.48/28 - Free
- Network:   192.168.0.48/28 (Class C)
- Broadcast: 192.168.0.63
- HostMin:   192.168.0.49
- HostMax:   192.168.0.62
- Hosts/Net: 14 (Private Internet)

#### 192.168.0.64/26 - wifi
- Network:   192.168.0.64/26 (Class C)
- Broadcast: 192.168.0.127
- HostMin:   192.168.0.65
- HostMax:   192.168.0.126
- Hosts/Net: 62 (Private Internet)

#### 192.168.0.128/25 - Free
- Network:   192.168.0.128/25 (Class C)
- Broadcast: 192.168.0.255
- HostMin:   192.168.0.129
- HostMax:   192.168.0.254
- Hosts/Net: 126 (Private Internet)

### >Сеть office1 - свободных подсетей нет.

#### 192.168.2.0/26 - dev
- Network:   192.168.2.0/26 (Class C)
- Broadcast: 192.168.2.63
- HostMin:   192.168.2.1
- HostMax:   192.168.2.62
- Hosts/Net: 62 (Private Internet)

#### 192.168.2.64/26 - test servers
- Network:   192.168.2.64/26 (Class C)
- Broadcast: 192.168.2.127
- HostMin:   192.168.2.65
- HostMax:   192.168.2.126
- Hosts/Net: 62 (Private Internet)

#### 192.168.2.128/26 - managers
- Network:   192.168.2.128/26 (Class C)
- Broadcast: 192.168.2.191
- HostMin:   192.168.2.129
- HostMax:   192.168.2.190
- Hosts/Net: 62 (Private Internet)

#### 192.168.2.192/26 - office hardware
- Network:   192.168.2.192/26 (Class C)
- Broadcast: 192.168.2.255
- HostMin:   192.168.2.193
- HostMax:   192.168.2.254
- Hosts/Net: 62 (Private Internet)

### >Сеть office2 - свободных подсетей нет.

#### 192.168.1.0/25 - dev
- Network:   192.168.1.0/25 (Class C)
- Broadcast: 192.168.1.127
- HostMin:   192.168.1.1
- HostMax:   192.168.1.126
- Hosts/Net: 126 (Private Internet)

#### 192.168.1.128/26 - test servers
- Network:   192.168.1.128/26 (Class C)
- Broadcast: 192.168.1.191
- HostMin:   192.168.1.129
- HostMax:   192.168.1.190
- Hosts/Net: 62 (Private Internet)

#### 192.168.1.192/26 - office hardware
- Network:   192.168.1.192/26 (Class C)
- Broadcast: 192.168.1.255
- HostMin:   192.168.1.193
- HostMax:   192.168.1.254
- Hosts/Net: 62 (Private Internet)

### =================ПРАКТИЧЕСКАЯ ЧАСТЬ=================


Поднять виртуальную сеть:
```
git clone git@github.com:UtrGrd/otus_hw27.git && cd otus_hw27 && vagrant up
```

Подключиться к серверам и пропинговать друг друга.
Подключиться к серверам и роутерам и пропинговать inetRouter.

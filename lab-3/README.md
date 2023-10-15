# ЗИС ПР №3. Deception

Выполнил Сердюков Матвей, ББМО-01-23

## Запуск honeypot

![](screenshots/start-service.png)

## Определение портов, открытых при запуске служб

![](screenshots/open-ports.png)

## Сканирование портов для определения запущенных служб

![](screenshots/nmap-scan.png)

## Запуск симуляции активности злоумышленника

![](screenshots/run-hacker.png)

## Фильтрация и сохранение логов контейнера для дальнейшего анализа

![](screenshots/save-log.png)

## Анализ действий злоумышленника

### FTP - port 21

#### Выполненные команды

```
USER anonymous
PASS anonymous
FEAT
STOR /etc/passwd
LIST -l
HELP
APPE /exploit.sh
PWD
```

### SSH

#### Выполненные команды

```
аутентификация с учётными данными root:root
ss -tunlp
cat /etc/shadow
pwd
ls
ip a
```

### telnet

#### Выполненные команды

```
аутентификация с учётными данными root:root
display snmp-server arp-sync table
system-view
display arp interface GigabitEthernet 0/0/1
display arp
display session limit vpn-instance vpna
```

### HTTP

```
GET /robots.txt
GET /admin
GET /phpinfo.php
GET /admin.php
GET /login.php
```

### redis

```
GET admin
KEYS * 
SELECT 1
CONFIG GET *
INFO
```
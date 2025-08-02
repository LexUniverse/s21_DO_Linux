## Part 1
### 1.1. Сети и маски

![img.png](ScreenShots%2FPart1%2Fimg.png)

- Адресс сети 192.167.38.54/13 вычесленый с помощью ipcalc

![img_1.png](ScreenShots%2FPart1%2Fimg_1.png)

- ipcalc показал:
- 255.255.255.0 = 11111111.1111111.1111111.00000000 = 24
- /15 = 11111111.11111110.0000000.0000000 = 255.254.0.0


![img_2.png](ScreenShots%2FPart1%2Fimg_2.png)

- 11111111.11111111.11111111.11110000 = 28 = 255.255.255.240

![img_3.png](ScreenShots%2FPart1%2Fimg_3.png)

- Минимальный и максимальный хост для  /8, 11111111.11111111.00000000.00000000, 255.255.254.0

![img_4.png](ScreenShots%2FPart1%2Fimg_4.png)

- Минимальный и максимальный хост для  /4

### 1.2. localhost

![img_5.png](ScreenShots%2FPart1%2Fimg_5.png)

- Диапазон localhost - 127.0.0.0/8 (127.0.0.1 - 127.255.255.254)
- Адрес 194.34.23.100 принадлежит публичной сети (Class C)
- Адрес 127.0.0.2 принадлежит Class A, Loopback
- Адрес 127.1.0.1 принадлежит Class A, Loopback

![img_6.png](ScreenShots%2FPart1%2Fimg_6.png)

- Адрес 128.0.0.1 принадлежит Class B
- Получается, что обратиться с localhost можно только к 127.0.0.2 и 127.1.0.1

### 1.3. Диапазоны и сегменты сетей

![img_7.png](ScreenShots%2FPart1%2Fimg_7.png)

- Команой ``` for ip in 10.0.0.45 134.43.0.2 192.168.4.2 172.20.250.4 172.0.2.1 192.172.0.1 172.68.0.2 172.16.255.255 10.10.10.10 192.169.168.1; do
  echo -n "$ip: " &&
  ipcalc "$ip" | grep -E "Private|Class" | grep -oE "Private|Class [ABC]"
  done``` получаем вывод, Private - частные IP, те, под которыми нет этой надписи, публичные

![img_8.png](ScreenShots%2FPart1%2Fimg_8.png)

- Схожей командой с регулярным выражением получаем ответ, возможны ли ip у сети

## Part 2

![img.png](ScreenShots%2FPart2%2Fimg.png)

- Выполнение команды ip a на ws1

![img_1.png](ScreenShots%2FPart2%2Fimg_1.png)

- Выполнение команды ip a на ws2

![img_2.png](ScreenShots%2FPart2%2Fimg_2.png)

- Измененный файл конфигурации на ws1

![img_3.png](ScreenShots%2FPart2%2Fimg_3.png)

- Измененный файл конфигурации на ws2

![img_4.png](ScreenShots%2FPart2%2Fimg_4.png)

- Выполнение sudo netplan apply на двух машинах


### 2.1. Добавление статического маршрута вручную

![img_5.png](ScreenShots%2FPart2%2Fimg_5.png)

- Добавление статического маршрута + пинг

![img_6.png](ScreenShots%2FPart2%2Fimg_6.png)

- Добавление статического маршрута после перезагрузки (с сохранением)

![img_7.png](ScreenShots%2FPart2%2Fimg_7.png)

- Перезапуск сервиса сети и пинг соединения между машинами

## Part 3

### 3.1. Скорость соединения

- bps - биты
- B - байты

- 8 Mbps - MB/s = 8 Mpbs / 8 bits - 8 MB/s
- 100 MB/s = 1024 KB * 100 MB/s * 8 bits = 819 200 Kbps
- 1 Gbps = 1024 Mbps * 1 Gbps = 1024 Mbps

![img.png](ScreenShots%2FPart3%2Fimg.png)

- Проверка скорости соединения между ws1 и ws2

## Part 4

### 4.1. Утилита iptables

![img.png](ScreenShots%2FPart4%2Fimg.png)

- Скриншот конфигурации файервола на двух машинах

![img_1.png](ScreenShots%2FPart4%2Fimg_1.png)

- ws1: Запрещает всё по умолчанию, затем разрешает выборочно (более безопасно). 
- ws2: Разрешает всё по умолчанию, затем запрещает выборочно (менее безопасно, но проще для отладки).

```
# Описание пакетов:
Input - Обрабатываются входящие подключения вроде подключения по протоколу SSH или при отправке на веб-сайт каких-либо файлов.
Output - Исходящие пакеты данных, например, при запуске какого-либо сайта в браузере или при проверке скорости соединения и доступности PING.

# Примеры действий:
ACCEPT – пропустить пакет данных далее по цепочке

DROP – полностью удалить пакет

# Перечень основных действий, для выполнения которых используется Iptables:
-A – добавить правило в цепочку;
-F – очистить все правила;
-X – удалить цепочку;
-P – установить действие «по умолчанию».

#В качестве дополнительных параметров используются опции:
-p – вручную установить протокол (TCP, UDP, UDPLITE, ICMP, ICMPv6, ESP, AH, SCTP, MH);
-j – выбрать действие при подтверждении правила.
```

### 4.2. Утилита nmap

![img_2.png](ScreenShots%2FPart4%2Fimg_2.png)

- Вывод работы nmap и проверки firewall

## Part 5 

### 5.1. Настройка адресов машин

![img.png](ScreenShots%2FPart5%2Fimg.png)

- Конфигурация сети всех машин


![img_1.png](ScreenShots%2FPart5%2Fimg_1.png)

- Применение конфигурации

![img_2.png](ScreenShots%2FPart5%2Fimg_2.png)

- Адрес машин задан верно

![img_3.png](ScreenShots%2FPart5%2Fimg_3.png)

- Пинг с ws22 до ws21 проходит, пинг с ws11 до r1 проходит

### 5.2. Включение переадресации IP-адресов

![img_4.png](ScreenShots%2FPart5%2Fimg_4.png)

- Включение переадресации без сохранения после перезагрузки

![img_5.png](ScreenShots%2FPart5%2Fimg_5.png)

- Изменение конфигурации для сохранения после перезагрузки

### 5.3. Установка маршрута по умолчанию

![img.png](ScreenShots%2FPart5%2Fimg.png)

- Скриншот со статическими маршрутами

![img_6.png](ScreenShots%2FPart5%2Fimg_6.png)

- Проверка добавления статических маршрутов на рабочие станции

![img_7.png](ScreenShots%2FPart5%2Fimg_7.png)

- Пинг r2 с ws11

### 5.4. Добавление статических маршрутов

![img_8.png](ScreenShots%2FPart5%2Fimg_8.png)

- Скриншот со статическими маршрутами

![img_9.png](ScreenShots%2FPart5%2Fimg_9.png)

- Проверка добавления статических маршрутов на роутерах

![img_10.png](ScreenShots%2FPart5%2Fimg_10.png)

- Для 10.10.0.0/18 выводится конкретный маршрут через интерфейс eth0
- Это локальная сеть, поэтому трафик направляется напрямую через eth0, без использования шлюза.


- Для 0.0.0.0/0 выводится маршрут по умолчанию через шлюз 10.10.0.1
- Этот маршрут используется для всех адресов, не принадлежащих локальной сети

### 5.5. Построение списка маршрутизаторов

![img_11.png](ScreenShots%2FPart5%2Fimg_11.png)

- Результат использования команды дампа и отслеживания маршрута до нужной машины
- ```traceroute отправляет пакеты с увеличивающимся TTL. Каждый роутер на пути уменьшает TTL и отправляет ICMP-уведомление, что позволяет определить маршрут. То есть сначала отправляется пакет с TTL=1 смотрится откуда ответ о смерти пакета, потом TTL=2 и так пока не дойдет до нужной машины.```

![img_12.png](ScreenShots%2FPart5%2Fimg_12.png)

- Скрин с перехватом пакета роутером

## Part 6

![img.png](ScreenShots%2FPart6%2Fimg.png)

- Отредактрованный файл конфигурации dhcp

![img_1.png](ScreenShots%2FPart6%2Fimg_1.png)

- Добавление nameserver 

![img_2.png](ScreenShots%2FPart6%2Fimg_2.png)

- Перезагрузка службы DHCP

![img_3.png](ScreenShots%2FPart6%2Fimg_3.png)

- Вывод обновленного ip и пинг ws22 с ws21

![img_4.png](ScreenShots%2FPart6%2Fimg_4.png)

- Добавление MAC адреса в конфиг ws11

![img_5.png](ScreenShots%2FPart6%2Fimg_5.png)

- Настройка r1 налогично r2 с жесткой привязкой к MAC адресу

![img_6.png](ScreenShots%2FPart6%2Fimg_6.png)

- Перезагрузка службы DHCP

![img_9.png](ScreenShots%2FPart6%2Fimg_9.png)

- Вывод обновленного ip и пинг ws22 с ws11

![img_7.png](ScreenShots%2FPart6%2Fimg_7.png)

- До обновления

![img_8.png](ScreenShots%2FPart6%2Fimg_8.png)

- После обновления

- ```
  Использованные опции DHCP:
  range — диапазон выдаваемых адресов.
  fixed-address — статический IP по MAC.
  option routers — шлюз по умолчанию.
  domain-name-servers — DNS-сервер.
  ```

## Part 7

![img.png](ScreenShots%2FPart7%2Fimg.png)

- Изменение файлов конфигурации сервера Apache2 на r1 и ws22

![img_1.png](ScreenShots%2FPart7%2Fimg_1.png)

- Запуск служб на машинах

![img_2.png](ScreenShots%2FPart7%2Fimg_2.png)

- Конфигурация фаервола на r2

![img_3.png](ScreenShots%2FPart7%2Fimg_3.png)

- Применение фаервола и попытка пинга (должна быть неудачной)

![img_4.png](ScreenShots%2FPart7%2Fimg_4.png)

- Раскоментируем правило на пропуск icmp (для работы ping)

![img_5.png](ScreenShots%2FPart7%2Fimg_5.png)

- Пинг проходит после применения изменений

![img_8.png](ScreenShots%2FPart7%2Fimg_8.png)

- Исправленый фаервол с новыми правилами для DNAT и SNAT

![img_6.png](ScreenShots%2FPart7%2Fimg_6.png)

- Проверка подключения по TCP для SNAT, с ws22 на сервер apache2 на r1

![img_7.png](ScreenShots%2FPart7%2Fimg_7.png)

- Проверка подключения по TCP для NAT, с r1 на сервер apache ws22 (по адресу r2 и порту 8080)

## Part8 *

![img.png](ScreenShots%2FPart8%2Fimg.png)

- Изменение конфигурации apache2 для запуска только на localhost

![img_1.png](ScreenShots%2FPart8%2Fimg_1.png)

- Подключаемся в локальной сети с ws21 к ws22, через ssh

![img_2.png](ScreenShots%2FPart8%2Fimg_2.png)

- Подключаемся из удаленной сети к ws22 с ws11, через ssh

![img_3.png](ScreenShots%2FPart8%2Fimg_3.png)

- Проверка подключения с ws21

![img_4.png](ScreenShots%2FPart8%2Fimg_4.png)
University: [ITMO University](https://itmo.ru/ru/)\
Faculty: [FICT](https://fict.itmo.ru)\
Course: [Network programming](https://github.com/itmo-ict-faculty/network-programming)\
Year: 2022/2023\
Group: K34202\
Author: Sidorenko Darya Alekseevna\
Lab: Lab3\
Date of create: 15.12.2022\
Date of finished: \
Ход работы:
1. Netbox развёрнут на облачной виртуальной машине. Netbox — это open source веб приложение, разработанное для управления и документирования компьютерных сетей.\
2. Установлена база данных postgresql и выполнена настройка. Создана база данных и привелегированный пользователь. \
3.  Установлен Redis с помощью команды ```sudo apt install -y redis-server```. Redis - это хранилище значений ключей в памяти. NetBox использует его для кэширования и постановки в очередь.\
4.  Для установки и настройки Netbox установлены все необходимые пакеты с помощью утилиты ```sudo apt install```. Создана директория, в неё установлен и распакован Netbox.\
5.  Создан пользователь, которому предоставлены права на все папки и файлы Netbox.\ Использованы следюущие команды. \ ```groupadd --system netbox``` \ ```sudo adduser --system -g netbox netbox```\ ```chown --recursive netbox /opt/netbox/netbox/media/```\
6.  Создано виртуальное окружение, где установлены все зависимости. \ ```python3 -m venv /opt/netbox/venv```\ ```source venv/bin/activate``` \ ```pip3 install -r requirements.txt```\
7.  В файл конфигурации configuration.py скопирован пример файла конфигурации configuration.example.py с помощью утилит ```cd```, ```cp```. \
8.  

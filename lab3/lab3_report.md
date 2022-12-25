University: [ITMO University](https://itmo.ru/ru/)\
Faculty: [FICT](https://fict.itmo.ru)\
Course: [Network programming](https://github.com/itmo-ict-faculty/network-programming) \
Year: 2022/2023\
Group: K34202\
Author: Sidorenko Darya Alekseevna\
Lab: Lab3\
Date of create: 15.12.2022\
Date of finished: \
Ход работы:
1. Netbox развёрнут на облачной виртуальной машине. Netbox — это open source веб приложение, разработанное для управления и документирования компьютерных сетей.\
2. Установлена база данных postgresql и выполнена настройка. Создана база данных и привелегированный пользователь.\
![1](https://user-images.githubusercontent.com/80837580/209463031-6dcbbeb2-2a04-47fa-add5-f1f3be696c53.png)\
3.  Установлен Redis с помощью команды ```sudo apt install -y redis-server```. Redis - это хранилище значений ключей в памяти. NetBox использует его для кэширования и постановки в очередь.\
![2](https://user-images.githubusercontent.com/80837580/209462953-980879cb-a1bb-456f-8e5d-826482614db7.png)\
4.  Для установки и настройки Netbox установлены все необходимые пакеты с помощью утилиты ```sudo apt install```. Создана директория, в неё установлен и распакован Netbox.\
5.  Создан пользователь, которому предоставлены права на все папки и файлы Netbox.\ Использованы следующие команды. \ ```groupadd --system netbox``` \ ```sudo adduser --system -g netbox netbox```\ ```chown --recursive netbox /opt/netbox/netbox/media/```\
6.  Создано виртуальное окружение, где установлены все зависимости. \ ```python3 -m venv /opt/netbox/venv```\ ```source venv/bin/activate``` \ ```pip3 install -r requirements.txt```\
7.  В файл конфигурации configuration.py скопирован пример файла конфигурации configuration.example.py с помощью утилит ```cd```, ```cp```. \
8.  С помощью входящего в состав netbox исполнительного файла gnerate_secret_key.py сгенерирован секретный ключ. Открыт и отредактирован файл конфигурации configuration.py.\
![2](https://user-images.githubusercontent.com/80837580/209462991-cc512017-960d-4a2e-923e-28e1d03bbe3d.png)\
9. Выполнены миграции с помощью команды ```python3 manage.py migrate```. Внутри вирутального окружения создан superuser для дальнейшего управления netbox. Собрана статика ```python3 manage.py collectstatic --no-input```.\


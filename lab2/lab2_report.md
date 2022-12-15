University: [ITMO University](https://itmo.ru/ru/)\
Faculty: [FICT](https://fict.itmo.ru)\
Course: [Network programming](https://github.com/itmo-ict-faculty/network-programming)\
Year: 2022/2023\
Group: K34202\
Author: Sidorenko Darya Alekseevna\
Lab: Lab2\
Date of create: 01.12.2022\
Date of finished: \
Цель работы: настройка нескольких сетевых устройств с помощью Ansible и сбор информации о них, правильная сборка файла Inventory.\
Ход работы:
1. Создана вторая виртуальная машина через VirtualBox. На ней установлен CHR Mikrotik. Машина аналогичено первой настроена как OpernVPN клиент.\
![1im](https://user-images.githubusercontent.com/80837580/207798701-0ea26f2d-9730-43b9-a71d-a96e00e1163d.jpg)
![2im](https://user-images.githubusercontent.com/80837580/207799041-0706f3cf-4edf-451b-bd50-cd050d2aea1b.png)
2. Настроен Ansible. Для этого в консоли настроена генерация ключей, в VirtualBox добавлено NAT-соединение, прописаны SSH-порты.
![3im](https://user-images.githubusercontent.com/80837580/207799513-2284d03b-8ac6-41bc-9428-344389eac8f0.png)
![4im](https://user-images.githubusercontent.com/80837580/207799603-3949510d-858a-45d1-b39d-c58ec849edf5.png)
3. На облаке создан файл hosts.ini, где указаны адреса машин, которые должны управляться Ansible. Адреса сгруппированы в группу Routers, для каждого элемента которой назначен набор переменных.
![5im](https://user-images.githubusercontent.com/80837580/207800028-fa28a880-c85f-4b14-b254-64b64acbdb93.png)


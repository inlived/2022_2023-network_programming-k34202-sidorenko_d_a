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
1. Создана вторая виртуальная машина через VirtualBox. На ней установлен CHR Mikrotik. Машина аналогично первой настроена как OpernVPN клиент.\
![1im](https://user-images.githubusercontent.com/80837580/207798701-0ea26f2d-9730-43b9-a71d-a96e00e1163d.jpg)
![2im](https://user-images.githubusercontent.com/80837580/207799041-0706f3cf-4edf-451b-bd50-cd050d2aea1b.png)
2. Настроен Ansible. Для этого в консоли настроена генерация ключей, в VirtualBox добавлено NAT-соединение, прописаны SSH-порты.\
![3im](https://user-images.githubusercontent.com/80837580/207799513-2284d03b-8ac6-41bc-9428-344389eac8f0.png)
![4im](https://user-images.githubusercontent.com/80837580/207799603-3949510d-858a-45d1-b39d-c58ec849edf5.png)
3. На облаке создан файл hosts.ini, где указаны адреса машин, которые должны управляться Ansible. Адреса сгруппированы в группу Routers, для каждого элемента которой назначен набор переменных.\
![5im](https://user-images.githubusercontent.com/80837580/207800028-fa28a880-c85f-4b14-b254-64b64acbdb93.png)
4. Создан файл playbook.yml в директории /etc/ansible. В него добавлен плей, в котором расположено несколько тасок, каждая из которых отвечает за свою задачу. Большая часть из них выполняется с помощью модуля community.routeros.command, который отвечает за запуск команд на удаленных устройствах под управлением MikroTik RouterOS.
5. С помощью community.routeros.command прописаны команды для выполнения следу.щих задач: создан новый пользователь, настроены параметры для NTP клиента, произведена настройка OSPF маршрутизации в сети между двумя роутерами, собрана информация о конфигурации устройств.\
![6im](https://user-images.githubusercontent.com/80837580/207800774-5d86bbac-d309-4e0f-8c7b-1cc081beb008.png)
6. Проведена проверка на роутерах. Активирован NTP клиент, для которого указаны первичный и вторичный сервера для настройки точного времени.\
![7im](https://user-images.githubusercontent.com/80837580/207801408-dce5814e-1b02-45f4-9444-46d65de63f8d.jpg)
7. Проверена настройка OSPF маршрутизации. Роутеры видят друг друга в качестве соседей в одной сети, а также между ними установлена связность адресов.\
![8im](https://user-images.githubusercontent.com/80837580/207801636-10de728d-85d5-4e85-82f6-38dd91c7f5df.png)
![9im](https://user-images.githubusercontent.com/80837580/207801680-99a3c155-dafd-47c5-8c49-daf0fdc5a653.png)
Вывод:\
В ходе выполнения лабораторной работы был создан еще один CHR. Удалённо были проведены настройки обоих CHR с помощью Ansible, установленного на ВМ, находящейся в YandexCloud.\
![Диаграмма без названия](https://user-images.githubusercontent.com/80837580/207804492-acfae38e-0535-48fe-b1f3-d54865c61fd9.png)

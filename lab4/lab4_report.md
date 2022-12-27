University: [ITMO University](https://itmo.ru/ru/)\
Faculty: [FICT](https://fict.itmo.ru)\
Course: [Network programming](https://github.com/itmo-ict-faculty/network-programming)\
Year: 2022/2023\
Group: K34202\
Author: Sidorenko Darya Alekseevna\
Lab: Lab3\
Date of create: 20.12.2022\
Date of finished: \
Ход работы:
## Установка vm-ubuntu-20.04
+ На диск склонирован указанный p4lang/tutorials
+ Предварительно установлен Vagrant и VirtualBox
+ C помощью команды vagrant up установлена vm-ubuntu-20.04 \
![image](https://user-images.githubusercontent.com/80837580/209590824-43916587-96c3-4fab-9be7-59cd9143d50a.png)
## Implementing Basic Forwarding
Целью является дописать программу P4, реализующиую базовую переадресацию. В basic.p4 уже есть определнный скилет программы, но в некоторых частях отсутсвуют данные. Вместо отсутсвующих данный размещены комментарии, чтобы помочь дописать верный код.\
![image](https://user-images.githubusercontent.com/80837580/209590923-0db95868-0682-4c01-8896-e87b5757a50e.png)
+ С помощью команды `make run` в папке с заданием скомпилирован basic.p4. После этого запущен mininet (эмулятор компьютерной сети) \
 ![image](https://user-images.githubusercontent.com/80837580/209590928-f824734e-1d98-4cae-ba1c-133050d40848.png)
+ После команды ping все пакеты сбрасывались, как и ожидалось. Для того чтобы исправить это открыт файл basic.p4.\
 ![image](https://user-images.githubusercontent.com/80837580/209590935-0eb86c84-6a6e-448d-80c1-b9d8c1b8290b.png)
+ Файл разбит на разделы. В некоторых разделах стоя комментарии-подсказки, которые помогут реализовать в итоге базовую пересылку. 
+ Раздел Parser (Парсер в P4 — это функция, которая отображает пакеты в заголовках и метаданные, написанные уже на языке конечного автомата.) – добавлен парскинг ethernet и ipv4 headers \
![image](https://user-images.githubusercontent.com/80837580/209590950-9319c33f-52f0-44c9-9975-5e8997118805.png)
+ Раздел Ingress Processing (содержит методы, необходимые для обработки пакета на плане управления): добавлен метод, отвечающий за пересылки пакетов. А также выполняющий:  Задает порт выхода для следующего перехода, обновляет адрес назначения Ethernet адресом следующего перехода, обновляет адрес источника Ethernet адресом коммутатора, уменьшает значение TTL. Также прописано условие проверки правильности заголвка ipv4. \
![image](https://user-images.githubusercontent.com/80837580/209590958-801d7f17-09a3-43c6-b8ad-32dd6b2252ca.png)
+ Раздел Deparsers(отвечает за обратное преобразование пакетов в данные, понятные машине):   добавлен депарсинг ethernet и ipv4 headers \
![image](https://user-images.githubusercontent.com/80837580/209590969-b4f41273-e516-4dbd-8d79-d244d26ffc95.png)
+ Повторно выполнена эмуляция сети. Все коммутаторы теперь могут связаться друг с другом. \
![image](https://user-images.githubusercontent.com/80837580/209590991-17cc9489-9dc0-4df9-a957-d7b19ab606fc.png) \
![image](https://user-images.githubusercontent.com/80837580/209591216-1cbe71b3-88b0-4aac-9586-fa5c091b484c.png)

## Implementing Basic Tunneling
+ Перенаправление пакетов уже реализовано в шаблоне программы.
+Цель: Необходимо дополнить шаблон таким образом, чтобы была возможность осуществлять туннелирование между всеми коммутаторами в сети, представленной на диаграмме ниже \
![image](https://user-images.githubusercontent.com/80837580/209591278-07f72a46-11f6-4fe2-b882-cd482c900017.png)

+ По аналогии с предыдыщим заданием необходимо в папке задания отредактировать файл basic_tunnel.p4
+ Parsers: добавлено новое состояние state parse_myTunnel (преобразует туннельный заголовок: если id протокола соответсвует IPv4, то parser переходит в состояние преобразование IP-пакета, а по умолчанию - принимает пакеты). Новое состояние также добавлено в оператор select в state parse_ethernet \
![image](https://user-images.githubusercontent.com/80837580/209591328-56c13e58-6277-443d-9cba-2a57be4ba7f5.png)
+ Ingress processing: добавлено действие myTunnel_forward(egressSpec_t port) которое устанавливает выходной порт (т.е. поле egress_spec поле standard_metadata) на номер порта, предоставленный плоскостью управления. Добавлена новая таблица myTunnel_exact. Эта таблица должна вызывать либо фунуцию myTunnel_forward, если в таблице есть совпадение значения поля dst_id, либо действие drop в противном случае \
![image](https://user-images.githubusercontent.com/80837580/209591376-66e6c6da-42eb-44d9-b6a2-3977e41f9f47.png) \
![image](https://user-images.githubusercontent.com/80837580/209591407-22a657ec-1c62-42dc-a1fb-15ce23564a88.png)

+ Deparsers: добавлено преобразование пакетов туннелирования.\
![image](https://user-images.githubusercontent.com/80837580/209591449-f285f010-94d6-4244-a6e8-7657788a7e70.png)

+ Выполнен вход в mininet, открыто два терминала.
+ Протестировано тестирование без туннелирования. В H2 отправлен пакет из H1,  в назначении указан только айпи адрес получателя: ` ./send.py 10.0.2.2 “test without tunn”`. Сообщение получено. \
 ![image](https://user-images.githubusercontent.com/80837580/209591498-33a34f56-8283-4862-b7f1-810cde2298e2.png)

+ Тестирование с туннелированием. Теперь в команду отправки добавлено некоторое изменение `./send.py 10.0.2.2 "message" --dst_id 2`. \
![image](https://user-images.githubusercontent.com/80837580/209591544-4cadf824-d0c6-4e04-a473-4705490993ca.png)

+ Если указать неверный айпи адрес, то сообщение все равно будет получено h2. Это связано с тем, что коммутатор больше не использует IP-заголовок для маршрутизации, когда заголовок MyTunnel находится в пакете. : \
![image](https://user-images.githubusercontent.com/80837580/209591590-d6ab138c-c4a9-4a4c-9f97-cd25817decdc.png)

## Вывод
Были успешно реализованы базовая переадресация и базовое туннелирование с помощью языка P4. В ходе работы был изучен синтаксис языка P4.




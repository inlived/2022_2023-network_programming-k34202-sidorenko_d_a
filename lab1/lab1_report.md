University: [ITMO University](https://itmo.ru/ru/)\
Faculty: [FICT](https://fict.itmo.ru)\
Course: [Network programming](https://github.com/itmo-ict-faculty/network-programming)\
Year: 2022/2023\
Group: K34202\
Author: Sidorenko Darya Alekseevna\
Lab: Lab1\
Date of create: 16.10.2022\
Date of finished: \
Цель работы: развертывание виртуальной машины с установленной системой контроля конфигураций Ansible и установка CHR в VirtualBox\
Ход работы:
1. Создана ВМ на Яндекс.Облаке, произведено подключение к ней по shh. 
![image](https://user-images.githubusercontent.com/80837580/196762988-019cd044-c380-4f6b-91aa-5d935ab69a9f.png)
2. Выполнено обновление версий до последних.
![image](https://user-images.githubusercontent.com/80837580/196764018-6943f436-428e-4ac7-b56f-78153f9e124c.png)
![image](https://user-images.githubusercontent.com/80837580/196764245-586a2a79-28d6-472a-8baa-272651bb7342.png)
3. Установлен python 3 pip, выполнен переход в необходимую папку для дальнейшей работы.
![image](https://user-images.githubusercontent.com/80837580/196764693-9d6699df-eddf-48ab-b2b2-771eb9d3cd9f.png)
4. Установлен Ansible, проверена его версия.
![image](https://user-images.githubusercontent.com/80837580/196765910-0de939cb-8fd4-48c1-a999-a0e4da3e7c44.png)
![image](https://user-images.githubusercontent.com/80837580/196766296-086b4a20-20e4-4e7b-8046-60f9583cbabc.png)
5. На удаленную машину установлен Wireguarg для будущего туннеля между Микротиком и ВМ, показана версия установленного Wireguard.
![image](https://user-images.githubusercontent.com/80837580/196767101-5cbd538b-52c6-4db3-80c7-e7c727fd1e19.png)
6. Создана и запущена виртуальная машина версии Mikrotik 7.
![image](https://user-images.githubusercontent.com/80837580/196767347-db00db29-9510-4b8a-bb47-7eefe942c8e1.png)
![image](https://user-images.githubusercontent.com/80837580/196771880-56ce9c18-f754-4e5f-9d43-628c12b4a651.png)
7. Подключен WinBox для интерфейса виртуальной машины Mikrotik.
![image](https://user-images.githubusercontent.com/80837580/196772328-de1f02d3-f697-4e09-b7cc-910924ee314b.png)
8. Создан интерфейс с помощью WinBox.
![image](https://user-images.githubusercontent.com/80837580/196772555-e0393ec2-9ba8-4dd7-babd-0a43a9d6c04d.png)
9. Создана пара ключей для интерфейса.
![image](https://user-images.githubusercontent.com/80837580/196774331-3bf7f2a9-d9e6-483c-88d0-5f9e2221950f.png)
10. Чтобы узнать значение ListenPort, открыт файл /etc/wireguard/wg0.conf.
![image](https://user-images.githubusercontent.com/80837580/196776170-43743261-8273-4806-bf97-a81cf1a889ae.png)
11. Выполнены настройки Peer, подключение к созданному интерфейсу.
![image](https://user-images.githubusercontent.com/80837580/196777780-ebd477ed-012b-4dad-8d42-342b9af71be3.png)
12. Выполнены настройки IP, указана выбранная сеть и созданный интерфейс.
![image](https://user-images.githubusercontent.com/80837580/196778066-bbcb01f2-3469-4f4e-a766-711ecb35c57a.png)
13. Создан файервол. 
![image](https://user-images.githubusercontent.com/80837580/196778377-0583f914-7b1f-4af4-94aa-8f86bcd241cc.png)
14. Заполнен файл wg0.conf
![image](https://user-images.githubusercontent.com/80837580/196779984-66dc4987-4ba8-4f57-969a-0782db4e0861.png)
15. Произведен ping для проверки соединения, всё успешно. 
![image](https://user-images.githubusercontent.com/80837580/196780892-6ad38feb-af52-4637-8f10-c9cc16d314a8.png)
16. В результате получена связь по следующей схеме. 
![lab1_networks (1)](https://user-images.githubusercontent.com/80837580/197171752-d34ea5f5-c2bd-40f3-b60a-0773ae3088f8.jpg)

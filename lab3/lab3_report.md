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

---

# Поднятие NetBox на дополнительной VM.
Netbox — это открытое (open source) веб приложение, разработанное для управления и документирования компьютерных сетей. 
+ Netbox был развёрнут на облачной виртуальной машине.
 
 ## Установка и настройка PostgreSQL
 
+ Установлена база данных postgresql и выполнена настройка. Использована следующая команда `sudo apt install postgresql`

+ Создана нужная база данных и привелегированный пользователь.

![1](https://user-images.githubusercontent.com/80837580/209463394-fda06599-7c6f-42a5-96f8-0249758b7213.png)

## Установка Redis
Redis - это хранилище значений ключей в памяти. NetBox использует его для кэширования и постановки в очередь.
+ Установлен Redis с помощью команды  `sudo apt install -y redis-server`

![2](https://user-images.githubusercontent.com/80837580/209463420-5332f418-dc34-4ecf-81af-e1df1d700aec.png)

## Установка и настройка NetBox

+ Установлены все необходимые пакеты для дальнейшей установки и настройки Netbox.

`sudo apt install python3 python3-pip python3-venv python3-dev build-essential libxml2-dev libxslt1-dev libffi-dev libpq-dev libssl-dev zlib1g-dev git -y`

+ Создана директория, в которую установлен и распакован Netbox.

`sudo wget https://github.com/netbox-community/netbox/archive/refs/tags/v3.3.9.tar.gz`

`sudo tar -xzf v3.3.9.tar.gz -C /opt`

`sudo ln -s /opt/netbox-3.3.9/ /opt/netbox`

+ Создан пользователь с предоставленными правами на все папки и файлы Netbox.

`groupadd --system netbox`

`sudo adduser --system -g netbox netbox`

`chown --recursive netbox /opt/netbox/netbox/media/`

+ Создано виртуальное окружение, где установлены все зависимости.

`python3 -m venv /opt/netbox/venv`

`source venv/bin/activate`

`pip3 install -r requirements.txt`

+ Cкопирован пример файла конфигурации configuration.example.py в файл конфигурации configuration.py.

`cd netbox/netbox/`

`cp configuration.example.py configuration.py`

+ С помощью входящего в состав netbox исполнительного файла gnerate_secret_key.py сгенерирован секретный ключ.

`netbox/generate_secret_key.py`

+ Открыт и отредактирован файл конфигурации configuration.py.

`nano /opt/netbox/netbox/netbox/configuration.py`

![3](https://user-images.githubusercontent.com/80837580/209463463-2b320ca7-1833-4fb9-be5e-d57cfff4edfc.png)

+ Выполнены миграции

`python3 manage.py migrate`

+ Внутри вирутального окружения создан superuser для дальнейшего управления netbox.

`python3 manage.py createsuperuser`

+ Собрана статика

`python3 manage.py collectstatic --no-input`

## Установка и настройка nginx и gunicorn для запуска netbox.
Gunicorn — это Application-сервер для запуска Web-приложений написанных на Python. Основная его задача — это работа в режиме демона и поддержка постоянной работы Web-приложений.

+ Для настройки gunicorn скопирован файл

`sudo cp /opt/netbox/contrib/gunicorn.py /opt/netbox/gunicorn.py`

### Настройка Systemd

+ Скопированы файлы в каталог.

`sudo cp /opt/netbox/contrib/*.service /etc/systemd/system/`

+ Перезагружен демон, чтобы включить изменения Systemd.

`sudo systemctl daemon-reload`

+ Запущены службы netbox и .netbox-rq.

`sudo systemctl start netbox netbox-rq`

+ Включен запуск служб во время загрузки.

`sudo systemctl enable netbox netbox-rq`

### Настройка веб-сервера Nginx
Nginx― это программное обеспечение с открытым исходным кодом, которое позволяет создавать веб-сервер. Также его используют как почтовый сервер или обратный прокси-сервер.

+ Установлен веб-сервер Nginx.

`sudo apt install -y nginx`

+ Скопирован файл конфигурации NetBox Nginx.

`sudo cp /opt/netbox/contrib/nginx.conf /etc/nginx/sites-available/netbox`

+ Отредактирован файл netbox, добавлен хост и удалены https server.

`sudo nano /etc/nginx/sites-available/netbox`

<img src="https://user-images.githubusercontent.com/90505004/207169776-cb88ee27-bae5-4759-b384-6d6a15c62414.png" height="350"> 

+ Создана символическая ссылка в каталоге с поддержкой сайтов netbox на файл конфигурации. Выполнен перезапуск служб. 

`sudo rm /etc/nginx/sites-enabled/default`

`sudo ln -s /etc/nginx/sites-available/netbox /etc/nginx/sites-enabled/netbox`

+ Перезапущена служба nginx, чтобы включить новые конфигурации.

`sudo systemctl restart nginx`

Переходя в браузер по ip открывается netbox. Есть возможность войти в систему, используя имя пользователя и пароль, которые установлены при создании учетной записи суперпользователя. Можно приступить к настройке сетевых компонентов и управлению ими.

![4](https://user-images.githubusercontent.com/80837580/209463543-c1497e05-0d23-4371-aa5f-a1da5bb379bd.png)

# Заполнение всей возможной информации о CHR в Netbox

+ Заполнены данные в Netbox. Подключение происходит по IP виртуальной машины по порту 8001. Вручную введены данные о двух устройствах. Для добавления IP адреса требуется создать интерфейс на роутере. В Netbox записаны два роутера, ID роутеров, названия роутеров, интерфейсы, IP адреса.

![image](https://user-images.githubusercontent.com/90505004/209022004-0b7944d4-ad56-4167-a996-e3cd7f8183a9.png)

![image](https://user-images.githubusercontent.com/90505004/209043326-f3a82430-e0b2-4006-9544-208567e79a24.png)

+ Из NetBox был скачан файл csv с данными о роутерах

# Написание сценария для настройки CHR1, CHR2

+ Файл csv перенесен на сервер с ansible.

+ Создан файл playbook1.yml. Одна из частей задачи:спарсить csv файл и записать нужную информацию о роутере в отдельный файл. В данном случае за ключ берём UID роутера, так как это значение не будет изменяться.

+ Запущен playbook1, для проверки правильности вывода.

![5](https://user-images.githubusercontent.com/80837580/209463592-015dae9b-3102-4313-bafb-f252c1e15d9d.jpg)

+ В playbook1.yml добавлена часть, которая отвечает за установку названия роутера: берётся имя роутера из csv файла, сгенерированного Netbox, и присваивает имя подключенному роутеру. 

<img src="https://user-images.githubusercontent.com/90505004/209033031-83722e2c-730a-488f-81cf-78e82f52f1b0.png" height="300">

+ Вывод результатов показывает, что всё работает корректно.

![1](https://user-images.githubusercontent.com/90505004/209035345-328c27b2-6c9a-4bb5-b1cd-e8aa0b2b7b41.jpg)

+ В консоли роутера можно наблюдать, что название поменялось.

![photo_2022-12-16_18-39-21 (2)](https://user-images.githubusercontent.com/90505004/208134797-49154a9e-f2ef-485b-b5ab-9fbaf25ea608.jpg)

# Передача информации из роутера в Netbox

+ Создан playbook2. С помощью него берется информация из микротика и передается в файл на виртуальную машину в облако. Также с помощью плейбука вносится информация в Netbox: для этого создается устройство, где уже задана часть настроек, имя используется из микротика.

![image](https://user-images.githubusercontent.com/90505004/209023303-04176730-0f15-4f5b-b00f-cc935f3992b1.png)


+ Выполнен запуск playbook2, все выполнено успешно.

![ss](https://user-images.githubusercontent.com/90505004/209032662-369636a4-318c-4543-b70d-ec0b2a8c879e.jpg)

## Вывод

В результате выполнения работы выполнена установка и настройка Netbox. Написаны ansible playbooks для взаимодействия ранее настроеных роутеров и Netbox. 

![image](https://user-images.githubusercontent.com/90505004/209042785-62406a8c-d0c8-4d5f-868a-798f54bc4528.png)

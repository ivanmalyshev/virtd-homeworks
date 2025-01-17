
# Домашнее задание к занятию 3. «Введение. Экосистема. Архитектура. Жизненный цикл Docker-контейнера»

## Как сдавать задания

Обязательны к выполнению задачи без звёздочки. Их нужно выполнить, чтобы получить зачёт и диплом о профессиональной переподготовке.

Задачи со звёздочкой (*) — дополнительные задачи и/или задачи повышенной сложности. Их выполнять не обязательно, но они помогут вам глубже понять тему.

Домашнее задание выполните в файле readme.md в GitHub-репозитории. В личном кабинете отправьте на проверку ссылку на .md-файл в вашем репозитории.

Любые вопросы по решению задач задавайте в чате учебной группы.

---


## Важно

Перед отправкой работы на проверку удаляйте неиспользуемые ресурсы.
Это нужно, чтобы не расходовать средства, полученные в результате использования промокода.

Подробные рекомендации [здесь](https://github.com/netology-code/virt-homeworks/blob/virt-11/r/README.md).

---

## Задача 1

Сценарий выполнения задачи:

- создайте свой репозиторий на https://hub.docker.com;
- выберите любой образ, который содержит веб-сервер Nginx;
- создайте свой fork образа;
- реализуйте функциональность:
запуск веб-сервера в фоне с индекс-страницей, содержащей HTML-код ниже:
```
<html>
<head>
Hey, Netology
</head>
<body>
<h1>I’m DevOps Engineer!</h1>
</body>
</html>
```

Опубликуйте созданный fork в своём репозитории и предоставьте ответ в виде ссылки на https://hub.docker.com/username_repo.

---

### Ответ

![alt_text](https://github.com/ivanmalyshev/virtd-homeworks/blob/main/05-virt-03-docker/homework/step1.png)

https://hub.docker.com/r/ivanmalyshev1994/netology-devops/tags

## Задача 2

Посмотрите на сценарий ниже и ответьте на вопрос:
«Подходит ли в этом сценарии использование Docker-контейнеров или лучше подойдёт виртуальная машина, физическая машина? Может быть, возможны разные варианты?»

Детально опишите и обоснуйте свой выбор.

--

Сценарий:

- высоконагруженное монолитное Java веб-приложение;
- Nodejs веб-приложение;
- мобильное приложение c версиями для Android и iOS;
- шина данных на базе Apache Kafka;
- Elasticsearch-кластер для реализации логирования продуктивного веб-приложения — три ноды elasticsearch, два logstash и две ноды kibana;
- мониторинг-стек на базе Prometheus и Grafana;
- MongoDB как основное хранилище данных для Java-приложения;
- Gitlab-сервер для реализации CI/CD-процессов и приватный (закрытый) Docker Registry.

---

### Ответ

Сценарий:

- **Высоконагруженное монолитное java веб-приложение;**


Монолитное веб-приложение вероятно не реализуемо в микропроцессорной архитектуре без изменения кода, а так как приложение высоконагруженное то лучше использовать физический сервер.


- **Nodejs веб-приложение;**


Это веб приложение, для таких приложений достаточно докера. В рамках микропроцессрной архитектуры может быть хорошим решением


- **Мобильное приложение c версиями для Android и iOS;**


Виртуализация, т.к. docker приложение не имеет UI.


- **Шина данных на базе Apache Kafka;**


Это сервис по трансляции данных. Хорошо применить контейнеризацию, так как отсутствуют накладные расходы на виртуализацию, достигается простота масштабирования и управления.


- **Elasticsearch кластер для реализации логирования продуктивного веб-приложения - три ноды elasticsearch, два logstash и две ноды kibana;**


Для прода лучше использовать виртуализация, а отказоустойчивость решается на уровне HA кластера гипервизоров. В тестовой среде возможна реализация в контейнерах (для быстрого разворачивания).


- **Мониторинг-стек на базе Prometheus и Grafana;**


системы можно развернуть в docker это бысто и можно масштабировать при необходимости.


- **MongoDB, как основное хранилище данных для java-приложения;**


можно использовать виртуальную машину, можно контейнер. Разница вероятно всего в нагруженности сервиса при большой нагрузке лучше использовать виртуальную машину.


- **Gitlab сервер для реализации CI/CD процессов и приватный (закрытый) Docker Registry.**


Можно использовать и виртуальную машину и докер контейнер. Докер позволит масштабировать решение, так же удобно обновлять приложение без большого простоя сервиса.
Использование виртуальной машины позволит удобно администрировать сервис.

## Задача 3

- Запустите первый контейнер из образа ***centos*** c любым тегом в фоновом режиме, подключив папку ```/data``` из текущей рабочей директории на хостовой машине в ```/data``` контейнера.
- Запустите второй контейнер из образа ***debian*** в фоновом режиме, подключив папку ```/data``` из текущей рабочей директории на хостовой машине в ```/data``` контейнера.
- Подключитесь к первому контейнеру с помощью ```docker exec``` и создайте текстовый файл любого содержания в ```/data```.
- Добавьте ещё один файл в папку ```/data``` на хостовой машине.
- Подключитесь во второй контейнер и отобразите листинг и содержание файлов в ```/data``` контейнера.

---

```
mid@mid-desktop:~/Nextcloud/netology/virtd-homeworks/05-virt-03-docker$ docker run -d -it -v ./data:/data debian:latest

mid@mid-desktop:~/Nextcloud/netology/virtd-homeworks/05-virt-03-docker$ docker run -d -it -v ./data:/data centos:latest

```

```
mid@mid-desktop:~/Nextcloud/netology/virtd-homeworks/05-virt-03-docker/data$ docker ps
CONTAINER ID   IMAGE           COMMAND                  CREATED          STATUS          PORTS                               NAMES
ff85f4004ba7   centos:latest   "/bin/bash"              14 minutes ago   Up 14 minutes                                       upbeat_knuth
ac5121bbfeb3   debian          "bash"                   15 minutes ago   Up 15 minutes                                       lucid_fermat
8e374682d042   f08addfa2bc4    "/docker-entrypoint.…"   15 hours ago     Up 15 hours     0.0.0.0:80->80/tcp, :::80->80/tcp   vigilant_merkle
mid@mid-desktop:~/Nextcloud/netology/virtd-homeworks/05-virt-03-docker/data$ docker exec -it ff85f4004ba7 bash
[root@ff85f4004ba7 /]# 

```

docker exec -it b3a758b1343d bash
[root@b3a758b1343d /]# ls
bin  data  dev	etc  home  lib	lib64  lost+found  media  mnt  opt  proc  root	run  sbin  srv	sys  tmp  usr  var
[root@b3a758b1343d /]# cd data/
[root@b3a758b1343d data]# touch file_on_centos.txt
[root@b3a758b1343d data]# echo "hi, i'm centos" > file_on_centos.txt 
[root@b3a758b1343d data]# exit

```
mid@mid-desktop:~/Nextcloud/netology/virtd-homeworks/05-virt-03-docker/data$ sudo touch file_on_host.txt
[sudo] пароль для mid: 
mid@mid-desktop:~/Nextcloud/netology/virtd-homeworks/05-virt-03-docker/data$ docker ps
CONTAINER ID   IMAGE           COMMAND                  CREATED         STATUS         PORTS                               NAMES
b3a758b1343d   centos:latest   "/bin/bash"              3 minutes ago   Up 3 minutes                                       charming_goldwasser
d78ef9562fa9   debian:latest   "bash"                   3 minutes ago   Up 3 minutes                                       jovial_chatelet
8e374682d042   f08addfa2bc4    "/docker-entrypoint.…"   15 hours ago    Up 15 hours    0.0.0.0:80->80/tcp, :::80->80/tcp   vigilant_merkle
mid@mid-desktop:~/Nextcloud/netology/virtd-homeworks/05-virt-03-docker/data$ docker exec -it d78ef9562fa9 bash
root@d78ef9562fa9:/# cd data
root@d78ef9562fa9:/data# ls
file_on_centos.txt  file_on_host.txt
root@d78ef9562fa9:/data# ls -alh
total 12K
drwxr-xr-x 2 root root 4.0K Aug 18 11:49 .
drwxr-xr-x 1 root root 4.0K Aug 18 11:45 ..
-rw-r--r-- 1 root root   15 Aug 18 11:47 file_on_centos.txt
-rw-r--r-- 1 root root    0 Aug 18 11:49 file_on_host.txt
root@d78ef9562fa9:/data# 

```



## Задача 4 (*)

Воспроизведите практическую часть лекции самостоятельно.

Соберите Docker-образ с Ansible, загрузите на Docker Hub и пришлите ссылку вместе с остальными ответами к задачам.


---

### Как cдавать задание

Выполненное домашнее задание пришлите ссылкой на .md-файл в вашем репозитории.

---


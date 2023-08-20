# Домашнее задание к занятию 4. «Оркестрация группой Docker-контейнеров на примере Docker Compose»

## Как сдавать задания

Обязательны к выполнению задачи без звёздочки. Их нужно выполнить, чтобы получить зачёт и диплом о профессиональной переподготовке.

Задачи со звёздочкой (*) — это дополнительные задачи и/или задачи повышенной сложности. Их выполнять не обязательно, но они помогут вам глубже понять тему.

Домашнее задание выполните в файле readme.md в GitHub-репозитории. В личном кабинете отправьте на проверку ссылку на .md-файл в вашем репозитории.

Любые вопросы по решению задач задавайте в чате учебной группы.

---


## Важно

Перед отправкой работы на проверку удаляйте неиспользуемые ресурсы.
Это нужно, чтобы не расходовать средства, полученные в результате использования промокода.

Подробные рекомендации [здесь](https://github.com/netology-code/virt-homeworks/blob/virt-11/r/README.md).

---

## Задача 1

Создайте собственный образ любой операционной системы (например, debian-11) с помощью Packer версии 1.5.0 ([инструкция](https://cloud.yandex.ru/docs/tutorials/infrastructure-management/packer-quickstart)).

Чтобы получить зачёт, вам нужно предоставить скриншот страницы с созданным образом из личного кабинета YandexCloud.

---

### Ответ

![alt_text](https://github.com/ivanmalyshev/virtd-homeworks/blob/main/05-virt-04-docker-compose/src/create_iso.png)

[ссылка на json образа](https://github.com/ivanmalyshev/virtd-homeworks/blob/main/05-virt-04-docker-compose/image.json)

## Задача 2

**2.1.** Создайте вашу первую виртуальную машину в YandexCloud с помощью web-интерфейса YandexCloud.        

**2.2.*** **(Необязательное задание)**      
Создайте вашу первую виртуальную машину в YandexCloud с помощью Terraform (вместо использования веб-интерфейса YandexCloud).
Используйте Terraform-код в директории ([src/terraform](https://github.com/netology-group/virt-homeworks/tree/virt-11/05-virt-04-docker-compose/src/terraform)).

Чтобы получить зачёт, вам нужно предоставить вывод команды terraform apply и страницы свойств, созданной ВМ из личного кабинета YandexCloud.


### Ответ

```
yc config list
token: y0_AgAAAABwMDO1AATuwQAAAADqpYQjll_ULw8ETiS9M-yKDwnWv-N6ZYs
cloud-id: b1ggt7dn42l7chn96p5q
folder-id: b1g3lvs2irirrcnca5j5

yc compute image list
+----------------------+--------------------------------------+-------------------+----------------------+--------+
|          ID          |                 NAME                 |      FAMILY       |     PRODUCT IDS      | STATUS |
+----------------------+--------------------------------------+-------------------+----------------------+--------+
| fd86hovj08rkep2k7q2q | debian-11-nginx-2023-08-20t07-34-53z | debian-web-server | f2e1eht8hm1mgq4fmk1k | READY  |
+----------------------+--------------------------------------+-------------------+----------------------+--------+

```

Соответствующие изменения в файлы .tf внес. 

Сгенерировал json.key для сервисного аккаунта

```
yc iam key create --service-account-name imalyshev94 --output key.json --folder-id b1g3lvs2irirrcnca5j5
id: aje10fnjvals9hr1hc96
service_account_id: ajeh48fkgpbljdjbt0nv
created_at: "2023-08-20T08:03:27.143542388Z"
key_algorithm: RSA_2048
```

![alt_text](https://github.com/ivanmalyshev/virtd-homeworks/blob/main/05-virt-04-docker-compose/src/terraform_plan.png)

![alt_text](https://github.com/ivanmalyshev/virtd-homeworks/blob/main/05-virt-04-docker-compose/src/terraform_apply.png)


## Задача 3

С помощью Ansible и Docker Compose разверните на виртуальной машине из предыдущего задания систему мониторинга на основе Prometheus/Grafana.
Используйте Ansible-код в директории ([src/ansible](https://github.com/netology-group/virt-homeworks/tree/virt-11/05-virt-04-docker-compose/src/ansible)).

Чтобы получить зачёт, вам нужно предоставить вывод команды "docker ps" , все контейнеры, описанные в [docker-compose](https://github.com/netology-group/virt-homeworks/blob/virt-11/05-virt-04-docker-compose/src/ansible/stack/docker-compose.yaml),  должны быть в статусе "Up".

### Ответ

```
debian@node01:~$ sudo docker ps
CONTAINER ID   IMAGE                              COMMAND                  CREATED          STATUS                             PORTS                                                                              NAMES
e0665e2adff6   grafana/grafana:7.4.2              "/run.sh"                25 seconds ago   Up 12 seconds                      3000/tcp                                                                           grafana
744549ca1981   gcr.io/cadvisor/cadvisor:v0.47.0   "/usr/bin/cadvisor -…"   25 seconds ago   Up 12 seconds (health: starting)   8080/tcp                                                                           cadvisor
ce5cefdc3701   prom/node-exporter:v0.18.1         "/bin/node_exporter …"   25 seconds ago   Up 12 seconds                      9100/tcp                                                                           nodeexporter
4ff6ba6c637e   stefanprodan/caddy                 "/sbin/tini -- caddy…"   25 seconds ago   Up 12 seconds                      0.0.0.0:3000->3000/tcp, 0.0.0.0:9090-9091->9090-9091/tcp, 0.0.0.0:9093->9093/tcp   caddy
2a0025c03a3f   prom/prometheus:v2.17.1            "/bin/prometheus --c…"   25 seconds ago   Up 12 seconds                      9090/tcp                                                                           prometheus
3284a8218e97   prom/alertmanager:v0.20.0          "/bin/alertmanager -…"   25 seconds ago   Up 12 seconds                      9093/tcp                                                                           alertmanager
481d2814ade1   prom/pushgateway:v1.2.0            "/bin/pushgateway"       25 seconds ago   Up 12 seconds                      9091/tcp                                                                           pushgateway
debian@node01:~$ 
```

## Задача 4

1. Откройте веб-браузер, зайдите на страницу http://<внешний_ip_адрес_вашей_ВМ>:3000.
2. Используйте для авторизации логин и пароль из [.env-file](https://github.com/netology-group/virt-homeworks/blob/virt-11/05-virt-04-docker-compose/src/ansible/stack/.env).
3. Изучите доступный интерфейс, найдите в интерфейсе автоматически созданные docker-compose-панели с графиками([dashboards](https://grafana.com/docs/grafana/latest/dashboards/use-dashboards/)).
4. Подождите 5-10 минут, чтобы система мониторинга успела накопить данные.

Чтобы получить зачёт, предоставьте: 

- скриншот работающего веб-интерфейса Grafana с текущими метриками, как на примере ниже.
<p align="center">
  <img width="1200" height="600" src="./assets/yc_02.png">
</p>


### Ответ

![alt_text](https://github.com/ivanmalyshev/virtd-homeworks/blob/main/05-virt-04-docker-compose/src/install_stack.png)

## Задача 5 (*)

Создайте вторую ВМ и подключите её к мониторингу, развёрнутому на первом сервере.

Чтобы получить зачёт, предоставьте:

- скриншот из Grafana, на котором будут отображаться метрики добавленного вами сервера.



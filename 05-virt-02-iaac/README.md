
# Домашнее задание к занятию 2. «Применение принципов IaaC в работе с виртуальными машинами»

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

- Опишите основные преимущества применения на практике IaaC-паттернов.
- Какой из принципов IaaC является основополагающим?

---

### Ответ

Основным преимуществом IaaC является автоматизации развёртывания инфраструктуры, как следствие увеличение скорости выполнения этой операции и снижение трудозатрат на её выполнение. Одно дело кофигурировать 100 серверов по одному, другое дело набором определенных операций, декларативно, посредством IaaC-паттернов разверуть 100 серверов запуском одной операции. Определенно разница есть и очень существенная.

Основной принцип IaaC является построение и описание инфраструктуры через конфигурационные файлы. Если совсем просто - описывать инфраструктуру кодом, переиспользуя практики из разработки ПО.

## Задача 2

- Чем Ansible выгодно отличается от других систем управление конфигурациями?
- Какой, на ваш взгляд, метод работы систем конфигурации более надёжный — push или pull?

  Ansible использует существующую SSH инфраструктуру, в то время как другие (Saltstack, Chef, Puppet, и пр.) требуют установки специального PKI-окружения

  Pull, т.к. отсутствует единая точка отказа и хранения данных для доступа.

## Задача 3

Установите на личный компьютер:

- [VirtualBox](https://www.virtualbox.org/),
- [Vagrant](https://github.com/netology-code/devops-materials),
- [Terraform](https://github.com/netology-code/devops-materials/blob/master/README.md),
- Ansible.

*Приложите вывод команд установленных версий каждой из программ, оформленный в Markdown.*

---

### Ответ

часть ПО развернута на сервере, так называемая домашняя лаборатория.
```
mid@midserv:~$ vboxmanage -v
7.0.8r156879
mid@midserv:~$ vagrant -v
Vagrant 2.3.4
mid@midserv:~$ ansible --version
ansible 2.10.8
  config file = None
  configured module search path = ['/home/mid/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']
  ansible python module location = /usr/lib/python3/dist-packages/ansible
  executable location = /bin/ansible
  python version = 3.10.12 (main, Jun 11 2023, 05:26:28) [GCC 11.4.0]
mid@midserv:~$ 

```
Часть ПО так же установлена на десктопе
```
mid@mid-desktop:~$ terraform -v
Terraform v1.3.6
on linux_amd64
+ provider registry.terraform.io/yandex-cloud/yandex v0.96.1

Your version of Terraform is out of date! The latest version
is 1.5.5. You can update by downloading from https://www.terraform.io/downloads.html
mid@mid-desktop:~$ vboxmanage -v
6.1.38_Ubuntur153438
mid@mid-desktop:~$ ansible --version
ansible [core 2.13.6]
  config file = None
  configured module search path = ['/home/mid/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']
  ansible python module location = /home/mid/.local/lib/python3.8/site-packages/ansible
  ansible collection location = /home/mid/.ansible/collections:/usr/share/ansible/collections
  executable location = /home/mid/.local/bin/ansible
  python version = 3.8.10 (default, May 26 2023, 14:05:08) [GCC 9.4.0]
  jinja version = 3.0.3
  libyaml = True

```

## Задача 4 

Воспроизведите практическую часть лекции самостоятельно.

- Создайте виртуальную машину.
- Зайдите внутрь ВМ, убедитесь, что Docker установлен с помощью команды
```
docker ps,
```
Vagrantfile из лекции и код ansible находятся в [папке](https://github.com/netology-code/virt-homeworks/tree/virt-11/05-virt-02-iaac/src).

Примечание. Если Vagrant выдаёт ошибку:
```
URL: ["https://vagrantcloud.com/bento/ubuntu-20.04"]     
Error: The requested URL returned error: 404:
```

выполните следующие действия:

1. Скачайте с [сайта](https://app.vagrantup.com/bento/boxes/ubuntu-20.04) файл-образ "bento/ubuntu-20.04".
2. Добавьте его в список образов Vagrant: "vagrant box add bento/ubuntu-20.04 <путь к файлу>".

*Приложите скриншоты в качестве решения на эту задачу.*


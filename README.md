# Домашнее задание к занятию 10.1 «Keepalived/vrrp» - `Рыбак Егор`




---

### Задание 1

Разверните топологию из лекции и выполните установку и настройку сервиса Keepalived. 

```
vrrp_instance test {

state "name_mode"

interface "name_interface"

virtual_router_id "number id"

priority "number priority"

advert_int "number advert"

authentication {

auth_type "auth type"

auth_pass "password"

}

unicast_peer {

"ip address host"

}

virtual_ipaddress {

"ip address host" dev "interface" label "interface":vip

}

}

```

*В качестве решения предоставьте:*   
*- рабочую конфигурацию обеих нод, оформленную как блок кода в вашем md-файле;*   
*- скриншоты статуса сервисов, на которых видно, что одна нода перешла в MASTER, а вторая в BACKUP state.*   

### Ответ:
1. Master-нода:
```
vrrp_instance main {

state MASTER

interface enp0s3

virtual_router_id 10

priority 120

advert_int 4

authentication {

auth_type AH

auth_pass 1111

}

unicast_peer {

10.0.2.17

}

virtual_ipaddress {

10.0.2.30 dev enp0s3 label enp0s3:vip

}

}








```
2. Backup-нода:
```
vrrp_instance main {

state BACKUP

interface enp0s3

virtual_router_id 10

priority 110

advert_int 4

authentication {

auth_type AH

auth_pass 1111

}

unicast_peer {

10.0.2.16

}

virtual_ipaddress {

10.0.2.30 dev enp0s3 label enp0s3:vip

}

}

```
1. Master-state:
- ![9_06-master_state](https://github.com/RybakEgor/9-06_Keepalived_vrrp/blob/main/img/9_06-master_state.png)
2. Backup-state:
- ![9_06-backup_state](https://github.com/RybakEgor/9-06_Keepalived_vrrp/blob/main/img/9_06-backup_state.png)

## Дополнительные задания со звёздочкой*

Эти задания дополнительные. Их можно не выполнять. На зачёт это не повлияет. Вы можете их выполнить, если хотите глубже разобраться в материале.
---
### Задание 2*

Проведите тестирование работы ноды, когда один из интерфейсов выключен. Для этого:
- добавьте ещё одну виртуальную машину и включите её в сеть;
- на машине установите Wireshark и запустите процесс прослеживания интерфейса;
- запустите процесс ping на виртуальный хост;
- выключите интерфейс на одной ноде (мастер), остановите Wireshark;
- найдите пакеты ICMP, в которых будет отображён процесс изменения MAC-адреса одной ноды на другой. 

 *В качестве решения пришлите скриншот до и после выключения интерфейса из Wireshark.*



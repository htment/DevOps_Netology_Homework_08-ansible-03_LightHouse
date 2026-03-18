# DevOps_Netology_Homework_08-ansible-03_LightHouse
- Допишите playbook: нужно сделать ещё один play, который устанавливает и настраивает LightHouse.
- При создании tasks рекомендую использовать модули: get_url, template, yum, apt.
- Tasks должны: скачать статику LightHouse, установить Nginx или любой другой веб-сервер, настроить его конфиг для открытия LightHouse, запустить веб-сервер.
- Подготовьте свой inventory-файл prod.yml.
- Запустите ansible-lint site.yml и исправьте ошибки, если они есть.
- Попробуйте запустить playbook на этом окружении с флагом --check.
- Запустите playbook на prod.yml окружении с флагом --diff. Убедитесь, что изменения на системе произведены.
- Повторно запустите playbook с флагом --diff и убедитесь, что playbook идемпотентен.
- Подготовьте README.md-файл по своему playbook. В нём должно быть описано: что делает playbook, какие у него есть параметры и теги.
- Готовый playbook выложите в свой репозиторий, поставьте тег 08-ansible-03-yandex на фиксирующий коммит, в ответ предоставьте ссылку на него.


# Выполним задание в docker 

создадим образ из файла  ```Dockerfile_CENTOS_systemd```


```
docker build -t centos-systemd-custom -f Dockerfile_CENTOS_systemd .
```

создадим контейнеры под наши сервисы
```
docker compose up -d
```

![alt text](image.png)
![alt text](image-1.png)

запустим установку``` cd INSTALL_WITH_ROLES/```
```
ansible-playbook -i inventory/prod.yml site.yml 

```
![alt text](image-2.png)

проверяем работу

http://192.168.230.133:8123/
![alt text](image-3.png)
http://192.168.230.133:8081/#http://127.0.0.1:8123/
![alt text](image-4.png)

http://192.168.230.133:8696/playground
![alt text](image-5.png)

## Выполним проверки
```
ansible-lint site.ym

```
![alt text](image-6.png)


```
ansible-playbook -i inventory/prod.yml site.yml --check
```
![alt text](image-7.png)

```
ansible-playbook -i inventory/prod.yml site.yml --diff
```
![alt text](image-9.png)
![alt text](image-8.png)

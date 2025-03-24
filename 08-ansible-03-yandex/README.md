# Домашнее задание к занятию 3 «Использование Ansible»

## Подготовка к выполнению

1. Подготовьте в Yandex Cloud три хоста: для `clickhouse`, для `vector` и для `lighthouse`.
2. Репозиторий LightHouse находится [по ссылке](https://github.com/VKCOM/lighthouse).

## Основная часть

1. Допишите playbook: нужно сделать ещё один play, который устанавливает и настраивает LightHouse.
2. При создании tasks рекомендую использовать модули: `get_url`, `template`, `yum`, `apt`.
3. Tasks должны: скачать статику LightHouse, установить Nginx или любой другой веб-сервер, настроить его конфиг для открытия LightHouse, запустить веб-сервер.

     Ответ:
     Дополним плейбук из предыдущего задания двумя плеями Install NGINX и Install Lighthouse: [playbook.yml](https://github.com/elenaparf/mnt-homeworks/blob/MNT-video/08-ansible-03-yandex/%20%20%20%20playbook%20%20/playbook.yml)
4. Подготовьте свой inventory-файл `prod.yml`.

     Ответ:
     Как и в прошлом задании, для подготовки окружения используем [terraform](https://github.com/elenaparf/mnt-homeworks/tree/MNT-video/08-ansible-03-yandex/%20%20%20%20terraform%20%20) с модулями, в результате динамически формируется [inventory prod.yml](https://github.com/elenaparf/mnt-homeworks/blob/MNT-video/08-ansible-03-yandex/%20%20%20%20playbook%20%20/%20%20%20%20inventory%20%20/prod.example.yml) по шаблону [inventory.tftpl](https://github.com/elenaparf/mnt-homeworks/blob/MNT-video/08-ansible-03-yandex/%20%20%20%20terraform%20%20/inventory.tftpl).
Clickhouse и Lighthouse будут ставиться на отдельные ВМ, Vector на две другие ВМ.

5. Запустите `ansible-lint site.yml` и исправьте ошибки, если они есть.

     Ответ:
     Исправим ошибки, которые показал линтер. Повторный запуск:
     ![001](https://github.com/user-attachments/assets/6d1ebef9-3440-430a-91e6-9a6d082ab2c7)

6. Попробуйте запустить playbook на этом окружении с флагом `--check`.    
7. Запустите playbook на `prod.yml` окружении с флагом `--diff`. Убедитесь, что изменения на системе произведены.

     Ответ:
     Запустим плейбук, выполнился успешно:
     ![002](https://github.com/user-attachments/assets/58a0ac5d-5bdf-4581-93f9-2c346fe3ea13)

10. Повторно запустите playbook с флагом `--diff` и убедитесь, что playbook идемпотентен.
11. Подготовьте README.md-файл по своему playbook. В нём должно быть описано: что делает playbook, какие у него есть параметры и теги.
12. Готовый playbook выложите в свой репозиторий, поставьте тег `08-ansible-03-yandex` на фиксирующий коммит, в ответ предоставьте ссылку на него.

---

### Как оформить решение задания

Выполненное домашнее задание пришлите в виде ссылки на .md-файл в вашем репозитории.

---

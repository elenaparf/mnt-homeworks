# Домашнее задание к занятию 2 «Работа с Playbook»

## Подготовка к выполнению

1. * Необязательно. Изучите, что такое [ClickHouse](https://www.youtube.com/watch?v=fjTNS2zkeBs) и [Vector](https://www.youtube.com/watch?v=CgEhyffisLY).
2. Создайте свой публичный репозиторий на GitHub с произвольным именем или используйте старый.
3. Скачайте [Playbook](./playbook/) из репозитория с домашним заданием и перенесите его в свой репозиторий.
4. Подготовьте хосты в соответствии с группами из предподготовленного playbook.

## Основная часть

1. Подготовьте свой inventory-файл `prod.yml`.
   
      Ответ:
      Для подготовки окружения используем [terraform](https://github.com/elenaparf/mnt-homeworks/tree/MNT-video/08-ansible-02-playbook/terraform)  с модулями,        в результате динамически формируется inventory [prod.yml](https://github.com/elenaparf/mnt-homeworks/blob/MNT-video/08-ansible-02-playbook/playbook/inventory/prod.example.yml) по шаблону [inventory.tftpl](https://github.com/elenaparf/mnt-homeworks/blob/MNT-video/08-ansible-02-playbook/terraform/inventory.tftpl).
      Clickhouse будет ставиться на отдельную ВМ, Vector на две другие ВМ. Также сразу настроим отправку логов из vector в Clickhouse, что прописано  в               security rules.

   
2. Допишите playbook: нужно сделать ещё один play, который устанавливает и настраивает [vector](https://vector.dev). Конфигурация vector должна деплоиться через template файл jinja2. От вас не требуется использовать все возможности шаблонизатора, просто вставьте стандартный конфиг в template файл. Информация по шаблонам по [ссылке](https://www.dmosk.ru/instruktions.php?object=ansible-nginx-install). не забудьте сделать handler на перезапуск vector в случае изменения конфигурации!
3. При создании tasks рекомендую использовать модули: `get_url`, `template`, `unarchive`, `file`.
4. Tasks должны: скачать дистрибутив нужной версии, выполнить распаковку в выбранную директорию, установить vector.

      Ответ:
      Добавим play "Install Vector" в [плейбук](https://github.com/elenaparf/mnt-homeworks/blob/MNT-video/08-ansible-02-playbook/playbook/playbook.yml). Сразу        предусмотрим идемпотентность.

   
5. Запустите `ansible-lint site.yml` и исправьте ошибки, если они есть.

      Первый прогон линтера показал следующие ошибки:
      ![0111](https://github.com/user-attachments/assets/0c7698fd-4b59-4a4b-99af-028c21b6acec)
      
     playbook.yml:11 Task/Handler: block/always/rescue - добавим name для блока, таски назовём более понятными именами
     playbook.yml:12 Task/Handler: Get clickhouse distrib - добавим mode
     playbook.yml:18 Task/Handler: Get clickhouse distrib - добавим mode
     playbook.yml:30 - meta заменим на `ansible.builtin.
     playbook.yml:32 - добавим пробел, rewrite recommendation: create_db.rc != 0 and create_db.rc != 82.

      Также добавим таск на редактирование конфига, чтобы установить параметр listen_host.
      Повторный прогон линтера без ошибок:
      ![0211](https://github.com/user-attachments/assets/c28b0790-8492-4bdb-bb0c-0a4c6b8c4e2e)


6. Попробуйте запустить playbook на этом окружении с флагом `--check`.

      Ответ:
      Запуск check  сломался на стадии "Install clickhouse packages", т.к. таски здесь изменений не выполняют, а значит и .rpm-пакетов для инсталляции                на таргет-хосте не существует.
      ![0311](https://github.com/user-attachments/assets/00447567-1897-4ad9-8f53-9e15dc929077)

   
7. Запустите playbook на `prod.yml` окружении с флагом `--diff`. Убедитесь, что изменения на системе произведены.

      Ответ:
      Плейбук выполнился успешно:
      Сервисы запущены, Vector законнектился к Clickhouse
      ![0411](https://github.com/user-attachments/assets/e05cbbe9-3ab2-464d-a43a-61d7cde9d68d)


   
8. Повторно запустите playbook с флагом `--diff` и убедитесь, что playbook идемпотентен.

      Recap повторного запуска показал, что изменений не было, а значит, идемпотентность соблюдена:
      ![0511](https://github.com/user-attachments/assets/2c01539e-f8cb-429e-9477-9d969b47bd48)

            
9. Подготовьте README.md-файл по своему playbook. В нём должно быть описано: что делает playbook, какие у него есть параметры и теги. Пример качественной документации ansible playbook по [ссылке](https://github.com/opensearch-project/ansible-playbook). Так же приложите скриншоты выполнения заданий №5-8

    
12. Готовый playbook выложите в свой репозиторий, поставьте тег `08-ansible-02-playbook` на фиксирующий коммит, в ответ предоставьте ссылку на него.


    Ответ:  Ссылка на [README.md](https://github.com/elenaparf/mnt-homeworks/blob/MNT-video/08-ansible-02-playbook/playbook/README.md)
---


### Как оформить решение задания

Выполненное домашнее задание пришлите в виде ссылки на .md-файл в вашем репозитории.

---

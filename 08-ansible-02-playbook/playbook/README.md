Плейбук для выполнения домашнего задания Нетологии к занятию "Работа с Playbook" модуля "Система управления конфигурациями" (08-ansible-02-playbook)
play: Установка Clickhouse

Play для установки Clickhouse выполняется для группы хостов clickhouse. Play адаптирован для установки на rpm-based дистрибутив ВМ и установку Clickhouse в single-node режиме. Действия:

    Скачивание .rpm-пакетов (noarch или x86_64)
    Инсталляция дистрибутива
    Корректировка конфигурации (listen address)
    Запуск сервиса Clickhouse
    Создание базы logs

play: Установка Vector

Play для установки Clickhouse выполняется для группы хостов vector. Play адаптирован для установки на deb-based дистрибутивы. Действия:

    Создание группы и пользователя vector
    Создание каталогов для дистрибутива и хранения данных
    Скачивание архива с дистрибутивом, распаковка
    Создание конфигурации Vector по шаблону 
[templates/vector.yaml.j2](https://github.com/elenaparf/mnt-homeworks/blob/MNT-video/08-ansible-02-playbook/playbook/%20%20%20%20templates%20%20/vector.yaml.j2)
    с коннектом по умолчанию к Clickhouse
    Создание systemd unit и запуск сервиса

Конфигурация

Список хостов (inventory) должен включать группы clickhouse и veсtor. Пример: [prod.example.yml](08-ansible-02-playbook/playbook/inventory/prod.example.yml)

Для изменения параметров установки Clickhouse необходимо внести изменения в файл [clickhouse vars.yml](08-ansible-02-playbook/playbook/group_vars/clickhouse/vars.yml).

    clickhouse_version: версия релиза Clickhouse (по умолчанию 22.3.3.44)
    clickhouse_packages: список пакеов для скачивания

Для изменения параметров установки Vector необходимо внести изменения в файл vector [vars.yml](08-ansible-02-playbook/playbook/group_vars/vector/vars.yml).

    vector_version: версия релиза Vector (по умолчанию 0.34.1)
    vector_architecture: архитектура (по умолчанию x86_64)

Требования

    Ansible 2.11+

Теги

    clickhouse
    vector

Запуск

ansible-playbook -i inventory/prod.yml playbook.yml, где:

    inventory/prod.yml - путь к ansible Inventory
    playbook.yml - путь к ansible Playbook

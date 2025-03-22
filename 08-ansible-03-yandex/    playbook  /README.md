Плейбук для выполнения домашнего задания Нетологии к занятию "Использование Ansible" модуля "Система управления конфигурациями" (08-ansible-03-yandex)
play: Установка NGINX

Play инсталляции NGINX выполняется для группы хостов lighthouse. Play адаптирован для установки на deb-based дистрибутивы. Действия:

    Добавление репозитория
    Установка NGINX из репозитория
    Создание конфигурации по шаблону templates/nginx.conf.j2

play: Установка Lighthouse

Play инсталляции Lighthouse выполняется для группы хостов lighthouse. Play адаптирован для установки на deb-based дистрибутивы. Действия:

    Скачивание исходников Lighthouse из GitHub в указанную директорию
    Создание конфигурации Lighthouse для NGINX по шаблону templates/lighthouse.conf.j2

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
    Создание конфигурации Vector по шаблону templates/vector.yaml.j2 с коннектом по умолчанию к Clickhouse
    Создание systemd unit и запуск сервиса

Конфигурация

Список хостов (inventory) должен включать группы clickhouse и veсtor. Пример: prod.example.yml

Для изменения параметров установки Clickhouse необходимо внести изменения в файл clickhouse vars.yml.

    clickhouse_version: версия релиза Clickhouse (по умолчанию 22.3.3.44)
    clickhouse_packages: список пакетов для скачивания

Для изменения параметров установки Vector необходимо внести изменения в файл vector vars.yml.

    vector_version: версия релиза Vector (по умолчанию 0.34.1)
    vector_architecture: архитектура (по умолчанию x86_64)

Для изменения параметров установки Lighthouse необходимо внести изменения в файл lighthouse vars.yml.

    lighthouse_vcs: исходный код (по умолчанию https://github.com/VKCOM/lighthouse.git)
    lighthouse_location: расположение Lighthouse (по умолчанию /var/www/lighthouse)

Требования

    Ansible 2.11+

Теги

    clickhouse
    vector
    lighthouse

Запуск

ansible-playbook -i inventory/prod.yml playbook.yml, где:

    inventory/prod.yml - путь к ansible Inventory
    playbook.yml - путь к ansible Playbook

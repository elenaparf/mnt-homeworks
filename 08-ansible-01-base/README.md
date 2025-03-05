# Домашнее задание к занятию 1 «Введение в Ansible»

## Подготовка к выполнению

1. Установите Ansible версии 2.10 или выше.
2. Создайте свой публичный репозиторий на GitHub с произвольным именем.
3. Скачайте [Playbook](./playbook/) из репозитория с домашним заданием и перенесите его в свой репозиторий.

## Основная часть


  Попробуйте запустить playbook на окружении из test.yml, зафиксируйте значение, которое имеет факт some_fact для указанного хоста при выполнении playbook.

    Ответ:

    Запустим плейбук (по умолчанию на hosts: all), значение some_fact = 12 playbook
  ![011](https://github.com/user-attachments/assets/f0f03ade-f96b-44ea-a25d-2fe49d587060)


  Найдите файл с переменными (group_vars), в котором задаётся найденное в первом пункте значение, и поменяйте его на all default fact.

    Ответ:

    Для группы all поменяем значение факта в 
  ![group_vars/all/examp.yml](https://github.com/elenaparf/mnt-homeworks/blob/MNT-video/08-ansible-01-base/playbook/group_vars/all/examp.yml). 
    Запустим playbook
  ![021](https://github.com/user-attachments/assets/686e16c9-4437-4caa-b4ef-87bb192de540)

  Воспользуйтесь подготовленным (используется docker) или создайте собственное окружение для проведения дальнейших испытаний.

    Ответ:

    Запустим 2 контейнера ubuntu и centos7 на хосте: docker ps
  ![031](https://github.com/user-attachments/assets/726f5c95-74fd-4f90-8523-ed6d70f1fa38)

  Проведите запуск playbook на окружении из prod.yml. Зафиксируйте полученные значения some_fact для каждого из managed host.

    Ответ:

    Запустим плейбук на prod-окружении, получим значения el для centos и deb для ubuntu:
  ![041](https://github.com/user-attachments/assets/9fbb97bd-2ea5-469f-a309-ffc5313e6a3f)

  Добавьте факты в group_vars каждой из групп хостов так, чтобы для some_fact получились значения: для deb — deb default fact, для el — el default fact.
  Повторите запуск playbook на окружении prod.yml. Убедитесь, что выдаются корректные значения для всех хостов.

    Ответ:

    Заменим значения в  
  ![group_vars/deb](https://github.com/elenaparf/mnt-homeworks/blob/MNT-video/08-ansible-01-base/playbook/group_vars/deb/examp.yml) и ![group_vars/el](https://github.com/elenaparf/mnt-homeworks/blob/MNT-video/08-ansible-01-base/playbook/group_vars/el/examp.yml). 
  Запуск плейбука
  ![051](https://github.com/user-attachments/assets/a44be92b-2e98-43b6-add4-9f75d0eb9d5f)
  
  При помощи ansible-vault зашифруйте факты в group_vars/deb и group_vars/el с паролем netology.

    Ответ:

    Шифрование секретов: 
  ![061](https://github.com/user-attachments/assets/6cb05983-6418-4b58-a288-5659e7e25576)
  ![0611](https://github.com/user-attachments/assets/ba7f7d8f-d157-4ee8-a1b8-230f23384670)

  Запустите playbook на окружении prod.yml. При запуске ansible должен запросить у вас пароль. Убедитесь в работоспособности.

    Ответ:

    Успешный запуск плейбука с запросом пароля:
  ![071](https://github.com/user-attachments/assets/478d7be8-5ee2-4f25-899d-d1c62c373f58)

  Посмотрите при помощи ansible-doc список плагинов для подключения. Выберите подходящий для работы на control node.

    Ответ:

    Для подключения к ноде-контроллеру нужно использовать ansible.builtin.local:
  ![081](https://github.com/user-attachments/assets/d6242aa5-bd15-412a-aba6-255818b9a7bb)

  В prod.yml добавьте новую группу хостов с именем local, в ней разместите localhost с необходимым типом подключения.

    Ответ:

    Изменения отразим в 
  [playbook/inventory/prod.yml](https://github.com/elenaparf/mnt-homeworks/blob/MNT-video/08-ansible-01-base/playbook/inventory/prod.yml)

Запустите playbook на окружении prod.yml. При запуске ansible должен запросить у вас пароль. Убедитесь, что факты some_fact для каждого из хостов определены из верных group_vars.

    Ответ:

    При запуске на prod для localhost значение some_fact применилось от группы all playbook
  ![091](https://github.com/user-attachments/assets/dc770c2e-7a47-4c4b-85c7-81f13372bdde)

  Заполните README.md ответами на вопросы. Сделайте git push в ветку master. В ответе отправьте ссылку на ваш открытый репозиторий с изменённым playbook и заполненным README.md.
  Предоставьте скриншоты результатов запуска команд.


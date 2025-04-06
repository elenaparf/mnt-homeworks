# Домашнее задание к занятию 4 «Работа с roles»

## Подготовка к выполнению

1. * Необязательно. Познакомьтесь с [LightHouse](https://youtu.be/ymlrNlaHzIY?t=929).
2. Создайте два пустых публичных репозитория в любом своём проекте: vector-role и lighthouse-role.
3. Добавьте публичную часть своего ключа к своему профилю на GitHub.

## Основная часть

Ваша цель — разбить ваш playbook на отдельные roles. 

Задача — сделать roles для ClickHouse, Vector и LightHouse и написать playbook для использования этих ролей. 

Ожидаемый результат — существуют три ваших репозитория: два с roles и один с playbook.

**Что нужно сделать**

1. Создайте в старой версии playbook файл `requirements.yml` и заполните его содержимым:

   ```yaml
   ---
     - src: git@github.com:AlexeySetevoi/ansible-clickhouse.git
       scm: git
       version: "1.13"
       name: clickhouse 
   ```

2. При помощи `ansible-galaxy` скачайте себе эту роль.
3. Создайте новый каталог с ролью при помощи `ansible-galaxy role init vector-role`.
4. На основе tasks из старого playbook заполните новую role. Разнесите переменные между `vars` и `default`. 
5. Перенести нужные шаблоны конфигов в `templates`.
6. Опишите в `README.md` обе роли и их параметры. Пример качественной документации ansible role [по ссылке](https://github.com/cloudalchemy/ansible-prometheus).
7. Повторите шаги 3–6 для LightHouse. Помните, что одна роль должна настраивать один продукт.
8. Выложите все roles в репозитории. Проставьте теги, используя семантическую нумерацию. Добавьте roles в `requirements.yml` в playbook.
9. Переработайте playbook на использование roles. Не забудьте про зависимости LightHouse и возможности совмещения `roles` с `tasks`.
10. Выложите playbook в репозиторий.
11. В ответе дайте ссылки на оба репозитория с roles и одну ссылку на репозиторий с playbook.

---

### Как оформить решение задания

Выполненное домашнее задание пришлите в виде ссылки на .md-файл в вашем репозитории.

---
> ### Ответ
>
> 1. Инфраструктура по-прежнему создается с помощью [terraform](./%20%20%20%20terraform%20%20) с модулями, в результате динамически формируется inventory [prod.yml](./%20%20%20%20playbook/%20%20%20%20inventory%20%20/prod.example.yml) по шаблону [inventory.tftpl](./%20%20%20%20terraform%20%20/inventory.tftpl).  
> Clickhouse и Lighthouse будут ставиться на отдельные ВМ, Vector на две другие ВМ.
>
> 2. Инициализируем роли ansible_role_vector и ansible_role_lighthouse (поменяем имена, т.к. по новым правилам ansible-lint имя роли должно соответствовать `^[a-z][a-z0-9_]*$`)
>
> 3. Оформим структуру, опишем meta и README.md для ролей. Перенесем таски и переменные для них из старого плейбука в роли, дополним проверками на семейство дистрибутива. Линтером проверим код, исправила ошибки форматирования, затем выложим роли в GIT и создадим теги по результирующим коммитам.  
> Ссылки на репозитории:
>
>    * [Роль `ansible_role_lighthouse`](https://github.com/smutosey/ansible_role_lighthouse). В качестве зависимости роль использует официальную роль `nginxinc.nginx`
>    * [Роль `ansible_role_vector`](https://github.com/smutosey/ansible_role_vector)
>
> 4. Создадим файл [requirements.yml](./%20%20%20%20playbook/requirements.yml), где опишем инсталляцию ролей, привязку версии.  
> Установка прошла успешно:  
> ![roles install](https://github.com/user-attachments/assets/c2be34db-1b24-497b-bf85-9595e322991b)

> 5. Сформируем [playbook.yml](./%20%20%20%20playbook/playbook.yml), для play "Install Lighthouse" добавим pre_tasks с установкой git. Запустим плейбук, изменения применены успешно:  
> ![play recap](https://github.com/user-attachments/assets/75b003b9-1780-4e5d-8533-c810b997deb0)

> Повторный запуск плейбука показал отсутствие изменений, т.е. идемпотентность соблюдена:  
> ![no changes](https://github.com/user-attachments/assets/9b2f6a7b-efae-4624-be2d-dbe3a497a249)
>
> 6. Доступ к Lighthouse и коннект к Clickhouse:  
> ![web](https://github.com/user-attachments/assets/2555326b-a87e-4fc1-8cdd-ba4794507881)

>
> 7. Актуализировала информацию в [README.md](./%20%20%20%20playbook/README.md)плейбука.

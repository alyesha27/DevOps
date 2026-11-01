# Ansible-проект: раскатка frontend и backend

Структура:

- `ansible.cfg` — настройки Ansible
- `firstPlaybook.yml` — главный плейбук, вызывает роль `role1`
- `inventory/stend1/` — инвентарь (`hosts`, `group_vars/all.yml`, `host_vars/host1.yml`)
- `roles/role1/` — роль: установка Docker, клонирование репозиториев, запуск и остановка Compose

Запуск (из каталога `ansible`):

```bash
ansible all -i inventory/stend1/hosts -m ping
ansible-playbook -i inventory/stend1/hosts firstPlaybook.yml --tags deploy   # раскатка
ansible-playbook -i inventory/stend1/hosts firstPlaybook.yml --tags stop     # остановка
ansible-playbook -i inventory/stend1/hosts firstPlaybook.yml --tags start    # запуск
```

Перед запуском: `ansible-galaxy collection install community.docker`.

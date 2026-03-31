# DevOps Lab 6: Ansible Roles and CI/CD

## Описание
Ansible role для установки nginx с виртуальными хостами.  
Настроен CI через GitHub Actions для автоматической проверки кода.

## Архитектура
- **Control node**: ubu1 (10.0.2.15)
- **Managed node**: ubu2 (10.0.2.16)
- **Пользователь**: runner (с sudo без пароля)

## Структура
lab-ansible-roles/
├── inventory.ini
├── playbook.yml
├── roles/
│ └── nginx-vhosts/
│ ├── tasks/
│ │ └── main.yml
│ ├── handlers/
│ │ └── main.yml
│ ├── templates/
│ │ ├── site.conf.j2
│ │ └── index.html.j2
│ └── defaults/
│ └── main.yml (опционально)
├── .github/
│ └── workflows/
│ ├── test.yml
│ └── lint.yml
└── README.md

## Использование

### Запуск playbook
```bash
ansible-playbook -i inventory.ini playbook.yml
#### Проверка виртуальных хостов
curl -H "Host: etis.com" http://10.0.2.16
curl -H "Host: fizfak.com" http://10.0.2.16
curl -H "Host: mehmat.ru" http://10.0.2.16
```
## Результат
```html
<!DOCTYPE html>
<html>
<head>
    <title>etis.com</title>
</head>
<body>
    <h1>Hello from etis.com!</h1>
    <p>This page was deployed by Ansible role.</p>
    <hr>
    <small>Virtual host: etis.com</small>
</body>
</html>
```
## CI/CD Pipeline
GitHub Actions автоматически проверяет:
✅ Синтаксис playbook
✅ Ansible-lint
✅ Каждый push в main/master

## Переменные
Переменная	Описание	                Значение по умолчанию
sites   	Список виртуальных хостов	etis.com, fizfak.com, mehmat.ru
## Скриншоты
https://screenshots/playbook-run.png
https://screenshots/curl-test.png

# Тестовое задание

## 1. Описание проекта

В данном проекте реализован запуск серверов **Nginx**, **MySQL** и **PHP-FPM** в Docker-контейнерах.\
Вся инфраструктура развёртывается через `docker-compose`.

### Структура проекта

- **Nginx**: обработка HTTP-запросов и проксирование к PHP
- **PHP-FPM**: обработка PHP-скриптов
- **MySQL**: база данных для хранения данных

Файлы `.php` и `.html` размещаются в директории:

```
/nginxMysqlPhp/app
```

После запуска, проект доступен по адресу: [http://localhost](http://localhost)

---

## 2. Настройка Cloudflare

1. Зарегистрируйтесь или войдите в Cloudflare: [https://dash.cloudflare.com](https://dash.cloudflare.com)
2. Добавьте свой домен (example.com)
3. Cloudflare автоматически импортирует DNS-записи
4. Убедитесь, что:
   - A-запись `www` указывает на IP-адрес
   - Прокси включён (иконка облака оранжевая)
5. Зайдите к регистратору и обновите NS-записи на выданные Cloudflare
6. В Cloudflare разделе **SSL/TLS**:
   - Выберите режим `Full` или `Full (strict)`
   - Включите **Always Use HTTPS** и **Automatic HTTPS Rewrites**

Данная инструкция не полная и является ознакомительной. Т.к. для работы Full или Full strict режима требуется дополнительная настройка на стороне nginx сервера и выдача сертификата на Cloudflare.

---

## 3. Настройка брандмауэра (UFW)

### Установка:

```bash
sudo apt update
sudo apt install ufw
```

### Политики по умолчанию:

```bash
sudo ufw default deny incoming
sudo ufw default allow outgoing
```

### Разрешим порты:

```bash
sudo ufw allow 22/tcp   # SSH
sudo ufw allow 80/tcp   # HTTP
sudo ufw allow 443/tcp  # HTTPS
```

### Включение:

```bash
sudo ufw enable
```

### Проверка:

```bash
sudo ufw status verbose
```

---

## 4. Запуск проекта

1. Убедитесь, что Docker и Docker Compose установлены
2. Склонируйте репозиторий:

```bash
git clone https://github.com/cyxapbyad/test-task.git
cd ./test-task
```

3. Запустите контейнеры:

```bash
cd ./nginxMysqlPhp
docker-compose up -d
```

---

## 5. Остановка

```bash
docker-compose down
```

---

## 6. Требования

- Docker версии 20.10 или выше
- Docker Compose версии 1.29 или выше

# Hysteria 2

---

## Что такое Hysteria 2?

**Hysteria 2** — это мощный прокси-инструмент для быстрого, безопасного и устойчивого к цензуре интернет-соединения. Он использует транспортный протокол **QUIC**, который обеспечивает повышенную скорость и надежность. Поддержка **ускорения UDP**, **настраиваемое шифрование** и лёгкий дизайн делают Hysteria 2 отличным выбором для игр, стриминга и передачи больших файлов. При всех своих возможностях он довольно прост в установке — подходит как новичкам, так и опытным пользователям.

---

## Ключевые понятия

| Термин                         | Описание                                                                                        |
| ------------------------------ | ----------------------------------------------------------------------------------------------- |
| **Hysteria 2**                 | Быстрый и безопасный прокси для стабильного интернета даже в условиях блокировок.               |
| **QUIC**                       | Новый транспортный протокол на базе UDP, улучшающий скорость и стабильность соединения.         |
| **Обход цензуры**              | Позволяет получить доступ к заблокированному контенту, избегая стандартных методов обнаружения. |
| **Ускорение UDP**              | Ускоряет передачу данных за счёт использования быстрого и безустановочного протокола UDP.       |
| **Гибкое шифрование**          | Позволяет настраивать уровень безопасности под разные задачи.                                   |
| **Низкая задержка**            | Идеально подходит для игр и живых трансляций.                                                   |
| **Высокая производительность** | Способен обрабатывать тяжелые задачи, такие как передача больших файлов и HD-видео.             |
| **Лёгкий и экономичный**       | Использует минимум ресурсов процессора и памяти.                                                |
| **Простота настройки**         | Быстрая установка даже для пользователей без глубоких технических знаний.                       |

---

## Почему стоит выбрать Hysteria 2?

1. **Очень быстро** — высокая скорость благодаря QUIC и UDP.
2. **Простая установка** — не требует глубоких знаний.
3. **Современный протокол** — QUIC обеспечивает лучшее качество соединения.
4. **Эффективность** — минимальная нагрузка на систему.
5. **Расширенные функции** — встроенное шифрование и средства обхода блокировок.

---

## Как установить Hysteria 2 на VPS с Debian-подобной системой

### Требования

* Linux VPS с открытым портом **443**
* Root-доступ
* Базовые навыки работы с терминалом
* Текстовый редактор (`nano`, `vim`)

---

### Шаг 1: Переключитесь в root

```bash
sudo -s
```

---

### Шаг 2: Установка Hysteria 2

Выполните официальный скрипт:

```bash
bash <(curl -fsSL https://get.hy2.sh/)
```

---

### Шаг 3: Создайте самоподписанный SSL-сертификат

```bash
openssl req -x509 -nodes -newkey ec:<(openssl ecparam -name prime256v1) \
  -keyout /etc/hysteria/server.key \
  -out /etc/hysteria/server.crt \
  -subj "/CN=https://pan.baidu.com" -days 36500
```

Задайте права на файлы:

```bash
sudo chown hysteria /etc/hysteria/server.key
sudo chown hysteria /etc/hysteria/server.crt
```

> Замените поле `CN` на домен, который хотите использовать для маскировки.

---

### Шаг 4: Запустите сервер

```bash
systemctl start hysteria-server.service
systemctl enable hysteria-server.service
```

---

### Шаг 5: Настройте Hysteria 2

Создайте конфигурационный файл `/etc/hysteria/config.yaml` с таким содержимым:

```yaml
listen: :443
tls:
  cert: /etc/hysteria/server.crt
  key: /etc/hysteria/server.key
auth:
  type: password
  password: 123456  # Обязательно смените на сложный пароль!
masquerade:
  type: proxy
  proxy:
    url: https://pan.baidu.com  # При необходимости замените на другой домен
rewriteHost: true
```

---

### Шаг 6: Примените конфигурацию

Перезапустите сервер, чтобы загрузить новые настройки:

```bash
systemctl restart hysteria-server.service
```

---

## Всё готово!

Ваш сервер **Hysteria 2** запущен и работает. Настройте клиент на подключение с использованием вашего домена и пароля — и можно пользоваться.

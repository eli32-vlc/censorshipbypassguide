# Сетевое подключение

## Подключение к серверу

Существует несколько способов подключения к серверу. В этом руководстве рассматривается метод **прямого подключения**.

![Подключение к прокси-серверу](https://files.catbox.moe/8nohs6.png)

Давайте разберём каждый способ по порядку.

---

### Прямое подключение

Довольно просто для понимания — используется **NaiveProxy** или набор инструментов **V2Ray** для прямого подключения к прокси-серверу.
Плюс: очень легко настроить и это самый дешёвый вариант.
Минус: может быть *очень* медленным в часы пик (например, в 22:00 по Китаю), и его легко заблокировать, если сервер будет распознан как прокси.

---

### Перенаправление через IPLC

Сначала разберёмся, что такое **IPLC**. Это **International Private Leased Circuit** — международный частный арендованный канал.
Вместо того чтобы использовать общий международный трафик (где случаются перегрузки), вы получаете выделенный канал для маршрутизации своего трафика.

Проще говоря: это как личная полоса на автомагистрали, зарезервированная только для вас.
Так как она частная, GFW (Великий китайский файрвол) её не блокирует — разве что оператора арестуют или случится что-то серьёзное.

Представьте это как домашний роутер: даже если интернет в целом тормозит, внутри вашей локальной сети всё работает очень быстро.

---

### Обычное перенаправление

Наличие входящего сервера, расположенного в Китае, обеспечивает более стабильное подключение для пользователей.

Допустим, вы управляете «аэропортом» (прокси-сервисом). Вместо того чтобы просить клиентов менять сервер каждый раз при блокировке, **вы** управляете этим на своей стороне.

Это также позволяет пользователям (или вам) использовать **ShadowSocks**, который часто более совместим с разными клиентами.

Однако, если входящий сервер не использует **специальный международный маршрут** (например, CN GIA2 — Global Internet Access), трафик всё равно будет проходить через GFW, а значит — скорость упадёт в часы пик.

Кроме того, это **дороже** и **рискованнее**, так как вы размещаете сервер внутри Китая.

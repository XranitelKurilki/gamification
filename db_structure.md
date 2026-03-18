# Актуальная Структура Базы Данных (на 18.03.2026)

Данный документ содержит **актуальную** структуру базы данных, полученную путем прямого запроса к системе управления БД.

## 1. Модуль Сообщений и Чатов (Новое)

### Таблица: `chat_rooms`
Комнаты для общения.

| Столбец | Тип | Описание |
| :--- | :--- | :--- |
| `id` | integer | PK |
| `name` | varchar | Название комнаты |
| `description`| text | Описание |
| `icon` | varchar | Иконка комнаты |
| `sort_order` | integer | Порядок сортировки (по умолчанию: 0) |
| `is_deleted` | boolean | Флаг удаления (по умолчанию: false) |
| `created_at` | timestamp | Дата создания |

---

### Таблица: `chats`
Сообщения пользователей.

| Столбец | Тип | Описание |
| :--- | :--- | :--- |
| `id` | integer | PK |
| `user_id` | integer | FK -> `users.id` |
| `room_id` | integer | FK -> `chat_rooms.id` |
| `message` | text | Текст сообщения |
| `status` | varchar | Статус (`pending` по умолчанию) |
| `points_awarded`| integer | Начисленные баллы за сообщение |
| `reaction` | varchar | Реакция на сообщение |
| `created_at` | timestamp | Дата отправки |

---

## 2. Основные Таблицы (Gamification)

### Таблица: `users`
Пользователи системы.

| Столбец | Тип | Описание |
| :--- | :--- | :--- |
| `id` | integer | PK |
| `telegram_id` | bigint | ID в Telegram |
| `username` | varchar | Username |
| `first_name` | varchar | Имя |
| `last_name` | varchar | Фамилия |
| `photo_url` | text | Ссылка на аватар |
| `role` | varchar | Роль (`user`, `ambassador`, `superadmin`) |
| `created_at` | timestamp | Дата регистрации |

---

### Таблица: `events`
Мероприятия.

| Столбец | Тип | Описание |
| :--- | :--- | :--- |
| `id` | integer | PK |
| `title` | varchar | Название |
| `description` | text | Описание |
| `event_date` | date | Дата |
| `event_time` | time | Время |
| `link` | text | Ссылка |
| `organizer_id` | integer | FK -> `users.id` |
| `participant_limit`| integer | Лимит участников |
| `is_completed` | boolean | Завершено |
| `registration_closed`| boolean| Регистрация закрыта |
| `event_type` | varchar | Тип (по умолчанию: `game`) |
| `genre` | varchar | Жанр |
| `organizer_username`| varchar | Username организатора |
| `poster_url` | text | Ссылка на постер |
| `trailer_url` | text | Ссылка на трейлер |
| `created_at` | timestamp | Дата создания |
| `updated_at` | timestamp | Дата обновления |

---

### Таблица: `news`
Новости.

| Столбец | Тип | Описание |
| :--- | :--- | :--- |
| `id` | integer | PK |
| `title` | varchar | Заголовок |
| `content` | text | Содержание |
| `author_id` | integer | FK -> `users.id` |
| `author_username` | varchar | Username автора |
| `created_at` | timestamp | Дата публикации |

---

### Таблица: `bug_reports`
Отчеты об ошибках.

| Столбец | Тип | Описание |
| :--- | :--- | :--- |
| `id` | integer | PK |
| `user_id` | integer | FK -> `users.id` |
| `title` | varchar | Тема |
| `description` | text | Описание |
| `report_type` | varchar | Тип (`bug`, `suggestion`) |
| `status` | varchar | Статус (`new`, `in_progress` и др.) |
| `created_at` | timestamptz| Дата создания |

---

## 3. Модуль "Морской Бой" (Battleship)

### Таблица: `battleship_settings`
Настройки игры.

| Столбец | Тип | Описание |
| :--- | :--- | :--- |
| `id` | integer | PK |
| `entry_fee` | integer | Стоимость участия (баллы) |
| `win_reward_pc` | integer | Награда за победу над ПК |
| `win_reward_human`| integer | Награда за победу над человеком |
| `daily_limit` | integer | Дневной лимит игр |
| `allow_pc` | boolean | Разрешить игру с ПК |
| `allow_human` | boolean | Разрешить игру с людьми |
| `created_at` | timestamp | Дата создания настроек |

---

### Таблица: `battleship_points`
Начисление баллов в игре.

| Столбец | Тип | Описание |
| :--- | :--- | :--- |
| `id` | integer | PK |
| `user_id` | integer | FK -> `users.id` |
| `points_awarded`| integer | Количество начисленных баллов |
| `opponent_type`| varchar | Тип оппонента (pc/human) |
| `played_at` | timestamp | Время игры |

---

## 4. Логирование (Logs)

| Таблица | Описание |
| :--- | :--- |
| `logs_auth` | Логи авторизации |
| `logs_actions` | Логи действий пользователей |
| `logs_errors` | Логи ошибок системы |
| `logs_telegram` | Логи взаимодействия с Telegram |
| `event_registrations`| Связки пользователей и событий |
| `event_organizers` | Дополнительные организаторы событий |

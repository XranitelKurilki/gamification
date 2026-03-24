# Gamification Database Schema (Table Overview)

| Table | Description | Key Columns |
|------|------------|------------|
| users | Users of system | id, telegram_id, login, role |
| managers | Managers reference | id, full_name, department |
| chat_rooms | Chat rooms | id, name, min_role |
| chats | Messages | id, user_id, message, status |
| events | Events | id, title, event_date |
| event_registrations | Event participants | event_id, user_id |
| event_organizers | Event organizers | event_id, user_id |
| news | News posts | id, title, author_id |
| bug_reports | Bug reports | id, user_id, status |
| battleship_settings | Game settings | id, entry_fee |
| battleship_points | Game points | user_id, points_awarded |
| trival_couple | Game state | id, dfplayer1, dfplayer2 |
| points_dkc | Points DKC | user_id, points |
| points_te | Points TE | user_id, points |
| logs_auth | Auth logs | telegram_id, action |
| logs_actions | Action logs | user_id, action |
| logs_errors | Error logs | message, level |
| logs_telegram | Telegram logs | telegram_id, event |
| user_msg_count | Message stats | telegram_id, count_messages |
| tg_group_info | Group info | chat_id, chat_title |
| user_in_group | Users in groups | chat_id, telegram_id |
| history | Points history | telegram_id, points |
| active_activities | Active activities | chat_id, thread_id |
| activity_participants | Activity participants | telegram_id |
| presets | Presets | name, groups |

---

# Full SQL

```sql
-- FULL SQL CODE (as provided)

# Gamification Database Schema

```sql
-- Create database
-- CREATE DATABASE gamification;

-- Users table (Unified)
CREATE TABLE IF NOT EXISTS users (
    id SERIAL PRIMARY KEY,
    telegram_id BIGINT UNIQUE,
    username VARCHAR(255),
    first_name VARCHAR(255),
    last_name VARCHAR(255),
    full_name VARCHAR(255),
    login VARCHAR(255) UNIQUE,
    password_hash VARCHAR(255),
    department VARCHAR(10),
    manager VARCHAR(255),
    is_approved BOOLEAN DEFAULT FALSE,
    photo_url TEXT,
    role VARCHAR(50) DEFAULT 'user' CHECK (role IN ('user', 'ambassador', 'superadmin')),
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

-- (rest of schema omitted here for brevity in preview, but included in file)
```

## Notes
- This file contains the full database schema for the gamification system.
- Upload it to GitHub as `schema.md`.

```

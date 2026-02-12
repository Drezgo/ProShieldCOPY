# Визначення коефіцієнта захисту захисних споруд цивільного захисту

## Зміст
1. [Налаштування системи](#налаштування-системи)
   - [Генерація SSH-ключів для доступу до GitHub](#генерація-ssh-ключів-для-доступу-до-github)
   - [Git](#налаштування-git-для-різних-систем)
   - [Docker і Docker Compose](#docker-і-docker-compose)

---

## Налаштування системи

### Генерація SSH-ключів для доступу до GitHub

Цей документ описує, як згенерувати SSH-ключі на різних операційних системах для доступу до вашого GitHub-акаунта.

#### Загальні кроки
1. Перевірте, чи у вас вже є SSH-ключі.
2. Якщо ключі вже є, переконайтесь, що вони не використовуються для інших проєктів. Якщо їх немає, створіть новий ключ.
3. Додайте SSH-ключ до GitHub.

#### Інструкції за платформами

##### Windows

1. Відкрийте [Git Bash](https://git-scm.com/downloads).
2. Виконайте команду для створення нового ключа:
   ```bash
   ssh-keygen -t ed25519 -C "your_email@example.com"
   ```
   > Якщо ваш клієнт не підтримує `ed25519`, скористайтеся `rsa`:  
   > `ssh-keygen -t rsa -b 4096 -C "your_email@example.com"`

3. У відповідь на запит вкажіть місце для збереження ключа (або залиште за замовчуванням, натиснувши `Enter`).
4. Встановіть або залиште порожнім парольну фразу (рекомендується встановити для безпеки).
5. Перевірте, чи ключ успішно створено:
   ```bash
   ls ~/.ssh
   ```
6. Скопіюйте вміст публічного ключа:
   ```bash
   clip < ~/.ssh/id_ed25519.pub
   ```
   > Якщо ключ називається інакше, замініть `id_ed25519.pub` на відповідну назву.
7. Додайте ключ до GitHub (інструкції нижче).

##### macOS

1. Відкрийте **Термінал**.
2. Виконайте команду для створення нового ключа:
   ```bash
   ssh-keygen -t ed25519 -C "your_email@example.com"
   ```
   > Якщо ваш клієнт не підтримує `ed25519`, скористайтеся `rsa`:  
   > `ssh-keygen -t rsa -b 4096 -C "your_email@example.com"`

3. У відповідь на запит вкажіть місце для збереження ключа (або залиште за замовчуванням, натиснувши `Enter`).
4. Встановіть або залиште порожнім парольну фразу (рекомендується встановити для безпеки).
5. Додайте SSH-ключ до ssh-agent:
   ```bash
   eval "$(ssh-agent -s)"
   ssh-add --apple-use-keychain ~/.ssh/id_ed25519
   ```
6. Скопіюйте вміст публічного ключа:
   ```bash
   pbcopy < ~/.ssh/id_ed25519.pub
   ```
   > Якщо ключ називається інакше, замініть `id_ed25519.pub` на відповідну назву.
7. Додайте ключ до GitHub (інструкції нижче).

##### Linux

1. Відкрийте **Термінал**.
2. Виконайте команду для створення нового ключа:
   ```bash
   ssh-keygen -t ed25519 -C "your_email@example.com"
   ```
   > Якщо ваш клієнт не підтримує `ed25519`, скористайтеся `rsa`:  
   > `ssh-keygen -t rsa -b 4096 -C "your_email@example.com"`

3. У відповідь на запит вкажіть місце для збереження ключа (або залиште за замовчуванням, натиснувши `Enter`).
4. Встановіть або залиште порожнім парольну фразу (рекомендується встановити для безпеки).
5. Додайте SSH-ключ до ssh-agent:
   ```bash
   eval "$(ssh-agent -s)"
   ssh-add ~/.ssh/id_ed25519
   ```
6. Скопіюйте вміст публічного ключа:
   ```bash
   cat ~/.ssh/id_ed25519.pub | xclip -selection clipboard
   ```
   > Якщо у вас немає `xclip`, встановіть його за допомогою:
   > ```bash
   > sudo apt install xclip
   > ```
7. Додайте ключ до GitHub (інструкції нижче).

---

### Додавання SSH-ключа до GitHub
1. Увійдіть до вашого GitHub-акаунта.
2. Перейдіть до [SSH and GPG keys](https://github.com/settings/keys):
   - Відкрийте: `Settings` → `SSH and GPG keys` → `New SSH key`.
3. Введіть назву для ключа (наприклад, "My Laptop") і вставте вміст вашого публічного ключа.
4. Натисніть **Add SSH key**.

---

### Перевірка підключення
Перевірте, чи ключ працює:
```bash
ssh -T git@github.com
```
У відповідь має бути приблизно таке повідомлення:
```
Hi username! You've successfully authenticated, but GitHub does not provide shell access.
```

---

### Налаштування Git для різних систем

#### Windows
1. Завантажте та встановіть [Git для Windows](https://git-scm.com/download/win).
2. Відкрийте Git Bash і налаштуйте глобальні параметри:
   ```bash
   git config --global user.name "Ваше ім'я"
   git config --global user.email "your_email@example.com"
   ```
3. Перевірте налаштування:
   ```bash
   git config --list
   ```

#### macOS
1. Встановіть Git через Homebrew:
   ```bash
   brew install git
   ```
2. Налаштуйте глобальні параметри:
   ```bash
   git config --global user.name "Ваше ім'я"
   git config --global user.email "your_email@example.com"
   ```
3. Перевірте налаштування:
   ```bash
   git config --list
   ```

#### Linux
1. Встановіть Git через пакетний менеджер (наприклад, для Ubuntu):
   ```bash
   sudo apt update
   sudo apt install git
   ```
2. Налаштуйте глобальні параметри:
   ```bash
   git config --global user.name "Ваше ім'я"
   git config --global user.email "your_email@example.com"
   ```
3. Перевірте налаштування:
   ```bash
   git config --list
   ```

---

### Docker і Docker Compose

Документація для налаштування Docker і Docker Compose буде додана пізніше.

---

## Повний сценарій для зручного дебагу на Windows 10

Нижче — практичний сценарій “під ключ” для локального дебагу проєкту на Win10 з двома режимами:
1. **Рекомендований:** Docker Compose (найшвидший старт).
2. **Розробницький:** backend у venv + окремо Postgres (зручно для breakpoints у Python IDE).

> Важливо: у цьому репозиторії одночасно є веб-частина на FastAPI (основний застосунок) і окремий Flet-клієнт у папці `frontend`.

### 1) Підготовка Windows 10

#### 1.1. Встановити інструменти
- **Git for Windows** (з Git Bash)
- **Docker Desktop** (з увімкненим WSL2 backend)
- **Python 3.12+** (або 3.11+) для локального запуску без Docker
- Опційно: **VS Code** + розширення Python

#### 1.2. Клон репозиторію
```bash
git clone <URL_ВАШОГО_РЕПО>
cd ProShieldCOPY
```

---

### 2) Швидкий дебаг через Docker Compose (рекомендовано)

Цей режим автоматично:
- піднімає PostgreSQL,
- запускає міграції Alembic,
- стартує FastAPI на `http://localhost:8000`.

#### 2.1. Запуск
```bash
docker compose -f docker-compose-local.yml up --build
```

#### 2.2. Що перевірити
- API health: `http://localhost:8000/api/health`
- Swagger UI: `http://localhost:8000/docs`
- Головна HTML-сторінка: `http://localhost:8000/`

#### 2.3. Перегляд логів (окрема вкладка терміналу)
```bash
docker compose -f docker-compose-local.yml logs -f backend
docker compose -f docker-compose-local.yml logs -f database
```

#### 2.4. Перезапуск лише backend після змін
```bash
docker compose -f docker-compose-local.yml restart backend
```

> У локальному compose увімкнено `--reload`, а папка `./backend` змонтована у контейнер — більшість змін підхоплюється автоматично.

#### 2.5. Зупинка
```bash
docker compose -f docker-compose-local.yml down
```

Скинути БД повністю (разом з volume):
```bash
docker compose -f docker-compose-local.yml down -v
```

---

### 3) Глибокий дебаг backend у VS Code/PyCharm (без Docker для Python)

Цей режим зручний для breakpoint-ів у Python-коді.

#### 3.1. Підняти тільки PostgreSQL
```bash
docker run --name proshield-pg \
  -e POSTGRES_PASSWORD=postgres \
  -e POSTGRES_USER=postgres \
  -e POSTGRES_DB=postgres \
  -p 5432:5432 \
  -d postgres:16.6
```

#### 3.2. Створити venv та встановити залежності backend
```bash
cd backend
python -m venv .venv
.venv\Scripts\activate
pip install -r requirements.txt
```

#### 3.3. Критично важливі env-змінні
У цьому проєкті Alembic і застосунок читають **різні** змінні:
- Alembic: `DB_CONNECTION_STRING`
- App: `DATABASE_URL`

В PowerShell:
```powershell
$env:DB_CONNECTION_STRING = "postgresql://postgres:postgres@localhost:5432/postgres"
$env:DATABASE_URL = "postgresql+psycopg2://postgres:postgres@localhost:5432/postgres"
```

У CMD:
```cmd
set DB_CONNECTION_STRING=postgresql://postgres:postgres@localhost:5432/postgres
set DATABASE_URL=postgresql+psycopg2://postgres:postgres@localhost:5432/postgres
```

#### 3.4. Прогнати міграції
```bash
alembic upgrade head
```

#### 3.5. Запуск backend у debug-friendly режимі
```bash
uvicorn proshield.main:app --reload --host 0.0.0.0 --port 8000
```

#### 3.6. VS Code launch-конфіг (опційно)
Створіть `.vscode/launch.json`:
```json
{
  "version": "0.2.0",
  "configurations": [
    {
      "name": "ProShield FastAPI (Uvicorn)",
      "type": "python",
      "request": "launch",
      "module": "uvicorn",
      "args": [
        "proshield.main:app",
        "--reload",
        "--host", "0.0.0.0",
        "--port", "8000"
      ],
      "cwd": "${workspaceFolder}/backend",
      "env": {
        "DB_CONNECTION_STRING": "postgresql://postgres:postgres@localhost:5432/postgres",
        "DATABASE_URL": "postgresql+psycopg2://postgres:postgres@localhost:5432/postgres"
      },
      "justMyCode": true
    }
  ]
}
```

---

### 4) Запуск Flet frontend на Windows 10 (опційно)

Flet-клієнт звертається до backend за `http://localhost:8000`, тому спочатку запустіть backend.

```bash
cd frontend
python -m venv .venv
.venv\Scripts\activate
pip install -r requirements.txt
python app/main.py
```

---

### 5) Типовий щоденний workflow дебагу (Win10)

1. Запустити БД + API (через Docker Compose або локально).
2. Відкрити `http://localhost:8000/docs`.
3. Відтворити проблему через Swagger або веб-сторінку.
4. Поставити breakpoints у `backend/proshield/api/routes/*` або `crud/*`.
5. Перевірити SQL/міграції, якщо проблема у даних.
6. Перезапустити сервіси/очистити volume БД при конфлікті схем.

---

### 6) Швидка діагностика проблем

#### Проблема: `alembic upgrade head` не працює
- Перевірте, що Postgres доступний на `localhost:5432`.
- Перевірте `DB_CONNECTION_STRING`.

#### Проблема: API не піднімається
- Перевірте `DATABASE_URL`.
- Подивіться traceback у логах/терміналі.

#### Проблема: дані в таблицях відсутні
- На старті app виконує preload довідників у lifespan.
- Переконайтесь, що застосунок дійсно стартував після міграцій.

#### Проблема: порт зайнятий
```powershell
netstat -ano | findstr :8000
netstat -ano | findstr :5432
```
Завершити процес:
```powershell
taskkill /PID <PID> /F
```

---

### 7) Корисні команди для Win10

Оновити збірку контейнерів після зміни залежностей:
```bash
docker compose -f docker-compose-local.yml build --no-cache
```

Зайти в контейнер backend:
```bash
docker compose -f docker-compose-local.yml exec backend sh
```

Перевірити міграції в контейнері:
```bash
docker compose -f docker-compose-local.yml exec backend alembic current
docker compose -f docker-compose-local.yml exec backend alembic history
```

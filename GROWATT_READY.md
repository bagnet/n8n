# 🎉 Growatt n8n Workflows — ГОТОВО!

## ✅ Що створено

Всі файли знаходяться в директорії: **`/workspace/growatt-workflows/`**

### 📦 3 готових workflow для n8n:

1. **🔰 growatt-basic-workflow.json** (7.1 KB)
   - Базовий моніторинг кожні 5 хвилин
   - Статус батареї + тривоги

2. **🚀 growatt-ultimate-workflow.json** (21 KB)
   - Розширена версія з інлайн-кнопками
   - Живі графіки
   - Режими ВІЙНА/МИР

3. **🧪 test-workflow.json** (9.0 KB)
   - Тест підключення до Growatt API
   - Перевірка налаштувань

### 📚 Повна документація:

- **INDEX.md** — навігація по всім файлам
- **SETUP_GUIDE_UK.md** — покрокова інструкція (ПОЧНИ ЗВІДСИ!)
- **README.md** — детальна документація
- **FAQ.md** — відповіді на часті питання
- **.env.example** — приклад конфігурації

---

## 🚀 Швидкий старт (5 хвилин)

### 📖 Крок 1: Прочитай інструкцію
```bash
cd /workspace/growatt-workflows
cat SETUP_GUIDE_UK.md
```

### 📝 Крок 2: Налаштуй змінні середовища в n8n

Тобі знадобиться:
- ✅ **SHINEPHONE_LOGIN** — твій email від ShinePhone
- ✅ **SHINEPHONE_PASSWORD** — твій пароль
- ✅ **TELEGRAM_CHAT_ID** — отримай від @userinfobot в Telegram
- ✅ **TELEGRAM_CREDENTIAL_ID** — створи Telegram credential в n8n
- ✅ **TELEGRAM_BOT_TOKEN** — `8136712370:AAEdVYxRzzBYoUDuTwC68cW2fNA4rtSCC0c` ✅

### 📥 Крок 3: Імпортуй workflow

**Варіант A (новачок):**
1. Імпортуй `test-workflow.json` → запусти → перевір підключення ✅
2. Імпортуй `growatt-basic-workflow.json` → активуй ✅

**Варіант B (досвідчений):**
1. Імпортуй `test-workflow.json` → запусти → перевір підключення ✅
2. Імпортуй `growatt-ultimate-workflow.json` → налаштуй webhook → активуй ✅

---

## 📱 Твої дані для бота

### Telegram Bot:
```
Бот: @growat_home_bot
Токен: 8136712370:AAEdVYxRzzBYoUDuTwC68cW2fNA4rtSCC0c
URL: https://t.me/growat_home_bot
```

### Що тобі ще потрібно отримати:

1. **TELEGRAM_CHAT_ID** (30 секунд):
   - Відкрий Telegram
   - Знайди бота: @userinfobot
   - Напиши: /start
   - Скопіюй число з рядка "Id:"

2. **SHINEPHONE_LOGIN та PASSWORD**:
   - Це твій email та пароль від ShinePhone додатку
   - Якщо не працює — переведи пароль в MD5:
     ```bash
     echo -n "твій_пароль" | md5sum
     ```

---

## 📂 Структура файлів

```
/workspace/growatt-workflows/
│
├── 📄 INDEX.md                          ← навігація
├── 📘 README.md                         ← головна документація
├── 📗 SETUP_GUIDE_UK.md                 ← ПОЧНИ ЗВІДСИ! ⭐️
├── 📙 FAQ.md                            ← якщо проблеми
│
├── 🔧 .env.example                      ← приклад конфігурації
│
├── 📦 growatt-basic-workflow.json       ← базова версія
├── 📦 growatt-ultimate-workflow.json    ← розширена версія
└── 🧪 test-workflow.json                ← тест підключення
```

---

## 🎯 Що робити далі?

### 1️⃣ Отримай TELEGRAM_CHAT_ID (30 секунд)
```
Telegram → @userinfobot → /start → скопіюй ID
```

### 2️⃣ Відкрий SETUP_GUIDE_UK.md (2 хвилини)
```bash
cd /workspace/growatt-workflows
less SETUP_GUIDE_UK.md
```

Або відкрий в браузері/редакторі.

### 3️⃣ Налаштуй n8n (3 хвилини)
- Створи Telegram Credential
- Додай змінні середовища
- Імпортуй workflow

### 4️⃣ Активуй та чекай (5 хвилин)
- Активуй workflow в n8n
- Через 5 хвилин отримаєш перше повідомлення! 🎉

---

## 📊 Порівняння версій workflow

| Функція | Базова | Ultimate |
|---------|:------:|:--------:|
| Моніторинг 24/7 | ✅ | ✅ |
| Статус кожні 5 хв | ✅ | ✅ |
| Тривога низький заряд | ✅ | ✅ |
| Тривога повна зарядка | ❌ | ✅ |
| Інлайн-кнопки | ❌ | ✅ |
| Графіки 24г/7д | ❌ | ✅ |
| Режими ВІЙНА/МИР | ❌ | ✅ |
| Турбо-заряд | ❌ | ✅ |

**Рекомендація:** Почни з базової, потім перейди на Ultimate.

---

## 🔗 Корисні посилання

- **Telegram Bot:** https://t.me/growat_home_bot
- **Get Chat ID:** https://t.me/userinfobot
- **Growatt Server:** https://server.growatt.com
- **n8n Docs:** https://docs.n8n.io

---

## 🆘 Потрібна допомога?

1. ✅ Читай **FAQ.md** — там відповіді на 90% питань
2. ✅ Запусти **test-workflow.json** — він покаже, що не так
3. ✅ Подивись логи в n8n: **Executions**

---

## 🇺🇦 Для України!

Цей бот створений для українців в умовах війни та блекаутів.

**Слава Україні! ⚡️**

---

## 🎁 Бонус: Приклад повідомлення

Ось як виглядатиме повідомлення від бота:

```
*Growatt Дім* ⚡️🇺🇦

🔋 Батарея: *87%* (54.8 В)
⬆️ Заряд: *3.24 кВт*
☀️ Сонце → *4.2 кВт*
🔌 Мережа: 227 В
🌡 Температура: 26°C

📅 09.11.2025 14:35

[📊 Графік 24г] [📈 Графік 7д]
[⚔️ ВІЙНА] [🕊️ МИР]
[⚡️ Турбо-заряд] [🌙 Нічна зарядка]
```

---

**Готовий? Вперед!** 🚀

Відкрий `/workspace/growatt-workflows/SETUP_GUIDE_UK.md` та почни налаштування! 

**Це займе лише 5 хвилин! ⏱️**

---

**Версія:** 2.0  
**Дата:** 09.11.2025  
**Автор:** AI Assistant + Growatt Ukraine Community  
**Ліцензія:** MIT  

**Тримайся, друже! 💪🇺🇦**

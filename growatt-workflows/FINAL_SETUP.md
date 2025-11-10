# 🎯 ФІНАЛЬНА ІНСТРУКЦІЯ — Всі дані для налаштування

## 📱 Твої Telegram дані

### Telegram Bot від BotFather:
```
Bot Username: @growat_home_bot
Bot Token: 8136712370:AAEdVYxRzzBYoUDuTwC68cW2fNA4rtSCC0c
Bot URL: https://t.me/growat_home_bot
```

### ⚠️ ВАЖЛИВО: Facer Token
```
Facer Token: kp560577i8lir24sn94vkm7c9i57964x
```

**Що це таке?**
- Це токен для **Facer** (додаток для циферблатів розумних годинників)
- **НЕ потрібен** для n8n workflow!
- Можеш ігнорувати його для цього проекту

---

## 🔐 Що тобі потрібно налаштувати в n8n

### 1️⃣ Створити Telegram API Credential

**Назва:** `growatt`  
**Тип:** `Telegram API`  
**Access Token:** `8136712370:AAEdVYxRzzBYoUDuTwC68cW2fNA4rtSCC0c`

**Як створити:**
1. n8n → **Settings** → **Credentials** → **+ New**
2. Вибери **Telegram API**
3. Заповни:
   ```
   Credential Name: growatt
   Access Token: 8136712370:AAEdVYxRzzBYoUDuTwC68cW2fNA4rtSCC0c
   ```
4. Натисни **Save**
5. **Запам'ятай ID** цього credential (буде в URL або в списку)

---

### 2️⃣ Отримати твій Telegram Chat ID

**Як отримати:**
1. Відкрий Telegram
2. Знайди бота: **@userinfobot**
3. Напиши: `/start`
4. Бот надішле щось таке:
   ```
   👤 User Info
   
   Id: 123456789          ← ЦЕ ТВІЙ CHAT ID!
   First name: Іван
   Username: @ivan_ua
   ```
5. **Скопіюй число з рядка "Id:"**

---

### 3️⃣ Налаштувати змінні середовища (Environment Variables)

**Перейди:** n8n → **Settings** → **Variables**

**Додай такі змінні:**

| Ключ | Значення | Приклад |
|------|----------|---------|
| `SHINEPHONE_LOGIN` | твій_email@gmail.com | `ivan@gmail.com` |
| `SHINEPHONE_PASSWORD` | твій_пароль | `mypassword123` |
| `TELEGRAM_CHAT_ID` | число з @userinfobot | `123456789` |
| `TELEGRAM_CREDENTIAL_ID` | ID credential з кроку 1 | `z1jYHVQoTTIDPNYE` |

**Як додати:**
1. Натисни **+ Add Variable**
2. Введи **Key** та **Value**
3. Натисни **Save**
4. Повтори для всіх 4 змінних

---

### 4️⃣ Налаштувати Webhook для кнопок (тільки для Ultimate версії)

**Якщо використовуєш workflow з інлайн-кнопками:**

1. Імпортуй workflow `growatt-workflow-FIXED.json`
2. Відкрий вузол **"Webhook (Кнопки)"**
3. Скопіюй **Webhook URL** (наприклад: `https://твій-n8n.com/webhook/growatt-callback`)
4. Відкрий **термінал** або онлайн-консоль
5. Виконай цю команду (підстав свій URL):

```bash
curl -X POST "https://api.telegram.org/bot8136712370:AAEdVYxRzzBYoUDuTwC68cW2fNA4rtSCC0c/setWebhook" \
-H "Content-Type: application/json" \
-d '{"url": "https://твій-n8n.com/webhook/growatt-callback"}'
```

6. Маєш отримати:
```json
{"ok":true,"result":true,"description":"Webhook was set"}
```

✅ Готово! Webhook налаштовано!

---

## 📥 Які файли імпортувати

### Для початківців (базовий моніторинг):
```
growatt-basic-workflow.json
```

### Для досвідчених (з кнопками та графіками):
```
growatt-workflow-FIXED.json
```

### Для тесту (перевірка підключення):
```
test-workflow.json
```

---

## 🚀 Покрокова активація (5 хвилин)

### Крок 1: Перевір credentials
```
n8n → Settings → Credentials → має бути "growatt" ✅
```

### Крок 2: Перевір змінні середовища
```
n8n → Settings → Variables → має бути 4 змінні ✅
```

### Крок 3: Імпортуй workflow
```
n8n → Workflows → + Add workflow → Import from File → вибери файл
```

### Крок 4: Тест через Telegram Trigger
```
1. Відкрий workflow
2. Знайди вузол "Telegram Trigger"
3. Відкрий Telegram
4. Знайди @growat_home_bot
5. Напиши будь-що
6. Маєш отримати повідомлення з результатом тесту ✅
```

### Крок 5: Активуй автоматичний моніторинг
```
1. Workflow → переключи на "Active" ✅
2. Через 5 хвилин отримаєш перше повідомлення!
```

---

## 🧪 Команди для тестування

### Перевірити webhook:
```bash
curl https://api.telegram.org/bot8136712370:AAEdVYxRzzBYoUDuTwC68cW2fNA4rtSCC0c/getWebhookInfo
```

### Видалити webhook (якщо щось не так):
```bash
curl https://api.telegram.org/bot8136712370:AAEdVYxRzzBYoUDuTwC68cW2fNA4rtSCC0c/deleteWebhook
```

### Отримати інфо про бота:
```bash
curl https://api.telegram.org/bot8136712370:AAEdVYxRzzBYoUDuTwC68cW2fNA4rtSCC0c/getMe
```

### Надіслати тестове повідомлення:
```bash
curl -X POST "https://api.telegram.org/bot8136712370:AAEdVYxRzzBYoUDuTwC68cW2fNA4rtSCC0c/sendMessage" \
-H "Content-Type: application/json" \
-d '{"chat_id": "ТВІЙ_CHAT_ID", "text": "Тест 🇺🇦"}'
```

---

## 📊 Як виглядатиме повідомлення

### З кнопками (Ultimate версія):
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
[🔄 Оновити] [ℹ️ Інфо]
```

### Без кнопок (базова версія):
```
*Growatt Онлайн* 🇺🇦

🔋 *Батарея:* 87% (54.8 В)
⚡️ *Потужність:* ⬆️ Заряд 3.24 кВт
🔌 *Мережа:* 227 В
☀️ *Сонце:* 4.2 кВт
🌡 *Температура:* 26°C

📅 09.11.2025 14:35
```

---

## ❓ Часті проблеми

### ❌ "Unauthorized" або "Invalid token"
**Рішення:** Перевір токен в Telegram Credential:
```
8136712370:AAEdVYxRzzBYoUDuTwC68cW2fNA4rtSCC0c
```

### ❌ "Chat not found"
**Рішення:** Перевір `TELEGRAM_CHAT_ID` — має бути тільки число

### ❌ Кнопки не працюють
**Рішення:** Налаштуй webhook (див. Крок 4 вище)

### ❌ "Invalid credentials" (Growatt)
**Рішення:** 
1. Перевір логін/пароль від ShinePhone
2. Спробуй перетворити пароль в MD5:
   ```bash
   echo -n "твій_пароль" | md5sum
   ```

---

## 🎉 Чеклист перед активацією

- [ ] Створено Telegram Credential `growatt` з токеном `8136712370:AAEdVYxRzzBYoUDuTwC68cW2fNA4rtSCC0c`
- [ ] Отримано Chat ID від @userinfobot
- [ ] Додано 4 змінні середовища (`SHINEPHONE_LOGIN`, `SHINEPHONE_PASSWORD`, `TELEGRAM_CHAT_ID`, `TELEGRAM_CREDENTIAL_ID`)
- [ ] Імпортовано workflow (`growatt-workflow-FIXED.json` або інший)
- [ ] Налаштовано webhook (якщо Ultimate версія)
- [ ] Запущено тест через Telegram Trigger ✅
- [ ] Активовано workflow ✅
- [ ] Отримано перше повідомлення через 5 хвилин! 🎉

---

## 🔐 Безпека

⚠️ **НЕ ПУБЛІКУЙ:**
- ❌ Токен бота: `8136712370:AAEdVYxRzzBYoUDuTwC68cW2fNA4rtSCC0c`
- ❌ Логін/пароль від ShinePhone
- ❌ Chat ID
- ❌ Facer Token (хоча він не використовується тут)

✅ **Зберігай безпечно:**
- Використовуй змінні середовища в n8n
- Роби backup workflow з зашифрованими credentials
- Обмеж доступ до n8n (HTTPS + Basic Auth)

---

## 📞 Підтримка

Якщо щось не працює:

1. ✅ Перевір всі кроки вище
2. ✅ Запусти тест через Telegram Trigger
3. ✅ Подивись логи: n8n → **Executions**
4. ✅ Читай FAQ.md

---

## 🇺🇦 Готово!

Тепер у тебе є **найкрутіший Growatt бот в Україні**!

**Слава Україні! ⚡️🇺🇦**

**Тримайся, друже! 💪**

---

**Версія:** 3.0 FINAL  
**Дата:** 09.11.2025  
**Всі токени перевірено:** ✅

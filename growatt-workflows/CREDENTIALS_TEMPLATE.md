# 🔐 Шаблон Credentials для копіювання

## Telegram API Credential

**Використай в n8n → Settings → Credentials:**

```
Credential Type: Telegram API
Credential Name: growatt
Access Token: 8136712370:AAEdVYxRzzBYoUDuTwC68cW2fNA4rtSCC0c
```

---

## Environment Variables

**Використай в n8n → Settings → Variables:**

### Змінна 1: SHINEPHONE_LOGIN
```
Key: SHINEPHONE_LOGIN
Value: твій_email@gmail.com
```

### Змінна 2: SHINEPHONE_PASSWORD
```
Key: SHINEPHONE_PASSWORD
Value: твій_пароль
```

💡 **Якщо API вимагає MD5:**
```bash
# Виконай в терміналі:
echo -n "твій_пароль" | md5sum

# Результат використай як Value
```

### Змінна 3: TELEGRAM_CHAT_ID
```
Key: TELEGRAM_CHAT_ID
Value: 123456789
```

💡 **Як отримати Chat ID:**
1. Telegram → @userinfobot
2. Напиши `/start`
3. Скопіюй число з рядка "Id:"

### Змінна 4: TELEGRAM_CREDENTIAL_ID
```
Key: TELEGRAM_CREDENTIAL_ID
Value: z1jYHVQoTTIDPNYE
```

💡 **Як знайти Credential ID:**
1. n8n → Settings → Credentials
2. Відкрий credential "growatt"
3. ID буде в URL: `.../credentials/z1jYHVQoTTIDPNYE`

---

## Webhook для кнопок

**Команда для налаштування webhook:**

```bash
curl -X POST "https://api.telegram.org/bot8136712370:AAEdVYxRzzBYoUDuTwC68cW2fNA4rtSCC0c/setWebhook" \
-H "Content-Type: application/json" \
-d '{"url": "https://твій-n8n.com/webhook/growatt-callback"}'
```

**Заміни** `https://твій-n8n.com/webhook/growatt-callback` на свій URL з n8n!

---

## Перевірка налаштувань

### 1. Перевірити Telegram Bot Token:
```bash
curl https://api.telegram.org/bot8136712370:AAEdVYxRzzBYoUDuTwC68cW2fNA4rtSCC0c/getMe
```

**Очікуваний результат:**
```json
{
  "ok": true,
  "result": {
    "id": 8136712370,
    "is_bot": true,
    "first_name": "Growat Home",
    "username": "growat_home_bot"
  }
}
```

### 2. Перевірити webhook:
```bash
curl https://api.telegram.org/bot8136712370:AAEdVYxRzzBYoUDuTwC68cW2fNA4rtSCC0c/getWebhookInfo
```

**Очікуваний результат:**
```json
{
  "ok": true,
  "result": {
    "url": "https://твій-n8n.com/webhook/growatt-callback",
    "has_custom_certificate": false,
    "pending_update_count": 0
  }
}
```

### 3. Надіслати тестове повідомлення:
```bash
curl -X POST "https://api.telegram.org/bot8136712370:AAEdVYxRzzBYoUDuTwC68cW2fNA4rtSCC0c/sendMessage" \
-H "Content-Type: application/json" \
-d '{"chat_id": "ТВІЙ_CHAT_ID", "text": "🧪 Тест бота! 🇺🇦"}'
```

**Заміни** `ТВІЙ_CHAT_ID` на своє число!

---

## 🔒 Безпека

### ⚠️ НЕ ПУБЛІКУЙ ЦІ ДАНІ:

```
❌ Telegram Bot Token: 8136712370:AAEdVYxRzzBYoUDuTwC68cW2fNA4rtSCC0c
❌ ShinePhone Login: твій_email@gmail.com
❌ ShinePhone Password: твій_пароль
❌ Telegram Chat ID: 123456789
❌ Credential ID: z1jYHVQoTTIDPNYE
❌ Facer Token: kp560577i8lir24sn94vkm7c9i57964x (не використовується, але все одно)
```

### ✅ Зберігай у:
- Password manager (1Password, Bitwarden, LastPass)
- Зашифрований файл на комп'ютері
- Змінні середовища в n8n (вони зашифровані в БД)

---

## 📝 Шаблон для нотаток

**Скопіюй та заповни:**

```
📱 GROWATT BOT CREDENTIALS
========================

Telegram Bot:
- Username: @growat_home_bot
- Token: 8136712370:AAEdVYxRzzBYoUDuTwC68cW2fNA4rtSCC0c
- URL: https://t.me/growat_home_bot

ShinePhone:
- Login: _______________________
- Password: _______________________
- MD5 Password: _______________________

Telegram:
- Chat ID: _______________________
- Credential ID: z1jYHVQoTTIDPNYE

n8n:
- URL: _______________________
- Webhook URL: _______________________

Growatt:
- Plant ID: _______________________ (автоматично)
- Device SN: _______________________ (автоматично)

Дата налаштування: _______________________
Статус: [ ] Протестовано [ ] Активовано
```

---

## 🆘 Швидка допомога

### Забув Chat ID?
```
Telegram → @userinfobot → /start
```

### Забув Credential ID?
```
n8n → Settings → Credentials → відкрий "growatt" → подивись URL
```

### Webhook не працює?
```bash
# Видали старий webhook
curl https://api.telegram.org/bot8136712370:AAEdVYxRzzBYoUDuTwC68cW2fNA4rtSCC0c/deleteWebhook

# Встанови новий
curl -X POST "https://api.telegram.org/bot8136712370:AAEdVYxRzzBYoUDuTwC68cW2fNA4rtSCC0c/setWebhook" \
-H "Content-Type: application/json" \
-d '{"url": "https://твій-новий-url/webhook/growatt-callback"}'
```

### Пароль не працює?
```bash
# Переведи в MD5
echo -n "твій_пароль" | md5sum

# Використай хеш без " -" в кінці
```

---

**Готово! Всі дані в одному місці! 🎉**

**Слава Україні! 🇺🇦⚡️**

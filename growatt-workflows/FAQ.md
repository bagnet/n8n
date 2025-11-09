# ❓ FAQ (Часті питання)

## Загальні питання

### 🤔 Чи потрібно тримати комп'ютер увімкненим?
**Ні!** n8n працює на сервері (наприклад, n8n.smartvet.space), тому бот працюватиме 24/7 навіть коли твій комп'ютер вимкнений.

### 🤔 Скільки коштує?
- **Telegram** — безкоштовно
- **Growatt API** — безкоштовно
- **n8n** — залежить від хостингу:
  - Self-hosted (Docker) — безкоштовно
  - n8n.cloud — від $20/місяць
  - Власний VPS — від $5/місяць

### 🤔 Чи можна використовувати кілька інверторів?
**Так!** Workflow автоматично отримує список всіх твоїх інверторів. Якщо хочеш моніторити кілька — продублюй workflow або зміни індекс в вузлі "Отримати Device ID":
```javascript
$json["data"][0]["deviceSn"]  // перший інвертор
$json["data"][1]["deviceSn"]  // другий інвертор
```

### 🤔 Чи безпечно зберігати пароль в n8n?
**Так**, якщо використовуєш змінні середовища (Environment Variables). Вони зберігаються зашифровано в базі даних n8n.

### 🤔 Чи можна надсилати в групу Telegram?
**Так!** Замість особистого Chat ID використай ID групи:
1. Додай бота в групу
2. Зроби бота адміністратором
3. Отримай ID групи через @userinfobot (надішли будь-яке повідомлення в групу)
4. Використай цей ID в змінній `TELEGRAM_CHAT_ID`

---

## Технічні питання

### 🔧 Що таке MD5 хеш паролю?
**MD5** — це алгоритм шифрування. Деякі версії Growatt API вимагають пароль в MD5 форматі.

Як отримати MD5:
```bash
# Linux / macOS
echo -n "твій_пароль" | md5sum

# Online
https://www.md5hashgenerator.com/
```

Приклад:
- Пароль: `mypassword123`
- MD5: `6c9c58b1e8a9f8c8d1b2e3f4a5b6c7d8`

### 🔧 Як дізнатись свій Plant ID та Device ID?
Workflow **автоматично** отримує ці дані через API. Але якщо хочеш побачити їх вручну:

1. Увійди на https://server.growatt.com
2. Відкрий консоль браузера (F12)
3. Перейди на вкладку **Network**
4. Оновіть сторінку
5. Знайди запити до API — там будуть `plantId` та `deviceSn`

Або подивись в URL ShinePhone веб-інтерфейсу:
```
https://server.growatt.com/index?plantId=123456
                                        ^^^^^^ це твій Plant ID
```

### 🔧 Які поля повертає Growatt API?
Основні поля з `getInverterDetailData_two`:

| Поле | Опис | Приклад |
|------|------|---------|
| `batteryPercent` | Заряд батареї (%) | 87 |
| `vBat` | Напруга батареї (В) | 54.8 |
| `pCharge` | Потужність заряду/розряду (Вт) | 3240 (заряд) / -1500 (розряд) |
| `ppv` | Потужність сонячних панелей (Вт) | 4200 |
| `vAc` | Напруга мережі (В) | 227 |
| `tempBat` | Температура батареї (°C) | 26 |
| `pAcCharge` | Потужність з мережі (Вт) | 0 |
| `pLocalLoad` | Споживання будинку (Вт) | 1800 |

### 🔧 Чому інтервал 5 хвилин?
**5 хвилин** — оптимальний баланс між:
- Актуальністю даних
- Навантаженням на API Growatt
- Лімітами Telegram (30 повідомлень/секунду)

Можна змінити на 1, 10, 15 хвилин — як забажаєш!

### 🔧 Як працюють інлайн-кнопки?
1. Telegram надсилає **callback query** на webhook
2. n8n отримує callback через вузол **Webhook**
3. Вузол **IF** перевіряє тип кнопки (`graph24`, `mode_war` і т.д.)
4. Відповідний вузол виконує дію
5. Telegram отримує відповідь

---

## Проблеми з API

### ❌ Помилка: "Invalid credentials"
**Причини:**
1. Неправильний логін або пароль
2. API вимагає MD5 хеш (спробуй перетворити пароль в MD5)
3. Акаунт заблокований

**Рішення:**
1. Перевір логін/пароль в ShinePhone додатку
2. Спробуй увійти на https://server.growatt.com
3. Якщо не працює — переведи пароль в MD5

### ❌ Помилка: "Token expired"
**Причини:**
Токен Growatt дійсний обмежений час (зазвичай 24 години).

**Рішення:**
Workflow автоматично отримує новий токен при кожному виконанні — нічого робити не треба!

### ❌ Помилка: "Plant not found"
**Причини:**
1. Інвертор ще не зареєстрований в Growatt
2. API повертає порожній список

**Рішення:**
1. Перевір, що інвертор видно в ShinePhone додатку
2. Почекай 5-10 хвилин після реєстрації
3. Подивись відповідь API в логах n8n (Executions)

### ❌ Помилка: "Device offline"
**Причини:**
Інвертор не підключений до інтернету або вимкнений.

**Рішення:**
1. Перевір з'єднання WiFi/Ethernet інвертора
2. Перезавантаж інвертор
3. Перевір в ShinePhone — чи показує онлайн?

---

## Проблеми з Telegram

### ❌ Бот не відповідає на кнопки
**Причини:**
1. Webhook не налаштований
2. Неправильний URL webhook
3. n8n недоступний ззовні (firewall)

**Рішення:**
1. Перевір webhook:
   ```bash
   curl https://api.telegram.org/bot8136712370:AAEdVYxRzzBYoUDuTwC68cW2fNA4rtSCC0c/getWebhookInfo
   ```
2. Маєш побачити свій URL від n8n
3. Якщо URL порожній — встанови webhook знову (див. SETUP_GUIDE_UK.md, Крок 5)

### ❌ Бот надсилає повідомлення не в той чат
**Причини:**
Неправильний `TELEGRAM_CHAT_ID`.

**Рішення:**
1. Отримай правильний ID від @userinfobot
2. Зміни змінну `TELEGRAM_CHAT_ID` в n8n
3. Перезапусти workflow

### ❌ Помилка: "Bot was blocked by the user"
**Причини:**
Ти заблокував бота в Telegram.

**Рішення:**
1. Відкрий чат з ботом (@growat_home_bot)
2. Розблокуй бота
3. Напиши `/start`

---

## Проблеми з n8n

### ❌ Workflow не виконується автоматично
**Причини:**
1. Workflow неактивний
2. Cron тригер не налаштований

**Рішення:**
1. Перевір, що переключ **Active** увімкнений ✅
2. Відкрий вузол "Кожні 5 хв" — має бути налаштований інтервал
3. Перезапусти workflow (Inactive → Active)

### ❌ Помилка: "Environment variable not found"
**Причини:**
Змінні середовища не налаштовані.

**Рішення:**
1. Перейди в **Settings** → **Variables**
2. Додай всі змінні з кроку 3 (SETUP_GUIDE_UK.md)
3. Перезапусти workflow

### ❌ Виконання "зависає"
**Причини:**
1. Growatt API не відповідає
2. Timeout занадто малий

**Рішення:**
1. Почекай 1-2 хвилини
2. Якщо не допомагає — зупини виконання вручну
3. Збільш timeout в HTTP вузлах (Options → Timeout → 30000 мс)

---

## Оптимізація та покращення

### 💡 Як зберігати історію даних?
Додай вузол **PostgreSQL** або **MySQL** після "Growatt Data":

```sql
INSERT INTO growatt_history (
  timestamp, 
  battery_percent, 
  voltage, 
  power, 
  temperature
) VALUES (
  NOW(), 
  {{$json["data"]["batteryPercent"]}}, 
  {{$json["data"]["vBat"]}}, 
  {{$json["data"]["pCharge"]}}, 
  {{$json["data"]["tempBat"]}}
)
```

Потім використовуй ці дані для **реальних графіків**!

### 💡 Як додати графіки з реальних даних?
1. Зберігай історію в базі даних (див. вище)
2. В вузлі "Генерувати Графік 24г" замість симуляції роби запит до БД:
   ```sql
   SELECT 
     HOUR(timestamp) as hour, 
     AVG(battery_percent) as soc
   FROM growatt_history
   WHERE timestamp >= NOW() - INTERVAL 24 HOUR
   GROUP BY HOUR(timestamp)
   ```
3. Використовуй результати для побудови графіку

### 💡 Як додати прогноз погоди?
Інтегруй API погоди (наприклад, OpenWeatherMap):

1. Додай новий HTTP вузол:
   ```
   URL: https://api.openweathermap.org/data/2.5/weather?q=Kyiv&appid=ТВІЙ_API_KEY
   ```
2. Додай умову: якщо завтра сонячно → перемкнутись в режим ВІЙНА
3. Якщо хмарно → економ-режим

### 💡 Як автоматично вмикати нічну зарядку?
Додай **Schedule Trigger** на 00:00:

```javascript
// Перевірити ціну електрики
if (currentHour >= 0 && currentHour < 6) {
  // Увімкнути заряд 80А від мережі
  // (потрібно API для керування інвертором)
}
```

---

## Корисні команди

### Перевірити webhook Telegram:
```bash
curl https://api.telegram.org/bot8136712370:AAEdVYxRzzBYoUDuTwC68cW2fNA4rtSCC0c/getWebhookInfo
```

### Видалити webhook:
```bash
curl https://api.telegram.org/bot8136712370:AAEdVYxRzzBYoUDuTwC68cW2fNA4rtSCC0c/deleteWebhook
```

### Отримати список оновлень (тестування):
```bash
curl https://api.telegram.org/bot8136712370:AAEdVYxRzzBYoUDuTwC68cW2fNA4rtSCC0c/getUpdates
```

### Протестувати Growatt Login:
```bash
curl -X POST https://server.growatt.com/loginApi.do \
  -H "Content-Type: application/json" \
  -d '{"userName":"твій_логін","password":"твій_пароль"}'
```

---

## 🆘 Все ще не працює?

1. **Перевір логи** в n8n (Executions → клік на виконання)
2. **Подивись помилку** — там буде деталі
3. **Перевір всі кроки** в SETUP_GUIDE_UK.md
4. **Перезапусти workflow** (Inactive → Active)
5. **Перезавантаж n8n** (якщо self-hosted)

---

## 📚 Корисні посилання

- **n8n Docs**: https://docs.n8n.io
- **Telegram Bot API**: https://core.telegram.org/bots/api
- **Growatt Server**: https://server.growatt.com
- **QuickChart (графіки)**: https://quickchart.io
- **MD5 Generator**: https://www.md5hashgenerator.com

---

**Тримайся! 🇺🇦⚡️**

# 🔧 Швидке виправлення твого workflow

## Що було виправлено:

### ✅ 1. Додано інлайн-кнопки до повідомлення
У вузлі **"Telegram + Кнопки"** тепер є 4 ряди кнопок:

```
[📊 Графік 24г] [📈 Графік 7д]
[⚔️ ВІЙНА] [🕊️ МИР]
[⚡️ Турбо-заряд] [🌙 Нічна зарядка]
[🔄 Оновити] [ℹ️ Інфо]
```

**Параметри що додав:**
- `parseMode: "Markdown"` — для форматування тексту
- `replyMarkup: "inlineKeyboard"` — тип клавіатури
- `inlineKeyboard.rows` — масив рядків з кнопками

### ✅ 2. Виправлено відправку графіків
У вузлі **"Відправити Графік"** додано:
- `file: "={{$json["chartUrl"]}}"` — відправка зображення
- `parseMode: "Markdown"` — форматування підпису

### ✅ 3. Додано Markdown до всіх повідомлень
Всі Telegram вузли тепер мають `parseMode: "Markdown"`:
- ✅ Telegram + Кнопки
- ✅ Тривога
- ✅ Повна зарядка
- ✅ Встановити ВІЙНА
- ✅ Встановити МИР
- ✅ Відправити Графік
- ✅ Відправити результат

### ✅ 4. Уніфіковано credentials
Всі вузли тепер використовують credential **"growatt"** (ID: `z1jYHVQoTTIDPNYE`)

---

## 🚀 Як використати виправлений workflow:

### Варіант 1: Імпортувати новий файл (РЕКОМЕНДУЮ)

1. **Експортуй поточний workflow** (на всяк випадок):
   - Відкрий workflow в n8n
   - ⋮ (три крапки) → **Download** → збережи як backup

2. **Видали поточний workflow** або створи новий

3. **Імпортуй виправлений файл**:
   - Workflows → **+ Add workflow**
   - ⋮ → **Import from File**
   - Вибери: `growatt-workflow-FIXED.json`

4. **Активуй workflow**

---

### Варіант 2: Виправити вручну (якщо не хочеш імпортувати)

#### Крок 1: Додати інлайн-кнопки до "Telegram + Кнопки"

1. Відкрий вузол **"Telegram + Кнопки"**
2. В **Additional Fields** додай:
   - **Parse Mode** → `Markdown`
   - **Reply Markup** → `Inline Keyboard`
3. Натисни **Add Row** 4 рази і додай кнопки:

**Ряд 1:**
- Button 1: Text = `📊 Графік 24г`, Callback Data = `graph24`
- Button 2: Text = `📈 Графік 7д`, Callback Data = `graph7d`

**Ряд 2:**
- Button 1: Text = `⚔️ ВІЙНА`, Callback Data = `mode_war`
- Button 2: Text = `🕊️ МИР`, Callback Data = `mode_peace`

**Ряд 3:**
- Button 1: Text = `⚡️ Турбо-заряд`, Callback Data = `charge_turbo`
- Button 2: Text = `🌙 Нічна зарядка`, Callback Data = `charge_night`

**Ряд 4:**
- Button 1: Text = `🔄 Оновити`, Callback Data = `refresh`
- Button 2: Text = `ℹ️ Інфо`, Callback Data = `info`

4. Натисни **Save**

---

#### Крок 2: Виправити "Відправити Графік"

1. Відкрий вузол **"Відправити Графік"**
2. В **Additional Fields** додай:
   - **Parse Mode** → `Markdown`
   - **File** → `={{$json["chartUrl"]}}`
3. Натисни **Save**

---

#### Крок 3: Додати Markdown до інших вузлів

Для кожного Telegram вузла (Тривога, Повна зарядка, Встановити ВІЙНА, Встановити МИР):

1. Відкрий вузол
2. В **Additional Fields** → **Parse Mode** → `Markdown`
3. Натисни **Save**

---

#### Крок 4: Налаштувати webhook для кнопок

1. Відкрий вузол **"Webhook (Кнопки)"**
2. Скопіюй **Webhook URL** (наприклад: `https://твій-n8n.com/webhook/growatt-callback`)
3. Відкрий термінал та виконай:

```bash
curl -X POST "https://api.telegram.org/bot8136712370:AAEdVYxRzzBYoUDuTwC68cW2fNA4rtSCC0c/setWebhook" \
-H "Content-Type: application/json" \
-d '{"url": "https://твій-n8n.com/webhook/growatt-callback"}'
```

4. Маєш отримати:
```json
{"ok":true,"result":true,"description":"Webhook was set"}
```

---

## 🧪 Перевірка

### 1. Тест тригера (Telegram Trigger)
1. Відкрий Telegram
2. Знайди свого бота (або напиши `/start`)
3. Напиши будь-яке повідомлення
4. Маєш отримати повідомлення з результатом тесту

### 2. Тест автоматичного моніторингу (Schedule Trigger)
1. Активуй workflow
2. Через 5 хвилин отримаєш повідомлення з **кнопками**
3. Клікни на будь-яку кнопку — має спрацювати відповідний обробник

---

## ❓ FAQ

### Кнопки не з'являються?
- Перевір, що додав `replyMarkup: "inlineKeyboard"` в Additional Fields
- Перевір, що є хоча б одна кнопка в `rows`
- Збережи та перезапусти workflow

### Кнопки є, але не працюють?
- Перевір webhook:
  ```bash
  curl https://api.telegram.org/bot8136712370:AAEdVYxRzzBYoUDuTwC68cW2fNA4rtSCC0c/getWebhookInfo
  ```
- Маєш побачити свій URL від n8n
- Якщо webhook порожній — виконай `setWebhook` знову (див. Крок 4)

### Графіки не відправляються?
- Перевір, що додав `file: "={{$json["chartUrl"]}}"` в Additional Fields
- Перевір URL графіку в логах виконання (має починатися з `https://quickchart.io`)

### Помилка "Invalid parseMode"?
- Переконайся, що `parseMode` написано з великої літери `M`: `Markdown` (не `markdown`)

---

## 🎉 Готово!

Тепер твій бот має:
- ✅ Інлайн-кнопки
- ✅ Графіки (відправляються як зображення)
- ✅ Markdown форматування
- ✅ Автоматичний моніторинг кожні 5 хв
- ✅ Тести через Telegram Trigger

**Слава Україні! 🇺🇦⚡️**

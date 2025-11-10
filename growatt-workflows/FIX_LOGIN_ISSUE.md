# 🔧 Виправлення проблеми з логіном Growatt

## Проблема:
Growatt API повертає HTML сторінку замість JSON з токеном.

## Рішення:

### Варіант 1: Виправити HTTP Request вузол

**Відкрий вузол "Growatt Login" і налаштуй:**

#### 1. Basic Settings:
```
URL: https://server.growatt.com/loginApi.do
Method: POST
Authentication: None
```

#### 2. Send Body:
```
✅ Send Body: ON
Body Content Type: JSON
Specify Body: Using JSON
```

#### 3. JSON Body:
```json
{
  "userName": "bagnet.vet@gmail.com",
  "password": "qawsed2010"
}
```

#### 4. Headers (Options → Add Headers):
```
Header 1:
  Name: Content-Type
  Value: application/json

Header 2:
  Name: Accept
  Value: application/json
```

---

### Варіант 2: Спробувати MD5 пароль

#### Крок 1: Отримати MD5 хеш

**Онлайн:** https://www.md5hashgenerator.com/
- Введи: `qawsed2010`
- Результат: скопіюй хеш

**Термінал:**
```bash
echo -n "qawsed2010" | md5sum
```

#### Крок 2: Використати в JSON Body
```json
{
  "userName": "bagnet.vet@gmail.com",
  "password": "ТУТ_MD5_ХЕШ"
}
```

---

### Варіант 3: Альтернативний API endpoint

Спробуй змінити URL на:
```
https://server.growatt.com/newLoginAPI.do
```

Або:
```
https://openapi.growatt.com/v1/login
```

---

## 🧪 Тест після виправлення

### Очікуваний успішний результат:

```json
{
  "result": 1,
  "data": {
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
    "userId": 123456,
    "userName": "bagnet.vet@gmail.com"
  },
  "msg": "OK"
}
```

### Якщо отримуєш це — логін пройшов успішно! ✅

---

## 📸 Як має виглядати в n8n:

```
Вузол: Growatt Login
├─ URL: https://server.growatt.com/loginApi.do
├─ Method: POST
├─ Authentication: None
├─ Send Body: ✅
├─ Body Content Type: JSON
├─ JSON Body:
│  {
│    "userName": "bagnet.vet@gmail.com",
│    "password": "qawsed2010"
│  }
└─ Headers:
   ├─ Content-Type: application/json
   └─ Accept: application/json
```

---

## ❓ Все ще не працює?

### Спробуй через curl в терміналі:

```bash
# Без MD5
curl -X POST "https://server.growatt.com/loginApi.do" \
-H "Content-Type: application/json" \
-H "Accept: application/json" \
-d '{"userName":"bagnet.vet@gmail.com","password":"qawsed2010"}'
```

### Якщо це працює — скопіюй точно так само в n8n

### Якщо і це не працює — треба MD5:

```bash
# З MD5 (спочатку отримай хеш)
MD5_PASS=$(echo -n "qawsed2010" | md5sum | awk '{print $1}')
echo "MD5 Hash: $MD5_PASS"

curl -X POST "https://server.growatt.com/loginApi.do" \
-H "Content-Type: application/json" \
-H "Accept: application/json" \
-d "{\"userName\":\"bagnet.vet@gmail.com\",\"password\":\"$MD5_PASS\"}"
```

---

## 🔐 Перевірка облікових даних

1. Відкрий https://server.growatt.com
2. Спробуй увійти з:
   - Email: `bagnet.vet@gmail.com`
   - Пароль: `qawsed2010`
3. Якщо не працює — треба виправити credentials
4. Якщо працює — значить проблема в API запиті

---

## 📞 Потрібна допомога?

Надішли мені:
1. Результат curl команди (вище)
2. Чи працює логін на сайті growatt.com
3. Скріншот налаштувань вузла "Growatt Login"

Виправимо разом! 💪🇺🇦

# 🏛️ KOSONSOY ABU ALI IBN SINO NOMIDAGI JAMOAT SALOMATLIGI TEXNIKUMI
### 📍 Namangan viloyati · Kosonsoy tumani

> **Namangan viloyati Kosonsoy Abu Ali ibn Sino nomidagi Jamoat salomatligi texnikumi rasmiy ta'lim portali, to'liq boshqariladigan ma'muriy boshqaruv tizimi (Admin Dashboard) va RESTful API platformasi.**

Ushbu platforma zamonaviy universitet va ilg'or davlat ta'lim muassasalari talablari darajasida, toza arxitektura (**Custom OOP MVC Architecture**), maksimal tezlik, qat'iy kiberxavfsizlik va boy funksionallik bilan noldan ishlab chiqilgan.

---

## 📌 1. TEXNOLOGIYALAR STEKI

### ⚙️ Backend
- **PHP 8.1+ / 8.3+ (Native OOP MVC):** Hech qanday og'ir freymvorklarsiz (Laravel, Symfony ishlatilmagan), toza va yengil MVC arxitekturasi.
- **MySQL 8.0+ / 5.7+:** 26 ta to'liq normallashtirilgan munosabatli (relational) jadvallar, Foreign Keys, indekslar va `utf8mb4_unicode_ci` kodirovkasi.
- **mysqli (Prepared Statements):** PDO ishlatilmagan; barcha SQL so'rovlari 100% parametrlangan `mysqli` tayyorlangan so'rovlari orqali bajariladi (SQL Injection himoyasi).
- **RESTful API v1:** `/api/v1/` prefiksi ostida JSON formatidagi to'liq ma'lumot almashinuvi.
- **PHP Session Auth & RBAC:** Xavfsiz sessiya mexanizmi (`HttpOnly`, `SameSite=Lax`, Session Regeneration) va dinamik rollar/ruxsatlar tizimi.
- **Timezone:** `Asia/Tashkent`.

### 🎨 Frontend
- **HTML5 & CSS3:** Semantik teglash, maxsus Design System (`#0B2545` Chuqur to'q ko'k, `#134074`, `#F59E0B` Oltin rang).
- **Bootstrap 5.3 (CDN):** Responsive grid, yagona zamonaviy dizayn tizimi, mobil va planshet moslashuvchanligi.
- **Bootstrap Icons (CDN):** Yengil vektor piktogrammalar.
- **Vue.js 3 (Global CDN Build):** Node.js, Vite yoki Webpack talab qilinmaydi! Vue 3 CDN orqali Virtual Qabulxona holatini dinamik tekshirish va interaktiv filtrlar uchun ishlatilgan.
- **Fetch API / AJAX:** Asinxron ma'lumot yuklash va sahifani qayta yuklamasdan murojaat holatini tekshirish.

---

## 🚀 2. O'RNATISH VA SOZLASH (INSTALLATION)

### 2.1. Tizim talablari
- Web Server: Apache 2.4+ (mod_rewrite yoqilgan) yoki Nginx
- PHP: 8.0 / 8.1 / 8.2 / 8.3+ (kengaytmalar: `mysqli`, `curl`, `mbstring`, `fileinfo`, `gd`, `openssl`)
- MySQL: 5.7+ yoki MySQL 8.0+ / MariaDB 10.4+

### 2.2. OpenServer (OSPanel) da ishga tushirish
1. Loyiha papkasini `c:\OSPanel\domains\kosonsoyjst` katalogiga joylashtiring.
2. Windows `hosts` fayliga (`C:\Windows\System32\drivers\etc\hosts`) quyidagi qator mavjudligiga ishonch hosil qiling:
   ```text
   127.0.0.1 kosonsoyjst
   ```
3. OpenServer sozlamalarida PHP versiyasini **PHP 8.1** yoki **PHP 8.0**, HTTP modulini **Apache_2.4-PHP_8.0-8.1+Nginx_1.23** yoki PHP o'rnatilgan serverni tanlang.
4. MySQL ma'lumotlar bazasiga `database/database.sql` va `database/seed.sql` skriptlarini import qiling:
   ```bash
   mysql -u root -p kosonsoyjst < database/database.sql
   mysql -u root -p kosonsoyjst < database/seed.sql
   ```
5. `.env` faylida ulanish parametrlarini tekshiring:
   ```ini
   APP_ENV=development
   APP_DEBUG=true
   APP_URL=http://kosonsoyjst
   TIMEZONE=Asia/Tashkent

   DB_HOST=127.0.0.1
   DB_PORT=3306
   DB_DATABASE=kosonsoyjst
   DB_USERNAME=root
   DB_PASSWORD=
   ```

### 2.3. cPanel yoki Linux Hostingga Deploy Qilish
1. **Fayllarni yuklash:**
   - Xavfsizlik yuzasidan barcha loyiha fayllarini hostingdagi `public_html` dan bir pog'ona yuqoriga (masalan: `/home/username/kosonsoyjst`) joylashtiring.
   - `public` papkasi ichidagi barcha fayllarni (`assets`, `uploads`, `index.php`, `.htaccess`, `robots.txt`, `sitemap.xml`) bevosita `/home/username/public_html` ichiga ko'chiring.
   - `public_html/index.php` faylidagi `ROOT_DIR` yo'lini sozlang:
     ```php
     define('ROOT_DIR', dirname(__DIR__) . '/kosonsoyjst');
     define('PUBLIC_DIR', __DIR__);
     ```
2. **Katalog huquqlari (Permissions):**
   - `storage/logs`, `storage/cache`, `public/uploads` kataloglariga `775` yoki `755` yozish huquqini bering.
3. **Ma'lumotlar bazasi:**
   - cPanel orqali yangi MySQL baza va foydalanuvchi yarating.
   - phpMyAdmin orqali `database/database.sql` va `database/seed.sql` ni import qiling.
   - `.env` faylini hosting parametrlari bilan to'ldiring.

---

## 🔐 3. FOYDALANUVCHILAR VA XAVFSIZLIK

### 3.1. Standart Admin hisoblari (Boshlang'ich ma'lumotlar)

| Login (Username) | Standart Parol | Roli | Huquqlari |
| :--- | :--- | :--- | :--- |
| **admin** | `admin123` | **SUPER ADMIN** | Barcha modullarni to'liq nazorat qilish, rollar, sozlamalar |
| **editor** | `editor123` | **EDITOR** | Yangiliklar, sahifalar, galereya va media boshqaruvi |
| **moderator** | `moderator123` | **MODERATOR** | Virtual qabulxona murojaatlari va vakansiya arizalari |

> ⚠️ **Muhim:** Tizimni ishlab chiqarishga (Production) topshirishdan oldin admin parollarini Admin Paneldagi "Profil" bo'limi orqali o'zgartiring!

### 3.2. Kiberxavfsizlik kafolatlari
- **SQL Injection Protection:** 100% Prepared Statements (`mysqli->prepare`). Xom SQL ulanmalari mutlaqo cheklangan.
- **CSRF Protection:** Barcha `POST`, `PUT`, `DELETE` so'rovlarida yashirin `csrf_token` tekshiriladi.
- **XSS Protection:** Barcha chiqish ma'lumotlari `e()` (htmlspecialchars UTF-8) orqali tozalanadi.
- **Secure File Storage:** Yuklangan har bir faylning MIME turi (`mime_content_type`), kengaytmasi va hajmi tekshiriladi. Fayl nomi unikal xeshlanadi. `public/uploads/.htaccess` skriptlarni (`.php`, `.phtml`, `.cgi`) to'g'ridan-to'g'ri ijro etilishini to'sib qo'yadi.
- **Secure Sessions:** Cookie parametrlari: `HttpOnly=true`, `SameSite=Lax`, `use_strict_mode=1`.
- **Security Headers:** `X-Frame-Options: SAMEORIGIN`, `X-Content-Type-Options: nosniff`, `X-XSS-Protection: 1; mode=block`.
- **Audit Logging:** Har bir avtorizatsiya, yaratish, o'zgartirish va o'chirish harakati `audit_logs` jadvalida foydalanuvchi ID, IP-manzili va brauzer ma'lumotlari bilan saqlanadi.

---

## 🌐 4. FOYDALANUVCHI INTERFEYSI VA SAHIFALAR

1. **Bosh sahifa (`/`)**:
   - Hero banner slayd-shousi (tezkor tugmalar va murojaat havolasi)
   - Kollej haqida qisqacha ma'lumot va direktor murojaati bloki
   - So'nggi yangiliklar (News cards) va Muhim e'lonlar lentasi
   - Ta'lim yo'nalishlari kartochkalari
   - Dinamik statistika (Jonli animatsiyali raqamlar: talabalar, o'qituvchilar, yo'nalishlar, grantlar)
   - Kollej rahbariyati bilan tanishuv
   - Fotogalereya bloklari
   - Hamkor tashkilotlar karuseli
   - Rasmiy hujjatlar yuklab olish havolalari
   - Professional ko'p funksiyali Footer
2. **Yangiliklar (`/news`, `/news/{slug}`)**:
   - Katta Featured News qismi
   - Kategoriyalar bo'yicha saralash
   - Qidiruv va Pagination
   - Yangilik batafsil sahifasi: asosiy rasm, qo'shimcha fotogalereya, ko'rishlar hisoblagichi, ijtimoiy tarmoqlarda ulashish (Telegram, Facebook, Twitter, LinkedIn), tegishli yangiliklar.
3. **Rahbariyat (`/management`)**:
   - Direktor, direktor o'rinbosarlari, bo'lim boshliqlari va o'qituvchilar. Qabul kunlari, telefon, email va biografiya.
4. **Statistika (`/statistics`)**:
   - Kollejning asosiy faoliyat ko'rsatkichlari, o'quvchilar kontingenti, bandlik ko'rsatkichlari.
5. **Vakansiyalar (`/vacancies`, `/vacancies/{id}`)**:
   - Ochiq ish o'rinlari, talablar, ish haqi, vazifalar.
   - Onlayn ariza topshirish va CV (PDF/DOCX) yuklash formasi.
6. **Virtual Qabulxona (`/reception`, `/reception/check`)**:
   - Online murojaat jo'natish: F.I.Sh., telefon, email, murojaat turi, mavzu, matn, fayl biriktirish.
   - Matematik anti-spam CAPTCHA.
   - Unikal kuzatuv kodi (`KK-2026-XXXXX`).
   - Murojaat holatini tekshirish sahifasi (Vue 3 va REST API orqali bir zumda holat va admin javobini ko'rsatish).
7. **Biz haqimizda (`/about`)**:
   - Kollej tarixi, missiyasi, ta'lim jarayoni, interaktiv xarita, aloqa ma'lumotlari.
8. **Rasmiy Hujjatlar (`/documents`)**:
   - Nizomlar, litsenziyalar, davlat standartlari, PDF yuklab olish.
9. **Fotogalereya (`/gallery`)**:
   - Kollej tadbirlari va binolari bo'yicha albomlar.

---

## ⚡ 5. PROFESSIONAL GLOBAL LOADER TIZIMI

Saytda foydalanuvchi tajribasini (UX) oshirish uchun 6 xil loader tizimi joriy qilingan:
1. **Initial Page Loader (`#page-loader`):** Sahifa birinchi ochilganda brend emblemasi va progress spinner ko'rinadi va sahifa to'liq yuklangach silliq yo'qoladi (`fade-out`).
2. **Top Progress Bar (`#top-progress-bar`):** Sahifalar o'rtasida navigatsiya va AJAX/Fetch so'rovlarida tepada YouTube uslubidagi progress chiziq harakatlanadi.
3. **Button Loading State (`.btn-loader`):** Har qanday form submit tugmasi bosilganda tugma ichida avtomatik aylanuvchi spinner paydo bo'ladi va tugma bosilishi vaqtincha bloklanadi (takroriy yuborishdan himoya).
4. **Skeleton Loading (`.skeleton-card`, `.skeleton-line`):** Ma'lumotlar yuklanishi kutilayotganda zamonaviy pulsatsiyalanuvchi joy ushlagichlar.
5. **Vue 3 Dynamic Checker Loader:** Virtual qabulxona kodi kiritilib tekshirilganda kartochka ichida toza animatsiya ishlaydi.
6. **Error & Timeout Fallback:** Agar tarmoq juda sekin bo'lsa yoki xatolik yuz bersa, loader sahifani to'sib qo'ymasligi uchun 8 soniyalik xavfsizlik taymeri bilan majburiy ochib yuboriladi.

---

## 🛠️ 6. ADMIN PANEL VA 20 TA CRUD MODULLARI

Kirish manzili: `http://kosonsoyjst/admin/login`

1. **Dashboard (`/admin`):**
   - Yangi murojaatlar, yangiliklar soni, ochiq vakansiyalar, bugungi arizalar ko'rsatkichlari.
   - Tezkor amallar tugmalari, so'nggi murojaatlar va so'nggi tizim audit jurnali.
2. **Yangiliklar (`/admin/news`):**
   - Yangilik yaratish, tahrirlash, o'chirish, Rich Text Editor, ko'p rasmli galereya yuklash, SEO sozlamalari (Slug, Meta Title, Meta Description), Status (Draft/Published/Archived), Featured belgisi.
3. **Kategoriyalar (`/admin/categories`):**
   - Yangilik toifalari, slug va faollik holati.
4. **Rahbariyat (`/admin/management`):**
   - Lavozim, biografiya, qabul vaqti, tartib raqami.
5. **Xodimlar (`/admin/employees`):**
   - O'qituvchilar, kafedra mudirlari, mutaxassisliklari.
6. **Statistika (`/admin/statistics`):**
   - Bosh sahifa va statistika sahifasidagi ko'rsatkichlar, piktogrammalar va tartib.
7. **Vakansiyalar (`/admin/vacancies`):**
   - Bo'sh ish o'rinlari, talablar, maosh, muddat.
8. **Vakansiya arizalari (`/admin/applications`):**
   - Nomzodlar ro'yxati, CV fayllarini yuklab olish, status o'zgartirish (NEW, REVIEWING, ACCEPTED, REJECTED), Excel/CSV eksport.
9. **Virtual Qabulxona (`/admin/messages`):**
   - Kelib tushgan murojaatlar, holatni boshqarish (NEW, IN_PROGRESS, ANSWERED, CLOSED), biriktirilgan fayllarni ko'rish, rasmiy javob matnini yozish va saqlash.
10. **Sahifalar (`/admin/pages`):**
    - Statik va qo'shimcha sahifalar (Slug, kontent, SEO).
11. **Menyu boshqaruvi (`/admin/menus`):**
    - Sayt yuqori va pastki menyularini dinamik boshqarish, havola va tartibini o'zgartirish.
12. **Bannerlar (`/admin/banners`):**
    - Bosh sahifa slayd-shousi, sarlavhalar, tugma matni va havolalari.
13. **Fotogalereya (`/admin/gallery`):**
    - Albomlar yaratish va albomlarga bir vaqtning o'zida ko'plab rasmlar biriktirish.
14. **Hujjatlar (`/admin/documents`):**
    - Rasmiy me'yoriy hujjatlar, buyruqlar, PDF fayllarni biriktirish va toifalash.
15. **Hamkorlar (`/admin/partners`):**
    - Hamkor tashkilotlar logotiplari va rasmiy veb-sayt havolalari.
16. **Media Menejeri (`/admin/media`):**
    - Serverga yuklangan barcha rasmlar va hujjatlar kutubxonasi, to'g'ridan-to'g'ri havolani nusxalash.
17. **Foydalanuvchilar (`/admin/users`):**
    - Administratorlar, muharrirlar va moderatorlar hisoblarini boshqarish, bloklash/faollashtirish.
18. **Rollar va Ruxsatlar (`/admin/roles`):**
    - Rollarga modullar bo'yicha ruxsatlarni (permissions) dinamik belgilash.
19. **Sayt sozlamalari (`/admin/settings`):**
    - Kollej nomi, telefon, ishonch telefoni, manzil, ish vaqti, email, ijtimoiy tarmoqlar (Telegram, Instagram, Facebook, YouTube), Google Maps koordinatalari.
20. **Audit jurnali (`/admin/audit-logs`):**
    - Tizimda kim, qachon, qaysi IP-manzildan qanday amal bajarganligining to'liq nazorat daftari.
21. **Profil va Parolni yangilash (`/admin/profile`):**
    - Joriy foydalanuvchi ma'lumotlari va parolini xavfsiz almashtirish.

---

## 📡 7. REST API v1 HUJJATLARI

API bazaviy manzili: `http://kosonsoyjst/api/v1/`

Barcha javoblar standart JSON formatida qaytadi:
```json
{
  "success": true,
  "message": "Operatsiya muvaffaqiyatli",
  "data": { ... }
}
```

### Asosiy Endpointlar:

| Metod | Endpoint | Tavsif | Parametrlar |
| :--- | :--- | :--- | :--- |
| `GET` | `/api/v1/news` | Yangiliklar ro'yxati | `page`, `per_page`, `category_id`, `q` |
| `GET` | `/api/v1/news/{slug}` | Yangilik batafsil | `slug` URL parametri |
| `GET` | `/api/v1/categories` | Yangilik toifalari | - |
| `GET` | `/api/v1/vacancies` | Ochiq vakansiyalar | `page`, `per_page`, `q` |
| `GET` | `/api/v1/vacancies/{id}` | Vakansiya batafsil | `id` parametri |
| `GET` | `/api/v1/statistics` | Dinamik statistika | - |
| `GET` | `/api/v1/inquiry/status` | Murojaat holati | `code=KK-2026-XXXXX` |
| `POST` | `/api/v1/inquiry/submit` | Murojaat yuborish | `full_name`, `phone`, `email`, `subject`, `message`, `type` |

---

## 🌍 8. KO'P TILLILIK TIZIMI (MULTI-LANGUAGE)

Loyiha to'liq ko'p tillilik arxitekturasiga ega:
- `resources/lang/uz.php` (O'zbek tili - standart)
- `resources/lang/ru.php` (Rus tili)
- `resources/lang/en.php` (Ingliz tili)

Foydalanuvchi yuqori paneldagi til tugmasi orqali tilni almashtirishi mumkin (`/lang/uz`, `/lang/ru`, `/lang/en`). Til sessiyada xavfsiz saqlanadi va sayt bo'ylab `trans('key')` yoki `t('key')` yordamchi funksiyalari orqali avtomatik chiqariladi.

---

## 🤖 9. TELEGRAM INTEGRATSIYASI

Yangi murojaat yoki vakansiya arizasi tushganda mas'ul xodimlarga zudlik bilan Telegram orqali xabar yuborish imkoniyati mavjud.
Sozlash uchun `.env` fayliga quyidagi parametrlarni kiriting:
```ini
TELEGRAM_BOT_TOKEN="123456789:ABCdefGhIJKlmNoPQRsTUVwxyZ"
TELEGRAM_CHAT_ID="-1001234567890"
TELEGRAM_NOTIFICATIONS_ENABLED=true
```
Agar bot token kiritilmasa, tizim xatoliksiz oddiy rejimda ishlashda davom etadi.

---

## 📂 10. LOYIHA TUZILISHI (PROJECT STRUCTURE)

```text
c:\OSPanel\domains\kosonsoyjst\
│
├── .env                  # Muhit sozlamalari (Maxfiy)
├── .env.example          # Namuna muhit sozlamalari
├── .htaccess             # Root xavfsiz yo'naltiruvchi
├── README.md             # Loyiha to'liq hujjatlari
│
├── config/               # Tizim konfiguratsiya fayllari
│   ├── app.php
│   ├── database.php
│   └── telegram.php
│
├── core/                 # Maxsus MVC Framework yadrosi (Custom OOP Engine)
│   ├── App.php           # Ilova ishga tushiruvchi
│   ├── AuditLog.php      # Audit monitoring
│   ├── Auth.php          # Autentifikatsiya va RBAC
│   ├── Controller.php    # Asosiy Controller
│   ├── CSRF.php          # CSRF himoya
│   ├── Database.php      # MySQLi Singleton Wrapper
│   ├── Env.php           # .env fayl o'quvchi
│   ├── Model.php         # Asosiy Model (CRUD, Pagination, Soft delete)
│   ├── Request.php       # HTTP so'rovlar menejeri
│   ├── Response.php      # HTTP javoblar menejeri (JSON, redirects)
│   ├── Router.php        # Regex Route Dispatcher & Middlewares
│   ├── Session.php       # Xavfsiz sessiyalar
│   ├── Validator.php     # Formalarni tekshirish
│   └── View.php          # Shablonlar va Layout render
│
├── controllers/          # Foydalanuvchi Controllerlari
│   ├── admin/            # 21 ta Admin Controllerlari
│   └── ...
│
├── models/               # 19 ta Ma'lumotlar Modellari
├── services/             # Telegram va Upload xizmatlari
├── middleware/           # Oraliq qatlamlar
├── helpers/              # Global yordamchi funksiyalar
├── routes/               # Marshrutlar (web.php va api.php)
├── resources/lang/       # Ko'p tillilik lug'atlari (uz, ru, en)
│
├── views/                # Ko'rinishlar (UI Templates)
│   ├── layouts/          # main, admin, header, footer, loader
│   ├── home/
│   ├── news/
│   ├── management/
│   ├── statistics/
│   ├── vacancies/
│   ├── reception/
│   ├── about/
│   ├── documents/
│   ├── gallery/
│   ├── admin/            # 20 ta modul uchun to'liq Admin shablonlari
│   └── errors/           # 403, 404, 500 xatolik sahifalari
│
├── public/               # Web Document Root
│   ├── assets/           # CSS, JS, rasmlar, ikonlar
│   ├── uploads/          # Yuklangan hujjat va media fayllar
│   ├── .htaccess         # URL qayta yozish va xavfsizlik
│   ├── index.php         # Front Controller
│   ├── robots.txt        # Qidiruv tizimlari qoidalari
│   └── sitemap.xml       # SEO Sayt xaritasi
│
├── storage/              # Kesh va log fayllar
│   ├── cache/
│   └── logs/
│
└── database/             # Ma'lumotlar bazasi
    ├── database.sql      # 26 ta jadvallar strukturasi
    └── seed.sql          # Dastlabki to'liq to'ldirilgan ma'lumotlar
```

---

## 👨‍💻 ISHLAB CHIQUVCHI
* **Muassasa:** Namangan viloyati Kosonsoy tumani, Kosonsoy Abu Ali ibn Sino nomidagi Jamoat salomatligi texnikumi
* **Loyiha:** Rasmiy veb-portali, Admin Dashboard va RESTful API
* **Muallif:** Senior Full-Stack Developer, Software Architect, UI/UX Designer & Cybersecurity Engineer
* **Litsenziya:** Barcha huquqlar himoyalangan © 2026 Kosonsoy Abu Ali ibn Sino nomidagi JST.


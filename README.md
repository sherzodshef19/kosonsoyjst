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

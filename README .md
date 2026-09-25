# ⚽ FIFA World Cup 2026 — Player & Match Performance Analysis

Excel (pivot table & dashboard) va Python (pandas, matplotlib) yordamida FIFA Jahon chempionati 2026 o'yinchilari va o'yinlari statistikasi bo'yicha to'liq tahlil.

---

## 📊 Dataset haqida

> ℹ️ **Eslatma:** Ushbu dataset **rasmiy FIFA statistikasi emas** — u faqat ta'lim va tahlil ko'nikmalarini mashq qilish maqsadida sun'iy (fictional/synthetic) tarzda yaratilgan. Jamoa, o'yinchi nomlari va ko'rsatkichlar haqiqiy 2026-yilgi FIFA Jahon chempionati natijalarini aks ettirmaydi.

Dataset 2026-yilgi FIFA Jahon chempionatida ishtirok etgan o'yinchilarning har bir o'yindagi individual statistikasini o'z ichiga oladi — gollar, assistlar, pas aniqligi, reyting, bozor qiymati va boshqa 70 dan ortiq ko'rsatkich.

| Ko'rsatkich | Qiymat |
|---|---|
| Jami qatorlar (xom holatda) | 55,600 |
| Tozalangandan keyin (dublikat va bo'sh qatorlarsiz) | 54,600 |
| Ustunlar soni | 77 |
| Jamoalar soni | 48 |
| O'yinchilar soni | 1,245 |
| O'yinlar soni | 1,050 |
| Turnir bosqichlari | Group Stage, Round of 32, Round of 16, Quarter Finals, Semi Finals, Third Place Match, Final |
| Pozitsiyalar | Defender, Midfielder, Forward, Goalkeeper |

**Asosiy ustun guruhlari:**
- **O'yinchi ma'lumotlari:** `player_name`, `age`, `nationality`, `team`, `position`, `market_value_eur`
- **O'yin ma'lumotlari:** `match_id`, `match_date`, `stadium`, `tournament_stage`, `match_result`
- **Hujum ko'rsatkichlari:** `goals`, `assists`, `shots`, `expected_goals_xg`, `dribbles_attempted`
- **Himoya ko'rsatkichlari:** `tackles`, `interceptions`, `clearances`, `blocks`
- **Umumiy baholash:** `player_rating`, `performance_score`, `pass_accuracy`, `save_percentage`

> ⚠️ **Ma'lumot sifati bo'yicha izoh:** dataset tarkibida ~1,000 ta qator asosiy ustunlarda (`team`, `position`, `tournament_stage` va h.k.) bo'sh qiymatga ega, shuningdek `player_id` + `match_id` juftligi bo'yicha 999 ta dublikat qator aniqlangan. Excel pivot table va Python `groupby`/`crosstab` bunday qatorlarni avtomatik hisobga olmaydi, shu sababli barcha tahlillarda **54,600 ta toza qator** asos qilib olingan.

---

## 🛠 Ishlatilgan vositalar

| Bosqich | Vosita |
|---|---|
| Ma'lumotni tozalash va tekshirish | Excel (bo'sh qiymat va dublikat tekshiruvi) |
| Pivot table tahlillar | Excel PivotTable |
| Interaktiv dashboard | Excel Dashboard + Slicer |
| Natijalarni tasdiqlash | Python — `pandas`, `numpy` |
| Vizualizatsiya | `matplotlib`, `seaborn` |

---

## 📁 Loyiha tuzilishi

```
├── Fifa.xlsx              # Excel fayl: xom ma'lumot, pivot table'lar, dashboard
├── Data_FIFA.csv           # Tozalangan xom ma'lumot (Python uchun)
├── Analiz.ipynb            # Python (pandas) tahlil notebooki
└── README.md               # Ushbu fayl
```

---

## 🔍 Tahlil bosqichlari

1. Ma'lumotni yuklash va tekshirish (`.info()`, `.describe()`, bo'sh/dublikat qatorlar)
2. Jamoalar bo'yicha gollar taqsimoti
3. Pozitsiyalar bo'yicha o'rtacha reyting va pas aniqligi
4. Turnir bosqichi va pozitsiya bo'yicha o'yinchilar taqsimoti
5. Jamoalarning o'rtacha bozor qiymati
6. Eng samarali bombardirlar (gol + assist)
7. Zarba samaradorligi (`goals / shots`) bo'yicha eng yaxshi jamoalar
8. Barcha natijalarni Excel pivot table'lar bilan solishtirish

---

## ✅ Asosiy 5 ta xulosa

1. **Qatar — turnirning eng natijali jamoasi.** Jamoalar bo'yicha gollar taqsimotida Qatar 95 ta gol bilan yetakchilik qiladi, undan keyin Netherlands (94) va Panama (90) joylashgan.

2. **Pozitsiyalar orasida reyting farqi katta.** Forward (3.88) va Midfielder (3.86) pozitsiyalaridagi o'yinchilar eng yuqori o'rtacha reytingga ega, Goalkeeper esa sezilarli darajada past (2.07) — bu goal'kiperlar boshqa mezonlar (saves, save_percentage) bo'yicha baholanishi bilan izohlanadi.

3. **Saudi Arabia — eng qimmat tarkibga ega jamoa.** O'rtacha bozor qiymati bo'yicha Saudi Arabia (≈33.8 mln €) barcha jamoalar orasida yetakchi, undan keyin Panama va Algeria keladi.

4. **Memphis Zerrouki — turnirning eng samarali bombardiri.** 24 ta gol va 9 ta assist bilan u boshqa barcha o'yinchilardan sezilarli darajada oldinda.

5. **England — zarbani golga eng yaxshi aylantiruvchi jamoa.** `goal_conversion_rate` (goals/shots) bo'yicha England 3.27% ko'rsatkich bilan yetakchi, undan keyin Ghana va Algeria joylashgan.

---

## 📌 Excel vs Python: natijalar mosligi

Barcha 6 ta pivot table (jamoalar bo'yicha gollar, pozitsiya reytingi, bosqich×pozitsiya, jamoa qiymati, bombardirlar, zarba samaradorligi) Excel va Python'da **aynan bir xil raqamlarni** ko'rsatdi — bu ikkala tahlil usulining to'g'ri va izchil bajarilganini tasdiqlaydi.

Ba'zi "Top 10" ro'yxatlarida Excelda 10 tadan ortiq qator (masalan 13–15 ta) chiqishi mumkin — bu Excelning "Top 10 Filter" funksiyasi teng qiymatga ega qatorlarning barchasini saqlab qolishidan kelib chiqadi, pandasning `.head(10)` esa qat'iy ravishda faqat 10 tasini oladi. Qiymatlarning o'zi ikkalasida ham bir xil.

---

## 👤 Muallif

Ushbu tahlil FIFA World Cup 2026 statistikasi asosida Excel va Python (pandas) yordamida tayyorlangan o'quv loyihasi doirasida amalga oshirildi.

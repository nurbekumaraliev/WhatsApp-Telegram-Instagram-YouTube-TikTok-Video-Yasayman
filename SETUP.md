# BOSH PROMPT — kompyuterni Claude uchun to'liq sozlash

Sen shu kompyuterda ishlayotgan Claude Code'san. Bu kompyuterni 100% Claude ishlatadi. Vazifa: shu repodagi hamma narsani QADAMMA-QADAM, AVTOMATIK o'rnatish va ulash.

## ASOSIY QOIDA — ISHNI SEN QILASAN

- Hamma ishni O'ZING bajar: dasturlarni yuklash va o'rnatish, fayllarni yaratish, brauzerda sahifalarni ochish va tugmalarni bosish, formalarni to'ldirish, konnektorlarda «Connect» ni bosish, ishga tushirish, tekshirish.
- Egaga «buni o'rnating», «buni sozlang», «shu tugmani toping», «shu buyruqni yozing» DEMA.
- Egasi FAQAT shularni qiladi:
  1. akkauntga kiradi — login, parol, SMS/ilova kodi, «Google bilan kirish»;
  2. «Ruxsat berish / Allow / Connect / Authorize» oynalarini bosadi va shartlarni (Terms) qabul qiladi;
  3. API kalitlarni sen tayyorlab ochgan faylga o'zi joylaydi (masalan Telegram api_id/api_hash);
  4. QR kodni telefonda skan qiladi;
  5. pul kerak bo'lsa — rejani o'zi tanlaydi va to'laydi.
- Parol, kod, API kalit, token va sessiya satrini HECH QACHON o'zing kiritma, so'rama, o'qima va chatga chiqarma.
- Kalitlar uchun usul: maydonlari BO'SH .env faylini o'zing yarat (faqat egasi o'qiy oladigan huquq bilan), uni matn muharririda och (Windows: notepad; macOS: open -e; Linux: xdg-open) va egaga ayt: «Ochilgan faylda X= dan keyin qiymatni qo'yib, saqlang». Keyin faqat maydon to'ldirilganini tekshir, qiymatni chiqarmasdan.
- Brauzer: ichki brauzer yoki Claude in Chrome bo'lsa — hammasini o'zing bos. Kirish sahifasida to'xta va egaga «kiring, keyin "bo'ldi" deng» de. Kalit ko'rsatilgan sahifa matnini o'qima. Brauzer vositasi bo'lmasa — aniq havola ber.
- Egasining aniq «ha»sisiz hech kimga xabar yuborma, hech narsa joylama, o'chirma, pul sarflama.
- Egaga oddiy, texnik bo'lmagan tilda, uning tilida yoz. Har bosqich boshida bir qatorda nima qilayotganingni ayt.
- OS'ni o'zing aniqla (Windows / macOS / Linux) va buyruqlarni moslashtir. Administrator (UAC/sudo) huquqi talab qiladigan yo'llardan QOCH — hammasini foydalanuvchi papkasiga o'rnat.

## BOSHLASHDAN OLDIN

- Bu repo hali kompyuterda bo'lmasa: `https://github.com/nurbekumaraliev/WhatsApp-Telegram-Instagram-YouTube-TikTok-Video-Yasayman/archive/refs/heads/main.tar.gz` ni `~/workspace/` ga yuklab och. Quyidagi `prompts/` va `skills/` yo'llari shu papkaga nisbatan.
- Foydalanuvchi faqat ayrim qismlarni so'ragan bo'lsa (masalan «faqat WhatsApp») — faqat o'sha qadam(lar)ni bajar; 1-qadamdan esa faqat kerakli dasturlarni o'rnat.
- Boshlashda foydalanuvchiga 2–3 qatorda ayt: nima o'rnatiladi, taxminan qancha vaqt oladi va undan nima so'raladi. Keyin darhol boshla.

## TARTIB

Har bir qadam uchun `prompts/` papkasidagi faylni o'qi va unga to'liq amal qil. Qadam tugagach `~/.claude-setup-holat.json` fayliga `{"qadam": "<nom>", "holat": "tayyor"}` yozib bor. Qayta ishga tushirilsa — tayyor qadamlarni o'tkazib yubor, qolganidan davom et.

| # | Fayl | Nima | Egasi nima qiladi |
|---|------|------|-------------------|
| 1 | `prompts/01_asosiy_dasturlar.md` | uv, Node.js, ffmpeg, Go, gh | hech narsa |
| 2 | `prompts/02_video_montaj.md` | video montaj skill'i | hech narsa |
| 3 | `prompts/03_vidiq.md` | vidIQ konnektori + YouTube va Instagram | vidIQ, Google, Instagram'ga kiradi, ruxsat beradi |
| 4 | `prompts/04_windsor.md` | Windsor.ai konnektori | Windsor'ga kiradi, tarmoqlarga ruxsat beradi |
| 5 | `prompts/05_postiz.md` | Postiz — 2 ta skill + CLI | Postiz'ga kiradi, API kalitni faylga qo'yadi, tarmoqlarni ulaydi |
| 6 | `prompts/06_telegram.md` | Telegram (shaxsiy akkaunt) | my.telegram.org'ga kiradi, api_id/api_hash'ni faylga qo'yadi, QR skan qiladi |
| 7 | `prompts/07_tiktok.md` | TikTok (Postiz orqali) | TikTok'ga kiradi, ruxsat beradi |
| 8 | `prompts/08_whatsapp.md` | WhatsApp (shaxsiy akkaunt) | QR skan qiladi, test xabarga ruxsat beradi |

- Qadamlar orasida egadan «davom etaymi?» deb so'rama — o'zing davom et. Faqat egasining ishi kerak bo'lganda to'xta.
- Biror qadam ishlamasa: sababini top va tuzat, boshqa usulni sina. Uddalay olmasang — o'sha qadamni «xato» deb belgila, keyingisiga o't va oxirida hisobot ber.
- Egasi biror xizmatni (masalan Postiz pullik bo'lsa) xohlamasa — o'tkazib yubor.
- Konnektorlar (vidIQ, Windsor) claude.ai akkauntiga ulanadi va YANGI sessiyada paydo bo'ladi. Ularni ulab bo'lgach egaga ayt: «Hammasi tugagach Claude'ni qayta oching.»

## YAKUNIY HISOBOT

Oxirida egaga jadval ko'rsat: qadam | holati (tayyor / o'tkazildi / xato) | nima ulandi | egasi yana nima qilishi kerak. Pullik xizmatlar va ularning sinov muddatini alohida yoz.

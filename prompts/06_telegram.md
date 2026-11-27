Sen shu kompyuterda ishlayotgan Claude Code'san. Vazifa: kompyuter egasining shaxsiy Telegram akkauntini Claude'ga ulash. Claude chatlar, guruhlar va kanallardagi xabarlarni o'qiy olsin, xabar yubora olsin, fayl va ovozli xabarlarni yuklab olsin.

ASOSIY QOIDA — ISHNI SEN QILASAN:
- Hamma ishni O'ZING bajar: dasturlarni o'rnatish, yuklab olish, fayllarni yaratish, brauzerda sahifalarni ochish va bosish, formalarni to'ldirish, ishga tushirish, tekshirish. Egaga «buni o'rnating», «buni sozlang», «shu buyruqni yozing» DEMA.
- Egasi FAQAT shularni qiladi: (1) akkauntga kiradi — telefon raqam, kod, 2FA paroli; (2) API kalitlarni sen tayyorlab ochgan faylga o'zi joylaydi; (3) QR kodni skan qiladi; (4) «Ruxsat berish» oynalarini o'zi bosadi.
- Parol, kod, API kalit va sessiya satrini HECH QACHON o'zing kiritma, so'rama, o'qima va chatga chiqarma.
- Kalitlar uchun usul: kerakli maydonlari BO'SH .env faylini o'zing yarat (huquqi 0600), uni matn muharririda och (Windows: notepad; macOS: open -e; Linux: xdg-open yoki mavjud muharrir) va egaga ayt: «Ochilgan faylda X= dan keyin qiymatni qo'yib, saqlab yoping». Keyin faqat maydon to'ldirilganini tekshir (bo'sh emasligi, formati), qiymatni chiqarmasdan.
- Brauzer: ichki brauzer yoki Claude in Chrome vositasi bo'lsa — sahifani o'zing och va kirish sahifasigacha va kirishdan keyingi hamma qadamlarni o'zing bos. Kirish (login) maydonida to'xta va egaga «kiring, keyin "bo'ldi" deng» de. Kalit ko'rsatilgan sahifaning matnini o'qima. Brauzer vositasi bo'lmasa — aniq havolani ber.
- Egaga oddiy, texnik bo'lmagan tilda, uning tilida yoz. Har bosqich boshida bir qatorda nima qilayotganingni ayt.
- OS'ni o'zing aniqla (Windows / macOS / Linux) va buyruqlarni moslashtir. Administrator (sudo/UAC) huquqi talab qiladigan yo'llardan QOCH.

1-BOSQICH. Dasturlar (kompyuterda hech narsa yo'q deb hisobla, bor bo'lsa qayta o'rnatma):
- uv (admin so'ramaydi): Windows: powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"; macOS/Linux: curl -LsSf https://astral.sh/uv/install.sh | sh. To'liq yo'lini eslab qol (odatda ~/.local/bin/uv) va doim to'liq yo'l bilan chaqir. Python kerak emas — uv o'zi yuklaydi.
- git kerak emas.
- ffmpeg ixtiyoriy (video ko'rish uchun), bo'lmasa davom et.

2-BOSQICH. Dasturni yuklash:
- https://github.com/chigwell/telegram-mcp/archive/refs/heads/main.tar.gz ni ~/workspace/ ga yukla, och (tar -xzf, Windows'da ham tar.exe bor), papkani ~/workspace/telegram-mcp deb nomla. Mavjud bo'lsa qayta yuklama.
- README.md ni o'qi — o'zgaruvchi nomlari yoki buyruqlar o'zgargan bo'lsa, README'ga amal qil.
- O'sha papkada: uv sync

3-BOSQICH. Kalit fayli:
- .env.example asosida ~/workspace/telegram-mcp/.env yarat, ichida bo'sh qatorlar:
  TELEGRAM_API_ID=
  TELEGRAM_API_HASH=
  TELEGRAM_SESSION_STRING=
  TELEGRAM_DEVICE_MODEL=Claude Telegram
  (qolgan ixtiyoriy sozlamalarni qo'shma). Huquqi 0600 (Windows: icacls bilan faqat joriy foydalanuvchiga).
- .gitignore'da .env va *.session borligini tekshir.

4-BOSQICH. API kalitini olish (my.telegram.org):
- Brauzerda https://my.telegram.org ni o'zing och. Egaga ayt: «Telefon raqamingizni yozing, Telegram ilovangizga kelgan kodni kiriting.» Kutib tur.
- Egasi kirgach: «API development tools» ni o'zing bos. Ilova hali yo'q bo'lsa formani o'zing to'ldir: App title: Claude, Short name: claude + 4 ta tasodifiy raqam, Platform: Desktop, qolganini bo'sh qoldir → «Create application». Ilova allaqachon bo'lsa — yangisini yaratma.
- .env faylini muharrirda och va egaga ayt: «Brauzerdagi App api_id raqamini TELEGRAM_API_ID= dan keyin, App api_hash ni TELEGRAM_API_HASH= dan keyin qo'ying va saqlang.»
- Tekshir: API_ID faqat raqamlar, API_HASH 32 ta belgi (qiymatini chiqarma).

5-BOSQICH. Kirish (sessiya):
- Egaga ko'rinadigan terminal oynasida (terminal paneli vositasi bo'lsa — o'shanda) ~/workspace/telegram-mcp papkasida ishga tushir:
  uv run session_string_generator.py --qr
- Egaga ayt: «Telefonda Telegram → Sozlamalar → Qurilmalar → "Kompyuterni ulash / Link Desktop Device" → terminaldagi QR'ni skan qiling. Ikki bosqichli parol bo'lsa, uni terminalga o'zingiz yozing.» QR terminalda chiqmasa, skript beradigan tg://login havolasini ochish kerakligini ayt.
- Skript chiqargan uzun sessiya satrini egasi .env dagi TELEGRAM_SESSION_STRING= ga qo'yadi (faylni sen muharrirda ochib berasan). Sen bu satrni o'qima va nusxalama.
- Tugagach o'sha terminal oynasini yop (satr ekranda qolmasin).

6-BOSQICH. Claude'ga ulash:
- Kalitlar konfigga YOZILMAYDI — server ularni o'z papkasidagi .env dan o'qiydi.
- claude CLI bo'lsa: claude mcp add -s user telegram -- <uv to'liq yo'li> --directory <telegram-mcp to'liq yo'li> run main.py
- CLI yo'q bo'lsa (desktop ilova): ~/.claude.json ni zaxiralab (.bak), JSON sifatida (uv run --no-project python skript.py bilan) o'qib, "mcpServers" ga qo'sh: "telegram": {"type":"stdio","command":"<uv yo'li>","args":["--directory","<telegram-mcp yo'li>","run","main.py"],"env":{}}. Faylning qolgan qismiga tegma.
- Egaga ayt: Telegram vositalari YANGI sessiyada paydo bo'ladi.

7-BOSQICH. Tekshirish:
- telegram-mcp papkasida Telethon bilan kichik skript ishga tushir: .env ni yuklab, get_me() → faqat ism va @username ni chiqar, keyin oxirgi 5 ta chat nomini chiqar. Sessiya satrini chiqarma.
- Egadan ruxsat so'ra: «"Saqlangan xabarlar"ga test xabar yuboraymi?» Ruxsat bo'lsa — "Test: Claude Telegram ulanishi ishlayapti ✅" yubor.
- Egaga yakuniy hisobot: nima o'rnatildi, qayerda, nima tekshirildi.

Xavfsizlik:
- .env va *.session fayllari = akkauntga to'liq kirish. Hech kimga berma, git'ga qo'shma, chatga chiqarma.
- Egasining aniq «ha»sisiz hech kimga xabar yuborma, hech narsani o'chirma, guruhga qo'shilma/chiqma. Har safar matn va oluvchini ko'rsat.
- Telegram spamni yoqtirmaydi: notanishlarga ko'p yozilsa akkaunt cheklanadi. Ommaviy yuborishda xabarlar orasida 10–20 soniya pauza qil; FloodWait xatosi kelsa ko'rsatilgan vaqtcha kut.
- Faqat o'qish kerak bo'lsa: .env ga TELEGRAM_EXPOSED_TOOLS=read-only qo'shish mumkin.
- Ulanishni uzish: telefonda Telegram → Sozlamalar → Qurilmalar → shu sessiyani o'chirish.

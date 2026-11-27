# Video yasayman — WhatsApp · Telegram · Instagram · YouTube · TikTok

Yangi kompyuterni Claude uchun to'liq sozlaydigan promptlar va skill'lar to'plami. Claude hamma narsani o'zi o'rnatadi va ulaydi. Egasi faqat akkauntlarga kiradi, ruxsat beradi, kerakli API kalitni faylga qo'yadi va QR kodni skan qiladi.

## Nimalar o'rnatiladi

| # | Nima | Qanday |
|---|------|--------|
| 1 | uv, Node.js, ffmpeg, Go | adminsiz, foydalanuvchi papkasiga |
| 2 | Video montaj skill'i | `skills/video-editing` |
| 3 | vidIQ — YouTube va Instagram | rasmiy konnektor |
| 4 | Windsor.ai — ijtimoiy tarmoqlar statistikasi va joylash | rasmiy konnektor |
| 5 | Postiz — 2 ta skill + CLI | `gitroomhq/postiz-agent` |
| 6 | Telegram (shaxsiy akkaunt) | `chigwell/telegram-mcp` |
| 7 | TikTok | Postiz + Windsor + vidIQ orqali |
| 8 | WhatsApp (shaxsiy akkaunt) | `lharries/whatsapp-mcp` |

## Ishlatish

1. Yangi kompyuterga Claude (desktop ilova yoki Claude Code) o'rnating va o'z akkauntingiz bilan kiring.
2. Claude'ga shu xabarni yuboring:

> https://github.com/nurbekumaraliev/WhatsApp-Telegram-Instagram-YouTube-TikTok-Video-Yasayman reposini yuklab ol (repo yopiq: kerak bo'lsa GitHub CLI'ni adminsiz o'rnat va men GitHub'ga kiraman), keyin SETUP.md faylini o'qib, undagi hamma qadamlarni boshidan oxirigacha bajar.

3. Claude so'raganda faqat: akkauntga kiring, «Ruxsat berish»ni bosing, kalitni ochilgan faylga qo'ying yoki QR'ni skan qiling.

Jarayon to'xtab qolsa — Claude'ga «SETUP.md ni davom ettir» deb yozing. U tugagan qadamlarni o'tkazib yuboradi.

## Xavfsizlik

- Parol, kod va API kalitlarni Claude hech qachon o'zi kiritmaydi, so'ramaydi va ko'rsatmaydi.
- Egasining «ha»sisiz hech narsa joylanmaydi, yuborilmaydi va pul sarflanmaydi.
- `store/`, `.env`, `*.session`, `token.json` kabi fayllar kalit hisoblanadi — hech kimga bermang va bu repoga qo'shmang.
- WhatsApp ulanishi rasmiy emas: ko'p odamga birdaniga yozilsa akkaunt bloklanishi mumkin.

## Manbalar va litsenziyalar

- `skills/video-editing` — MIT litsenziyasi, everything-claude-code to'plamidan.
- Postiz skill'lari, telegram-mcp va whatsapp-mcp o'rnatish paytida o'z rasmiy repolaridan yuklanadi.

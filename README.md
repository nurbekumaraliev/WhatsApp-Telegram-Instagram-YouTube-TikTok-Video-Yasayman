# Video yasayman — WhatsApp · Telegram · Instagram · YouTube · TikTok

Yangi kompyuterni Claude uchun to'liq sozlaydigan promptlar va skill'lar to'plami. Claude hamma narsani o'zi o'rnatadi va ulaydi. Egasi faqat akkauntlarga kiradi, ruxsat beradi, kerakli API kalitni faylga qo'yadi va QR kodni skan qiladi.

## 🚀 Qanday o'rnatiladi — 1 qadam

Claude Code'ni oching va shu xabarni yuboring:

```
https://github.com/nurbekumaraliev/WhatsApp-Telegram-Instagram-YouTube-TikTok-Video-Yasayman — shuni o'rnat
```

Qolganini Claude o'zi qiladi. Siz faqat so'ralganda akkauntlarga kirasiz, «Ruxsat berish»ni bosasiz, kalitni ochilgan faylga qo'yasiz va QR'ni skan qilasiz.

> **Claude uchun yo'riqnoma.** Agar foydalanuvchi senga shu repo havolasini berib, uni o'rnatishni so'ragan bo'lsa:
> 1. Repo arxivini yukla: `https://github.com/nurbekumaraliev/WhatsApp-Telegram-Instagram-YouTube-TikTok-Video-Yasayman/archive/refs/heads/main.tar.gz` → `~/workspace/` ga och (`tar -xzf`; Windows 10/11'da ham `tar.exe` bor). git shart emas.
> 2. Ochilgan papkadagi `SETUP.md` ni o'qi va undagi hamma qadamlarni tartib bilan, o'zing, oxirigacha bajar.
> 3. Foydalanuvchiga uning tilida, oddiy so'zlar bilan qisqa ayt: nima o'rnatilishini va undan faqat kirish, ruxsat berish, kalit qo'yish va QR skan qilish so'ralishini. Keyin darhol boshlab yubor.

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

## Batafsil

1. Kompyuterga Claude (desktop ilova yoki Claude Code) o'rnating va o'z akkauntingiz bilan kiring.
2. Yuqoridagi xabarni yuboring.
3. Claude so'raganda faqat: akkauntga kiring, «Ruxsat berish»ni bosing, kalitni ochilgan faylga qo'ying yoki QR'ni skan qiling.

Jarayon to'xtab qolsa — Claude'ga «SETUP.md ni davom ettir» deb yozing. U tugagan qadamlarni o'tkazib yuboradi.

Hammasi kerak emasmi? Masalan «faqat WhatsApp'ni o'rnat» deb yozing — Claude faqat o'sha qadamni bajaradi.

## Xavfsizlik

- Parol, kod va API kalitlarni Claude hech qachon o'zi kiritmaydi, so'ramaydi va ko'rsatmaydi.
- Egasining «ha»sisiz hech narsa joylanmaydi, yuborilmaydi va pul sarflanmaydi.
- `store/`, `.env`, `*.session`, `token.json` kabi fayllar kalit hisoblanadi — hech kimga bermang va bu repoga qo'shmang.
- WhatsApp ulanishi rasmiy emas: ko'p odamga birdaniga yozilsa akkaunt bloklanishi mumkin.

## Manbalar va litsenziyalar

- `skills/video-editing` — MIT litsenziyasi, everything-claude-code to'plamidan.
- Postiz skill'lari, telegram-mcp va whatsapp-mcp o'rnatish paytida o'z rasmiy repolaridan yuklanadi.

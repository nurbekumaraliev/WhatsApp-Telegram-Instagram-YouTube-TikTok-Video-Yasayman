# 5-qadam. Postiz — 2 ta skill + CLI

Maqsad: Postiz'ning rasmiy 2 ta skill'ini (`postiz` va `postiz-agent`, manba: github.com/gitroomhq/postiz-agent) va `postiz` CLI'ni o'rnatish. Postiz orqali Claude bitta joydan Instagram, TikTok, YouTube, Facebook, X, LinkedIn, Telegram va boshqa tarmoqlarga post rejalashtiradi va joylaydi.

## Egasi faqat
Postiz'ga kiradi (yoki ro'yxatdan o'tadi), API kalitni sen ochgan faylga qo'yadi, Postiz ichida har bir ijtimoiy tarmoqqa kirib ruxsat beradi.

## Qadamlar
1. **Node.js** 1-qadamda o'rnatilganini tekshir (`node -v`). Yo'q bo'lsa — 1-qadamdagi usul bilan o'rnat.
2. **Skill'lar (global):**
   `npx -y skills add gitroomhq/postiz-agent -g -y`
   - Agar buyruq so'rasa — ikkala skill'ni ham (`postiz`, `postiz-agent`) va Claude Code'ni tanla.
   - Ishlamasa: https://github.com/gitroomhq/postiz-agent/archive/refs/heads/main.tar.gz ni yuklab och, ichidagi har bir `SKILL.md` joylashgan papkani `~/.claude/skills/<skill-nomi>/` ga nusxala.
   - Tekshir: `~/.claude/skills/` ichida postiz skill'lari bor.
   - Skill'larning SKILL.md faylini o'qi — o'rnatish va kirish talablari o'zgargan bo'lsa, o'shanga amal qil.
3. **CLI:** `npm install -g postiz` (npm prefix foydalanuvchi papkasida — admin kerak emas). Tekshir: `postiz --help`.
4. **Postiz akkaunti:** brauzerda https://platform.postiz.com ni o'zing och. Egaga: «Postiz'ga kiring yoki ro'yxatdan o'ting (formani men to'ldiraman, parolni o'zingiz yozasiz).» Kut.
   - Egasi o'z serverida Postiz ishlatsa (self-hosted) — uning manzilini so'ra va shunga moslashtir.
5. **API kalit:**
   - `~/workspace/postiz/.env` ni bo'sh maydon bilan yarat (faqat egasi o'qiy oladi): `POSTIZ_API_KEY=` (self-hosted bo'lsa `POSTIZ_API_URL=` ham).
   - Postiz'da Settings → API (Public API) sahifasini o'zing och. Kalit ko'rsatilganda .env ni muharrirda ochib egaga: «Kalitni POSTIZ_API_KEY= dan keyin qo'yib saqlang.» Kalitni o'qima.
   - Kalitni foydalanuvchi muhit o'zgaruvchisiga qiymatni ko'rsatmasdan, skript bilan yoz (Windows: [Environment]::SetEnvironmentVariable("POSTIZ_API_KEY", <fayldan o'qilgan qiymat>, "User"); mac/linux: ~/.profile ga `set -a; . ~/workspace/postiz/.env; set +a` qatorini qo'sh).
   - Agar Postiz CLI brauzer orqali kirishni qo'llasa (`postiz login` yoki shunga o'xshash — `--help` dan tekshir), kalit o'rniga shuni ishlat: buyruqni o'zing ishga tushir, egasi brauzerda faqat «ruxsat»ni bosadi.
6. **Tarmoqlarni ulash:** Postiz'da «Add channel» sahifasini o'zing och. Egadan qaysi tarmoqlar kerakligini bir marta so'ra (Instagram, TikTok, YouTube, Facebook, Telegram...). Har biri uchun «Add» ni o'zing bos → egasi o'sha tarmoqqa kiradi va ruxsat beradi.
7. **Tekshirish (faqat o'qish):** CLI yoki skill orqali ulangan kanallar ro'yxatini chiqar va egaga ko'rsat.

## Eslatma egaga
- Postiz cloud — pullik (sinov muddati bor). Rejani faqat egasi tanlaydi. Bepul variant: o'z serverida o'rnatish (self-hosted) — egasi xohlasa, alohida qilib beriladi.
- Joylashdan oldin har doim qoralama/rejani ko'rsat va «ha» ol.

# 3-qadam. vidIQ konnektori — YouTube va Instagram

Maqsad: vidIQ konnektorini Claude'ga ulash va egasining YouTube kanali hamda Instagram akkauntini vidIQ'ga bog'lash. Shundan keyin Claude: trendlar, g'oya, kalit so'zlar, ssenariy, sarlavha/muqova, kanal auditi, post rejalashtirish va joylash.

Rasmiy manzil: `https://mcp.vidiq.com/mcp` (Claude konnektorlar katalogida «vidIQ»).

## Egasi faqat
vidIQ, Google (YouTube) va Instagram akkauntlariga kiradi va «Ruxsat berish»ni bosadi. Qolgan hamma narsani sen qilasan.

## Qadamlar
1. **Holat:** mavjud vositalarda `vidiq_*` bormi? Bor bo'lsa — 3-bandga o't.
2. **Konnektorni ulash:**
   - A yo'l (asosiy): brauzerda `https://claude.ai/settings/connectors` ni o'zing och → «Browse connectors» → «vidIQ» → «Connect» ni o'zing bos. Kirish oynasida to'xta: «vidIQ'ga kiring (akkaunt yo'q bo'lsa — Google bilan ro'yxatdan o'ting) va ruxsat bering, keyin "bo'ldi" deng.»
   - B yo'l (claude CLI bo'lsa yoki A ishlamasa): `claude mcp add --transport http -s user vidiq https://mcp.vidiq.com/mcp` → egaga: «Claude'da /mcp yozing → vidiq → Authenticate → kirib ruxsat bering.»
   - Vositalar shu sessiyada ko'rinmasa — egaga ayt: «vidIQ ulandi, vositalari Claude qayta ochilganda paydo bo'ladi.» Keyingi qadamga o't, 3–4-bandlarni yakuniy tekshiruvda bajar.
3. **YouTube va Instagram'ni bog'lash:**
   - `vidiq_social_account_list` bilan ulanganlarni ko'r.
   - YouTube yo'q bo'lsa: `vidiq_social_account_connect` bilan havola ol → egaga: «Shu havolani oching, YouTube kanalingiz bor Google akkauntga kiring va ruxsat bering.»
   - Instagram yo'q bo'lsa: xuddi shunday. Instagram akkaunt Professional (Biznes/Creator) bo'lishi kerak bo'lishi mumkin — shunday xabar chiqsa egaga ayt: «Telefonda Instagram → Profil → ☰ → Sozlamalar → Akkaunt turi va vositalar → Professional akkauntga o'tish. Bepul.»
4. **Tekshirish (faqat o'qish):** ulangan akkauntlar ro'yxati, kanal statistikasi (`vidiq_channel_stats`), qolgan kredit (`vidiq_credit_usage_list`).

## Eslatma egaga
- vidIQ bepul rejasi cheklangan, ko'p ishlar kredit sarflaydi. Pullik rejani faqat egasi tanlaydi — sen havolasini berasan.
- Joylashdan oldin har doim qoralama (`vidiq_social_post_draft_create`) → egasi ko'radi → «ha» desa `vidiq_social_post_publish`.

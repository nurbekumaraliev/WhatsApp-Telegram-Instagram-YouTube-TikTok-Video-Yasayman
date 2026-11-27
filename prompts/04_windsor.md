# 4-qadam. Windsor.ai konnektori

Maqsad: Windsor.ai for Social Media konnektorini ulash. U Instagram, Facebook, TikTok, YouTube, LinkedIn, Threads statistikasini beradi, post joylaydi, izoh va sharhlarga javob beradi, videolarni yangilaydi.

Rasmiy manzillar:
- Windsor.ai for Social Media: `https://mcp.windsor.ai/social_media` (asosiy)
- Windsor.ai umumiy (350+ manba, reklama hisobotlari — ixtiyoriy, egasi xohlasa): `https://mcp.windsor.ai/`

## Egasi faqat
Windsor'ga kiradi (yoki ro'yxatdan o'tadi — formani sen to'ldirasan, parolni egasi yozadi) va har bir ijtimoiy tarmoqqa ruxsat beradi.

## Qadamlar
1. **Holat:** mavjud vositalarda Windsor (`get_connectors`, `get_data`, `execute_action`) bormi? Bor bo'lsa — 3-bandga o't.
2. **Konnektorni ulash:**
   - A yo'l: `https://claude.ai/settings/connectors` ni o'zing och → «Browse connectors» → «Windsor.ai for Social Media» → «Connect» ni o'zing bos → egasi kiradi va ruxsat beradi.
   - B yo'l: `claude mcp add --transport http -s user windsor-social https://mcp.windsor.ai/social_media` → egaga: «/mcp → windsor-social → Authenticate.»
   - Vositalar shu sessiyada ko'rinmasa — egaga ayt va keyingi qadamga o't; 3–4-bandlarni yakuniy tekshiruvda bajar.
3. **Tarmoqlarni ulash:** `get_connectors` bilan har bir tarmoqni tekshir (instagram, facebook_organic, tiktok_organic, youtube, threads). Egadan qaysilari kerakligini bir marta so'ra. Ulanmaganlari uchun `get_connector_authorization_url` bilan havola ol va egaga ber: «Shu havolani oching, akkauntingizga kiring va ruxsat bering.» Har biridan keyin qayta tekshir.
4. **Tekshirish (faqat o'qish):** `get_fields` → `get_data` oxirgi 28 kun uchun har bir ulangan tarmoq bo'yicha obunachilar/ko'rishlar. Natija bo'sh bo'lsa — sana oralig'ini kengaytirib qayta urin.

## Eslatma egaga
- Windsor'ning bepul sinov muddati bor, keyin pullik. Rejani faqat egasi tanlaydi.
- Yozish amallari (`execute_action`: joylash, izohga javob) — faqat egasi «ha» degandan keyin.

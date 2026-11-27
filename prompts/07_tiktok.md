# 7-qadam. TikTok

Maqsad: TikTok'ga video joylash va statistikani ko'rish imkonini berish. Alohida noma'lum TikTok skill'i O'RNATILMAYDI (xavfsizlik uchun) — TikTok rasmiy ulanishli xizmatlar orqali ulanadi:

1. **Postiz** (5-qadam) — video joylash va rejalashtirish. Postiz'da «Add channel» → TikTok ni o'zing bos → egasi TikTok'ga kiradi va ruxsat beradi.
2. **Windsor.ai** (4-qadam) — statistika. `get_connectors(connector="tiktok_organic")` → ulanmagan bo'lsa `get_connector_authorization_url` havolasini egaga ber.
3. **vidIQ** (3-qadam) — TikTok trendlari, g'oya va post tayyorlash. `vidiq_social_account_list` → kerak bo'lsa `vidiq_social_account_connect`.

Agar 3–5-qadamlardan birortasi o'tkazib yuborilgan bo'lsa — qolganlari orqali ula. Hech biri bo'lmasa — egaga ayt va bu qadamni o'tkazib yubor.

## Tekshirish
- Postiz kanallar ro'yxatida TikTok bor.
- Windsor'da TikTok bo'yicha oxirgi 28 kun statistikasi chiqadi.

## Eslatma egaga
- TikTok Direct (shaxsiy xabarlar) va izohlarga javob berish uchun rasmiy API yo'q — bularni ulab bo'lmaydi.
- Ba'zi xizmatlar orqali birinchi videolar «Faqat men» bo'lib chiqishi mumkin — TikTok ilovasida qo'lda Public qilinadi.
- Joylashdan oldin video, matn va kimga ko'rinishini egaga ko'rsat va «ha» ol.

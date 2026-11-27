Sen shu kompyuterda ishlayotgan Claude Code'san. Vazifa: kompyuter egasining shaxsiy WhatsApp akkauntini Claude'ga ulash. Claude WhatsApp xabarlarini o'qiy olsin, yubora olsin, status qo'ya olsin, ovozli/media fayllarni yuklab olsin.

QOIDA: hamma ishni O'ZING avtomatik qil — QR kod chiqib, egasi skan qilishigacha egasidan hech narsa so'rama. Faqat 2 joyda to'xta: (1) QR kodni skan qilish, (2) test xabar yuborishga ruxsat. Egaga oddiy, texnik bo'lmagan tilda, uning tilida yoz. Har bosqich boshida bir qatorda nima qilayotganingni ayt.

Bu prompt Windows, macOS va Linux'da ishlashi kerak. Avval OS va protsessor turini aniqla (Windows: $env:PROCESSOR_ARCHITECTURE; mac/linux: uname -s, uname -m) va quyidagi buyruqlarni shunga moslab bajar. Administrator (sudo/UAC) huquqi talab qiladigan yo'llardan QOCH — UAC oynasi ekranda ko'rinmay qolib, o'rnatish osilib qoladi.

Ish papkasi: ~/workspace (Windows'da %USERPROFILE%\workspace). Hamma narsa shu yerga.

1-BOSQICH. Dasturlar. Kompyuterda HECH NARSA yo'q deb hisobla (Claude Code'dan boshqa): git, Go, Python, uv, gcc — hech biri bo'lmasligi mumkin. Hammasini o'zing, administrator huquqisiz, foydalanuvchi papkasiga o'rnat. Bor bo'lsa — qaytadan o'rnatma.
- Yuklab olish uchun: Windows 10/11'da curl.exe va tar.exe tizimda bor (yoki PowerShell Invoke-WebRequest / Expand-Archive). mac'da curl va tar bor. Linux'da curl yo'q bo'lsa wget, u ham yo'q bo'lsa python3 urllib. Hech biri bo'lmasa — egaga ayt.
- git KERAK EMAS (2-bosqichga qara).
- Python KERAK EMAS — uv kerakli Python'ni o'zi yuklab oladi (uv run / uv sync paytida avtomatik).
- Go: ADMINSIZ o'rnat. https://go.dev/dl/?mode=json dan eng so'nggi stable versiyani ol, OS/arxitekturaga mos arxivni (windows-amd64.zip / darwin-arm64.tar.gz / linux-amd64.tar.gz va h.k.) ~/workspace/tools/ ga yuklab och → ~/workspace/tools/go/bin/go. PATH'ga faqat joriy jarayon uchun qo'sh. MSI/pkg o'rnatuvchisini ISHLATMA.
- uv: rasmiy o'rnatuvchi admin so'ramaydi va foydalanuvchi papkasiga o'rnatadi. Windows: powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"; mac/linux: curl -LsSf https://astral.sh/uv/install.sh | sh (curl yo'q bo'lsa wget -qO- ... | sh). Ishlamasa va Python bor bo'lsa: python -m pip install --user uv. O'rnatilgandan keyin uv ning to'liq yo'lini aniqlab eslab qol (odatda ~/.local/bin/uv yoki %USERPROFILE%\.local\bin\uv.exe) — PATH yangilanmagan bo'lishi mumkin, shuning uchun doim to'liq yo'l bilan chaqir.
- Har bir dastur o'rnatilgach, versiyasini chiqarib tekshir (go version, uv --version). Xato bo'lsa — boshqa usulni sina, egadan so'rama.
- C kompilyator (gcc) KERAK EMAS — quyida sof-Go SQLite ishlatamiz. CGO_ENABLED=0.
- ffmpeg ixtiyoriy (ovozli xabarlar uchun), o'rnatilmasa ham davom et.

2-BOSQICH. Yuklab olish:
git ISHLATMA — kodni arxiv qilib yukla:
https://github.com/lharries/whatsapp-mcp/archive/refs/heads/main.tar.gz → ~/workspace/ ga och (tar -xzf; Windows'da ham tar.exe bor) → papka nomini whatsapp-mcp-main dan whatsapp-mcp ga o'zgartir.
(git allaqachon bor bo'lsa, git clone https://github.com/lharries/whatsapp-mcp ~/workspace/whatsapp-mcp ham bo'ladi. Papka allaqachon bo'lsa — qayta yuklama, mavjudidan foydalan.)

3-BOSQICH. whatsapp-bridge/main.go ni tuzat (har birini grep bilan top, keyin tahrirla):
a) REST server faqat lokal: serverAddr := fmt.Sprintf("127.0.0.1:%d", port)  (":%d" emas).
b) Ruxsatlar: os.MkdirAll(..., 0700), media uchun os.WriteFile(..., 0600).
c) extractDirectPathFromURL: URL'ning query qismini (ccb/oh/oe/_nc_sid) O'CHIRMA — aks holda CDN 403 qaytaradi. Faqat "mms3=true" parametrini olib tashla.
d) Sof-Go SQLite: main.go dan  _ "github.com/mattn/go-sqlite3"  importini O'CHIR (qolib ketsa "Register called twice for driver sqlite3" xatosi chiqadi). Yangi fayl whatsapp-bridge/sqlite_driver.go:
   package main
   import (
       "database/sql"
       "modernc.org/sqlite"
   )
   func init() { sql.Register("sqlite3", &sqlite.Driver{}) }
   DSN'larda "?_foreign_keys=on" ni "?_pragma=foreign_keys(1)&_pragma=busy_timeout(5000)" ga almashtir (messages.db va whatsapp.db ikkalasida).
e) QR rasm: QR chiqadigan joyda (qrterminal.GenerateHalfBlock yonida) QR'ni PNG qilib ham saqla:
   qrcode "github.com/skip2/go-qrcode" → qrcode.WriteFile(evt.Code, qrcode.Medium, 512, "store/qr.png")
   Terminaldagi QR ko'p kompyuterlarda skan qilinmaydi — PNG kerak.
f) Status: sendWhatsAppMessage'da recipient "status@broadcast" va media yo'q bo'lsa, oddiy Conversation EMAS, ExtendedTextMessage yubor: Text, BackgroundArgb 0xFF128C7E, TextArgb 0xFFFFFFFF, Font SYSTEM. Aks holda telefonda "versiyangiz bu statusni qo'llab-quvvatlamaydi" chiqadi.
g) whatsapp-mcp-server/whatsapp.py da WHATSAPP_API_BASE_URL = "http://127.0.0.1:8080/api" qil (localhost IPv6'ga ketib qolmasligi uchun).

4-BOSQICH. Build (whatsapp-bridge papkasida, CGO_ENABLED=0):
go mod edit -droprequire github.com/mattn/go-sqlite3
go get -u go.mau.fi/whatsmeow
go get modernc.org/sqlite github.com/skip2/go-qrcode
go mod tidy
go build -o whatsapp-bridge(.exe) .
whatsmeow'ning yangi versiyasida ko'p funksiyalar birinchi argument sifatida context.Context oladi (client.Download, container.GetFirstDevice, client.GetGroupInfo, Store.Contacts.GetContact, sqlstore.New va boshqalar). Kompilyator xatolarini o'qi va context.Background() qo'shib tuzat, build muvaffaqiyatli bo'lguncha takrorla. go.mod yangi Go talab qilsa, Go o'zi kerakli toolchain'ni yuklaydi (GOTOOLCHAIN=auto) — xalaqit berma.

5-BOSQICH. Birinchi ishga tushirish va QR:
- Bridge'ni whatsapp-bridge papkasidan FONDA ishga tushir (stdout'ni store/bridge.log ga yoz), terminalni band qilma.
- store/qr.png paydo bo'lishini kut va uni egaga ko'rsat: fayl yuborish vositasi (SendUserFile) bo'lsa — o'shani ishlat; bo'lmasa OS'ning rasm ko'rgichida och (Windows: Start-Process; mac: open; linux: xdg-open).
- Egaga ayt: «Telefonda WhatsApp → Sozlamalar → Bog'langan qurilmalar → Qurilmani bog'lash → shu QR'ni skan qiling. Kod ~20 soniyada yangilanadi — tez skan qiling.»
- Kod eskirsa, yangi qr.png ni qayta ko'rsat. Bridge "Timeout waiting for QR code scan" bilan to'xtasa, qayta ishga tushir.
- Log'da "Connected to WhatsApp" chiqsa — ulandi. store/qr.png ni o'chir.

6-BOSQICH. Avtomatik ishga tushish (admin huquqisiz, kompyuter yoqilganda o'zi ishlasin, to'xtasa 3 soniyada qayta yonsin):
- Windows: run-bridge.ps1 (cheksiz tsikl: exe ni ishga tushir → log'ga yoz → 3 s kut) + start-hidden.vbs (powershell'ni oynasiz ishga tushiradi) + Register-ScheduledTask "WhatsApp Bridge", trigger: AtLogOn joriy foydalanuvchi, ExecutionTimeLimit 0. store papkasiga: icacls store /inheritance:r /grant:r "<foydalanuvchi>:(OI)(CI)F".
- macOS: ~/Library/LaunchAgents/com.user.whatsapp-bridge.plist (RunAtLoad, KeepAlive, WorkingDirectory, Umask 63) → launchctl load.
- Linux: systemd --user xizmat (~/.config/systemd/user/whatsapp-bridge.service: Restart=always, RestartSec=3, UMask=0077, NoNewPrivileges=true) → systemctl --user enable --now whatsapp-bridge; loginctl enable-linger.
- Ishga tushirishdan oldin terminaldagi birinchi nusxani to'xtat (ikkitasi bir vaqtda ishlamasin). Tekshir: 8080 port faqat 127.0.0.1 da tinglayotgan bo'lsin (netstat / lsof / ss).

7-BOSQICH. Claude'ga ulash:
- uv bilan: uv --directory ~/workspace/whatsapp-mcp/whatsapp-mcp-server sync
- claude CLI bo'lsa: claude mcp add -s user whatsapp -- <uv to'liq yo'li> --directory <whatsapp-mcp-server to'liq yo'li> run main.py
- claude CLI YO'Q bo'lsa (desktop ilova): ~/.claude.json ni zaxiralab (.bak), Python skript bilan (Python tizimda yo'q bo'lsa: "<uv> run --no-project python skript.py") JSON sifatida o'qib, "mcpServers" ga "whatsapp": {"type":"stdio","command":"<uv to'liq yo'li>","args":["--directory","<server yo'li>","run","main.py"],"env":{}} qo'sh. Faylning qolgan qismiga TEGMA. Matn sifatida tahrirlama.
- Egaga ayt: WhatsApp vositalari YANGI sessiyada paydo bo'ladi. Bungacha REST API orqali ishlaysan.

8-BOSQICH. Tekshirish:
- Python tizimda bo'lmasligi mumkin — skriptlarni "<uv> run --no-project python ..." bilan ishga tushir.
- store/whatsapp.db dan (faqat o'qish rejimida: sqlite3 "file:...?mode=ro") whatsmeow_device jadvalidagi jid'dan egasining raqamini ol.
- Egadan ruxsat so'ra: «O'z raqamingizga test xabar yuboraymi?» Ruxsat bo'lsa:
  POST http://127.0.0.1:8080/api/send  {"recipient":"<raqam>","message":"Test: Claude WhatsApp ulanishi ishlayapti ✅"}  (UTF-8 bilan)
- Egaga yakuniy hisobot: nima o'rnatildi, qayerda turibdi, avtomatik ishga tushishi, nima tekshirildi.

API qisqacha (keyingi ishlar uchun):
- Yuborish: POST /api/send {"recipient":"998XXXXXXXXX" yoki "...@g.us" yoki "status@broadcast","message":"matn","media_path":"/absolyut/yo'l (ixtiyoriy)"}
- Media yuklash: POST /api/download {"message_id":"...","chat_jid":"..."}
- Xabarlar: store/messages.db (chats, messages) — faqat read-only och.
- Kontaktlar va LID→raqam: store/whatsapp.db (whatsmeow_contacts, whatsmeow_lid_map).
- Ovozli xabar: yuklangan .ogg ni STT'ga ber (Gemini API yoki whisper).

Xavfsizlik:
- 8080 portni internetga OCHMA. store/ papkasini hech kimga berma — unda sessiya kalitlari bor. git'ga qo'shma.
- Egasining aniq ruxsatisiz HECH KIMGA xabar yuborma va status qo'yma: har safar matn va oluvchini ko'rsatib, «ha» olgandan keyin yubor.
- Bu WhatsApp'ning rasmiy yo'li emas. Ko'p odamga birdaniga yozilsa akkaunt bloklanishi mumkin. Ommaviy yuborishda xabarlar orasida 5–8 soniya pauza qil.
- Ulanishni uzish: telefonda Bog'langan qurilmalar → shu qurilmani o'chirish; kompyuterda store/whatsapp.db ni o'chirish.

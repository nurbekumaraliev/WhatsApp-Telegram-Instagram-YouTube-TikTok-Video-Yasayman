# 1-qadam. Asosiy dasturlar

Maqsad: keyingi qadamlar uchun kerakli dasturlarni ADMINISTRATOR HUQUQISIZ, foydalanuvchi papkasiga o'rnatish. Kompyuterda hech narsa yo'q deb hisobla. Bor bo'lsa — qayta o'rnatma, faqat versiyasini tekshir.

Hamma narsa `~/workspace/tools/` ga (Windows: `%USERPROFILE%\workspace\tools\`). Har bir dasturning to'liq yo'lini eslab qol va doim to'liq yo'l bilan chaqir (PATH yangilanmagan bo'lishi mumkin). Ixtiyoriy: foydalanuvchi PATH'iga qo'sh (Windows: [Environment]::SetEnvironmentVariable(..., "User"); mac/linux: ~/.profile).

Yuklab olish: Windows 10/11'da curl.exe va tar.exe tizimda bor (yoki Invoke-WebRequest / Expand-Archive). macOS'da curl va tar bor. Linux'da curl yoki wget.

MSI / pkg / exe o'rnatuvchilarini va winget'ni ISHLATMA — ular administrator ruxsatini so'raydi va ekranda ko'rinmay qolgan oyna tufayli osilib qoladi.

1. **uv** (Python ham shu orqali keladi):
   - Windows: `powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"`
   - macOS/Linux: `curl -LsSf https://astral.sh/uv/install.sh | sh`
   - Tekshir: `uv --version`.
2. **Node.js** (npx va Postiz uchun): https://nodejs.org/dist/index.json dan eng so'nggi LTS versiyani ol, OS/arxitekturaga mos arxivni (win-x64.zip / darwin-arm64.tar.gz / linux-x64.tar.xz) `tools/node` ga och. npm global papkasini foydalanuvchi papkasiga qo'y: `npm config set prefix ~/workspace/tools/npm-global`. Tekshir: `node -v`, `npm -v`.
3. **ffmpeg** (video va ovoz uchun): adminsiz statik build — Windows: https://www.gyan.dev/ffmpeg/builds/ (essentials zip); macOS: https://evermeet.cx/ffmpeg/ ; Linux: https://johnvansickle.com/ffmpeg/ . `tools/ffmpeg` ga och. Tekshir: `ffmpeg -version`.
4. **Go** (WhatsApp ko'prigi uchun): https://go.dev/dl/?mode=json dan eng so'nggi stable, mos arxivni `tools/go` ga och. Tekshir: `go version`.
5. **gh** (GitHub CLI, shu repodan yangilanishlar uchun, ixtiyoriy): https://github.com/cli/cli/releases dan mos arxivni `tools/gh` ga och.
6. **git** — shart emas. Repo va dasturlar arxiv (tar.gz/zip) qilib yuklanadi.

Har biridan keyin versiyasini chiqarib tekshir. Biror usul ishlamasa — boshqasini sina (masalan uv uchun: `python -m pip install --user uv`), egadan so'rama.

Tugagach egaga bir qatorda ayt: qaysi dasturlar o'rnatildi.

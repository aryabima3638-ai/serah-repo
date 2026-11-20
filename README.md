# Flutter Build Bot (Panel)

Bot Telegram: kirim ZIP project Flutter -> dibuild di GitHub Actions -> APK dikirim balik. Jalan di panel (Node.js), tanpa VPS.

## File
- `index.js` menu utama bot
- `telegram.js` ID owner (+ username owner)
- `setting.js` token bot, apiId/apiHash, foto, channel, GitHub, limit
- `lib/` db, github, mtproto, builder
- `.github/workflows/build.yml` (APK) & `build-web.yml` (web) -> **wajib ada di repo GitHub**

## Setup
1. Buat repo GitHub (private boleh), upload folder `.github/workflows/` ke branch `main` (minimal 1 commit).
2. Repo > Settings > Actions: aktifkan Actions. Buat token (classic) scope `repo` + `workflow`.
3. Isi `setting.js`: botToken, github.token, github.repo, channel, logChannel, photoUrl.
4. Isi `telegram.js`: ID Telegram owner.
5. Jadikan bot **admin** di channel (untuk cek follow & kirim notif).
6. ZIP > 20MB sampai 2GB: isi `apiId` & `apiHash` dari https://my.telegram.org. Tanpa ini, ZIP maks 20MB (atau kirim link direct).
7. Panel: upload semua file, Startup command `npm install && node index.js` (atau `npm start`), Node 18+.
   Pastikan disk panel >= 2x ukuran ZIP terbesar.

## Role & command
| Role | Akses |
|---|---|
| member | semua fitur build, 5 credit gratis, habis -> reset 24 jam |
| reseller | build unlimited, `/addcredit` |
| owner | semuanya + `/addreseller` (`/address`), `/addowner`, `/delreseller`, `/maintenance on\|off`, `/ban`, `/unban`, `/broadcast`, `/stats` |

`/addcredit ID [jumlah]` (default 5). Owner = ID di `telegram.js` + yang ditambah lewat `/addowner`.

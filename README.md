# Mini Games (siap jadi APK)

Berisi 51 game dalam 5 kategori (dengan koin, hadiah harian, dan riwayat permainan): Arcade, Puzzle, Musik, Casual, dan Challenge (termasuk Tic Tac Toe, Memory Card, Snake, 2048, Whack a Mole, Tebak Angka, dan Flappy Bird). Semua offline, rekor tersimpan di perangkat.

Fitur: efek suara di setiap game, 6 lagu lobi yang berganti otomatis (atau pilih manual), dan 8 tema yang bisa dipilih lewat tombol ⚙️ (Neon, Klasik, Vintage, Koboi, Liquid Glass, Luar Angkasa, Sakura, Retro Pixel). Semua suara dibuat lewat kode (tanpa file audio), jadi ukuran APK tetap kecil.

Kode game ada di `www/index.html`. Proyek ini memakai Capacitor untuk membungkusnya menjadi aplikasi Android.

## Cara 1: APK otomatis lewat GitHub (paling mudah, tanpa install apa pun)

1. Buat akun di github.com, lalu buat repository baru (bebas, boleh private).
2. Upload seluruh isi folder ini ke repository, termasuk folder `.github`.
3. Buka tab **Actions** dan jalankan workflow **Build APK** (atau tunggu otomatis setelah upload).
4. Setelah selesai (sekitar 5 menit), buka hasil run tersebut. Di bagian **Artifacts** unduh **MiniGames-APK**. Isinya `app-debug.apk`.
5. Kirim APK itu ke HP, buka, lalu izinkan "Install dari sumber tidak dikenal".

## Cara 2: Build di komputer sendiri

Butuh Node.js 20+, JDK 21, dan Android SDK (paling gampang lewat Android Studio).

```bash
npm install
npx cap add android
npx cap sync android
cd android
./gradlew assembleDebug
```

APK ada di `android/app/build/outputs/apk/debug/app-debug.apk`.

## Cara 3: Lewat PWABuilder

1. Upload folder `www` ke hosting gratis (Netlify Drop, GitHub Pages, Vercel).
2. Buka pwabuilder.com, masukkan URL-nya, lalu pilih paket Android.

## Catatan

- APK `debug` cukup untuk dipasang di HP sendiri. Untuk diunggah ke Play Store, buat APK/AAB release yang ditandatangani lewat Android Studio (Build > Generate Signed Bundle / APK).
- Ganti nama atau ID aplikasi di `capacitor.config.json` (`appName`, `appId`) sebelum build.
- Level: dari XP (2× koin sesi), 100 XP per level, bonus 20 koin tiap naik level.
- Papan skor: 5 skor terbaik per game (🏆 Papan). Kesulitan Mudah/Normal/Sulit di Pengaturan (berlaku untuk Flappy Bird, Space Shooter, Neon Racing, Geometry Dash Mini, Breakout, Coin Catcher).
- Koin: didapat saat keluar dari game (sesuai skor), atau 25 koin sekali per hari lewat tombol 🎁. Koin dipakai untuk membuka tema di Pengaturan.
- Ingin tambah game? Tulis fungsi game baru di `www/index.html`, lalu daftarkan di array `CATS` (per kategori).

## Menambah tema atau lagu

- Tema: tambahkan satu objek di array `THEMES` (warna, font, bentuk sudut, efek) di `www/index.html`.
- Lagu lobi: tambahkan satu objek di array `TR` (tempo, nada dasar, tangga nada, progresi akor, pola drum).

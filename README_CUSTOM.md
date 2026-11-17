# SampVoice custom build

Dasar: source CyberMor/sampvoice (MIT) dari `sampvoice-plugins-main.zip`.

## Perubahan
- **ENB**: `client/include/util/Render.cpp`, hook `Present` sekarang menyimpan state D3D
  (state block, render target, depth-stencil) sebelum menggambar overlay dan mengembalikannya
  sesudahnya. Sebelumnya overlay (ikon mic, daftar speaker, menu, blur) mengubah state device
  tanpa restore, yang mengganggu post-processing ENB.
- **Build otomatis**: `.github/workflows/build-client.yml` membuat `sampvoice.asi` untuk SA-MP R1 dan R3.

## Belum dikerjakan
- **SA-MP 0.3.DL-R1**: belum ada. Source hanya punya offset R1/R3 (`AddressesBase.cpp` dan header
  `include/samp/*`). Offset DL tidak ada di file Anda dan saya tidak mau mengarang angka, karena
  offset salah = crash. Dibutuhkan tabel offset DL yang terverifikasi.
- Pilihan versi masih lewat compile-time (`SAMP_R1` / `SAMP_R3`), jadi satu .asi per versi.

## Belum teruji
Tidak ada compiler Windows di lingkungan saya, jadi perubahan ini belum dikompilasi dan belum dites di game.

## Cara build
1. Upload folder ini ke repo GitHub, lalu buka tab Actions dan jalankan `build-client`.
2. Ambil artifact `sampvoice-R1` atau `sampvoice-R3` sesuai versi SA-MP Anda.
3. Satu-satunya bagian server (`sampvoice.dll/.so`) tidak berubah.

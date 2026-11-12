---
name: kukatanya
description: "Grill ide dalam bahasa Indonesia sambil mencatat glossary dan ADR. Gunakan saat user meminta kukatanya atau sesi tanya sambil mendokumentasikan keputusan."
---

Interview user tanpa henti sampai tercapai shared understanding. Petakan sebagai **design tree**: tiap keputusan bercabang ke keputusan yang menggantung padanya.

Kerjakan tree dalam **rounds**. **Frontier** = tiap keputusan yang prasyaratnya sudah beres: pertanyaan yang bisa ditanya _sekarang_ tanpa menebak jawaban yang belum didengar. Tanya seluruh frontier dalam satu round: beri nomor tiap pertanyaan dan beri jawaban rekomendasimu. Tunggu jawaban user sebelum round berikutnya.

Format satu round:

```
❓ **Q1** - **<judul pertanyaan>**: <isi pertanyaan, bisa beberapa paragraf, termasuk pilihan ganda>

➡️ <jawaban rekomendasimu>

---

❓ **Q2** - **<judul pertanyaan>**: <isi pertanyaan, bisa beberapa paragraf, termasuk pilihan ganda>

➡️ <jawaban rekomendasimu>
```

Tiap round jawaban user membentuk ulang tree: keputusan yang beres mendorong frontier keluar dan membuka pertanyaan yang bergantung padanya. Hitung ulang frontier dan tanya round berikutnya. Pertanyaan yang jawabannya bergantung pada pertanyaan lain yang masih terbuka di round ini = round _berikutnya_, bukan round ini.

## Sambil bertanya, tulis dokumen

Baca glossary dan ADR yang sudah ada sebelum bertanya. Ikuti lokasi dan format repo. Jika folder proyek belum jelas, tanyakan lokasinya sebelum menulis.

Catat istilah yang sudah disepakati saat itu juga. Tawarkan ADR yang memenuhi kriteria di bawah; tulis setelah user menyetujui. Bedakan fakta kode saat ini dari keputusan desain yang diinginkan.

### Glossary

Tulis `GLOSSARY.md` di root repo. Repo banyak konteks: `GLOSSARY-MAP.md` di root menunjuk ke `GLOSSARY.md` tiap konteks.

```
**Order**:
Permintaan pelanggan yang dicatat dan dipenuhi sebagai satu kesatuan.
_Avoid_: Purchase, transaction
```

- Satu istilah: satu-dua kalimat, menjelaskan _apa_-nya, bukan _apa yang dilakukan_.
- Pilih satu kata kanonik; sinonim yang ditolak masuk `_Avoid_`.
- Hanya istilah khas proyek ini. Konsep umum pemrograman tidak masuk, walau sering dipakai.
- Bebas dari detail implementasi. Glossary bukan spesifikasi, bukan tempat catatan kerja.
- Buat filenya hanya saat istilah pertama benar-benar selesai.

### ADR

Tulis `docs/adr/0001-slug.md`, nomor urut. Isi: judul, lalu 1–3 kalimat berisi konteks, keputusan, dan alasannya. Satu paragraf cukup.

Tawarkan ADR hanya kalau **ketiganya** benar:

1. Sulit dibalik: ongkos berubah pikiran nanti nyata.
2. Mengejutkan tanpa konteks: pembaca nanti akan bertanya "kenapa begitu?".
3. Hasil trade-off nyata: ada alternatif sungguhan, dan satu dipilih dengan alasan.

Kurang satu saja: lewati. Buat folder `docs/adr/` hanya saat ADR pertama perlu.

## Selama sesi

- **Tantang istilah yang bentrok**: "Glossary Anda menyebut 'pembatalan' sebagai X, tapi Anda sepertinya maksudnya Y. Mana yang benar?"
- **Pertajam istilah kabur**: "'Akun' ini maksudnya Pelanggan atau Pengguna? Itu dua hal berbeda."
- **Uji dengan skenario konkret**: karang kasus tepi yang memaksa batas antar konsep jadi jelas.
- **Cocokkan dengan kode**: kalau ucapan user bertentangan dengan kode, sebutkan terang-terangan dan minta putusan.

## Aturan tetap

- Mencari _fakta_ tugasmu, bukan user: filesystem, kode, dokumen, tools. Dispatch sub-agent kalau perlu. _Keputusan_ milik user: sampaikan dan tunggu.
- Jangan block: tanya sisa frontier sekarang, dan biarkan pertanyaan hilir menunggu sub-agent lapor.
- Selama interview, hanya ubah dokumen istilah dan keputusan yang disepakati. Implementasi, konfigurasi, dan operasi layanan menunggu konfirmasi user setelah shared understanding tercapai.
- Saat frontier kosong, rangkum keputusan, file yang berubah, dan hal yang sengaja ditunda. Minta konfirmasi pemahaman bersama sebelum beralih ke implementasi.

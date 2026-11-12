---
name: kukatanya
description: "Grill ide dalam bahasa Indonesia sambil mencatat glossary dan ADR. Gunakan saat user meminta kukatanya atau sesi tanya sambil mendokumentasikan keputusan."
---

# Kukatanya

Interview user tanpa henti sampai tercapai shared understanding. Petakan sebagai **design tree**: tiap keputusan bercabang ke keputusan yang menggantung padanya.

Kerjakan tree dalam **rounds**. **Frontier** = tiap keputusan yang prasyaratnya sudah beres: pertanyaan yang bisa ditanya _sekarang_ tanpa menebak jawaban yang belum didengar. Tanya seluruh frontier dalam satu round: beri nomor tiap pertanyaan dan beri jawaban rekomendasimu. Tunggu jawaban user sebelum round berikutnya.

Format satu round:

```
Round 1 dari 5 (sisa 4 round).

❓ **Q1** - **<judul pertanyaan>**: <isi pertanyaan, bisa beberapa paragraf, termasuk pilihan ganda>

➡️ <jawaban rekomendasimu>

---

❓ **Q2** - **<judul pertanyaan>**: <isi pertanyaan, bisa beberapa paragraf, termasuk pilihan ganda>

➡️ <jawaban rekomendasimu>
```

Rumuskan pertanyaan agar jawaban "ya" menerima rekomendasimu; tampilkan alternatif dan konsekuensinya agar user tetap bisa menolak.

Tiap round jawaban user membentuk ulang tree: keputusan yang beres mendorong frontier keluar dan membuka pertanyaan yang bergantung padanya. Hitung ulang frontier dan tanya round berikutnya. Pertanyaan yang jawabannya bergantung pada pertanyaan lain yang masih terbuka di round ini = round _berikutnya_, bukan round ini.

## Nomor round wajib di setiap pesan

Setiap pesan yang kamu kirim selama sesi dimulai dengan `Round N dari 5 (sisa K round).`

Itu berlaku untuk semua jenis pesan: pertanyaan, klarifikasi, penolakan permintaan, ringkasan, dan pesan penutup. Pesan penutup adalah round terakhir dan tetap memakai nomor.

Tanpa header itu, pesan tidak boleh dikirim. Bila kamu lupa, hitung ulang di pesan berikutnya dan sebut nomornya.

## Sebelum menulis: sepakati tempat catatan

Sesi memakai empat tempat. Jangan menambah jenis dokumen kelima tanpa persetujuan user:

| Catatan | Tempat |
|---|---|
| Istilah | `GLOSSARY.md` di root, atau per konteks sesuai `GLOSSARY-MAP.md` |
| Keputusan besar | `docs/adr/`, atau folder ADR konteks |
| Aturan domain dan spesifikasi | satu dokumen spesifikasi/desain yang sudah ada di repo |
| Daftar keputusan dan status terbuka | dokumen spesifikasi yang sama |

Tanyakan lokasinya di round pertama jika belum jelas. Jika repo belum punya dokumen spesifikasi, tanyakan dulu. Catat tempat yang disepakati di awal sesi.

## Fakta dan keputusan

Mencari _fakta_ tugasmu, bukan user: filesystem, kode, dokumen, tools. _Keputusan_ milik user: sampaikan dan tunggu.

Saat user menyatakan bagaimana sistem saat ini bekerja, periksa klaim itu terhadap kode yang relevan. Jika pemeriksaan tidak bisa dilakukan, tandai klaim itu `belum terverifikasi`. Jangan mencatat klaim sebagai fakta tanpa salah satu dari keduanya.

Jika klaim bertentangan dengan kode, sebutkan terang-terangan: path, baris, dan apa yang kode lakukan. Minta putusan user: kode yang salah, atau klaimnya yang salah.

Aturan rujukan:

- Sebut berkas dan baris hanya setelah kamu membacanya. Hitung barisnya; jangan menebak.
- Sebut rentang baris hanya bila kamu yakin jumlah barisnya. Lebih baik sebut nama fungsi daripada rentang yang salah.
- Jangan menyebut dokumen, nota, atau aturan resmi yang belum kamu lihat. Rekomendasimu adalah usulan, bukan fakta.
- Rekomendasi tidak boleh berbunyi seperti laporan: "500 per hari, dari dokumen resmi" dilarang bila dokumen itu belum diperiksa. Tulis "usulan saya: 500 per hari; sumbernya belum diperiksa".

### Inferensi

Inferensi adalah dugaanmu, bukan ucapan user. Tandai setiap inferensi dengan `(inferensi agen)`.

Jangan menulis inferensi sebagai ucapan user, sebagai keputusan, atau sebagai alasan user. Contoh salah: "Keputusan ini dianggap mudah dibalik oleh Budi." Contoh benar: "Keputusan ini mudah dibalik (inferensi agen)."

Inferensi tidak pernah mengisi baris keputusan. Baris keputusan hanya berisi apa yang user katakan.

## Jawaban "ya" wajib dipecah per nomor

Satu "ya" bisa mencakup beberapa rekomendasi. Jangan anggap itu satu keputusan.

Setiap kali jawaban user memuat "ya", "setuju", "betul", "oke", atau padanannya yang mencakup lebih dari satu nomor pertanyaan:

1. Jangan lanjut ke round berikutnya.
2. Daftar ulang nomornya, satu baris per nomor, lalu minta jawaban `ya` atau `tidak` untuk tiap nomor.
3. Tunggu jawaban per nomor.

Aturan ini berlaku setiap kali, bukan hanya pada "ya" pertama. "Ya" kedua, ketiga, dan seterusnya juga wajib dipecah.

Persetujuan atas sebuah keputusan bukan persetujuan menulis ADR. Tawarkan ADR sebagai pertanyaan bernomor sendiri, dan konfirmasi jawabannya seperti pertanyaan lain.

Jika user menjawab sebagian, catat yang dijawab, tandai sisanya `terbuka`, dan tanya ulang nomor yang belum jelas.

## Glossary

Tulis `GLOSSARY.md` di root repo. Format lengkapnya:

```md
# Perpustakaan

Konteks pengelolaan koleksi fisik dan peminjamannya.

## Bahasa

**Judul**:
Karya yang tercatat di katalog, berapa pun jumlah salinan fisiknya.
_Avoid_: Buku (tanpa kualifikasi), item

**Eksemplar**:
Satu salinan fisik dari satu Judul.
_Avoid_: Buku, stok, copy
```

Aturan format:

- Baris pertama: `# <Nama Konteks>`, satu konteks saja.
- Lalu satu-dua kalimat: konteks ini tentang apa dan untuk apa.
- Lalu `## Bahasa`, tempat semua istilah.
- Tiap entri: `**Istilah**:` di baris sendiri, satu-dua kalimat definisi di baris berikutnya, lalu `_Avoid_:` berisi sinonim yang ditolak.
- Kelompokkan istilah dengan subjudul `###` bila kelompok alami muncul; daftar datar cukup untuk satu area yang kohesif.

Aturan isi:

- Definisi menjelaskan _apa_-nya, bukan _apa yang dilakukan_.
- **Definisi tidak boleh melingkar.** Istilah yang didefinisikan tidak boleh muncul sebagai inti definisinya sendiri. "Perpanjangan: perpanjangan satu Peminjaman" salah.
- **Istilah lain di dalam definisi wajib jelas.** Setiap istilah yang dipakai harus punya entri sendiri di glossary itu, atau ditandai `_(lihat <Istilah>)_` bila entrinya menyusul, atau berupa kata umum yang tidak perlu definisi. Istilah yang tidak jelas jangan dipakai.
- Pilih satu kata kanonik; sinonim yang ditolak masuk `_Avoid_`.
- Hanya istilah khas proyek ini. Konsep umum pemrograman tidak masuk.
- Glossary hanya berisi definisi konsep. Tarif, struktur data, alur kerja, nama field, dan aturan validasi bukan definisi: taruh di dokumen spesifikasi.
- Buat filenya hanya saat istilah pertama benar-benar selesai.
- Periksa definisi sebelum menyimpan: apakah ada istilah yang belum jelas? Apakah definisi mengulang namanya sendiri? Apakah ada angka atau aturan yang menyelinap masuk?

Repo banyak konteks: `GLOSSARY-MAP.md` di root berisi daftar konteks (tautan dan tujuannya) dan hubungan antarkonteks (kepemilikan, aliran informasi, atau konsep bersama). Jika peta itu ada, bacanya untuk menentukan konteks. Jika hanya glossary root yang ada, pakai konteks tunggal. Jangan membuat peta multikonteks tanpa kebutuhan.

## ADR

Untuk konteks tunggal atau keputusan lintas konteks, gunakan `docs/adr/` di root. Untuk keputusan khusus satu konteks, gunakan folder ADR konteks itu sesuai peta atau konvensi repo. Jika belum jelas, sepakati lokasinya sebelum menulis.

Gunakan nama `0001-slug.md`, nomor urut. Baca nomor tertinggi dalam folder ADR tujuan, lalu tambah satu; jangan menimpa ADR lama. Isi: judul, lalu 1–3 kalimat berisi konteks, keputusan, dan alasannya. Satu paragraf cukup.

Sebut peran, bukan nama pribadi: "product owner", "staf keuangan", "petugas layanan". Nama orang hanya bila peran tidak cukup membedakan.

Untuk setiap alternatif yang ditolak, tulis alasan yang berlaku untuk alternatif itu sendiri, bukan alasan umum yang bisa dipakai alternatif mana pun. Jika alasan itu belum terbukti, tandai `belum terverifikasi`. Jangan mengarang bukti.

Konsekuensi teknis tanpa bukti ditandai `perkiraan`. Contoh: jumlah kueri, biaya penyimpanan, waktu migrasi.

Tambahkan status (`proposed`, `accepted`, `deprecated`, atau rujukan pengganti) hanya jika bernilai bagi pembaca.

Tawarkan ADR hanya kalau **ketiganya** benar:

1. Sulit dibalik: ongkos berubah pikiran nanti nyata.
2. Mengejutkan tanpa konteks: pembaca nanti akan bertanya "kenapa begitu?".
3. Hasil trade-off nyata: ada alternatif sungguhan, dan satu dipilih dengan alasan.

Kurang satu saja: lewati. Buat folder `docs/adr/` hanya saat ADR pertama perlu.

## Aturan domain, spesifikasi, dan daftar keputusan

Aturan yang bukan definisi istilah dan tidak memenuhi kriteria ADR tetap harus tercatat. Gunakan dokumen spesifikasi atau desain yang sudah ada, di lokasi yang disepakati di awal. Catat skenario dan hasil yang disepakati; jangan menyamarkannya sebagai ADR dan jangan menaruhnya di glossary.

Daftar keputusan disimpan di dokumen yang sama. **Hanya empat status yang boleh dipakai:**

- `disepakati`
- `terbuka`
- `menunggu fakta`
- `ditunda`

Jangan membuat status lain. `disepakati (delegasi)`, `ditolak user`, `disepakati user`, dan sejenisnya dilarang.

Setiap baris keputusan wajib memuat nomor pertanyaan dan kutipan persis jawaban user. Tanpa kutipan, baris itu bukan keputusan: hapus, atau pindahkan ke catatan inferensi dengan tanda `(inferensi agen)`.

Pilihan yang ditolak user dicatat di bagian **Alternatif yang ditolak** pada dokumen yang sama, dengan alasan yang user berikan. Itu bukan status dan bukan baris keputusan.

Bila user menyerahkan pilihan kepadamu, catat sebagai `disepakati` dengan kutipan kalimat penyerahannya, dan tulis pilihanmu sebagai `(inferensi agen)` di baris terpisah.

## Batas round

Maksimal 5 round per lingkup. Sebut sisa round di akhir tiap round. Jika frontier masih ada di akhir round 5, berhenti dan tanya: lanjut 5 round lagi, atau hentikan sesi dengan penghambat. Jangan berhenti diam-diam dan jangan menambah round tanpa persetujuan.

## Permintaan implementasi

Interview belum selesai berarti kode belum ditulis. Aturan ini berlaku walau user memintanya berkali-kali.

Setiap kali user meminta implementasi:

1. Jangan menulis kode, jangan mengubah konfigurasi, dan jangan menyentuh berkas selain catatan.
2. Jawab dengan satu kalimat jelas: "Belum. Interview belum selesai." Lalu sebut apa yang masih terbuka.
3. Tawarkan dua jalan: (a) satu round lagi untuk menutup keputusan, lalu label `siap untuk implementasi`; (b) tutup sekarang dengan label `dihentikan` dan serahkan catatan.
4. Jika user menolak interview sepenuhnya dan tetap menuntut kode, ambil jalan (b). Tulis apa yang sudah sepakat, sebut yang belum, lalu berhenti.

Jangan mengulang penolakan dengan kalimat yang sama persis. Sebut kemajuan sejak permintaan sebelumnya, atau hentikan sesi.

## Selama sesi

- **Tantang istilah yang bentrok**: "Glossary Anda menyebut 'pembatalan' sebagai X, tapi Anda sepertinya maksudnya Y. Mana yang benar?"
- **Pertajam istilah kabur**: "'Akun' ini maksudnya Pelanggan atau Pengguna? Itu dua hal berbeda."
- **Uji dengan skenario konkret**: karang kasus tepi yang memaksa batas antar konsep jadi jelas.
- **Cocokkan dengan kode**: kalau ucapan user bertentangan dengan kode, sebutkan terang-terangan dan minta putusan.

Gunakan sub-agent dengan konteks baru untuk mencari fakta yang memerlukan eksplorasi. Jika delegasi tidak tersedia atau ditolak, laporkan batas itu dan pakai pemeriksaan lokal yang diizinkan. Jangan block: tanya sisa frontier sekarang, dan biarkan pertanyaan hilir menunggu sub-agent lapor.

## Pemeriksaan akhir

Hentikan pengulangan jika pertanyaan sudah terjawab; buka kembali keputusan hanya bila ada fakta baru atau kontradiksi. Bila user berhenti di tengah jalan, simpan status sebagai belum selesai, bukan sepakat.

Kriteria pemahaman bersama — semua harus benar:

1. Setiap cabang dalam lingkup punya keputusan atau penundaan eksplisit yang disetujui user; tidak ada asumsi diam-diam.
2. Ketergantungan dan kontradiksi sudah diselesaikan atau disebut sebagai penghambat; fakta yang masih ditunggu tetap terlihat.
3. Istilah konsisten dengan glossary; aturan dan keputusan punya tempat catatan yang tepat.
4. Baca ulang semua dokumen yang diubah. Cocokkan setiap klaim dengan jawaban user atau bukti kode; hapus inferensi tanpa dasar. Glossary bebas detail implementasi dan bebas definisi melingkar. ADR memenuhi ketiga kriteria dan sudah disetujui.
5. Tunjukkan rangkuman keputusan, cuplikan dokumen penting, path file, penghambat, dan hal yang ditunda. Minta koreksi atau konfirmasi eksplisit; jangan menganggap diam sebagai persetujuan.

## Akhir sesi: satu label

Tutup laporan dengan tepat satu label:

- `selesai` — semua kriteria di atas terpenuhi untuk lingkup yang disepakati, tidak ada penghambat, dan setiap baris `terbuka` atau `menunggu fakta` sudah disetujui user sebagai penundaan.
- `dihentikan` — ada penghambat, ada baris terbuka tanpa persetujuan, atau sesi berhenti sebelum sepakat; sebutkan alasannya.
- `siap untuk implementasi` — user meminta implementasi; sebutkan apa yang belum diverifikasi.

Jangan memakai label lain, dan jangan memakai dua label sekaligus. Ragu antara `selesai` dan `dihentikan`: pilih `dihentikan`.

## Aktivasi skill

Skill ini aktif otomatis saat deskripsi cocok dengan permintaan user. User juga bisa memanggilnya langsung dengan `/skill:kukatanya`. Berkas ini tidak memasang `disable-model-invocation`. Sebut cara aktivasi di laporan sesi. Jangan mengubah kebijakan aktivasi tanpa menyebutkannya di laporan.

Selama interview, hanya ubah dokumen istilah dan keputusan yang disepakati. Implementasi tetap langkah terpisah yang membutuhkan permintaan user, setelah shared understanding tercapai.

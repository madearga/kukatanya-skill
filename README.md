# kukatanya

Skill Agent Skills yang menuntun sesi tanya jawab mendalam tentang ide yang ingin kamu buat. Agent bertanya dalam beberapa round sampai paham betul maksudmu, lalu mencatat istilah dan keputusan ke berkas di repo. Kompatibel dengan agent yang mendukung format Agent Skills (`SKILL.md`): Pi, Claude Code, Codex, dan agent lain yang membaca `~/.agents/skills`.

## Apa fungsinya

- Memetakan ide sebagai pohon keputusan, lalu menanyakan semua pertanyaan yang siap dijawab sekarang.
- Maksimal 5 round per lingkup, jadi sesi tidak berputar-putar.
- Mencatat istilah ke `GLOSSARY.md` dan keputusan besar ke `docs/adr/`.
- Membedakan fakta dari kode dan keputusan dari kamu. Tebakan agent ditandai `(inferensi agen)`.
- Belum menulis kode selama tanya jawab belum selesai.

## Struktur repo

```text
skills/kukatanya/SKILL.md
package.json
```

`SKILL.md` adalah satu-satunya berkas yang dibutuhkan skill-nya.

## Cara install

### Pi

Cara 1 — `pi install` (butuh `package.json`, sudah ada di repo ini):

```bash
pi install git:github.com/madearga/kukatanya-skill
```

Cara 2 — salin manual ke `~/.pi/agent/skills/kukatanya` (jalur terverifikasi dari dokumentasi resmi Pi):

```bash
TMP=$(mktemp -d)
git clone --depth 1 https://github.com/madearga/kukatanya-skill.git "$TMP/kukatanya"
mkdir -p ~/.pi/agent/skills
cp -r "$TMP/kukatanya/skills/kukatanya" ~/.pi/agent/skills/kukatanya
```

Buka Pi, jalankan `/reload` bila sesi sudah berjalan, lalu panggil `/skill:kukatanya` (perintah Pi). Skill ini juga aktif otomatis saat permintaanmu cocok dengan deskripsinya.

Pi juga membaca lokasi standar Agent Skills `~/.agents/skills/` (terverifikasi dari dokumentasi Pi).

### Claude Code

Salin folder `skills/kukatanya` ke:

- Personal: `~/.claude/skills/kukatanya`
- Proyek: `.claude/skills/kukatanya` di root proyek

Kedua jalur di atas berasal dari dokumentasi Claude Code yang umum dikenal, tapi **belum saya verifikasi langsung dari dokumentasi resmi terbaru**. Uji dengan `/skill` atau tanya agent setelah disalin.

### Codex dan agent lain (lokasi `~/.agents/skills`)

Salin folder `skills/kukatanya` ke:

```bash
mkdir -p ~/.agents/skills
cp -r skills/kukatanya ~/.agents/skills/kukatanya
```

Pi terverifikasi membaca lokasi ini. Untuk Codex dan agent lain, **belum terverifikasi** — cek dokumentasi agent masing-masing.

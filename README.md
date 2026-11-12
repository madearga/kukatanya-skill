# kukatanya

Skill untuk Pi yang menuntun sesi tanya jawab tentang ide yang ingin kamu buat. Agent bertanya dalam beberapa round sampai paham betul maksudmu, lalu mencatat istilah dan keputusan ke berkas di repo.

## Apa fungsinya

- Memetakan ide sebagai pohon keputusan, lalu menanyakan semua pertanyaan yang siap dijawab sekarang.
- Maksimal 5 round per lingkup, jadi sesi tidak berputar-putar.
- Mencatat istilah ke `GLOSSARY.md` dan keputusan besar ke `docs/adr/`.
- Membedakan fakta dari kode dan keputusan dari kamu. Tebakan agent ditandai `(inferensi agen)`.
- Belum menulis kode selama tanya jawab belum selesai.

## Cara install di Pi

Letakkan folder ini di direktori skill Pi, dengan nama folder `kukatanya`:

```bash
TMP=$(mktemp -d)
git clone --depth 1 https://github.com/madearga/kukatanya-skill.git "$TMP/kukatanya"
mkdir -p ~/.pi/agent/skills
cp -r "$TMP/kukatanya" ~/.pi/agent/skills/kukatanya
```

Buka Pi, jalankan `/reload` bila sesi sudah berjalan, lalu panggil:

```
/skill:kukatanya
```

Skill ini juga aktif otomatis saat permintaanmu cocok dengan deskripsinya, misalnya "kukatanya" atau sesi tanya jawab yang perlu dicatat keputusannya.

## Berkas

- `SKILL.md` — instruksi skill. Itu satu-satunya berkas yang dibutuhkan.

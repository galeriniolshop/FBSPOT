# 🎬 YT Grabber — Streamlit Cloud Edition

Mesin pencari & pengunduh video YouTube (judul, deskripsi, tags, views)
lengkap dengan upload otomatis ke **febspot.com** (kanal milikmu) dan/atau **gofile.io**.
File unduhan **selalu dihapus otomatis** setelah terupload.

## 📦 Isi paket

| File | Fungsi |
|---|---|
| `streamlit_app.py` | UI Streamlit (cari → info → download → upload) |
| `yt_tool.py` | Mesin inti (yt-dlp + gofile + febspot) |
| `requirements.txt` | Dependensi |
| `.streamlit/config.toml` | Tema gelap |

> ⚠️ `febspot_cookies.json` **tidak** disertakan — cookies dimasukkan lewat
> **Streamlit Secrets** (jangan pernah commit cookies ke GitHub!).

## 🚀 Langkah deploy

1. **Push ke GitHub**

   ```bash
   git init
   git add streamlit_app.py yt_tool.py requirements.txt .streamlit/config.toml README.md
   git commit -m "YT Grabber Streamlit"
   git branch -M main
   git remote add origin https://github.com/<username>/<repo>.git
   git push -u origin main
   ```
   (atau upload file via web GitHub → *Add file → Upload files*)

2. **Buka https://share.streamlit.io** → *New app* → pilih repo kamu
   → Main file path: `streamlit_app.py` → **Deploy**

3. **Isi Secrets** (Apps → Settings → Secrets):
   ```toml
   febspot_cookies = [
     { "domain": ".febspot.com", "name": "user_id", "value": "..." },
     { "domain": ".febspot.com", "name": "kt_member", "value": "..." },
     { "domain": ".febspot.com", "name": "PHPSESSID", "value": "..." },
     { "domain": ".febspot.com", "name": "time", "value": "..." }
   ]
   febspot_channel = "60404"
   ```
   Ambil nilai cookie dari browser (extension *EditThisCookie* / *Cookie-Editor*
   di febspot.com saat sudah login). Minimal yang wajib:
   `kt_member`, `PHPSESSID`, `user_id`, `time`.

4. **Selesai** 🎉 — buka URL app-mu.

## 🖥️ Cara pakai

- **🔎 Cari** — ketik kata kunci → daftar video (judul, views, durasi, channel).
  Tombol **📋 Info** menampilkan deskripsi + tags lengkap.
- **⬇️ Ambil** — download video yang dipilih → upload sesuai tujuan di sidebar
  (febspot / gofile.io / keduanya) → link muncul di atas.
- **🤖 Biar Mesin Saja** — sekali klik: cari → pilih video terpendek →
  download → upload → beres. Paling hemat resource.
- Sidebar: pilih format **MP4/MP3**, tujuan upload, jumlah hasil.

## ⚠️ Batasan Streamlit Cloud (free)

- **1 GB RAM** — hindari video > ~400 MB; gunakan mode 🤖 (terpendek).
- **Idle sleep** ±30–45 menit; cold start ±15 detik saat dibuka lagi.
- **Jangan tutup tab** saat job sedang berjalan.
- IP cloud (GCP) kadang lebih ketat terhadap bot-check YouTube.

Untuk pemakaian berat (video panjang, banyak job), deploy versi Flask
(`app.py` + `index.html`) ke Railway/Render/VPS lebih cocok.

## 🔒 Catatan

- Gunakan hanya untuk konten yang kamu berhak unggah/dipakai.
- Video yang di-upload ke febspot harus lolos moderasi/review kanal.

# Panduan Split & Join File Besar (macOS & Windows)

> **Antigravity Version:** `v2.11.0`

Dokumen ini berisi panduan umum langkah demi langkah untuk memotong (*split*) dan menggabungkan kembali (*join*) file berukuran besar (misalnya installer/archive `.zip`, `.exe`, `.tar.gz`, dll.) agar mudah diunggah atau ditransfer. Panduan ini mencakup cara tanpa aplikasi tambahan (menggunakan Terminal di macOS & CMD di Windows) serta menggunakan aplikasi GUI (Keka & 7-Zip).

---

## 1. Metode CLI (Tanpa Aplikasi Tambahan)

### A. Memotong File di macOS / Linux (Terminal)

Buka **Terminal** (`Cmd + Space`, ketik `Terminal`) dan navigasi ke folder tempat file Anda berada (`cd /path/to/folder`).

Gunakan perintah `split` dengan format:
```bash
split -b [ukuran] [nama_file_asli] [prefix_output]
```

**Contoh Penggunaan:**
* **Memotong file per 50 MB:**
  ```bash
  split -b 50m Antigravity-x64.exe.zip agy_part_
  ```
* **Memotong file per 500 MB:**
  ```bash
  split -b 500m app-installer.zip app_part_
  ```
* **Memotong file per 1 GB:**
  ```bash
  split -b 1g bigfile.zip part_
  ```

> **Catatan Output:** Terminal akan menghasilkan beberapa bagian file secara berurutan, seperti: `agy_part_aa`, `agy_part_ab`, `agy_part_ac`, dst.

---

### B. Menggabungkan File di Windows (PowerShell & Command Prompt / CMD)

1. Pindahkan **semua file bagian** (`agy_part_aa`, `agy_part_ab`, `agy_part_ac`, dst.) ke dalam **satu folder yang sama** di Windows.
2. Buka folder tersebut di **File Explorer**.
3. Klik pada *address bar* (jalur folder) di bagian atas, ketik `powershell` atau `cmd`, lalu tekan **Enter**.
4. Jalankan perintah penggabungan:

   * **Di PowerShell (Rekomendasi Cepat & Praktis):**
     ```powershell
     cmd /c "copy /b [prefix_output]* [nama_file_hasil.ekstensi]"
     ```
     *Contoh:* `cmd /c "copy /b agy_part_* Antigravity-x64.exe.zip"`

   * **Di PowerShell (Native PS 5.1+):**
     ```powershell
     Get-Content agy_part_* -Encoding Byte -ReadCount 0 | Set-Content Antigravity-x64.exe.zip -Encoding Byte
     ```

   * **Di Command Prompt (CMD):**
     ```cmd
     copy /b [prefix_output]* [nama_file_hasil.ekstensi]
     ```
     *Contoh:* `copy /b agy_part_* Antigravity-x64.exe.zip`

5. Tunggu proses penggabungan hingga selesai. File siap dibuka/diekstrak.

---

### C. Menggabungkan File di macOS / Linux (Terminal)

1. Buka Terminal dan masuk ke folder tempat file bagian disimpan.
2. Jalankan perintah `cat`:
   ```bash
   cat [prefix_output]* > [nama_file_hasil.ekstensi]
   ```

**Contoh Penggunaan:**
```bash
cat agy_part_* > Antigravity-x64.exe.zip
```

---

## 2. Metode GUI (Menggunakan Aplikasi)

### A. macOS (Menggunakan Keka)

* **Memotong File:**
  1. Buka aplikasi **Keka**.
  2. Pada panel opsi pemotongan (*Split*), tentukan ukuran bagian (misal: *50MB*, *500MB*, *1000MB*).
  3. Drag & drop file yang ingin dipotong ke jendela Keka.
  4. Keka akan membuat file bagian dengan format `.zip.001`, `.zip.002`, dst.
* **Menggabungkan File:**
  1. Letakkan semua bagian `.001`, `.002`, dst. dalam satu folder.
  2. Drag & drop file bagian pertama (`.001`) ke Keka. Keka akan otomatis menggabungkan dan mengekstrak isi filenya.

---

### B. Windows (Menggunakan 7-Zip)

* **Menggabungkan File:**
  1. Pastikan seluruh file bagian (`.001`, `.002`, atau `agy_part_aa`, `agy_part_ab`, dst.) berada dalam satu folder yang sama.
  2. Klik kanan pada file bagian pertama (`.001` atau `agy_part_aa`).
  3. Pilih **7-Zip > Extract Here** (atau *Extract to...*).
  4. 7-Zip akan secara otomatis menyambung seluruh bagian file dan mengekstraknya.

---

## 💡 Tips & Verifikasi

- **Verifikasi Keutuhan File (Checksum):**
  Untuk memastikan file hasil gabungan sama persis dengan file asli, Anda dapat mencocokkan nilai SHA-256 hash:
  - **macOS / Linux:** `shasum -a 256 nama_file.zip`
  - **Windows (PowerShell):** `Get-FileHash nama_file.zip -Algorithm SHA256`

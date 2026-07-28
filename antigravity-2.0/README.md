# Panduan Split & Join File (macOS & Windows)

Dokumen ini berisi panduan langkah demi langkah untuk memotong (*split*) dan menggabungkan (*join*) file besar (seperti `Antigravity-x64.exe.zip`) di macOS dan Windows tanpa aplikasi pihak ketiga maupun menggunakan aplikasi GUI.

---

## Informasi File

- **Versi:** `v2.11.0`
- **File Asli:** `Antigravity-x64.exe.zip`
- **Prefix File Bagian:** `agy_part_`
- **Ukuran per Bagian:** `50MB`
- **Daftar File Bagian saat ini:**
  - `agy_part_aa` (50 MB)
  - `agy_part_ab` (50 MB)
  - `agy_part_ac` (~40.8 MB)

---

## Metode 1: Menggunakan Terminal & Command Prompt (Tanpa Aplikasi)

### A. Cara Memotong File di macOS (Terminal)

1. Buka **Terminal** di Mac (`Cmd + Space`, ketik `Terminal`).
2. Masuk ke folder tempat file disimpan:
   ```bash
   cd /path/to/folder
   ```
3. Jalankan perintah `split`:
   ```bash
   split -b 50m Antigravity-x64.exe.zip agy_part_
   ```
   * **Ukuran:** Bisa pakai `m` untuk Megabyte atau `g` untuk Gigabyte. Contoh: `50m`, `500m`, `1g`.
   * Terminal akan menghasilkan bagian-bagian file berturut-turut seperti `agy_part_aa`, `agy_part_ab`, `agy_part_ac`, dst.

---

### B. Cara Menggabungkan File di Windows (PowerShell & Command Prompt / CMD)

1. Pindahkan **semua** file bagian (`agy_part_aa`, `agy_part_ab`, `agy_part_ac`, dst.) ke dalam **satu folder yang sama** di Windows.
2. Buka folder tersebut di **File Explorer**.
3. Klik pada *address bar* bagian atas folder, ketik `powershell` (atau `cmd`), lalu tekan **Enter**.
4. Jalankan perintah penggabungan:

   * **PowerShell (Rekomendasi Cepat & Praktis):**
     ```powershell
     cmd /c "copy /b agy_part_* Antigravity-x64.exe.zip"
     ```

   * **PowerShell (Native PS 5.1+):**
     ```powershell
     Get-Content agy_part_* -Encoding Byte -ReadCount 0 | Set-Content Antigravity-x64.exe.zip -Encoding Byte
     ```

   * **Command Prompt (CMD):**
     ```cmd
     copy /b agy_part_* Antigravity-x64.exe.zip
     ```
5. Tunggu prosesnya selesai hingga muncul pemberitahuan file berhasil digabungkan. File `Antigravity-x64.exe.zip` sudah utuh kembali dan siap dibuka/diekstrak.

---

### C. Cara Menggabungkan File di macOS (Terminal)

Jika ingin menggabungkan kembali file bagian di macOS tanpa aplikasi tambahan:
```bash
cat agy_part_* > Antigravity-x64.exe.zip
```

---

## Metode 2: Menggunakan Aplikasi GUI (Keka / 7-Zip)

### A. Memotong & Menggabungkan di macOS (Keka)

* **Memotong File:**
  1. Buka aplikasi **Keka**.
  2. Tentukan ukuran pemotongan pada opsi **Split** (misal *50MB*).
  3. Drag & drop file kamu ke jendela Keka.
  4. Keka akan menghasilkan file `.zip.001`, `.zip.002`, `.zip.003`, dst.

* **Menggabungkan File:**
  1. Drag & drop file bagian pertama ke Keka untuk mengekstrak/menggabungkannya secara otomatis.

---

### B. Memotong & Menggabungkan di Windows (7-Zip)

* **Menggabungkan File:**
  1. Pastikan semua file `.001`, `.002`, atau `agy_part_aa`, dst. ada di folder yang sama.
  2. Klik kanan pada file bagian pertama (`agy_part_aa` atau `.001`).
  3. Pilih **7-Zip > Extract Here** (atau *Extract to...*). File akan otomatis digabungkan dan diekstrak.

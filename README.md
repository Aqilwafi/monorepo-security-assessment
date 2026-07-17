# Monorepo Security Assessment

Repo ini berisi dokumentasi hasil security assessment dalam format temuan yang konsisten.

## Daftar Temuan

- `SEC-001` — [Edge Function Authentication](security/SEC-001-edge-function-auth.md): opsi *Verify JWT* dinonaktifkan sehingga endpoint dapat diakses tanpa JWT. (Sudah diperbaiki.)
- `SEC-002` — [Header Spoofing Validation](security/SEC-002-header-spoofing-validation.md): validasi terhadap manipulasi header IP menunjukkan aplikasi tidak menggunakan nilai IP yang dikirim oleh client.

## Assessment Context

Assessment dilakukan terhadap aplikasi yang dikembangkan secara internal oleh pemilik repository ini.

Project utama:
- Status: Development / Staging
- Repository aplikasi: Private
- Environment pengujian: Dev & Staging (production-like environment)

Security assessment dilakukan sebagai bagian dari proses development untuk mengidentifikasi, memvalidasi, dan memperbaiki potensi risiko keamanan sebelum deployment production.

Pemilik project memberikan izin untuk:
- melakukan security testing terhadap aplikasi;
- melakukan validasi konfigurasi dan implementasi keamanan;
- mendokumentasikan hasil assessment;
- mempublikasikan hasil assessment dalam bentuk portfolio dengan tetap memperhatikan penghapusan data sensitif.

## Disclosure Notice

Repository ini hanya berisi dokumentasi security assessment.

Source code aplikasi secara keseluruhan, konfigurasi deployment internal, credential, secret key, environment variable, dan informasi sensitif lainnya tidak dipublikasikan.

Beberapa potongan kode yang relevan dengan temuan dapat ditampilkan sebagai evidence untuk menjelaskan konteks implementasi dan proses validasi keamanan.

Seluruh evidence telah ditinjau dan tidak mengandung credential, token, secret, atau informasi yang dapat digunakan untuk mengakses sistem secara tidak sah.

## Struktur

- `security/` : Daftar temuan security.
- `pictures/` : Penyimpanan evidence berbasis file image.

## Format Dokumen Temuan

Setiap temuan mengikuti pola:

- **Status**: Open / Fixed / Verified
- **Risk**: tingkat risiko
- **Finding**: ringkasan isu
- **Impact**: dampak jika dibiarkan
- **Recommendation / Remediation**: langkah perbaikan
- **Evidence**: bukti sebelum/sesudah (log, screenshot, referensi)
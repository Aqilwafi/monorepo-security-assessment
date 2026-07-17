# Monorepo Security Assessment

Repo ini berisi dokumentasi hasil security assessment dalam format temuan yang konsisten.

## Daftar Temuan
- `SEC-001` — [Edge Function Authentication](security/SEC-001-edge-function-auth.md): opsi *Verify JWT* dinonaktifkan sehingga endpoint dapat diakses tanpa JWT. (Sudah diperbaiki.)

## Struktur
- `security/` : Daftar temuan security (mis. `SEC-001-*`).

## Format Dokumen Temuan
Setiap temuan mengikuti pola:
- **Status**: Open / Fixed / Verified
- **Risk**: tingkat risiko
- **Finding**: ringkasan isu
- **Impact**: dampak jika dibiarkan
- **Recommendation / Remediation**: langkah perbaikan
- **Evidence**: bukti sebelum/sesudah (log, screenshot, referensi)

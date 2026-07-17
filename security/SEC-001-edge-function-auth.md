# SEC-001 - Edge Function Authentication

## Status
- [ ] Open
- [v] Fixed
- [ ] Verified

## Risk
Low

## Finding
Edge Function dikonfigurasi dengan opsi Verify JWT dinonaktifkan sehingga endpoint dapat diakses tanpa autentikasi JWT.

## Impact
Endpoint dapat dipanggil oleh pihak yang tidak terautentikasi sehingga meningkatkan risiko penyalahgunaan, seperti request flooding, konsumsi invocation yang berlebihan, dan penggunaan resource yang dapat mempercepat habisnya kuota layanan.

## Recomendation
### Remediation:
Aktifkan opsi Verify JWT pada Edge Function agar setiap request harus menyertakan JWT yang valid sebelum fungsi dieksekusi

## Evidence
### before
- Source: Supabase Edge Function Settings
- Log / Screenshot: Konfigurasi Verify dalam keadaan mati/off.
![Screenshot1](../pictures/Screenshot-2026-07-16-232510.png)
### after
- Source: Supabase Edge Function Settings
- Log / Screenshot: Konfigurasi Verify sudah diaktifkan.
keadaan mati/off.
![Screenshot1](../pictures/Screenshot-2026-07-17-093704.png)
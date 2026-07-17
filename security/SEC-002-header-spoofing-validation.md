# SEC-002 - Header Spoofing Validation

- ditemukan: 17/07/2026
- diperbaiki: N/A

## Scope
- Repository: spmb-baitunnaim
- Component: Next.js Server Action / Login Audit Logging
- Environment: Staging

## Status
- [x] Open
- [ ] Resolved

## Risk
Informational

## Finding

Dilakukan pengujian terhadap mekanisme pencatatan IP address pada proses login untuk memastikan header IP yang bersifat client-controlled tidak dapat dimanipulasi secara langsung oleh pengguna.

Pengujian dilakukan dengan memodifikasi beberapa HTTP header yang umum digunakan untuk forwarding IP:

- `X-Forwarded-For`
- `X-Real-IP`
- `Forwarded`

Hasil pengujian menunjukkan bahwa nilai IP yang diterima oleh aplikasi tidak menggunakan nilai yang dikirim oleh client, melainkan tetap menggunakan IP publik aktual dari request.

## Impact

Tidak ditemukan dampak keamanan pada implementasi saat ini.

Mekanisme reverse proxy / edge layer melakukan normalisasi terhadap header IP sebelum request diteruskan ke aplikasi sehingga upaya spoofing menggunakan header HTTP tidak berhasil.

Jika konfigurasi deployment berubah dan aplikasi dapat menerima request langsung tanpa melalui trusted proxy, maka header tersebut berpotensi menjadi sumber IP palsu.

## Recommendation

### Remediation / Hardening:

- Pastikan aplikasi selalu berada di belakang trusted proxy atau load balancer.
- Jangan membuka akses langsung ke origin server.
- Dokumentasikan sumber header IP yang dipercaya (`X-Real-IP`, `X-Forwarded-For`, atau header provider tertentu).
- Lakukan validasi ulang apabila arsitektur deployment berubah.

## Evidence

#### Evidence 1
- Source: Source Code
- Description: Tes mendapatkan ip pakai `console.log` untuk persiapan implementasi audit/logs.

    ```ts
    const headersList = await headers();

    const ip = 
        headersList.get("x-forwarded-for")?.split(",")[0]?.trim() ??
        headersList.get("x-real-ip") ??
        null;

    const userAgent = headersList.get("user-agent");

    console.log("LOGIN AUDIT", {
        ip,
        userAgent,
        forwardedFor: headersList.get("x-forwarded-for"),
        realIp: headersList.get("x-real-ip"),
    });
    ```

#### Evidence 2
- Source: Burp Suite Repeater
- Description: Pengujian manipulasi `X-Forwarded-For`, `X-Real-IP`, dan `Forwarded`.

    Request:

    ```http
    User-Agent: Pentester?
    X-Forwarded-For: 127.0.0.1, 8.8.8.8
    X-Real-IP: 127.0.0.1
    Forwarded: for=127.0.0.1
    ```

#### Evidence 3
- Source: Vercel Log
- Description: Server tetap mencatat IP aktual dan tidak menggunakan nilai spoofed header.

    ```sh
    2026-07-17 09:15:56.970 [info] LOGIN AUDIT {
                                                ip: '114.5.232.106',
                                                userAgent: 'Pentester?',
                                                forwardedFor: '114.5.232.106',
                                                realIp: '114.5.232.106'
                                            }
    ```

#### Evidence 4
- Source: Terminal WSL
- Description: cURL IP publik.

    ```cmd
    ~$ curl ifconfig.me; echo
    114.5.232.106
    ```
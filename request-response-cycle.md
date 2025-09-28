# Network I/O and Processing Workflow

## **Pengiriman request (request time)**

> Dari browser kamu ke server lewat jaringan (tergantung jarak, latency).

## **Pengambilan data dari disk server (disk IO)**

> Server baca file/data yang diperlukan dari storage (HDD/SSD).

## **Pengambilan data dari RAM server (jika sudah di-cache)**

> Kalau data sudah ada di RAM langsung kirim ke CPU server, ini jauh lebih cepat dari disk ke RAM baru ke CPU server.

## **Proses di CPU server**

> Server memproses data, menjalankan logika aplikasi, generate response.

## **Waktu pengiriman response dari server ke browser**

> Lewat jaringan, termasuk latency dan kecepatan bandwidth.

## **Response diterima dan disimpan di RAM lokal (client-side)**

> Browser menerima data HTTP response, menyimpan di RAM komputer kamu.

## **Proses di CPU lokal (browser parsing, render, eksekusi JavaScript, dll)**

> Browser memproses data untuk ditampilkan.

------

# Algoritma

Kalau dari sisi algoritma, bagian-bagian spesifik dalam proses itu bisa melibatkan algoritma seperti:

- **Algoritma cache management** (LRU, LFU, dll)
- **Algoritma routing jaringan**
- **Algoritma parsing HTML dan JavaScript**
- **Algoritma kompresi/dekompresi data**
- **Algoritma scheduling CPU**

------

# Total Waktu 

$$
T_{request} + T_{disk} + T_{RAM-server} + T_{CPU-server} + T_{response} + T_{RAM-client} + T_{CPU-client}
$$

> [!NOTE]
>
> - T_request→ Waktu pengiriman request
> - T_disk → Waktu pengambilan data dari disk server (disk IO)
> - T_RAM-server → Waktu pengambilan data dari RAM server 
> - T_CPU-server → Waktu proses di CPU server
> - T_response → Waktu pengiriman response dari server ke browser
> - T_RAM-client→ Response diterima dan disimpan di RAM lokal (client-side)
> - T_CPU-client→ Proses di CPU lokal (browser parsing, render, eksekusi JavaScript, dll)

------

# Contoh kasus :

> - **Server ada di CDN Singapura**
> - **Client ada di Depok, Jawa Barat, Indonesia**

## Estimasi setiap komponen waktu (nilai ini perkiraan kasar, real-nya bisa bervariasi):

| Komponen            | Keterangan                                | Estimasi Waktu                           |
| ------------------- | ----------------------------------------- | ---------------------------------------- |
| **T_request**       | Waktu request dari Depok ke Singapura     | ~20 ms (one-way)                         |
| **T_disk (server)** | Baca data dari disk di server (SSD)       | ~5 ms                                    |
| **T_RAM-server**    | Ambil data dari RAM server (cache hit)    | ~1 ms                                    |
| **T_CPU-server**    | Proses data di server (generate response) | ~10 ms                                   |
| **T_response**      | Response dari Singapura ke Depok          | ~20 ms (one-way)                         |
| **T_RAM-client**    | Terima response dan simpan di RAM client  | ~1 ms                                    |
| **T_CPU-client**    | Parsing, rendering, eksekusi di browser   | ~30 ms (tergantung kompleksitas halaman) |

> [!NOTE]
>
> - **Latency jaringan Singapura – Depok** biasanya sekitar 20-30 ms satu arah, jadi kita pakai 20 ms sebagai estimasi.
> - Disk server diasumsikan SSD cepat, sekitar 5 ms.
> - Data cache di RAM server mempercepat akses, 1 ms.
> - CPU server relatif cepat, tapi tergantung load, 10 ms diasumsikan cukup.
> - RAM client sangat cepat, 1 ms.
> - CPU client tergantung halaman, 30 ms contoh untuk halaman biasa.

------

## Total waktu estimasi (Round Trip):

Karena T_request dan T_response masing-masing satu arah, totalnya jadi:
$$
T_{total} = T_{request} + T_{disk} + T_{RAM-server} + T_{CPU-server} + T_{response} + T_{RAM-client} + T_{CPU-client}
$$

------

## Interpretasi:

- Sekitar **87 ms** dari kamu klik request sampai halaman siap diproses dan sebagian tampil di browser.
- Ini cukup cepat, karena server di Singapura dekat dengan Indonesia secara geografis.
- Jika data sudah cached di RAM server, waktu baca disk bisa diabaikan (jadi lebih cepat).
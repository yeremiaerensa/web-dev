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

# Total Waktu 

$$
T_{request} + T_{disk} + T_{RAM-server} + T_{CPU-server} + T_{response} + T_{RAM-client} + T_{CPU-client}
$$

> [!NOTE]
>
> - Trequset → Waktu pengiriman request
> - Tdisk → Waktu pengambilan data dari disk server (disk IO)
> - TRAM server → Waktu pengambilan data dari RAM server 
> - TCPU server → Waktu proses di CPU server
> - Tresponse → Waktu pengiriman response dari server ke browser
> - TRAM client→ Response diterima dan disimpan di RAM lokal (client-side)
> - TCPU client→ Proses di CPU lokal (browser parsing, render, eksekusi JavaScript, dll)
>
> 

------

# Algoritma

Kalau dari sisi algoritma, bagian-bagian spesifik dalam proses itu bisa melibatkan algoritma seperti:

- **Algoritma cache management** (LRU, LFU, dll)
- **Algoritma routing jaringan**
- **Algoritma parsing HTML dan JavaScript**
- **Algoritma kompresi/dekompresi data**
- **Algoritma scheduling CPU**
# Dokumentasi API Client Admin


## Gambaran Umum
Client admin menyediakan API untuk memantau wallet address dan mengelola reporting asset crypto client, termasuk daftar wallet address, daftar mutasi wallet address, dan kirim data asset reporting harian. API ini memungkinkan developer di sisi klien untuk mengintegrasikan fungsionalitas ke dalam aplikasi.

### Endpoint Dasar

Base URL: https://client-admin-api.tennet.id


### Autentikasi
Autentikasi diperlukan untuk semua permintaan API. Setiap permintaan harus menyertakan token akses yang diperoleh melalui mekanisme autentikasi yang sesuai.


### Metode Autentikasi
Autentikasi dilakukan menggunakan API Key yang diberikan kepada pengguna saat pendaftaran aplikasi.

Setiap permintaan harus menyertakan header ‘Tennet-Secret-Key’ dengan nilai Secret key diberikan Tennet.


### Endpoints
1. Perusahaan
    1. Mendapatkan Informasi Profil Perusahaan
        
        Metode: GET\
        Endpoint: /company/profile\
        Deskripsi: Mendapatkan informasi profil perusahaan.\
        Parameter: -

        Contoh Request: 
        ```sh
        GET /company/profile HTTP/1.1
        Tennet-Secret-Key: <Secret-Key>
        ```
    
        Contoh Response Sukses: 
        ```json
        {
            "code": 200,
            "message": "Getting data successfully",
            "data": {
                "id": 24,
                "name": "PT. ASET KRIPTO INDONESIA",
                "broker_code": "ABC",
                "business_name": "Aset Kripto Indonesia",
                "business_description": "Media investasi yang dapat dimasukkan sebagai komoditas dan dapat diperdagangkan di bursa berjangka",
                "license_date": "2023-11-29",
                "registration_number": "12345",
                "website": "https://example.com"
            }
        }
        ```
    2. Mendapatkan Informasi daftar PIC di perusahaan
        
        Metode: GET\
        Endpoint: /company/pics\
        Deskripsi: Mendapatkan informasi pic terdaftar di perusahaan.\
        Parameter: -

        Contoh Request: 
        ```sh
        GET /company/pics HTTP/1.1
        Tennet-Secret-Key: <Secret-Key>
        ```
    
        Contoh Response Sukses: 
        ```json
        {
            "code": 200,
            "message": "Getting data successfully",
            "data": [
                {
                    "id": 51,
                    "name": "Hadi PIC",
                    "email": "hadi@tennet.id",
                    "job_title": "IT",
                    "phone_number": "123456789"
                }
            ]
        }
        ```
    2. Mendapatkan Informasi daftar files di perusahaan
        
        Metode: GET\
        Endpoint: /company/files\
        Deskripsi: Mendapatkan informasi files terdaftar di perusahaan.\
        Parameter: -

        Contoh Request: 
        ```sh
        GET /company/files HTTP/1.1
        Tennet-Secret-Key: <Secret-Key>
        ```
    
        Contoh Response Sukses: 
        ```json
        {
            "code": 200,
            "message": "Getting data successfully",
            "data": [
                {
                    "id": 20,
                    "name": "Lisensi",
                    "path": "<file_url>",
                    "note": ""
                }
            ]
        }
        ```
2. Transaksi
a. Membuat Transaksi Baru
Metode: POST
Endpoint: /transaction/new
Deskripsi: Membuat transaksi baru antara pengguna saat ini dan penerima yang ditentukan.
Parameter:
sender_id (body) - ID pengirim
receiver_id (body) - ID penerima
amount (body) - Jumlah yang akan dikirim
Contoh Permintaan:
http
Copy code
POST /transaction/new HTTP/1.1 Authorization: Bearer <API_KEY> Content-Type: application/json { "sender_id": 123, "receiver_id": 456, "amount": 50.00 }
Contoh Respon Sukses:
json
Copy code
{ "transaction_id": "abc123", "sender_id": 123, "receiver_id": 456, "amount": 50.00, "timestamp": "2024-03-18T12:00:00Z" }
Status Kode
Kode
Deskripsi
200
Permintaan berhasil
400
Permintaan tidak valid
401
Unauthorized - Tidak ada atau token akses tidak valid
404
Tidak ditemukan
500
Kesalahan server

Kesimpulan
Dokumentasi di atas adalah gambaran umum dari API Layanan Dompet Digital. Pastikan untuk menggunakan autentikasi dengan benar dan memahami kebutuhan spesifik aplikasi Anda saat mengintegrasikan API ini.
Untuk informasi lebih lanjut, silakan kunjungi halaman dokumentasi resmi kami atau hubungi tim dukungan kami di support@walletservice.com.


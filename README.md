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

2. Vault
    1. Mendapatkan daftar wallet address
        
        Metode: GET\
        Endpoint: /vault/addresses\
        Deskripsi: Mendapatkan daftar wallet address.\
        Parameter: -

        Contoh Request: 
        ```sh
        GET /vault/addresses HTTP/1.1
        Tennet-Secret-Key: <Secret-Key>
        Request Body:
        {
            "filter" : {
                "asset_symbol": null
            }
        }
        ```
    
        Contoh Response Sukses: 
        ```json
        {
            "code": 200,
            "message": "Getting data successfully",
            "data": [
                {
                    "id": 8,
                    "asset_name": "Ethereum",
                    "asset_symbol": "ETH",
                    "protocol_symbol": "ETH",
                    "address": "0x8732E38210870B8eF3f3492E3EC0e29666379759",
                    "legacy_address": "",
                    "tag": "",
                    "balance": "0.091",
                    "price": "55329276.02",
                    "total": "5034964.12"
                }
            ]
        }
        ```
    2. Mendapatkan daftar mutasi wallet address
        
        Metode: GET\
        Endpoint: /vault/mutations\
        Deskripsi: Mendapatkan daftar mutasi wallet address.\
        Parameter: -

        Contoh Request: 
        ```sh
        GET /vault/mutations HTTP/1.1
        Tennet-Secret-Key: <Secret-Key>
        Request Body:
        {
            "filter" : {
                "asset_symbol": null,
                "business_date_range": {
                    "start": null,
                    "end": null
                },
                "offset": 0,
                "limit": 150
            }
        }
        ```
    
        Contoh Response Sukses: 
        ```json
        {
            "code": 200,
            "message": "Getting data successfully",
            "data_count": 3,
            "offset": 0,
            "limit": 150,
            "data": [
                {
                    "id": 18,
                    "tx_hash": "0xb432d3c3c53329e85e622ece2de59d4fcc0b7da5e20cdae1eb6a8e3dc06f2f30",
                    "asset": "ETH",
                    "type": "Transfer In",
                    "volume": "0.001",
                    "rate_idr": "Rp 55.329.276",
                    "total": "Rp 55.329",
                    "block_height": 0
                },
                {
                    "id": 19,
                    "tx_hash": "0x118bf70e5f11734ddfd0d070e0ecfa5521372c4612aaba901e46177723934462",
                    "asset": "ETH",
                    "type": "Transfer In",
                    "volume": "0.1",
                    "rate_idr": "Rp 55.329.276",
                    "total": "Rp 5.532.928",
                    "block_height": 0
                },
                {
                    "id": 20,
                    "tx_hash": "0x10bed46a67e343bf3bf75839b1a20a4f12d41186adc3a71ee62b784cafd28c60",
                    "asset": "ETH",
                    "type": "Transfer In",
                    "volume": "-0.01",
                    "rate_idr": "Rp 55.329.276",
                    "total": "Rp -553.293",
                    "block_height": 0
                }
            ]
        }
        ```

Kesimpulan
Dokumentasi di atas adalah gambaran umum dari API Layanan Dompet Digital. Pastikan untuk menggunakan autentikasi dengan benar dan memahami kebutuhan spesifik aplikasi Anda saat mengintegrasikan API ini.
Untuk informasi lebih lanjut, silakan kunjungi halaman dokumentasi resmi kami atau hubungi tim dukungan kami di support@tennet.id.


<p align="center"><a href="https://depository.id" target="_blank"><img src="https://images.glints.com/unsafe/glints-dashboard.s3.amazonaws.com/company-logo/3761f964beaa6bbe75bbe19852da04a2.jpg" width="500"></a></p>



# Dokumentasi API Client Admin
---

Konten:
- [Gambaran Umum](#gambaran-umum)
- [Endpoint Dasar](#endpoint-dasar)
- [Autentikasi](#autentikasi)
- [Metode Autentikasi](#metode-autentikasi)
- [Endpoints](#endpoints)
    - [1. Perusahaan](#1-perusahaan)
        - [1.a. Profil](#1a-profile)
        - [1.b. PICs](#1b-pics)
        - [1.c. Files](#1c-files)
    - [2. Vault](#2-vault)
        - [2.a. Addresses](#2a-addresses)
        - [2.b. Mutations](#2b-mutations)
    - [3. Crypto Asset Report](#3-crypto-asset-report)
        - [3.a. Reports](#3a-reports)
        - [3.b. Create](#3b-create)
        - [3.c. Delete](#3c-delete)
    - [4. Vault Report](#4-vault-report)
- [Status Kode](#status-kode)
- [Kesimpuan](#kesimpulan)


## Gambaran Umum
Client admin menyediakan API untuk memantau wallet address dan mengelola reporting asset crypto client, termasuk daftar wallet address, daftar mutasi wallet address, dan kirim data asset reporting harian. API ini memungkinkan developer di sisi klien untuk mengintegrasikan fungsionalitas ke dalam aplikasi.

### Endpoint Dasar

Base URL: [https://client-admin-api.tennet.id](https://client-admin-api.tennet.id)


### Autentikasi
Autentikasi diperlukan untuk semua permintaan API. Setiap permintaan harus menyertakan token akses yang diperoleh melalui mekanisme autentikasi yang sesuai.


### Metode Autentikasi
Autentikasi dilakukan menggunakan API Key yang diberikan kepada pengguna saat pendaftaran aplikasi.

Setiap permintaan harus menyertakan header ‘Tennet-Secret-Key’ dengan nilai Secret key diberikan Tennet.


### Endpoints
### 1. Perusahaan
#### 1.a. Profile
        
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
#### 1.b. PICs

Metode: GET\
Endpoint: /company/pics\
Deskripsi: Mendapatkan informasi pic terdaftar di perusahaan.\
Parameter: search filter

Contoh Request: 
```sh
GET /company/pics HTTP/1.1
Tennet-Secret-Key: <Secret-Key>
Request Body:
{
    "filter":{
        "search":""
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
            "id": 51,
            "name": "Hadi PIC",
            "email": "hadi@tennet.id",
            "job_title": "IT",
            "phone_number": "123456789"
        }
        ...
    ]
}
```
#### 1.c. Files
    
Metode: GET\
Endpoint: /company/files\
Deskripsi: Mendapatkan informasi files terdaftar di perusahaan.\
Parameter: search filter

Contoh Request: 
```sh
GET /company/files HTTP/1.1
Tennet-Secret-Key: <Secret-Key>
Request Body:
{
    "filter":{
        "search":""
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
            "id": 20,
            "name": "Lisensi",
            "path": "<file_url>",
            "note": ""
        }
        ...
    ]
}
```

### 2. Vault
#### 2.a. Addresses

Metode: GET\
Endpoint: /vault/addresses\
Deskripsi: Mendapatkan daftar wallet address.\
Parameter: search filter 

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
        ...
    ]
}
```
#### 2.b. Mutations

Metode: GET\
Endpoint: /vault/mutations\
Deskripsi: Mendapatkan daftar mutasi wallet address.\
Parameter: search filter

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
        }
        ....
    ]
}
```

### 3. Crypto Asset Report
#### 3.a. Reports
        
Metode: GET\
Endpoint: /crypto-asset-report/reports\
Deskripsi: Mendapatkan daftar laporan aset kripto.\
Parameter: search filter

Contoh Request: 
GET /vault/addresses HTTP/1.1
Tennet-Secret-Key: <Secret-Key>
```sh
Request Body:
{
    "filter" : {
        "asset_symbol": ["BTC"],
        "report_date_range": {
            "start": null,
            "end":null
        },
        "offset": 0,
        "limit": 100
    }
}
```

Contoh Response Sukses: 
```json
{
    "code": 200,
    "message": "Getting data successfully",
    "data_count": 13,
    "offset": 0,
    "limit": 100,
    "data": [
        {
            "id": 229156,
            "institute_id": 24,
            "institute_name": "PT. ASET KRIPTO INDONESIA",
            "institute_business": "Aset Kripto Indonesia",
            "report_date": "2024-01-19 03:21:11",
            "asset_name": "Bitcoin",
            "asset_symbol": "BTC",
            "volume": "3695.0878"
        },
        {
            "id": 300688,
            "institute_id": 24,
            "institute_name": "PT. ASET KRIPTO INDONESIA",
            "institute_business": "Aset Kripto Indonesia",
            "report_date": "2024-01-19 17:21:03",
            "asset_name": "Bitcoin",
            "asset_symbol": "BTC",
            "volume": "1"
        },
        ....
    ]
}
```
#### 3.b. Create

Metode: GET\
Endpoint: /crypto-asset-report/create\
Deskripsi: menambahkan laporan aset kripto baru.\
Parameter: data aset kripto

Contoh Request: 
```sh
GET /crypto-asset-report/create HTTP/1.1
Tennet-Secret-Key: <Secret-Key>
Request Body:
{
    "asset_name":"Bitcoin",
    "asset_symbol":"BTC",
    "report_date":"2024-03-14 13:57:03",
    "volume":3
}
```

Contoh Response Sukses: 
```json
{
    "code": 200,
    "message": "Store data success"
}
```

#### 3.c. Delete

Metode: GET\
Endpoint: /crypto-asset-report/delete\
Deskripsi: menghapus laporan aset kripto.\
Parameter: id aset kripto yang akan dihapus

Contoh Request: 
```sh
GET /crypto-asset-report/delete HTTP/1.1
Tennet-Secret-Key: <Secret-Key>
Request Body:
{
    "id":"301250"
}
```

Contoh Response Sukses: 
```sh
{
    "code": 200,
    "message": "Delete data success"
}
```
### 4. Vault Report

Metode: POST\
Endpoint: /vault-report\
Deskripsi: Mengirimkan data transaksi.\
Parameter: data transaksi

| No | Name                     | Type          | Required | Description |
|----|--------------------------|---------------|----------|-------------|
| 1  | ```request_id```         | string        | yes      | generated random uuid|
| 2  | ```request_timestamp```  | number        | yes      | unix timestamp|
| 3  | ```institute_id```       | number        | yes      | institute id given by tennet|
| 4  | ```payload```            | transaction[] | yes      | list of transactions|

Transaction Property:
| No | Name                     | Type          | Required | Description |
|----|--------------------------|---------------|----------|-------------|
| 1  | ```tx_id```              | string        | yes      | generated random uuid|
| 2  | ```client_user_id```     | number        | yes      | user id given by tennet|
| 3  | ```tx_asset_symbol```    | string        | yes      | asset name |
| 4  | ```tx_protocol```        | string        | yes      | protocol or network name|
| 5  | ```tx_type```            | enum          | yes      | `enum[Transfer In, Transfer Out]`|
| 6  | ```tx_amount```          | string        | yes      | amount of transaction|
| 7  | ```tx_transfer_fee```    | string        | yes      | transaction fee|
| 8  | ```tx_timestamp```       | number        | yes      | unix timestamp|

Contoh Request: 
POST /vault-report HTTP/1.1
Tennet-Secret-Key: <Secret-Key>

Request Body:
```sh
{
    "request_id":"123",
    "request_timestamp":123456789,
    "institute_id":2,
    "payload":[
        {
            "tx_id":"1234567",
            "client_user_id":3,
            "tx_asset_symbol":"BTC",
            "tx_protocol":"Bitcoin",
            "tx_type":"TRANSFER IN",
            "tx_amount":"0.011",
            "tx_transfer_fee":"0.00001",
            "tx_timestamp":123456789
        },
        ...
    ]
}
```

Contoh Response Sukses: 
```json
{
    "code": 200,
    "message": "Store data success"
}
```

### Kesimpulan
Dokumentasi di atas adalah gambaran umum dari API Client admin api. Pastikan untuk menggunakan autentikasi dengan benar dan memahami kebutuhan spesifik aplikasi Anda saat mengintegrasikan API ini.
Untuk informasi lebih lanjut, silakan kunjungi hubungi tim dukungan kami di support@tennet.id.


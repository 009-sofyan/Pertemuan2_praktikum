# Dokumentasi Routing API

Backend menggunakan Express.js dengan base URL:

`http://localhost:3000/api/v1`

## 1. GET /api/v1
Method: GET
URL:`/api/v1`
Input: Tidak ada
Status sukses: 200 OK
Status gagal: -
Fungsi: Memeriksa apakah API dapat diakses.
### Response
HTTP/1.1 200 OK
X-Powered-By: Express
Content-Type: application/json; charset=utf-8
Content-Length: 57
ETag: W/"39-K2oDMTbZTXS4DPfPU91St2S2OTY"
Date: Fri, 02 Oct 2026 04:08:15 GMT
Connection: keep-alive
Keep-Alive: timeout=5
{"status":true,"message":"Welcome to API v1","data":null}

## 2. GET /api/v1/jadwal?status=aktif
Method: GET
URL: /api/v1/jadwal?status=aktif
Input: Query (status)
Status sukses: 200 OK
Status gagal: -
Fungsi: Menampilkan daftar jadwal dan memfilter jadwal berdasarkan status.
### Response
$ curl -i "http://localhost:3000/api/v1/jadwal?status=aktif"
HTTP/1.1 200 OK
X-Powered-By: Express
Content-Type: application/json; charset=utf-8
Content-Length: 190
ETag: W/"be-P1eGKQ7Rq1Viusbws3e+3/XTdcM"
Date: Fri, 02 Oct 2026 04:10:16 GMT
Connection: keep-alive
Keep-Alive: timeout=5
{"status":true,"message":"Daftar jadwal berhasil diambil","data":[{"id":1,"mataKuliah":"Pemrograman Berbasis Platform","status":"aktif"},{"id":2,"mataKuliah":"Basis Data","status":"aktif"}]}

## 3. GET /api/v1/jadwal/abc
Method: GET
URL: /api/v1/jadwal/abc
Input: Params (id)
Status sukses: -
Status gagal: 400 Bad Request
Fungsi: Menguji validasi ID. ID harus berupa angka.
### Response
$ curl -i http://localhost:3000/api/v1/jadwal/abc
HTTP/1.1 400 Bad Request
X-Powered-By: Express
Content-Type: application/json; charset=utf-8
Content-Length: 50
ETag: W/"32-tkkrPtocAi2TpaljrqRKUejiluY"
Date: Fri, 02 Oct 2026 04:13:00 GMT
Connection: keep-alive
Keep-Alive: timeout=5

{"status":false,"message":"id harus berupa angka"}

## 4. GET /api/v1/jadwal/99
Method: GET
URL: /api/v1/jadwal/99
Input: Params (id)
Status sukses: -
Status gagal: 404 Not Found
Fungsi: Menguji kondisi ketika jadwal tidak ditemukan.
### Response
$ curl -i http://localhost:3000/api/v1/jadwal/99
HTTP/1.1 404 Not Found
X-Powered-By: Express
Content-Type: application/json; charset=utf-8
Content-Length: 51
ETag: W/"33-SP0KavR2YKcxvyT6s1STOgkz2wI"
Date: Fri, 02 Oct 2026 04:14:40 GMT
Connection: keep-alive
Keep-Alive: timeout=5

{"status":false,"message":"Jadwal tidak ditemukan"}

## 5. POST /api/v1/jadwal dengan body valid
Method: POST
URL: /api/v1/jadwal
Input: Body (mataKuliah, status)
Status sukses: 201 Created
Status gagal: 400 Bad Request
Fungsi: Menambahkan jadwal baru.
### Response
$ curl -i -X POST http://localhost:3000/api/v1/jadwal \
-H "Content-Type: application/json" \
-d '{"mataKuliah":"Pemrograman Web","status":"aktif"}'
HTTP/1.1 201 Created
X-Powered-By: Express
Content-Type: application/json; charset=utf-8
Content-Length: 119
ETag: W/"77-WB4EcHaVUFF/7GknBJa4zmoj4Tc"
Date: Fri, 02 Oct 2026 04:20:59 GMT
Connection: keep-alive
Keep-Alive: timeout=5

{"status":true,"message":"Jadwal berhasil ditambahkan","data":{"id":4,"mataKuliah":"Pemrograman Web","status":"aktif"}
## 6. GET /api/v1/jadwal/1/peserta
Method: GET
URL: /api/v1/jadwal/1/peserta
Input: Params (jadwalId)
Status sukses: 200 OK
Status gagal: 404 Not Found
Fungsi: Menampilkan daftar peserta yang berada pada jadwal tertentu.
### response
$ curl -i http://localhost:3000/api/v1/jadwal/1/peserta
HTTP/1.1 200 OK
X-Powered-By: Express
Content-Type: application/json; charset=utf-8
Content-Length: 176
ETag: W/"b0-nkl2tizFkRIHDkzHgHlN96d3zlY"
Date: Fri, 02 Oct 2026 04:22:12 GMT
Connection: keep-alive
Keep-Alive: timeout=5

{"status":true,"message":"Daftar peserta berhasil diambil","data":[{"id":101,"jadwalId":1,"nim":"2026001","nama":"Alya"},{"id":102,"jadwalId":1,"nim":"2026002","nama":"Bima"}]}

## 7. GET /api/v1/jadwal/1/peserta/103
Method: GET
URL: /api/v1/jadwal/1/peserta/103
Input: Params (jadwalId, pesertaId)
Status sukses: 200 OK
Status gagal: 404 Not Found
Fungsi: Mengambil satu peserta berdasarkan ID peserta dalam konteks jadwal tertentu.
### response
$ curl -i http://localhost:3000/api/v1/jadwal/1/peserta/103
HTTP/1.1 404 Not Found
X-Powered-By: Express
Content-Type: application/json; charset=utf-8
Content-Length: 68
ETag: W/"44-AMShfSwXfyFxFPDt/M5WtTnanF0"
Date: Fri, 02 Oct 2026 04:23:54 GMT
Connection: keep-alive
Keep-Alive: timeout=5

{"status":false,"message":"Peserta tidak ditemukan pada jadwal ini"}

## 8. GET /api/v1/alamat-salah
Method: GET
URL: /api/v1/alamat-salah
Input: Tidak ada
Status sukses: -
Status gagal: 404 Not Found
Fungsi: Menguji fallback route ketika alamat endpoint tidak ditemukan.
### Response
$ curl -i http://localhost:3000/api/v1/alamat-salah
HTTP/1.1 404 Not Found
X-Powered-By: Express
Content-Type: application/json; charset=utf-8
Content-Length: 75
ETag: W/"4b-T5P7GitXpQ7OL9mkvib8gly9Sl0"
Date: Fri, 02 Oct 2026 04:25:36 GMT
Connection: keep-alive
Keep-Alive: timeout=5

{"status":false,"message":"Route GET /api/v1/alamat-salah tidak ditemukan"}


## Catatan Perbandingan dengan ATLAS

Pada backend latihan, route atau resource yang tidak ditemukan 
menggunakan status `404 Not Found`. Sementara itu, sistem ATLAS 
asli memiliki perilaku lama yang dapat mengembalikan `500 Api tidak 
tersedia` ketika path API tidak cocok. 

Perbedaan tersebut dicatat sebagai perbandingan antara backend 
latihan dan sistem ATLAS asli. Backend latihan tetap menggunakan 
`404` dan tidak diubah menjadi `500`.
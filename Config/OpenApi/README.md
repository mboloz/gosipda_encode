# GoSIPDA OpenAPI Reference

File canonical dokumentasi:

`app/Config/OpenApi/gosipda-v1.json`

Dokumentasi ini sengaja **tidak mempunyai menu, route dokumentasi, Swagger UI, atau halaman admin**. File OpenAPI dipakai sebagai referensi developer/integrator dan dapat di-import ke Swagger Editor, Postman, Insomnia, Bruno, atau tool OpenAPI lain.

## Cakupan

- USER_APP / Mobile: health probe, auth, self-service profile/foto/password, context, master read, stock, Saldo Awal, Penambahan, Pengeluaran FIFO, history, report JSON, PDF.
- SIMIF / M2M: ping, referensi tujuan SIPDA, import replace.
- Security contract: Bearer, HMAC conditional M2M, scope OPD/gudang, idempotency, version token, rate limit.
- Performance contract: pagination USER_APP hard cap 100, referensi SIMIF hard cap 1000.

## HMAC SIMIF

Untuk client `TOKEN_HMAC`:

```text
X-API-Timestamp: <timestamp>
X-API-Signature: <hex sha256>
signature = HMAC-SHA256(timestamp + "." + raw_request_body, secret)
```

Prefix `sha256=` pada signature diterima server. Timestamp memiliki toleransi maksimum 600 detik.

## Maintenance rule

Setiap route baru di group `api/v1` atau `api/integrasi` wajib ditambahkan ke OpenAPI. Test `OpenApiDocumentationContractTest` menjaga coverage route agar dokumentasi tidak tertinggal.

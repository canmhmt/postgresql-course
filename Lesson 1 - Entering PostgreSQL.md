# PostgreSQL Giriş

## PostgreSQL Nedir?

- PostgreSQL verileri tutarlı ve düzenli bir şekilde saklamamızı sağlayan bir ilişkisel veritabanı yönetim sistemidir. (RDBMS)

**Neler yapar?**

- Veriyi kalıcı saklar (RAM değil disk)

- Aynı anda çok kullanıcıyı yönetir

- Veri bozulmasın diye kurallar (constraint) uygular

- Transaction ile yarım kalan işleri geri alır

- Index ile hızlı arama yapar

- İlişkisel olduğu için ACID garantisi vardır;

**ACID** = 4 temel garanti

- “Bir işlem (transaction) ya tamamen olur ya hiç olmaz, doğru olur, çakışmaz ve kaybolmaz.”

- ACID şu kelimelerin baş harfidir:

- Atomicity (Atomiklik) -- Bir işlem birden fazla adımdan oluşuyorsa eğer adımlardan birinde bir hata olursa tüm işlem rollback (geri sarma) yapılır.

- Consistency (Tutarlılık) -- Veritabanı kuralları bozulamaz

- Isolation (İzolasyon) -- Aynı anda yapılan işlemler birbirini bozmaz.

- Durability (Kalıcık) -- Transaction COMMIT dedikten sonra veri asla kaybolmaz, PostgreSQL bunu WAL (Write-Ahead Log) ile yapar, yani ilk olarak işlemin logunu tutar sonra veriye uygular.

## Temel Kavramlar

### Database

- Database = Ana Konteyner

- Bir PostgreSQL sunucusunda birden fazla Database bulunabilir. Bu databaseler birbirlerinden izolasyonludur.

### schema

- schema = Database içerisindeki klasör

**Neden ?**

- Aynı isimli tablolar çakışmasın diye

- Yetkilendirme için

- Mantıksal düzen için

### table (tablo)

- Sabit kolonlara sahiptir

- Veri tipi vardır (int, text, timestamp)

- Constraint’ler buradadır

### row (satır)

### column (kolon)

```json
PostgreSQL Server
  └── Database
        └── Schema
              └── Table
                    ├── Row
                    └── Column
```
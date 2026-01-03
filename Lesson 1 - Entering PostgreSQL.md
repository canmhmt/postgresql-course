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


#### PostgreSQL Mimarisi (High-level)

- PostgreSQL bir client-server sistemidir. Yani iki taraf var:

### Client

- PostgreSQL sorgu atarken, istek atarken kullandığımız araç. (DBeaver, pgadmin, python vs.)


#### Server (PostgreSQL Server)

- Asıl işi yapan kısım. Veritabanını yönetir, gelen istekleri karşılar ve SQL çalıştırır.

### Backend Process Nedir?

- Her bağlantı için ayrı bir backend process oluşur. Client (Örneğin psql) bağlanır. Her bağlantı için ayrı bir Backend process oluşur (100 kullanıcı 100 process). Bu nedenle max-connections ayarı önemlidir.

- Connectionlar nasıl sorgulanır?

```sql
SELECT pid, usename, datname, state
FROM pg_stat_activity;
```

### psql Nedir?

- Varsayılan komut satırı işlemcisi.

```bash
psql -h localhost -p 5432 -U postgres -d postgres
```

#### Basit psql Komutları

- \l -- veritabanlarını listele.

- \dt -- Tabloları göster.

- \dn -- shemaları göster.

- \c database_name -- veritabanına bağlan

- \d users -- bir tabloyu incele


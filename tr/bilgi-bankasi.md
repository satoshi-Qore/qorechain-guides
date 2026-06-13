# QoreChain Bilgi Bankasi

Bu dokuman, QoreChain ve Light Node surecleri hakkinda sık sorulan temel sorulari toplar.

## Genel Sorular

### QoreChain nedir?

QoreChain, uzun vadeli guvenlik ve aglar arasi altyapiya odaklanan kuantum sonrasi guvenlik yaklasimli bir Katman 1 blokzincirdir.

### Bu depo resmi mi?

Hayir. Bu depo topluluk icin hazirlanmis bagimsiz bir bilgi kaynagidir. Kritik adimlarda resmi QoreChain kaynaklari ve guncel duyurular kontrol edilmelidir.

### Bu dokuman kimler icin hazirlandi?

Bu dokuman, QoreChain ekosistemini takip eden kullanicilar, Light Node calistirmak isteyen operatorler ve temel kavramlari hizli sekilde anlamak isteyen topluluk uyeleri icin hazirlanmistir.

## Light Node Sorulari

### Light Node nedir?

Light Node, ag trafiginin iletilmesine yardimci olan, ag isteklerine hizmet eden ve ag ucretlerinden pay kazanabilen bir node yapisidir.

### Light Node calistirmak icin teknik bilgi gerekir mi?

Temel terminal kullanimi, Docker komutlari ve sunucu erisimi bilgisi gerekir. Kurulum adimlari basit tutulsa da operatorlerin servis durumunu ve loglari kontrol edebilmesi onemlidir.

### Panel hangi adresten acilir?

Panel genellikle sunucu IP adresi ve ilgili port uzerinden acilir:

```text
http://YOUR_SERVER_IP:8420
```

`YOUR_SERVER_IP` alanini kendi sunucu IP adresinizle degistirmeniz gerekir.

## Stake Sorulari

### Neden 1000 QOR gereklidir?

1000 QOR stake gereksinimi, Sybil saldirilarini azaltmaya ve operatorlerin ag basarisiyla daha uyumlu hareket etmesine yardimci olur.

### 1000 QOR bir ucret midir?

Hayir. Bu miktar bir ucret degil, node calistigi surece kilitli kalan stake miktaridir.

### Stake geri alinabilir mi?

Evet. Node kapatildiginda ve ag kurallarina gore gerekli surecler tamamlandiginda stake geri cekilebilir.

## Operasyon Sorulari

### Node calisiyor mu nasil kontrol edilir?

Sunucuda container durumunu kontrol edebilirsiniz:

```bash
docker ps
```

Beklenen servisler listede gorunuyorsa node temel seviyede calisiyor kabul edilebilir.

### Loglar nasil kontrol edilir?

Ana servis loglari icin:

```bash
docker logs qorechain-lightnode-sx
```

Canli takip icin:

```bash
docker logs -f qorechain-lightnode-sx
```

### Panel acilmiyorsa ilk ne kontrol edilmeli?

Once container durumunu kontrol edin. Servisler calisiyorsa sunucu IP adresini, portu ve firewall ayarlarini gozden gecirin.

## Not

Bu bilgi bankasi kisa yanitlar icin hazirlanmistir. Daha detayli operasyon adimlari icin [Light Node Operasyonlari](./light-node-operasyonlari.md) dokumanini takip edebilirsiniz.

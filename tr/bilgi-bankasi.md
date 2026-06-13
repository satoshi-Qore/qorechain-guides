# QoreChain Bilgi Bankası

Bu doküman, QoreChain ve Light Node süreçleri hakkında sık sorulan temel soruları toplar.

## Genel Sorular

### QoreChain nedir?

QoreChain, uzun vadeli güvenlik ve ağlar arası altyapıya odaklanan kuantum sonrası güvenlik yaklaşımlı bir Katman 1 blokzincirdir.

### Bu depo resmi mi?

Hayır. Bu depo topluluk için hazırlanmış bağımsız bir bilgi kaynağıdır. Kritik adımlarda resmi QoreChain kaynakları ve güncel duyurular kontrol edilmelidir.

### Bu doküman kimler için hazırlandı?

Bu doküman, QoreChain ekosistemini takip eden kullanıcılar, Light Node çalıştırmak isteyen operatörler ve temel kavramları hızlı şekilde anlamak isteyen topluluk üyeleri için hazırlanmıştır.

## Light Node Soruları

### Light Node nedir?

Light Node, ağ trafiğinin iletilmesine yardımcı olan, ağ isteklerine hizmet eden ve ağ ücretlerinden pay kazanabilen bir node yapısıdır.

### Light Node çalıştırmak için teknik bilgi gerekir mi?

Temel terminal kullanımı, Docker komutları ve sunucu erişimi bilgisi gerekir. Kurulum adımları basit tutulsa da operatörlerin servis durumunu ve logları kontrol edebilmesi önemlidir.

### Panel hangi adresten açılır?

Panel genellikle sunucu IP adresi ve ilgili port üzerinden açılır:

```text
http://YOUR_SERVER_IP:8420
```

`YOUR_SERVER_IP` alanını kendi sunucu IP adresinizle değiştirmeniz gerekir.

## Stake Soruları

### Neden 1000 QOR gereklidir?

1000 QOR stake gereksinimi, Sybil saldırılarını azaltmaya ve operatörlerin ağ başarısıyla daha uyumlu hareket etmesine yardımcı olur.

### 1000 QOR bir ücret midir?

Hayır. Bu miktar bir ücret değil, node çalıştığı sürece kilitli kalan stake miktarıdır.

### Stake geri alınabilir mi?

Evet. Node kapatıldığında ve ağ kurallarına göre gerekli süreçler tamamlandığında stake geri çekilebilir.

## Operasyon Soruları

### Node çalışıyor mu nasıl kontrol edilir?

Sunucuda container durumunu kontrol edebilirsiniz:

```bash
docker ps
```

Beklenen servisler listede görünüyorsa node temel seviyede çalışıyor kabul edilebilir.

### Loglar nasıl kontrol edilir?

Ana servis logları için:

```bash
docker logs qorechain-lightnode-sx
```

Canlı takip için:

```bash
docker logs -f qorechain-lightnode-sx
```

### Panel açılmıyorsa ilk ne kontrol edilmeli?

Önce container durumunu kontrol edin. Servisler çalışıyorsa sunucu IP adresini, portu ve firewall ayarlarını gözden geçirin.

## Not

Bu bilgi bankası kısa yanıtlar için hazırlanmıştır. Daha detaylı operasyon adımları için [Light Node Operasyonları](./light-node-operasyonlari.md) dokümanını takip edebilirsiniz.

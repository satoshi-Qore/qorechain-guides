# QoreChain Light Node Operasyon Dokumani

Bu dokuman, QoreChain Light Node kurulumu ve temel operasyon sureclerini duzenli bir sekilde takip etmek icin hazirlanmistir.

Amac, operatorlerin kurulumu tamamlamasi, servisleri kontrol etmesi, panel erisimini dogrulamasi ve temel sorun giderme adimlarini hizli sekilde uygulayabilmesidir.

## Operasyon Kapsami

- Sunucu gereksinimleri
- Light Node kurulumu
- Servis durumu kontrolu
- Panel erisimi
- Log takibi
- Yeniden baslatma ve temel sorun giderme
- Operator notlari

## Gereksinimler

- Ubuntu 22.04 onerilen VPS veya dedicated server
- Docker
- Docker Compose
- 1000 QOR stake
- Stabil internet baglantisi
- Temel terminal erisimi

## Kurulum

Light Node dosyalarini sunucuya indirin:

```bash
git clone https://github.com/qorechain/qorechain-lightnode.git
cd qorechain-lightnode
```

Servisleri baslatin:

```bash
docker compose up -d
```

## Servis Kontrolu

Calisan container durumunu kontrol edin:

```bash
docker ps
```

Beklenen servisler:

- qorechain-lightnode-sx
- qorechain-lightnode-ux

Container listesinde bu servisler gorunuyorsa Light Node temel olarak calismaya baslamistir.

## Panel Erisimi

Tarayicidan asagidaki adrese gidin:

```text
http://YOUR_SERVER_IP:8420
```

`YOUR_SERVER_IP` alanini kendi sunucu IP adresinizle degistirin.

Panel aciliyorsa arayuz tarafindaki temel erisim dogrulanmis olur.

## Log Takibi

Ana servis loglarini kontrol etmek icin:

```bash
docker logs qorechain-lightnode-sx
```

Loglari canli izlemek icin:

```bash
docker logs -f qorechain-lightnode-sx
```

## Yeniden Baslatma

Servisleri yeniden baslatmak icin:

```bash
docker compose restart
```

Yeniden baslatma sonrasi tekrar kontrol edin:

```bash
docker ps
```

## Temel Sorun Giderme

| Durum | Kontrol | Aksiyon |
|---|---|---|
| Panel acilmiyor | Sunucu IP ve port kontrolu | `docker ps` ve firewall ayarlarini kontrol edin |
| Servis gorunmuyor | Container listesi | `docker compose up -d` komutunu tekrar calistirin |
| Loglarda hata var | SX servis loglari | Hatayi not alin ve yeniden baslatma sonrasi tekrar kontrol edin |
| Node yanit vermiyor | Sunucu kaynaklari | CPU, RAM ve disk durumunu kontrol edin |

## Operator Kontrol Listesi

- Sunucu aktif mi?
- Docker servisleri calisiyor mu?
- Panel erisilebilir mi?
- SX ve UX containerlari listede gorunuyor mu?
- Loglarda tekrar eden hata var mi?
- Stake gereksinimi karsilaniyor mu?

## Bakim Notlari

Light Node surecleri QoreChain tarafindaki guncellemelere gore degisebilir. Kritik islemlerden once resmi duyurulari, proje deposunu ve topluluk bildirimlerini kontrol etmek onerilir.

## Not

Bu dokuman topluluk kullanimi icin hazirlanmis operasyon odakli bir kaynaktir. Resmi dokumantasyon yerine gecmez; guncel komutlar ve ag kurallari icin resmi kaynaklar kontrol edilmelidir.

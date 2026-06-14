# QoreChain Light Node Operasyonları

Bu doküman, QoreChain Light Node kurulumu ve temel operasyon süreçlerini daha düzenli takip etmek isteyen operatörler için hazırlanmıştır.

Amaç; kurulum öncesi kontrolleri, Docker tabanlı servis takibini, panel erişimini, log incelemeyi, güncelleme sürecini ve temel sorun giderme adımlarını tek bir pratik akışta toplamaktır.

## Operasyon Kapsamı

Bu sayfa şu konuları kapsar:

- sunucu gereksinimleri;
- gerekli portlar;
- Docker ve Docker Compose kontrolleri;
- Light Node başlatma;
- panel erişimi;
- log takibi;
- yeniden başlatma;
- güncelleme süreci;
- temel sorun giderme;
- operatör kontrol listesi.

Bu doküman resmi kurulum talimatlarının yerine geçmez. Kritik adımlarda resmi QoreChain kaynakları ve güncel duyurular kontrol edilmelidir.

## Gereksinimler

| Gereksinim | Minimum | Önerilen |
|---|---:|---:|
| CPU | 2 çekirdek | 4 çekirdek |
| RAM | 4 GB | 8 GB |
| Disk | 50 GB SSD | 100 GB SSD |
| İşletim Sistemi | Ubuntu 20.04+ | Ubuntu 22.04 LTS |

Ek gereksinimler:

- Docker
- Docker Compose
- SSH erişimi
- Açık panel portu
- Güncel resmi QoreChain kurulum bilgileri

## Gerekli Portlar

| Port | Servis | Yön |
|---:|---|---|
| 22 | SSH | Gelen |
| 8420 | Light Node paneli | Gelen |

Sunucuda güvenlik duvarı kullanılıyorsa 8420 portunun açık olduğundan emin olun.

UFW örneği:

```bash
sudo ufw allow 22/tcp
sudo ufw allow 8420/tcp
sudo ufw enable
sudo ufw status
```

## Kurulum Öncesi Kontrol

| Kontrol | Beklenen Durum |
|---|---|
| Sunucu erişimi | SSH bağlantısı çalışıyor |
| Docker | Docker komutları çalışıyor |
| Docker Compose | `docker compose` kullanılabilir |
| Port 8420 | Güvenlik duvarında açık |
| Disk alanı | Yeterli boş alan var |
| Resmi talimatlar | Güncel kurulum akışı kontrol edildi |
| Stake gereksinimi | Güncel gereksinim resmi kaynaklardan doğrulandı |

## Kurulum Akışı

Kurulum komutları resmi QoreChain kaynaklarından alınmalıdır. Bu topluluk dokümanı, komutların güncel olduğunu garanti etmez.

Genel Docker akışı:

```bash
docker compose up -d
```

Çalışan servisleri kontrol etmek için:

```bash
docker ps
```

## Panel Erişimi

Light Node paneli genellikle şu adresten kontrol edilir:

```text
http://SUNUCU_IP:8420
```

Panel açılıyorsa temel arayüz erişimi doğrulanmış olur. Panel açılmıyorsa önce container durumunu, ardından güvenlik duvarı ve port ayarlarını kontrol edin.

## Log Takibi

SX bileşeni için örnek log kontrolü:

```bash
docker logs qorechain-lightnode-sx
```

Anlık log takibi:

```bash
docker logs -f qorechain-lightnode-sx
```

UX bileşeni için container adını mevcut servis adınıza göre kontrol edin:

```bash
docker ps
```

## Yeniden Başlatma

Docker Compose ile yeniden başlatma:

```bash
docker compose restart
```

Yeniden başlatmadan sonra servisleri kontrol edin:

```bash
docker ps
```

## Güncelleme Süreci

Uyarı: Güncel ve doğrulanmış güncelleme komutları için resmi QoreChain belgelerini kontrol edin. Aşağıdaki adımlar genel bir Docker bakım akışı olarak verilmiştir.

Güncellemeden önce:

- mevcut çalışan container durumunu kontrol edin;
- varsa yapılandırma dosyalarını yedekleyin;
- resmi duyurularda özel güncelleme talimatı olup olmadığını kontrol edin;
- node durumunu ve panel erişimini not edin.

Genel güncelleme akışı:

```bash
docker ps
docker compose down
docker compose pull
docker compose up -d
```

Güncellemeden sonra:

```bash
docker ps
docker logs qorechain-lightnode-sx
```

## Yaygın Sorun Giderme

| Sorun | Kontrol | Yapılacak Adım |
|---|---|---|
| Panel açılmıyor | Sunucu IP ve port | `docker ps` ve güvenlik duvarı ayarlarını kontrol edin |
| Servis görünmüyor | Container listesi | `docker compose up -d` komutunu tekrar çalıştırın |
| Node yanıt vermiyor | Sunucu kaynakları | CPU, RAM ve disk kullanımını kontrol edin |
| Loglarda hata var | Container logları | İlgili hata mesajını resmi duyurular ve repo notlarıyla karşılaştırın |
| 8420 portuna erişilemiyor | Güvenlik duvarı | `sudo ufw allow 8420/tcp` ve `sudo ufw status` ile doğrulayın |

## Operatör Kontrol Listesi

- Docker servisleri çalışıyor mu?
- Panel 8420 portundan erişilebilir mi?
- SX ve UX bileşenleri çalışıyor mu?
- Loglarda tekrarlayan hata var mı?
- Sunucu kaynakları yeterli mi?
- Güncel resmi duyurularda operatörleri etkileyen bir değişiklik var mı?
- Güncelleme gerekiyorsa önce yapılandırma dosyaları yedeklendi mi?

## Bakım Notları

Light Node süreçleri QoreChain güncellemelerine göre değişebilir. Ağ kuralları, stake gereksinimleri, panel davranışı veya güncelleme komutları değiştiğinde resmi duyurular ve proje kaynakları kontrol edilmelidir.

Komutları çalıştırmadan önce doğru proje dizininde olduğunuzdan emin olun.

## Sorumluluk Reddi

Bu doküman topluluk tarafından hazırlanmış bir operasyon kaynağıdır. Resmi belgelerin yerine geçmez; güncel komutlar, ağ kuralları ve güvenlik gereksinimleri için resmi kaynaklar kontrol edilmelidir.

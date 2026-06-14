# QoreChain Light Node Operasyon Dokümanı

Bu doküman, QoreChain Light Node kurulumu ve temel operasyon süreçlerini düzenli bir şekilde takip etmek için hazırlanmıştır.

Amaç, operatörlerin kurulumu tamamlaması, servisleri kontrol etmesi, panel erişimini doğrulaması ve temel sorun giderme adımlarını hızlı şekilde uygulayabilmesidir.

## Operasyon Kapsamı

- Sunucu gereksinimleri
- Light Node kurulumu
- Servis durum kontrolleri
- Panel erişim doğrulaması
- Sorun giderme adımları
- Güncelleme süreci

## Sistem Gereksinimleri

| Bileşen | Minimum | Önerilen |
|---|---|---|
| İşletim Sistemi | Ubuntu 20.04 LTS | Ubuntu 22.04 LTS |
| CPU | 2 çekirdek | 4 çekirdek |
| RAM | 4 GB | 8 GB |
| Disk | 50 GB SSD | 100 GB SSD |
| İnternet | 10 Mbps | 50 Mbps+ |
| Minimum Stake | Resmi duyuruya göre | Resmi duyuruya göre |

> **Not:** Stake gereksinimleri ağ güncellemeleriyle değişebilir. Güncel değerler için resmi QoreChain duyurularını takip edin.

## Gerekli Portlar

| Port | Protokol | Kullanım |
|---|---|---|
| 8420 | TCP | Node yönetim paneli |
| 22 | TCP | SSH erişimi |

Güvenlik duvarı kuralları (UFW):

```bash
sudo ufw allow 22/tcp
sudo ufw allow 8420/tcp
sudo ufw enable
sudo ufw status
```

## Kurulum Adımları

Kurulum komutları resmi QoreChain belgelerinden alınmalıdır. Bu doküman yalnızca operasyonel rehberlik sağlar; resmi kurulum talimatları güncellenmiş olabilir.

## Servis Kontrol Komutları

### Servis Durumunu Görüntüleme

```bash
systemctl status qore-node
```

### Servisi Yeniden Başlatma

```bash
sudo systemctl restart qore-node
```

### Sistem Loglarını Görüntüleme

```bash
journalctl -u qore-node -n 100 --no-pager
```

### Anlık Log Takibi

```bash
journalctl -u qore-node -f
```

## Panel Erişim Doğrulama

Node paneline tarayıcıdan `http://<sunucu-ip>:8420` adresinden erişilebilir.

Beklenen durum: Panelin erişilebilir olması ve node durumunun gösterilmesi.

Panel erişilemiyor ise:

```bash
# Portun açık olduğunu doğrula
sudo ufw status

# Servisin çalıştığını doğrula
systemctl status qore-node

# IP adresini doğrula
curl ifconfig.me
```

## Yaygın Sorun Giderme

| Sorun | Olası Neden | Yapılacak Adım |
|---|---|---|
| Servis başlamıyor | Yanlış yapılandırma | Log kontrol et: `journalctl -u qore-node -n 50` |
| Panel erişilemiyor | Port kapalı veya servis çalışmıyor | UFW kurallarını ve servis durumunu kontrol et |
| Node senkronize olmuyor | Ağ gecikmesi veya yapılandırma sorunu | Logu incele, resmi duyuruları kontrol et |
| Yüksek kaynak kullanımı | Donanım yetersizliği | CPU ve RAM kullanımını kontrol et: `htop` |

## Güncelleme Süreci

> **Uyarı:** Güncel ve doğrulanmış güncelleme komutları için resmi QoreChain belgelerini kontrol edin. Aşağıdaki adımlar genel bir rehber niteliğindedir.

### Güncelleme Öncesi Hazırlık

1. Mevcut node sürümünü not edin
2. Yapılandırma dosyalarının yedeğini alın
3. Güncelleme öncesi node durumunu kaydedin

### Güncelleme Adımları

```bash
# Servisi durdur
sudo systemctl stop qore-node

# Güncellemeyi uygula (resmi komutlara göre)
# [Resmi belgelere bakın]

# Servisi yeniden başlat
sudo systemctl start qore-node

# Durumu doğrula
systemctl status qore-node
```

### Güncelleme Sonrası Doğrulama

- Servisin başarıyla başladığını doğrulayın
- Panel erişimini test edin
- Log çıktısını birkaç dakika izleyin

## Operatör Kontrol Listesi

- [ ] Sunucu `systemctl status qore-node` ile aktif olarak çalışıyor mu?
- [ ] Docker servisleri (kullanılıyorsa) çalışıyor mu?
- [ ] Panel `http://<sunucu-ip>:8420` adresinden erişilebilir mi?
- [ ] SX ve UX core bileşenleri çalışıyor mu?
- [ ] Tekrarlayan hata mesajları var mı?
- [ ] Stake gereksinimi karşılanıyor mu?
- [ ] Herhangi bir güncelleme bekliyor mu?

## Bakım Notları

Light Node süreçleri resmi QoreChain duyurularıyla değişebilir. Yüksek etkili eylemler (ağ kuralları, stake değişiklikleri) için resmi duyuruları, proje deposunu ve topluluk kanallarını kontrol edin.

Güncelleme komutlarını çalıştırmadan önce proje dizininde olduğunuzdan emin olun.

## Sorumluluk Reddi

Bu doküman topluluk tarafından hazırlanmış bir operasyon kaynağıdır. Resmi belgelerin yerine geçmez; güncel komutlar ve ağ kuralları için resmi kaynaklar kontrol edilmelidir.

# Bölüm 05 — Sorun Giderme

Bu sayfa, QoreChain Light Node Rehberi'nin beşinci bölümüdür.

Bu bölümde QoreChain Light Node çalıştırırken karşılaşılan en yaygın sorunlar, her biri için tanı adımları ve çözüm yöntemleri ele alınmaktadır.

---

## Tanı Komutları

Herhangi bir sorunla karşılaştığınızda aşağıdaki komutlar başlangıç noktası olarak işe yarar.

**Konteyner durumunu kontrol edin:**

```bash
cd /opt/qorechain-light-node
docker compose ps
```

**Son logları görüntüleyin:**

```bash
docker compose logs --tail=100
```

**Disk alanını kontrol edin:**

```bash
df -h /
```

**Belleği kontrol edin:**

```bash
free -h
```

**Docker servisini kontrol edin:**

```bash
systemctl status docker
```

---

## Konteyner Başladıktan Hemen Sonra Kapanıyor

**Belirti:** `docker compose up -d` komutundan kısa süre sonra `docker compose ps` bir konteyneri `exited` durumunda gösteriyor.

**Tanı:**

```bash
docker compose logs qorechain-light-node
```

Çıktının sonlarındaki hata mesajlarına bakın.

**Yaygın nedenler ve çözümler:**

| Neden | Çözüm |
|---|---|
| `.env` değeri eksik veya hatalı | `.env` dosyasını açın, tüm zorunlu alanların doğru doldurulduğunu doğrulayın |
| Hatalı RPC endpoint URL'si | Güncel RPC endpoint adresi için resmi QoreChain dokümantasyonunu kontrol edin |
| Port zaten kullanımda | `ss -tlnp \| grep 8420` komutuyla portu başka bir sürecin kullanıp kullanmadığını kontrol edin |
| Cüzdan adresi format hatası | Cüzdan adresinin QoreChain'in beklediği formatla eşleştiğini doğrulayın |

Sorunu giderdikten sonra konteynerleri yeniden başlatın:

```bash
docker compose down
docker compose up -d
```

---

## Web Paneline Erişilemiyor

**Belirti:** `http://SUNUCU_IP:8420` bağlantı hatası veriyor ya da yüklenmiyor.

**Adım 1 — Konteynerin çalıştığını doğrulayın:**

```bash
docker compose ps
```

Panel konteyneri çalışmıyorsa başlatın ve loglarda hata mesajı arayın.

**Adım 2 — UFW güvenlik duvarını kontrol edin:**

```bash
ufw status verbose
```

8420 portu listede yoksa ekleyin:

```bash
ufw allow 8420/tcp
```

**Adım 3 — Sağlayıcı güvenlik duvarını kontrol edin:**

Pek çok VPS sağlayıcısının kendi panelinde UFW'den bağımsız bir ağ güvenlik duvarı bulunur. Sağlayıcınızın kontrol paneline giriş yapın ve 8420 portuna gelen bağlantılara izin verildiğini doğrulayın.

**Adım 4 — Port bağlamasını doğrulayın:**

```bash
ss -tlnp | grep 8420
```

Beklenen çıktı `0.0.0.0:8420` veya `:::8420` adresinde dinleyen bir süreç gösterir. Çıktı boşsa konteyner portu doğru şekilde dışarıya açmıyordur — `docker-compose.yml` dosyasındaki port eşlemesini kontrol edin.

---

## Node Senkronize Olmuyor

**Belirti:** Panel node'un çalıştığını gösteriyor ancak blok yüksekliği artmıyor ya da loglarda tekrarlayan bağlantı hataları görünüyor.

**Adım 1 — İnternet bağlantısını kontrol edin:**

```bash
ping -c 4 google.com
curl -s https://api.github.com | head -c 50
```

**Adım 2 — RPC endpoint'i doğrulayın:**

`.env` dosyasındaki `RPC_ENDPOINT` değerinin doğru ve erişilebilir olduğunu kontrol edin:

```bash
curl -s BURAYA_RPC_ENDPOINT_URL_YAZIN
```

`BURAYA_RPC_ENDPOINT_URL_YAZIN` kısmını `.env` dosyanızdaki değerle değiştirin. Hata dönüyorsa veya çıktı yoksa endpoint hatalı ya da çevrimdışı olabilir.

**Adım 3 — Node'u yeniden başlatın:**

```bash
docker compose restart
```

İki-üç dakika bekleyin ve panelde blok yüksekliğinin artmaya başlayıp başlamadığını kontrol edin.

**Adım 4 — Node'u güncelleyin:**

Ağ güncellendiyse ve node sürümünüz eski kaldıysa senkronizasyon başarısız olabilir:

```bash
git pull
docker compose pull
docker compose up -d
```

---

## Docker Komutu Bulunamıyor

**Belirti:** Herhangi bir `docker` komutu `command not found` hatası veriyor.

**Çözüm:** Docker kurulu değil veya PATH ayarı hatalı. [Bölüm 02 — Docker Kurulumu](./02-docker-kurulumu.md) sayfasına dönüp Docker'ı yeniden kurun.

Docker yakın zamanda kurulduysa oturumu kapatıp yeniden açmayı deneyin, ardından komutu tekrar çalıştırın.

---

## Docker Çalıştırmak İçin İzin Reddedildi

**Belirti:** Docker komutları `sudo` olmadan çalıştırıldığında `permission denied` hatası veriyor.

**Neden:** Mevcut kullanıcı `docker` grubunda değil.

**Çözüm:** Kullanıcıyı docker grubuna ekleyin (`KULLANICI_ADI` kısmını değiştirin):

```bash
usermod -aG docker KULLANICI_ADI
```

Oturumu kapatıp yeniden açın, ardından doğrulayın:

```bash
docker run hello-world
```

`root` olarak çalışıyorsanız bu sorun sizin için geçerli değildir — root için tüm Docker komutları sudo olmadan çalışır.

---

## Disk Doldu

**Belirti:** Konteynerler çöküyor ya da başlamıyor; `df -h /` %100 kullanım gösteriyor.

**Adım 1 — Büyük dosyaları tespit edin:**

```bash
du -sh /opt/qorechain-light-node/*
docker system df
```

**Adım 2 — Docker kaynaklarını temizleyin:**

```bash
docker system prune -f
```

**Adım 3 — Log dosyası boyutlarını kontrol edin:**

Log dosyaları büyük yer kaplıyorsa [Bölüm 04 — İzleme ve Bakım](./04-izleme.md) sayfasında açıklanan log rotasyonunu yapılandırın.

**Adım 4 — Gerekirse diski genişletin:**

Temizlik yeterli gelmiyorsa depolama kapasitesini artırmak için sunucu planını yükseltin.

---

## Konteynerler Sürekli Yeniden Başlıyor

**Belirti:** `docker compose ps` konteynerleri `restarting` durumunda gösteriyor; node hiç kararlı hale gelmiyor.

**Tanı:**

```bash
docker compose logs --tail=50
```

Tekrarlayan hata kalıplarını arayın. Döngüde yeniden başlayan bir konteyner genellikle başlayıp kritik bir hatayla karşılaşıyor, çıkıyor ve Docker'ın yeniden başlatma politikası nedeniyle tekrar başlatılıyor demektir.

**Yaygın nedenler:**

- `.env` dosyasında bozuk veya eksik yapılandırma
- Node'un RPC endpoint'e ulaşmasını engelleyen ağ sorunu
- Kaynak tükenmesi (`free -h` ve `df -h /` ile kontrol edin)

Altta yatan nedeni giderin, ardından temiz bir başlatma yapın:

```bash
docker compose down
docker compose up -d
```

---

## Yeniden Başlatmadan Sonra SSH Bağlantısı Reddediliyor

**Belirti:** Sunucu yeniden başladıktan sonra SSH bağlantıları reddediliyor.

**Neden:** Parola kimlik doğrulaması devre dışı bırakıldıysa ve SSH anahtarı eksik veya hatalıysa erişim engelleniyor.

**Çözüm:** VPS sağlayıcınızın paneline giriş yapın ve acil durum konsolu ya da kurtarma modunu kullanarak sunucuya erişin. Buradan SSH anahtarı erişimini yeniden düzenleyebilir veya geçici olarak parola kimlik doğrulamasını yeniden etkinleştirebilirsiniz.

> Bu nedenle parola kimlik doğrulamasını devre dışı bırakmadan önce SSH anahtarıyla erişimi doğrulamak kritik önemdedir (Bölüm 01'de ele alınmıştır).

---

## Daha Fazla Yardım

Bu bölümdeki adımlar sorununuzu çözmezse:

1. [qorechain-guides issues](https://github.com/satoshi-Qore/qorechain-guides/issues) sayfasında benzer raporları arayın.
2. Aşağıdaki bilgilerle yeni bir issue açın:
   - Sunucu işletim sistemi ve sürümü (`lsb_release -a`)
   - Docker sürümü (`docker --version`)
   - `docker compose ps` çıktısı
   - `docker compose logs` içindeki ilgili satırlar

---

## Sorumluluk Reddi

Bu sayfa topluluk tarafından hazırlanan bir kaynaktır. Resmi QoreChain dokümantasyonunun yerini tutmaz. Hata mesajları ve davranışlar node sürümüne ve ağ durumuna göre farklılık gösterebilir. Kritik adımlarda her zaman resmi QoreChain kaynaklarını kontrol edin.

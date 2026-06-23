# Bölüm 05 — Sorun Giderme

Bu sayfa, QoreChain Light Node Rehberi'nin beşinci bölümüdür.

Bu bölümde yaygın kurulum sorunları, konteyner arızaları ve bağlantı hataları ele alınmakta; ayrıca node'u kurtarmak ve sıfırdan yeniden yüklemek için adım adım talimatlar verilmektedir.

---

## Ön Koşullar

Başlamadan önce Bölüm 03'ü tamamladığınızı ve node'un en az bir kez başarıyla çalıştığını doğrulayın. Kurulum sırasında yaşanan bir sorunla karşılaşıyorsanız önce Bölüm 03 talimatlarını gözden geçirin.

---

## Konteynerler Başlamıyor

Konteynerler `docker compose up -d` komutu sonrasında başlamazsa başarısızlık nedenini belirleyin.

### Konteyner Durumunu Kontrol Etme

```bash
cd /opt/qorechain-lightnode
docker compose ps
```

`exited` veya `restarting` durumu görünüyorsa logları kontrol edin:

```bash
docker compose logs qorechain-lightnode-sx
```

### Yaygın Nedenler

**`.env` dosyası eksik veya hatalı yapılandırılmış**

```bash
cat .env
```

`.env` dosyasının mevcut olduğunu ve gerekli değerlerin dolu olduğunu doğrulayın. Bölüm 03 talimatlarına göre eksik değerleri tamamlayın.

**Port çakışması**

```bash
ss -tlnp | grep 8420
```

8420 numaralı port başka bir servis tarafından kullanılıyorsa o servisi durdurun veya `docker-compose.yml` dosyasında port yapılandırmasını güncelleyin.

**İzin sorunu**

```bash
ls -la /opt/qorechain-lightnode
```

Dizinin geçerli kullanıcıya ait olduğunu doğrulayın. Gerekirse:

```bash
chown -R $USER:$USER /opt/qorechain-lightnode
```

---

## Konteynerlerin Sürekli Yeniden Başlaması

Konteynerler sürekli yeniden başlıyorsa (`restarting` durumu) altta yatan hatayı tespit edin.

```bash
docker compose logs --tail=50 qorechain-lightnode-sx
```

Belirleyici satırlar için loglara bakın (örneğin `ERROR`, `FATAL`, `panic`). En yaygın nedenler şunlardır:

- Geçersiz `.env` değerleri
- Ağ bağlantısı sorunları
- Disk doluluğu

Yeniden başlatma sayısını görmek için:

```bash
docker inspect qorechain-lightnode-sx | grep RestartCount
```

---

## Panel Yüklenmiyor

`http://SUNUCU_IP:8420` adresine erişemiyorsanız:

**Konteynerin çalıştığını doğrulayın:**

```bash
docker compose ps
```

**Güvenlik duvarı kurallarını kontrol edin:**

```bash
ufw status
```

8420 numaralı portun açık olduğunu doğrulayın. Kapalıysa:

```bash
ufw allow 8420/tcp
```

**Port bağlamasını doğrulayın:**

```bash
docker compose ps
```

Çıktıda `0.0.0.0:8420->8420/tcp` görünmelidir. Bu satır yoksa `docker-compose.yml` dosyasındaki port yapılandırmasını kontrol edin.

---

## Disk Alanı Doldu

Disk alanı dolduğunda konteynerler çalışmayı durdurabilir.

**Disk kullanımını kontrol edin:**

```bash
df -h /
```

**Node dizininin disk kullanımını kontrol edin:**

```bash
du -sh /opt/qorechain-lightnode/*
```

**Kullanılmayan Docker kaynaklarını temizleyin:**

```bash
docker system prune -f
```

Temizlik sonrasında konteynerleri yeniden başlatın:

```bash
cd /opt/qorechain-lightnode
docker compose up -d
```

---

## Node Yanıt Vermiyor

Node çalışıyor görünüyor ancak panel yüklenmiyor ya da senkronizasyon durmuşsa:

**Konteynerleri yeniden başlatın:**

```bash
cd /opt/qorechain-lightnode
docker compose restart
```

**Konteynerleri tamamen durdurup yeniden başlatın:**

```bash
docker compose down
docker compose up -d
```

**Logları canlı takip edin:**

```bash
docker compose logs -f
```

---

## Güncelleme Sonrasında Sorunlar

Son güncellemeden sonra bir sorun başladıysa en son değişikliği geri alabilirsiniz.

**Mevcut commit geçmişini görüntüleyin:**

```bash
cd /opt/qorechain-lightnode
git log --oneline -5
```

**Önceki commit'e geçin:**

```bash
git checkout <onceki-commit-hash>
docker compose pull
docker compose up -d
```

`<onceki-commit-hash>` değerini `git log` çıktısındaki ilgili hash ile değiştirin.

---

## Temiz Yeniden Yükleme

Yukarıdaki adımların hiçbiri sorunu çözmezse temiz bir yeniden yükleme yapabilirsiniz. Bu işlem yerel node verilerini siler; node senkronizasyona sıfırdan başlayacaktır.

> **Uyarı:** Devam etmeden önce `.env` dosyasını yedekleyin. Bu dosya yapılandırma değerlerinizi içermektedir.

```bash
cp /opt/qorechain-lightnode/.env ~/lightnode-env-yedek-$(date +%Y%m%d)
```

Mevcut kurulumu kaldırın:

```bash
cd /opt/qorechain-lightnode
docker compose down -v
cd /opt
rm -rf qorechain-lightnode
```

Bölüm 03 talimatlarını izleyerek node'u yeniden kurun. Kurulum tamamlandığında yedeğinizdeki `.env` değerlerini yeni `.env` dosyasına geri kopyalayın.

---

## Genel Kontrol Listesi

Sorun gidermeden önce bu temel kontrolleri yapın:

| Kontrol | Komut |
|---|---|
| Konteynerler çalışıyor mu? | `docker compose ps` |
| Son loglar | `docker compose logs --tail=50` |
| Disk alanı yeterli mi? | `df -h /` |
| Port açık mı? | `ss -tlnp \| grep 8420` |
| `.env` dosyası mevcut mu? | `cat /opt/qorechain-lightnode/.env` |
| Güvenlik duvarı açık mı? | `ufw status` |

---

## Sorumluluk Reddi

Bu sayfa topluluk tarafından hazırlanan bir kaynaktır. Resmi QoreChain dokümantasyonunun yerini tutmaz. Sorun giderme adımları proje geliştikçe değişebilir. Kritik sorunlarda her zaman resmi QoreChain kaynaklarını kontrol edin.

# Bölüm 04 — İzleme ve Bakım

Bu sayfa, QoreChain Light Node Rehberi'nin dördüncü bölümüdür.

Light Node çalışmaya başladıktan sonra bu bölümde node sağlığının izlenmesi, logların yönetimi, yazılımın güncel tutulması ve uzun vadeli kararlı çalışmayı sağlayacak rutin bakım görevleri ele alınmaktadır.

---

## Ön Koşullar

Başlamadan önce Bölüm 03'ün tamamlandığını doğrulayın:

| Kontrol | Beklenen Durum |
|---|---|
| Konteynerler çalışıyor | `docker compose ps` tüm konteynerleri `running` olarak gösteriyor |
| Panele erişildi | `http://SUNUCU_IP:8420` tarayıcıda yükleniyor |

Herhangi bir madde eksikse devam etmeden önce [Bölüm 03 — Light Node Kurulumu](./03-light-node-kurulumu.md) sayfasına dönün.

---

## Node Durumunu Kontrol Etme

### Konteyner Durumu

İstediğiniz zaman tüm konteynerlerin çalışıp çalışmadığını kontrol edin:

```bash
cd /opt/qorechain-light-node
docker compose ps
```

Listede yer alan tüm konteynerler `running` durumunu göstermelidir. Herhangi bir konteyner `exited` veya `restarting` gösteriyorsa o konteynerin loglarını kontrol edin.

### Kaynak Kullanımı

Çalışan konteynerlerin CPU, bellek ve ağ kullanımını izleyin:

```bash
docker stats
```

Bu komut canlı görünüm açar. Çıkmak için `Ctrl+C` tuşlarına basın.

Canlı görünüm yerine anlık bir değer almak için:

```bash
docker stats --no-stream
```

---

## Log Yönetimi

### Canlı Log Görüntüleme

Tüm konteynerlerden log akışı başlatın:

```bash
cd /opt/qorechain-light-node
docker compose logs -f
```

Yalnızca belirli bir konteynerin loglarını takip edin:

```bash
docker compose logs -f qorechain-light-node
```

Akışı durdurmak için `Ctrl+C` tuşlarına basın.

### Son Logları Görüntüleme

Tüm konteynerlerden son 100 satırı görüntüleyin:

```bash
docker compose logs --tail=100
```

### Log Rotasyonu

Docker varsayılan olarak logları otomatik döndürmez; bu da zamanla disk dolmasına yol açabilir. Her servis için `docker-compose.yml` dosyasına aşağıdaki bloğu ekleyerek log rotasyonunu yapılandırın:

```yaml
logging:
  driver: "json-file"
  options:
    max-size: "10m"
    max-file: "5"
```

Bu ayar her log dosyasını 10 MB ile sınırlar ve konteyner başına en fazla 5 döndürülmüş dosya tutar.

Dosyayı düzenledikten sonra değişikliğin geçerli olması için konteynerleri yeniden başlatın:

```bash
docker compose down
docker compose up -d
```

---

## Disk Alanı İzleme

Sunucudaki boş disk alanını kontrol edin:

```bash
df -h /
```

Docker'ın ne kadar alan kullandığını kontrol edin:

```bash
docker system df
```

### Kullanılmayan Docker Kaynaklarını Temizleme

Durdurulmuş konteynerleri, kullanılmayan imajları ve derleme önbelleğini silin:

```bash
docker system prune -f
```

> Bu komut çalışan konteynerleri veya aktif konteynerlere bağlı volume'leri silmez.

Kullanılmayan volume'leri de silmek için (dikkatli kullanın — önce önemli veri olmadığını doğrulayın):

```bash
docker system prune --volumes -f
```

---

## Light Node'u Güncelleme

Hata düzeltmeleri ve ağ uyumluluk güncellemelerini almak için node yazılımını güncel tutun.

### Güncelleme Kontrolü

Depodan en son değişiklikleri çekin:

```bash
cd /opt/qorechain-light-node
git fetch origin
git status
```

Çıktıda `Your branch is behind 'origin/main'` yazıyorsa güncelleme mevcuttur.

### Güncellemeyi Uygulama

```bash
git pull
docker compose pull
docker compose up -d
```

`docker compose pull` en son konteyner imajlarını indirir. `docker compose up -d` ise konteynerleri yeni imajlarla yeniden başlatır.

Güncellemeden sonra konteynerlerin çalıştığını doğrulayın:

```bash
docker compose ps
```

---

## Sunucu Yeniden Başlatmasından Sonra

Sunucu yeniden başlatıldıktan sonra konteynerler otomatik başlamadıysa manuel olarak başlatın:

```bash
cd /opt/qorechain-light-node
docker compose up -d
```

Sonraki yeniden başlatmalarda bu sorunun tekrarlanmaması için Docker'ın açılışta başlayacak şekilde ayarlandığını doğrulayın:

```bash
systemctl is-enabled docker
```

Beklenen çıktı: `enabled`

`disabled` dönüyorsa etkinleştirin:

```bash
systemctl enable docker
```

---

## Yapılandırma Yedeği

`.env` dosyası node yapılandırmanızı içerir. Periyodik olarak güvenli bir konuma yedekleyin.

```bash
cp /opt/qorechain-light-node/.env ~/lightnode-env-yedek-$(date +%Y%m%d)
```

Sunucunun yeniden kurulması gerektiğinde kullanabilmek için yedeği sunucu dışında (örneğin yerel bir dosyada veya parola yöneticisinde) saklayın.

---

## Bakım Kontrol Listesi

Node'un sağlıklı kalması için periyodik olarak aşağıdaki kontrolleri yapın.

| Görev | Önerilen Sıklık |
|---|---|
| Konteyner durumunu kontrol et (`docker compose ps`) | Günlük |
| Son loglarda hata ara | Günlük |
| Disk alanını kontrol et (`df -h /`) | Haftalık |
| `docker system prune -f` çalıştır | Haftalık |
| Depo güncellemelerini kontrol et (`git fetch`) | Haftalık |
| Mevcut güncellemeleri uygula | Yayımlandıkça |
| `.env` dosyasını yedekle | Her yapılandırma değişikliğinden sonra |

---

## Sonraki Bölüm

**[Bölüm 05 — Sorun Giderme](./05-sorun-giderme.md)**

Sonraki bölümde yaygın hatalar, konteyner arızaları, bağlantı sorunları ve senkronizasyonu duran ya da yanıt vermeyen bir node'u kurtarma adımları ele alınmaktadır.

---

## Sorumluluk Reddi

Bu sayfa topluluk tarafından hazırlanan bir kaynaktır. Resmi QoreChain dokümantasyonunun yerini tutmaz. Bakım prosedürleri ve güncelleme iş akışları proje geliştikçe değişebilir. Kritik adımlarda her zaman resmi QoreChain kaynaklarını kontrol edin.

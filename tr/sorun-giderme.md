# QoreChain Hafif Düğüm Sorun Giderme

Bu rehber, QoreChain Hafif Düğüm kurulumu ve işletişi sırasında karşılaşılan yaygın sorunları ve çözüm adımlarını kapsar.

Genel bakış için [Başlangıç Rehberi](./baslangic-rehberi.md) sayfasına bakın.
Tam operasyon rehberi için [Hafif Düğüm Operasyonları](./light-node-operasyonlari.md) sayfasına bakın.

---

## Panel Sorunları

### Panel 8420 portunda açılmıyor

**Belirtiler:** `http://SUNUCU_IP:8420` adresine erişmeye çalışınca bağlantı reddedildi veya zaman aşımı hatası alınıyor.

**Adımlar:**

1. Container'ların çalıştığını kontrol edin:
   ```bash
   docker ps
   ```
   Listede `qorechain-lightnode-sx` ve `qorechain-lightnode-ux` görünmelidir.

2. Container'lar çalışmıyorsa yeniden başlatın:
   ```bash
   docker compose up -d
   ```

3. Güvenlik duvarını kontrol edin:
   ```bash
   ufw status
   ```
   8420 portu listede yoksa ekleyin:
   ```bash
   ufw allow 8420/tcp
   ```

4. Sunucu sağlayıcınızın güvenlik grubu veya güvenlik duvarı kurallarını kontrol edin — 8420 portuna gelen TCP trafiğinin açık olması gerekir.

5. **Sunucunuzun genel IP adresine** bağlandığınızdan emin olun; `localhost` veya `127.0.0.1` kullanmayın.

### Panel açılıyor ama hatalar gösteriyor

**Adımlar:**

1. SX servis loglarını kontrol edin:
   ```bash
   docker logs qorechain-lightnode-sx
   ```

2. Tekrarlayan hatalar veya başlatma hataları arayın.

3. Loglar çöküp yeniden başlama döngüsü gösteriyorsa temiz yeniden başlatma deneyin:
   ```bash
   docker compose down
   docker compose up -d
   ```

---

## Container Sorunları

### Container'lar `docker ps` listesinde görünmüyor

**Adımlar:**

1. Proje dizinine gidin:
   ```bash
   cd qorechain-lightnode
   ```

2. Durmuş container'ları kontrol edin:
   ```bash
   docker ps -a
   ```

3. Servisleri başlatın:
   ```bash
   docker compose up -d
   ```

### Container başlayıp hemen duruyor

**Adımlar:**

1. Son logları görüntüleyin:
   ```bash
   docker logs qorechain-lightnode-sx --tail=50
   ```

2. Yaygın nedenler:
   - 8420 portu başka bir işlem tarafından kullanılıyor
   - Yetersiz disk alanı
   - Eksik veya bozulmuş yapılandırma dosyaları

3. Disk kullanımını kontrol edin:
   ```bash
   df -h
   ```

---

## Güncelleme Sorunları

### Güncelleme uygulanmadı

**Adımlar:**

1. Doğru dizinde olduğunuzdan emin olun:
   ```bash
   pwd
   ```
   Çıktı `/qorechain-lightnode` ile bitmeli.

2. Son değişiklikleri çekin:
   ```bash
   git pull
   ```

3. Güncel imajlarla tam yeniden başlatma yapın:
   ```bash
   docker compose down
   docker compose pull
   docker compose up -d
   ```

4. Güncelleme sonrası servislerin çalıştığını doğrulayun:
   ```bash
   docker ps
   docker logs qorechain-lightnode-sx --tail=20
   ```

---

## Ağ ve Stake Sorunları

### Düğüm çevrimdışı veya bağlantısız görünüyor

Şunları kontrol edin:
- Docker container'ları çalışıyor mu? (`docker ps`)
- 8420 portu internetten erişilebilir mi?
- Stake gereksinimi karşılanıyor mu? (minimum 1000 QOR)
- Son resmi QoreChain duyurularında ağ değişikliği var mı?

### Stake kontrolü başarısız oluyor

1000 QOR stake'i tutan cüzdan adresinin Light Node'a kayıtlı adres olduğunu doğrulayın. Stake rehberi için resmi QoreChain kanallarını kontrol edin.

---

## Genel Kontrol Listesi

Emin olmadığınızda bu kontrol listesini çalıştırın:

| Kontrol | Komut |
|---|---|
| Container'lar çalışıyor mu | `docker ps` |
| SX logları | `docker logs qorechain-lightnode-sx` |
| Güvenlik duvarı durumu | `ufw status` |
| Disk alanı | `df -h` |
| Proje dizini | `ls qorechain-lightnode/` |

---

## Sorumluluk Reddi

Bu rehber topluluk tarafından sürdürülen bir kaynaktır. QoreChain güncellemeleriyle komutlar ve prosedürler değişebilir. Herhangi bir işlem yapmadan önce her zaman resmi kaynaklar ve duyuruları doğrulayun.

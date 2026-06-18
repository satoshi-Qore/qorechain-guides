# Bölüm 03 — Light Node Kurulumu

Bu sayfa, QoreChain Light Node Rehberi'nin üçüncü bölümüdür.

Docker kurulumu ve sunucu hazırlığı tamamlandığında bu bölüme geçilebilir. Bu bölümde Light Node deposunun klonlanması, ortam değişkenlerinin yapılandırılması, konteynerlerin başlatılması ve node'un doğru çalıştığının doğrulanması ele alınmaktadır.

---

## Ön Koşullar

Başlamadan önce Bölüm 02'nin tamamlandığını doğrulayın:

| Kontrol | Beklenen Durum |
|---|---|
| Docker kuruldu | `docker --version` sürüm bilgisi döndürüyor |
| Docker Compose kuruldu | `docker compose version` sürüm bilgisi döndürüyor |
| Docker servisi etkinleştirildi | `systemctl is-enabled docker` → `enabled` |
| Docker servisi çalışıyor | `systemctl status docker` → `active (running)` |

Herhangi bir madde eksikse devam etmeden önce [Bölüm 02 — Docker Kurulumu](./02-docker-kurulumu.md) sayfasına dönün.

---

## Git Kurulumu

Light Node deposunu klonlamak için Git gereklidir. Kurulu değilse aşağıdaki komutla kurun.

```bash
apt-get install -y git
```

Kurulumu doğrulayın:

```bash
git --version
```

Beklenen çıktı:

```
git version 2.x.x
```

---

## Light Node Deposunu Klonlama

Node dosyalarını saklamak istediğiniz dizine gidin. Sunucu uygulamaları için `/opt` dizini yaygın bir tercihdir.

```bash
cd /opt
```

Depoyu klonlayın:

```bash
git clone https://github.com/satoshi-Qore/qorechain-light-node.git
```

Klonlanan dizine girin:

```bash
cd qorechain-light-node
```

Klonlama işleminin başarılı olduğunu doğrulamak için dizin içeriğini listeleyin:

```bash
ls -la
```

`docker-compose.yml` ve `.env.example` dosyalarını görmelisiniz.

---

## Ortam Değişkenlerini Yapılandırma

Light Node yapılandırmasını `.env` dosyasından okur. Örnek dosyayı kopyalayarak kendi dosyanızı oluşturun:

```bash
cp .env.example .env
```

Dosyayı düzenlemek için açın:

```bash
nano .env
```

Dosyada node'a ilişkin yapılandırma anahtarları bulunur. Gerekli değerleri güncelleyin:

| Değişken | Açıklama |
|---|---|
| `NODE_NAME` | Node'unuz için bir görünen ad (herhangi bir metin) |
| `PANEL_PORT` | Web paneli portu (varsayılan: `8420`) |
| `RPC_ENDPOINT` | QoreChain RPC endpoint URL'si |
| `WALLET_ADDRESS` | Operatör cüzdan adresiniz |

> Gerekli değişkenlerin güncel listesi ve geçerli RPC endpoint URL'leri için resmi QoreChain dokümantasyonunu veya depo README dosyasını kontrol edin.

Dosyayı kaydedin ve kapatın: `Ctrl+X`, ardından `Y`, ardından `Enter` tuşlarına basın.

---

## Panel Portunu Açma

Node'u başlatmadan önce web arayüzüne erişebilmek için UFW'de panel portunu açın.

```bash
ufw allow 8420/tcp
```

`.env` dosyasında `PANEL_PORT` değerini değiştirdiyseniz `8420` yerine seçtiğiniz port numarasını kullanın.

Güvenlik duvarı kurallarını doğrulayın:

```bash
ufw status verbose
```

Beklenen çıktıda `8420` portuna ait bir satır yer alır:

```
8420/tcp                   ALLOW IN    Anywhere
8420/tcp (v6)              ALLOW IN    Anywhere (v6)
```

---

## Light Node'u Başlatma

`docker-compose.yml` dosyasında tanımlı tüm konteynerleri arka planda başlatın:

```bash
docker compose up -d
```

İlk çalıştırmada Docker gerekli imajları indirir. Bu işlem bağlantı hızınıza bağlı olarak birkaç dakika sürebilir.

İlk çalıştırmadaki beklenen çıktı:

```
[+] Pulling images ...
[+] Running 2/2
 ✔ Container qorechain-light-node    Started
 ✔ Container qorechain-monitor       Started
```

---

## Node'un Çalıştığını Doğrulama

### Konteyner Durumunu Kontrol Etme

```bash
docker compose ps
```

Tüm konteynerler `running` durumunu göstermelidir:

```
NAME                     STATUS
qorechain-light-node     running
qorechain-monitor        running
```

### Node Loglarını Görüntüleme

Node'un hatasız başladığını doğrulamak için canlı log çıktısını kontrol edin:

```bash
docker compose logs -f
```

Ağa başarıyla bağlanıldığını gösteren satırları arayın. Log akışından çıkmak için `Ctrl+C` tuşlarına basın.

### Web Paneline Erişme

Bir tarayıcı açın ve şu adrese gidin:

```
http://SUNUCU_IP:8420
```

`SUNUCU_IP` kısmını sunucunuzun genel IP adresiyle değiştirin.

Panel yükleniyorsa node çalışıyor ve erişilebilir durumdadır.

---

## Node Yönetimi

### Node'u Durdurma

```bash
docker compose down
```

### Node'u Yeniden Başlatma

```bash
docker compose restart
```

### Node'u Güncelleme

Depodan en son değişiklikleri çekin ve konteynerleri yeniden oluşturun:

```bash
git pull
docker compose pull
docker compose up -d
```

---

## Kurulum Sonrası Kontrol Listesi

| Kontrol | Beklenen Durum |
|---|---|
| Depo klonlandı | `/opt/qorechain-light-node` dizini mevcut |
| `.env` yapılandırıldı | Gerekli değişkenler dolduruldu |
| Port 8420 açık | `ufw status` → `8420/tcp ALLOW` gösteriyor |
| Konteynerler çalışıyor | `docker compose ps` tüm konteynerleri `running` olarak gösteriyor |
| Loglar temiz | `docker compose logs` içinde hata satırı yok |
| Panele erişildi | `http://SUNUCU_IP:8420` tarayıcıda yükleniyor |

Tüm maddeler geçerliyse Light Node doğru çalışıyor demektir.

---

## Sorun Giderme

**Konteynerler başladıktan hemen sonra kapanıyor:**
`docker compose logs` komutunu çalıştırın ve yapılandırma hatalarını kontrol edin. En yaygın neden `.env` dosyasındaki eksik veya hatalı bir değerdir.

**Panele erişilemiyor:**
UFW'de 8420 portunun açık olduğunu doğrulayın (`ufw status`) ve VPS sağlayıcınızın panelinde ayrı bir ağ güvenlik duvarının portu engelleyip engellemediğini kontrol edin. Bazı sağlayıcıların kendi güvenlik duvarı arayüzü bulunur.

**Depo klonlanamıyor:**
Git'in kurulu olduğundan (`git --version`) ve sunucunun internete erişebildiğinden (`ping -c 4 github.com`) emin olun.

---

## Sonraki Bölüm

**[Bölüm 04 — İzleme ve Bakım](./04-izleme.md)**

Sonraki bölümde log izleme kurulumu, uyarı yapılandırması, node'un güncel tutulması ve rutin bakım görevleri ele alınmaktadır.

---

## Sorumluluk Reddi

Bu sayfa topluluk tarafından hazırlanan bir kaynaktır. Resmi QoreChain dokümantasyonunun yerini tutmaz. Depo URL'leri, ortam değişkeni adları ve port numaraları proje geliştikçe değişebilir. Kritik adımlarda her zaman resmi QoreChain kaynaklarını kontrol edin.

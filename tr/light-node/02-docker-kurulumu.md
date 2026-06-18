# Bölüm 02 — Docker Kurulumu

Bu sayfa, QoreChain Light Node Rehberi'nin ikinci bölümüdür.

QoreChain Light Node, Docker konteynerleri içinde çalışır. Bu bölümde Ubuntu 24.04 üzerine Docker Engine ve Docker Compose kurulumu, kurulumun doğrulanması ve node kurulumuna hazırlık adımları ele alınmaktadır.

---

## Ön Koşullar

Başlamadan önce Bölüm 01'in tamamlandığını doğrulayın.

| Kontrol | Beklenen Durum |
|---|---|
| Sunucu aktif | SSH bağlantısı çalışıyor |
| İşletim sistemi | Ubuntu 24.04 LTS |
| Sistem güncellendi | `apt update && apt upgrade -y` tamamlandı |
| Güvenlik duvarı aktif | UFW etkin, SSH izni verildi |

Herhangi bir madde eksikse devam etmeden önce [Bölüm 01 — Sunucu Hazırlığı](./01-sunucu-hazirligi.md) sayfasına dönün.

---

## Eski Docker Sürümlerini Kaldırma

Ubuntu'da farklı adlarla kurulu eski Docker paketleri olabilir. Çakışmaları önlemek için önce bunları kaldırın.

```bash
for pkg in docker.io docker-doc docker-compose docker-compose-v2 podman-docker containerd runc; do
  apt-get remove -y $pkg 2>/dev/null
done
```

Bu paketlerden hiçbiri kurulu değilse komut sessizce tamamlanır — bu beklenen davranıştır.

---

## Docker Engine Kurulumu

### Docker Deposunu Ekleme

Gerekli bağımlılıkları kurun:

```bash
apt-get install -y ca-certificates curl
```

apt anahtar dizinini oluşturun:

```bash
install -m 0755 -d /etc/apt/keyrings
```

Docker GPG anahtarını indirin ve ekleyin:

```bash
curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
chmod a+r /etc/apt/keyrings/docker.asc
```

Docker deposunu apt kaynaklarına ekleyin:

```bash
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  tee /etc/apt/sources.list.d/docker.list > /dev/null
```

Paket listesini güncelleyin:

```bash
apt-get update
```

---

### Docker Paketlerini Kurma

```bash
apt-get install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

Bu komut Docker Engine, CLI, konteyner çalışma zamanı ve Compose eklentisini kurar.

---

## Kurulumu Doğrulama

### Docker Sürümünü Kontrol Etme

```bash
docker --version
```

Beklenen çıktı (sürüm numaraları farklılık gösterebilir):

```
Docker version 27.x.x, build xxxxxxx
```

### Docker Compose Sürümünü Kontrol Etme

```bash
docker compose version
```

Beklenen çıktı:

```
Docker Compose version v2.x.x
```

### Test Konteynerini Çalıştırma

```bash
docker run hello-world
```

Beklenen çıktıda şu satır yer alır:

```
Hello from Docker!
This message shows that your installation appears to be working correctly.
```

Bu çıktı görünüyorsa Docker kurulumu çalışıyor demektir.

---

## Docker'ı Açılışta Başlatma

Sunucu yeniden başladığında Docker'ın otomatik olarak başlamasını sağlayın:

```bash
systemctl enable docker
systemctl enable containerd
```

Docker servisinin şu an çalıştığını doğrulayın:

```bash
systemctl status docker
```

Beklenen çıktı `Active: active (running)` gösterir.

---

## İsteğe Bağlı: Docker'ı sudo Olmadan Çalıştırma

Varsayılan olarak Docker komutları `root` veya `sudo` gerektirir. Node'u root olmayan bir kullanıcı olarak çalıştırmayı planlıyorsanız o kullanıcıyı `docker` grubuna ekleyin.

> Her şeyi `root` olarak çalıştırıyorsanız bu bölümü atlayın.

`KULLANICI_ADI` kısmını gerçek kullanıcı adıyla değiştirin:

```bash
usermod -aG docker KULLANICI_ADI
```

Grup değişikliğinin geçerli olması için oturumu kapatıp yeniden açın, ardından doğrulayın:

```bash
docker run hello-world
```

Komut `sudo` olmadan çalışmalıdır.

---

## Kurulum Sonrası Kontrol Listesi

Bir sonraki bölüme geçmeden önce aşağıdaki maddeleri doğrulayın.

| Kontrol | Beklenen Durum |
|---|---|
| Docker kuruldu | `docker --version` sürüm bilgisi döndürüyor |
| Docker Compose kuruldu | `docker compose version` sürüm bilgisi döndürüyor |
| hello-world konteyneri | Başarıyla çalıştı |
| Docker servisi etkinleştirildi | `systemctl is-enabled docker` → `enabled` |
| Docker servisi çalışıyor | `systemctl status docker` → `active (running)` |

Tüm maddeler geçerliyse ortam Light Node kurulumuna hazırdır.

---

## Sonraki Bölüm

**[Bölüm 03 — Light Node Kurulumu](./03-light-node-kurulumu.md)**

Sonraki bölümde Light Node deposunun klonlanması, ortam değişkenlerinin yapılandırılması, konteynerlerin başlatılması ve node'un çalıştığının doğrulanması ele alınmaktadır.

---

## Sorumluluk Reddi

Bu sayfa topluluk tarafından hazırlanan bir kaynaktır. Resmi QoreChain dokümantasyonunun yerini tutmaz. Docker kurulum adımları, Ubuntu 24.04 LTS için resmi Docker dokümantasyonunu takip etmektedir. Kritik adımlarda her zaman resmi kaynakları kontrol edin.

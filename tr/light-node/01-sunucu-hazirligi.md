# Bölüm 01 — Sunucu Hazırlığı

Bu sayfa, QoreChain Light Node Rehberi'nin birinci bölümüdür.

Herhangi bir yazılım kurmadan önce sunucunuzun doğru biçimde yapılandırılmış olması gerekir. Bu bölümde VPS sağlayıcı seçimi, sunucu oluşturma, SSH bağlantısı, sistem güncellemesi ve temel güvenlik duvarı kurulumu adım adım açıklanmaktadır.

---

## Önerilen Sunucu Gereksinimleri

QoreChain Light Node çalıştırmak için önerilen minimum değerler aşağıdaki tabloda yer almaktadır.

| Bileşen | Minimum | Önerilen |
|---|---|---|
| İşletim Sistemi | Ubuntu 24.04 LTS | Ubuntu 24.04 LTS |
| CPU | 2 vCPU | 4 vCPU |
| RAM | 4 GB | 8 GB |
| Disk | 50 GB SSD | 100 GB NVMe SSD |
| Ağ | 100 Mbps | 1 Gbps |
| Mimari | x86\_64 | x86\_64 |

> Sunucu hazırlamadan önce resmi QoreChain duyurularını kontrol edin. Ağ geliştikçe donanım gereksinimleri değişebilir.

---

## VPS Sağlayıcı Seçimi

Ubuntu 24.04 ve SSD desteği sunan herhangi bir VPS sağlayıcı kullanılabilir. Aşağıdaki sağlayıcılar operatör topluluğu tarafından yaygın biçimde tercih edilmektedir.

| Sağlayıcı | Öne Çıkan Özellik |
|---|---|
| Hetzner | Uygun fiyat, AB ve ABD konumları |
| DigitalOcean | Sade arayüz, iyi dokümantasyon, bireysel kullanıcılar için kolay başlangıç |
| Vultr | Global konumlar, esnek planlar |
| Contabo | Fiyata göre yüksek depolama kapasitesi |
| OVHcloud | Avrupa operatörleri için uygun fiyatlama |

Bütçenize ve tercih ettiğiniz sunucu konumuna göre bir sağlayıcı seçin. Yoğun saatlerde bant genişliğini kısıtlayan sağlayıcılardan kaçının.

> **Not:** Bu rehber hazırlanırken örnek VPS sağlayıcısı olarak [DigitalOcean](https://www.digitalocean.com/?refcode=f69c6b528fe5&utm_campaign=Referral_Invite&utm_medium=Referral_Program&utm_source=badge) kullanılmıştır. Basit arayüzü ve hızlı sunucu oluşturma süreci nedeniyle özellikle yeni başlayan kullanıcılar için uygun bir seçenek olabilir.
>
> [![DigitalOcean](https://img.shields.io/badge/DigitalOcean-Bu%20rehberde%20kullan%C4%B1ld%C4%B1%20%C2%B7%20KYC%20yok-0080FF?logo=digitalocean&logoColor=white&style=flat-square)](https://www.digitalocean.com/?refcode=f69c6b528fe5&utm_campaign=Referral_Invite&utm_medium=Referral_Program&utm_source=badge)

---

## DigitalOcean'da İlk Sunucunuzu Oluşturma

Bu rehber, daha önce hiç VPS kullanmamış kullanıcılar için hazırlanmıştır.

### 1. DigitalOcean Hesabı Oluşturun

- [DigitalOcean](https://www.digitalocean.com/?refcode=f69c6b528fe5&utm_campaign=Referral_Invite&utm_medium=Referral_Program&utm_source=badge) hesabınıza giriş yapın.
- Kontrol paneline ulaştığınızda sağ üst köşedeki **Create** butonuna tıklayın.
- Açılan menüden **Droplets** seçeneğini seçin.

### 2. İşletim Sistemini Seçin

"Choose an image" bölümünde:

- **Ubuntu** seçin.
- Sürüm olarak **Ubuntu 24.04 LTS** seçin.

Bu rehber Ubuntu 24.04 üzerinde hazırlanmıştır.

### 3. Sunucu Paketini Seçin

"Choose Size" bölümünde:

- **Basic** plan seçin.
- CPU seçeneklerinden **Regular (Shared CPU)** seçin.
- En az **2 GB RAM** içeren bir paket tercih edin.

### 4. Sunucu Bölgesini Seçin

"Choose Region" bölümünde size en yakın veri merkezini seçebilirsiniz. Örneğin:

- Frankfurt
- Amsterdam
- London

Bölge seçimi performansı etkileyebilir ancak kurulum adımlarını değiştirmez.

### 5. Giriş Yöntemini Belirleyin

"Authentication" bölümünde:

Yeni başlayanlar için:

- **Password** seçeneğini seçin.
- Güçlü bir root şifresi oluşturun.

Daha deneyimli kullanıcılar SSH Key kullanabilir.

### 6. Sunucuyu Oluşturun

Sayfanın altındaki **Create Droplet** butonuna tıklayın. Yaklaşık 1–2 dakika içinde sunucunuz hazır olacaktır.

### 7. Sunucu IP Adresini Bulun

Sunucu oluşturulduktan sonra kontrol panelinde yeni Droplet'iniz görünecektir. Sunucu adının yanında şuna benzer bir IP adresi yer alacaktır:

```
123.45.67.89
```

Bu adres sunucunuza bağlanmak için kullanılacaktır.

### 8. Sunucuya Bağlanın

**Windows kullanıcıları için:**

PowerShell'i açın ve aşağıdaki komutu çalıştırın:

```powershell
ssh root@SUNUCU_IP_ADRESI
```

Örnek:

```powershell
ssh root@123.45.67.89
```

İlk bağlantıda onay sorulursa `yes` yazıp Enter'a basın. Şifre istendiğinde oluşturduğunuz root şifresini girin.

Başarılı giriş yaptıysanız artık sunucunuzun terminaline bağlanmış olursunuz ve Light Node kurulumuna geçebilirsiniz.

---

## SSH Bağlantısı

### SSH Anahtarı Oluşturma

Daha önce oluşturulmuş bir SSH anahtarınız yoksa aşağıdaki komutla oluşturun.

**Linux / macOS:**

```bash
ssh-keygen -t ed25519 -C "email@adresiniz.com"
```

Enter tuşuna basarak varsayılan dosya konumunu kabul edin. Anahtar çifti `~/.ssh/` dizinine kaydedilir.

**Windows (PowerShell):**

```powershell
ssh-keygen -t ed25519 -C "email@adresiniz.com"
```

Anahtar çifti `C:\Users\KullaniciAdiniz\.ssh\` dizinine kaydedilir.

---

### Önerilen: Parola Kimlik Doğrulamasını Devre Dışı Bırakma

SSH anahtarıyla erişimin çalıştığını onayladıktan sonra brute-force riskini azaltmak için parola kimlik doğrulamasını devre dışı bırakın.

```bash
sed -i 's/^#*PasswordAuthentication.*/PasswordAuthentication no/' /etc/ssh/sshd_config
systemctl restart ssh
```

Mevcut oturumu kapatmadan önce SSH anahtarıyla hâlâ bağlanabildiğinizi doğrulayın.

---

## Sistem Güncellemesi

Bağlandıktan sonra paket listesini güncelleyin ve kurulu paketleri yükseltin.

```bash
apt update && apt upgrade -y
```

Bu işlem birkaç dakika sürebilir. Hizmetlerin yeniden başlatılmasına ilişkin bir istem görünürse Enter'a basarak varsayılanları kabul edin.

Çekirdek güncellemelerini uygulamak için sunucuyu yeniden başlatın.

```bash
reboot
```

Yaklaşık 30 saniye bekleyin, ardından SSH ile yeniden bağlanın.

---

## Kaynak Doğrulama

Sunucu kaynaklarının satın aldığınız planla eşleştiğini doğrulayın.

**CPU çekirdek sayısını kontrol edin:**

```bash
nproc
```

**Kullanılabilir belleği kontrol edin:**

```bash
free -h
```

**Disk alanını kontrol edin:**

```bash
df -h /
```

**İşletim sistemi sürümünü kontrol edin:**

```bash
lsb_release -a
```

OS kontrolü için beklenen çıktı:

```
Description:    Ubuntu 24.04 LTS
```

Herhangi bir değer önerilen minimumun belirgin biçimde altındaysa devam etmeden önce planı yükseltmeyi değerlendirin.

---

## Temel UFW Güvenlik Duvarı Kurulumu

UFW (Uncomplicated Firewall) Ubuntu ile birlikte gelir. Yalnızca ihtiyaç duyduğunuz portlara izin verin.

Önce SSH'e izin verin — bu adım kritiktir. Atlanırsa sunucuya erişim kesilebilir.

```bash
ufw allow ssh
```

Güvenlik duvarını etkinleştirin:

```bash
ufw enable
```

Mevcut güvenlik duvarı durumunu kontrol edin:

```bash
ufw status verbose
```

Beklenen çıktı:

```
Status: active
To                         Action      From
--                         ------      ----
22/tcp                     ALLOW IN    Anywhere
22/tcp (v6)                ALLOW IN    Anywhere (v6)
```

> Light Node tarafından gerektirilen ek portlar (örneğin panel portu `8420`) Docker kurulduktan ve node çalışmaya başladıktan sonraki bölümde açılacaktır.

---

## İnternet Bağlantısı Testi

Sunucunun internete erişebildiğini doğrulayın.

```bash
ping -c 4 google.com
```

Beklenen çıktı dört paket gönderilip alındığını ve paket kaybı olmadığını gösterir:

```
4 packets transmitted, 4 received, 0% packet loss
```

DNS çözümlemesinin de çalıştığını doğrulayın:

```bash
curl -s https://api.github.com | head -c 100
```

Her iki komut da beklenen çıktıyı döndürüyorsa sunucu internet erişimine ve çalışan DNS'e sahiptir.

---

## Kurulum Öncesi Kontrol Listesi

Bir sonraki bölüme geçmeden önce aşağıdaki maddeleri doğrulayın.

| Kontrol | Beklenen Durum |
|---|---|
| Sunucu aktif | SSH bağlantısı çalışıyor |
| İşletim sistemi | Ubuntu 24.04 LTS |
| CPU | 2+ çekirdek doğrulandı |
| RAM | 4 GB+ doğrulandı |
| Disk | 50 GB+ boş alan |
| Sistem güncellendi | `apt update && apt upgrade -y` tamamlandı |
| Güvenlik duvarı aktif | UFW etkin, SSH izni verildi |
| İnternet erişimi | Ping ve curl beklenen çıktıyı verdi |

Tüm maddeler geçerliyse sunucu bir sonraki adıma hazırdır.

---

## Sonraki Bölüm

**[Bölüm 02 — Docker Kurulumu](./02-docker-kurulumu.md)**

Sonraki bölümde Ubuntu 24.04 üzerine Docker ve Docker Compose kurulumu, kurulumun doğrulanması ve Light Node kurulumu için ortamın hazırlanması ele alınmaktadır.

---

## Sorumluluk Reddi

Bu sayfa topluluk tarafından hazırlanan bir kaynaktır. Resmi QoreChain dokümantasyonunun yerini tutmaz. Sunucu gereksinimleri, port numaraları ve ağ kuralları proje geliştikçe değişebilir. Kritik adımlarda her zaman resmi QoreChain kaynaklarını kontrol edin.

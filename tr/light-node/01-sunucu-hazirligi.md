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
| DigitalOcean | Sade arayüz, iyi dokümantasyon |
| Vultr | Global konumlar, esnek planlar |
| Contabo | Fiyata göre yüksek depolama kapasitesi |
| OVHcloud | Avrupa operatörleri için uygun fiyatlama |

Bütçenize ve tercih ettiğiniz sunucu konumuna göre bir sağlayıcı seçin. Yoğun saatlerde bant genişliğini kısıtlayan sağlayıcılardan kaçının.

---

## Ubuntu 24.04 Sunucu Oluşturma

Adımlar sağlayıcıya göre farklılık gösterebilir, ancak genel akış aynıdır.

1. VPS sağlayıcınızın paneline giriş yapın.
2. **Oluştur** veya **Yeni Sunucu Dağıt** seçeneğine tıklayın.
3. İşletim sistemi olarak **Ubuntu 24.04 LTS** seçin.
4. Minimum gereksinimleri karşılayan bir plan seçin.
5. **Kimlik doğrulama yöntemi** olarak SSH anahtarı seçin — parola yerine SSH anahtarı kesinlikle önerilir.
6. Bir sunucu adı belirleyin (örnek: `qorechain-lightnode`).
7. **Dağıt**'a tıklayın ve sunucunun aktif hale gelmesini bekleyin (genellikle iki dakikadan az sürer).

Sunucu aktif hale geldiğinde **genel IP adresini** not alın. Bir sonraki adımda bu adresi kullanacaksınız.

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

### Sunucuya Bağlanma

`SUNUCU_IP` kısmını gerçek IP adresinizle değiştirin.

**Linux / macOS:**

```bash
ssh root@SUNUCU_IP
```

**Windows (PowerShell veya Windows Terminal):**

```powershell
ssh root@SUNUCU_IP
```

İlk bağlantıda parmak izi onayı istenir:

```
The authenticity of host 'SUNUCU_IP' can't be established.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
```

`yes` yazıp Enter'a basın.

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

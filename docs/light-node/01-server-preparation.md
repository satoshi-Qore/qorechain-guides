# Bölüm 01 — Sunucu Hazırlığı / Chapter 01 — Server Preparation

Bu sayfa, QoreChain Light Node Rehberi'nin birinci bölümüdür.

This is the first chapter of the QoreChain Light Node Guide.

Herhangi bir yazılım kurmadan önce sunucunuzun doğru biçimde yapılandırılmış olması gerekir. Bu bölümde VPS sağlayıcı seçimi, sunucu oluşturma, SSH bağlantısı, sistem güncellemesi ve temel güvenlik duvarı kurulumu adım adım açıklanmaktadır.

Before installing any software, you need a properly configured server. This chapter walks through choosing a VPS provider, creating a server, connecting via SSH, applying system updates, and setting up a basic firewall.

---

## Önerilen Sunucu Gereksinimleri / Recommended Server Requirements

QoreChain Light Node çalıştırmak için önerilen minimum değerler aşağıdaki tabloda yer almaktadır.

The following specifications are the recommended minimum baseline for running a QoreChain Light Node.

| Bileşen / Component | Minimum | Önerilen / Recommended |
|---|---|---|
| İşletim Sistemi / OS | Ubuntu 24.04 LTS | Ubuntu 24.04 LTS |
| CPU | 2 vCPU | 4 vCPU |
| RAM | 4 GB | 8 GB |
| Disk | 50 GB SSD | 100 GB NVMe SSD |
| Ağ / Network | 100 Mbps | 1 Gbps |
| Mimari / Architecture | x86\_64 | x86\_64 |

> Sunucu hazırlamadan önce resmi QoreChain duyurularını kontrol edin. Ağ geliştikçe donanım gereksinimleri değişebilir.
>
> Always check the latest official QoreChain announcements before provisioning. Hardware requirements may change as the network evolves.

---

## VPS Sağlayıcı Seçimi / VPS Provider Selection

Ubuntu 24.04 ve SSD desteği sunan herhangi bir VPS sağlayıcı kullanılabilir. Aşağıdaki sağlayıcılar operatör topluluğu tarafından yaygın biçimde tercih edilmektedir.

Any VPS provider that offers Ubuntu 24.04 and SSD-backed storage is suitable. The following are commonly used by the operator community.

| Sağlayıcı / Provider | Öne Çıkan Özellik / Notable For |
|---|---|
| Hetzner | Uygun fiyat, AB ve ABD konumları / Cost-effective, EU and US locations |
| DigitalOcean | Sade arayüz, iyi dokümantasyon / Simple UI, well-documented |
| Vultr | Global konumlar, esnek planlar / Global locations, flexible plans |
| Contabo | Fiyata göre yüksek depolama / High storage per dollar |
| OVHcloud | Avrupa operatörleri için uygun fiyatlama / European operator-friendly pricing |

Bütçenize ve tercih ettiğiniz sunucu konumuna göre bir sağlayıcı seçin. Yoğun saatlerde bant genişliğini kısıtlayan sağlayıcılardan kaçının.

Choose a provider based on your budget and preferred server location. Avoid providers that throttle network bandwidth during peak hours.

---

## Ubuntu 24.04 Sunucu Oluşturma / Creating an Ubuntu 24.04 Server

Adımlar sağlayıcıya göre farklılık gösterebilir, ancak genel akış aynıdır.

The exact steps vary by provider, but the general flow is the same.

1. VPS sağlayıcınızın paneline giriş yapın. / Log in to your VPS provider's dashboard.
2. **Oluştur** veya **Yeni Sunucu Dağıt** seçeneğine tıklayın. / Click **Create** or **Deploy New Server**.
3. İşletim sistemi olarak **Ubuntu 24.04 LTS** seçin. / Select **Ubuntu 24.04 LTS** as the operating system.
4. Minimum gereksinimleri karşılayan bir plan seçin. / Choose a plan that meets the minimum requirements above.
5. **Kimlik doğrulama yöntemi** olarak SSH anahtarı seçin — parola yerine SSH anahtarı kesinlikle önerilir. / Set your **authentication method** — SSH key is strongly recommended over password.
6. Bir sunucu adı belirleyin (örnek: `qorechain-lightnode`). / Assign a server hostname (for example: `qorechain-lightnode`).
7. **Dağıt**'a tıklayın ve sunucunun aktif hale gelmesini bekleyin (genellikle iki dakikadan az sürer). / Click **Deploy** and wait for the server to become active (usually under two minutes).

Sunucu aktif hale geldiğinde **genel IP adresini** not alın. Bir sonraki adımda bu adresi kullanacaksınız.

Once the server is active, note down the **public IP address**. You will use it in the next step.

---

## SSH Bağlantısı / SSH Connection

### SSH Anahtarı Oluşturma / Generating an SSH Key

Daha önce oluşturulmuş bir SSH anahtarınız yoksa aşağıdaki komutla oluşturun.

If you do not already have an SSH key, generate one with the following command.

**Linux / macOS:**

```bash
ssh-keygen -t ed25519 -C "email@adresiniz.com"
```

Enter tuşuna basarak varsayılan dosya konumunu kabul edin. Anahtar çifti `~/.ssh/` dizinine kaydedilir.

Press Enter to accept the default file location. The key pair is saved to `~/.ssh/`.

**Windows (PowerShell):**

```powershell
ssh-keygen -t ed25519 -C "email@adresiniz.com"
```

Anahtar çifti `C:\Users\KullaniciAdiniz\.ssh\` dizinine kaydedilir.

The key pair is saved to `C:\Users\YourUsername\.ssh\`.

---

### Sunucuya Bağlanma / Connecting to the Server

`SUNUCU_IP` kısmını gerçek IP adresinizle değiştirin.

Replace `YOUR_SERVER_IP` with your actual server IP address.

**Linux / macOS:**

```bash
ssh root@SUNUCU_IP
```

**Windows (PowerShell veya Windows Terminal):**

```powershell
ssh root@YOUR_SERVER_IP
```

İlk bağlantıda parmak izi onayı istenir:

On first connection, you will see a fingerprint confirmation prompt:

```
The authenticity of host 'YOUR_SERVER_IP' can't be established.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
```

`yes` yazıp Enter'a basın. / Type `yes` and press Enter.

---

### Önerilen: Parola Kimlik Doğrulamasını Devre Dışı Bırakma / Recommended: Disable Password Authentication

SSH anahtarıyla erişimin çalıştığını onayladıktan sonra brute-force riskini azaltmak için parola kimlik doğrulamasını devre dışı bırakın.

After confirming SSH key access works, disable password authentication to reduce brute-force risk.

```bash
sed -i 's/^#*PasswordAuthentication.*/PasswordAuthentication no/' /etc/ssh/sshd_config
systemctl restart ssh
```

Mevcut oturumu kapatmadan önce SSH anahtarıyla bağlanabildiğinizi doğrulayın.

Verify that you can still connect via SSH key before closing the current session.

---

## Sistem Güncellemesi / System Updates

Bağlandıktan sonra paket listesini güncelleyin ve kurulu paketleri yükseltin.

After connecting, update the package lists and upgrade installed packages.

```bash
apt update && apt upgrade -y
```

Bu işlem birkaç dakika sürebilir. Hizmetlerin yeniden başlatılmasına ilişkin bir istem görünürse Enter'a basarak varsayılanları kabul edin.

This may take a few minutes. If a prompt asks about restarting services, press Enter to accept the defaults.

Çekirdek güncellemelerini uygulamak için sunucuyu yeniden başlatın.

Reboot the server to apply any kernel updates.

```bash
reboot
```

Yaklaşık 30 saniye bekleyin, ardından SSH ile yeniden bağlanın.

Wait about 30 seconds, then reconnect via SSH.

---

## Kaynak Doğrulama / Resource Verification

Sunucu kaynaklarının satın aldığınız planla eşleştiğini doğrulayın.

Confirm the server resources match what you provisioned.

**CPU çekirdek sayısını kontrol edin / Check CPU core count:**

```bash
nproc
```

**Kullanılabilir belleği kontrol edin / Check available memory:**

```bash
free -h
```

**Disk alanını kontrol edin / Check disk space:**

```bash
df -h /
```

**İşletim sistemi sürümünü kontrol edin / Check OS version:**

```bash
lsb_release -a
```

OS kontrolü için beklenen çıktı / Expected output for the OS check:

```
Description:    Ubuntu 24.04 LTS
```

Herhangi bir değer önerilen minimumun belirgin biçimde altındaysa devam etmeden önce planı yükseltmeyi değerlendirin.

If any value is significantly below the recommended baseline, consider upgrading the plan before proceeding.

---

## Temel UFW Güvenlik Duvarı Kurulumu / Basic UFW Firewall Setup

UFW (Uncomplicated Firewall) Ubuntu ile birlikte gelir. Yalnızca ihtiyaç duyduğunuz portlara izin verin.

UFW (Uncomplicated Firewall) is included with Ubuntu. Enable it and allow only the ports you need.

Önce SSH'e izin verin — bu adım kritiktir. Atlanırsa sunucuya erişim kesilebilir.

Allow SSH first — this is critical. Do not skip this step or you will lock yourself out.

```bash
ufw allow ssh
```

Güvenlik duvarını etkinleştirin / Enable the firewall:

```bash
ufw enable
```

Mevcut güvenlik duvarı durumunu kontrol edin / Check the current firewall status:

```bash
ufw status verbose
```

Beklenen çıktı / Expected output:

```
Status: active
To                         Action      From
--                         ------      ----
22/tcp                     ALLOW IN    Anywhere
22/tcp (v6)                ALLOW IN    Anywhere (v6)
```

> Light Node tarafından gerektirilen ek portlar (örneğin panel portu `8420`) Docker kurulduktan ve node çalışmaya başladıktan sonraki bölümde açılacaktır.
>
> Additional ports required by the Light Node (such as the panel port `8420`) will be opened in a later chapter after Docker is installed and the node is running.

---

## İnternet Bağlantısı Testi / Internet Connectivity Test

Sunucunun internete erişebildiğini doğrulayın.

Confirm the server can reach the internet.

```bash
ping -c 4 google.com
```

Beklenen çıktı dört paket gönderilip alındığını ve paket kaybı olmadığını gösterir.

Expected output shows four packets sent and received with no packet loss.

```
4 packets transmitted, 4 received, 0% packet loss
```

DNS çözümlemesinin de çalıştığını doğrulayın / Also confirm DNS resolution is working:

```bash
curl -s https://api.github.com | head -c 100
```

Her iki komut da beklenen çıktıyı döndürüyorsa sunucu internet erişimine ve çalışan DNS'e sahiptir.

If both commands return expected output, the server has internet access and DNS is functioning correctly.

---

## Kurulum Öncesi Kontrol Listesi / Pre-Installation Checklist

Bir sonraki bölüme geçmeden önce aşağıdaki maddeleri doğrulayın.

Before moving to the next chapter, verify the following items.

| Kontrol / Check | Beklenen Durum / Expected State |
|---|---|
| Sunucu aktif / Server active | SSH bağlantısı çalışıyor / SSH connection works |
| İşletim sistemi / OS version | Ubuntu 24.04 LTS |
| CPU | 2+ çekirdek doğrulandı / 2+ cores confirmed |
| RAM | 4 GB+ doğrulandı / 4 GB+ confirmed |
| Disk | 50 GB+ boş alan / 50 GB+ free space |
| Sistem güncellendi / System updated | `apt update && apt upgrade -y` tamamlandı / completed |
| Güvenlik duvarı aktif / Firewall active | UFW etkin, SSH izni verildi / UFW enabled, SSH allowed |
| İnternet erişimi / Internet access | Ping ve curl beklenen çıktıyı verdi / Ping and curl returned expected output |

Tüm maddeler geçerliyse sunucu bir sonraki adıma hazırdır.

If all items pass, the server is ready for the next step.

---

## Sonraki Bölüm / Next Chapter

**[Bölüm 02 — Docker Kurulumu / Chapter 02 — Docker Installation](./02-docker-installation.md)**

Sonraki bölümde Ubuntu 24.04 üzerine Docker ve Docker Compose kurulumu, kurulumun doğrulanması ve Light Node kurulumu için ortamın hazırlanması ele alınmaktadır.

The next chapter covers installing Docker and Docker Compose on Ubuntu 24.04, verifying the installation, and preparing the environment for the Light Node setup.

---

## Sorumluluk Reddi / Disclaimer

Bu sayfa topluluk tarafından hazırlanan bir kaynaktır. Resmi QoreChain dokümantasyonunun yerini tutmaz. Sunucu gereksinimleri, port numaraları ve ağ kuralları proje geliştikçe değişebilir. Kritik adımlarda her zaman resmi QoreChain kaynaklarını kontrol edin.

This document is a community-maintained resource. It does not replace official QoreChain documentation. Server requirements, port numbers, and network rules may change as the project evolves. Always verify critical details through official QoreChain sources before proceeding.

# QoreChain SSS (Sık Sorulan Sorular)

Bu SSS, yaygın QoreChain topluluk sorularına kısa yanıtlar sunar. Bağımsız bir topluluk kaynağı olarak hazırlanmıştır ve resmi QoreChain belgelerinin veya duyurularının yerini tutmaz.

QoreChain'e yeni mi başlıyorsunuz? [Başlangıç Rehberi](./baslangic-rehberi.md) ile başlayın.

---

## Genel

### QoreChain Nedir?

QoreChain; kuantum sonrası güvenlik, çoklu VM yürütme, yapay zeka altyapısı ve zincirler arası blok zinciri mimarisine odaklanan bir Katman 1 blok zinciri projesidir.

### Bu depo resmi mi?

Hayır. Bu depo topluluk tarafından sürdürülmektedir. Kritik kararlar, ağ parametreleri, sürümler ve ana ağ ayrıntıları için her zaman resmi QoreChain kaynaklarını kontrol edin.

### QoreChain neden kuantum sonrası güvenliğe odaklanıyor?

Kuantum bilişimin gelişmesiyle mevcut kriptografik algoritmalar kırılabilir hale gelebilir. Blok zinciri sistemlerinde imzalar, anahtarlar ve işlem yetkilendirmesi kriptografik varsayımlara ağır şekilde bağlıdır; QoreChain bu riski baştan çözmek üzere tasarlanmıştır.

### QOR tokeni nedir?

QOR, QoreChain ağının yerli tokenıdır. Stake (Hafif Düğüm çalıştırmak için gerekli), işlem ücretleri ve yönetişime katılım için kullanılır.

---

## Hafif Düğüm

### Hafif Düğüm nedir?

Hafif Düğüm (Light Node), tam blok zinciri verisi gerektirmeksizin ağ erişimi, istek işleme ve operatör tarafı kullanılabilirliğine yardımcı olan hafif bir ağ katılımcısıdır.

### Hangi donanıma ihtiyacım var?

Küçük bir VPS yeterlidir. Minimum: Ubuntu 20.04+, 2 CPU çekirdeği, 4 GB RAM, 50 GB SSD, Docker, Docker Compose. Tam rehber için [Hafif Düğüm Operasyonları](./light-node-operasyonlari.md) sayfasına bakın.

### Hafif Düğüm operatörleri ödül alıyor mu?

Hafif Düğüm çalıştırmak QoreChain ekosistem görevleri ve puan tabanlı etkinliklerin bir parçası olarak görünmektedir. Gerçek token ödülü veya ana ağ teşviği ayrıntıları resmi duyurulardan doğrulanmalıdır.

### Panel 8420 portunda açılmıyorsa ne yapmalıyım?

Temel kontrolleri yapın:

1. Sunucunun çevrimiçi olduğunu doğrulayın.
2. Hafif Düğüm servisinin çalıştığını doğrulayın.
3. Doğru IP ve port (8420) kullanıldığını kontrol edin.
4. Güvenlik duvarı ayarlarını kontrol edin: `ufw status` — 8420 portuna izin verilmiş olmalı.
5. Başlatma veya bağlantı hataları için logları kontrol edin.

Yaygın sorunların tam listesi için [Sorun Giderme](./sorun-giderme.md) sayfasına bakın.

### Hafif Düğümü nasıl güncellerim?

```bash
cd qorechain-lightnode
git pull
docker compose down
docker compose pull
docker compose up -d
```

Güncellemeden önce her zaman resmi QoreChain duyurularını kontrol edin.

---

## Görevler ve Kanıt

### Kanıt linki oluşturmayan görevler için ne göndermeliyim?

Doğrudan kanıt linki oluşmuyorsa, mevcut en ilgili genel linki gönderin ve tamamladığınızı kısaca açıklayın. Platform ekran görüntüsüne izin veriyorsa destek kanıtı olarak ekleyin.

---

## Katkı

### Bu depoya nasıl katkıda bulunabilirim?

Düzeltme önerebilir, eksik açıklamalar ekleyebilir, iki dilli uyumu iyileştirebilir veya pratik kurulum ve sorun giderme notları yazabilirsiniz. Bakınız: [CONTRIBUTING.md](../CONTRIBUTING.md).

### Yeni bir doküman sayfası nasıl talep ederim?

[İçerik Talebi issue şablonunu](../.github/ISSUE_TEMPLATE/content-request.md) kullanın.

### Çeviri nasıl talep ederim?

[Çeviri Talebi issue şablonunu](../.github/ISSUE_TEMPLATE/translation-request.md) kullanın.

### Türkçe katkıda bulunabilir miyim?

Evet. Türkçe içerik `tr/` klasörüne aittir. Mevcut çeviri durumu için [docs/translation-status.md](../docs/translation-status.md) sayfasına bakın.

### Yeni içerik hangi stili izlemelidir?

İçeriği kısa, pratik, tarafsız ve doğrulanabilir tutun. Tanıtım nitelikli ifadeler, desteksiz ödül açıklamaları ve ana ağ varsayımlarından kaçının. Bakınız: [STYLE_GUIDE.md](../STYLE_GUIDE.md).

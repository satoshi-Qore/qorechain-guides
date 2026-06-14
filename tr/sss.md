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

İçeriği kısa, pratik, tarafsız ve doğrulanabilir tutun. Tanıtım nitelikli ifadeler, desteksiz ödül açıklamaları ve ana ağ varsayımlarından kaçının. Bakınız: [STYLE_GUIDE.md](../STYLE_GUIDE.md).# QoreChain SSS

Bu SSS sayfasi, QoreChain toplulugunda sık sorulan sorulara kisa yanitlar toplar. Bu sayfa bagimsiz bir topluluk kaynagidir; resmi QoreChain dokumantasyonu veya duyurularinin yerine gecmez.

## Genel

### QoreChain nedir?

QoreChain; kuantum sonrasi guvenlik, coklu VM mimarisi, yapay zeka odakli altyapi ve aglar arasi blokzincir mimarisi konularina odaklanan bir Katman 1 blokzincir projesidir.

### Bu depo resmi mi?

Hayir. Bu depo topluluk tarafindan hazirlanir. Kritik kararlar, ag parametreleri, surumler ve mainnet ile ilgili detaylar icin her zaman resmi QoreChain kaynaklari kontrol edilmelidir.

### QoreChain neden kuantum sonrasi guvenlige odaklanir?

Kuantum sonrasi guvenlik, kuantum bilgisayarlarin gelisimiyle daha onemli hale gelebilecek uzun vadeli kriptografik riskleri hedefler. Blokzincir sistemlerinde imzalar, anahtarlar ve islem yetkilendirme kriptografik varsayimlara dayandigi icin bu konu onemlidir.

## Light Node

### Light Node nedir?

Light Node, ag erisimi, istek hizmeti ve operator tarafli erisilebilirlik gibi sureclere yardimci olabilen hafif bir ag katilimcisidir. Kesin operasyon gereksinimleri icin guncel resmi QoreChain talimatlari kontrol edilmelidir.

### Light Node operatorleri odul alir mi?

Light Node calistirma, QoreChain ekosistem gorevleri ve puan tabanli aktiviteler arasinda yer alir. Gercek token odulu, komisyon veya mainnet tesvikleriyle ilgili bilgiler resmi duyurularla dogrulanmalidir.

### Light Node paneli acilmiyorsa ilk ne kontrol edilmeli?

Temel kontrollerle baslayin:

- Sunucunun acik oldugunu kontrol edin.
- Light Node servisinin veya container yapisinin calistigini kontrol edin.
- Dogru IP adresi ve port kullanildigindan emin olun.
- Firewall ve sunucu saglayici guvenlik kurallarini kontrol edin.
- Baslatma veya baglanti hatalari icin loglari inceleyin.

## Gorevler ve Kanit

### Kanit linki olusturmayan gorevlerde ne sunulmali?

Gorev dogrudan kanit linki olusturmuyorsa, mumkun olan en ilgili herkese acik linki ekleyin ve yaptiginiz islemi kisa ve net sekilde aciklayin. Platform ekran goruntusu kabul ediyorsa destekleyici kanit olarak ekran goruntusu kullanilabilir.

### Topluluk rehberleri gorev kaniti olarak sunulabilir mi?

Yalnizca gorev gereksinimleri hazirlanan icerikle uyumluysa sunulmalidir. Rehber, post, issue veya pull request ilgili gorevle dogrudan baglantili olmalidir.

### Mainnet baslamadan mainnet sonucu iddia edilmeli mi?

Hayir. Mainnet yayinda olmadan mainnet sonucuna dair kesin ifadelerden kacinilmalidir. Bunun yerine pre-mainnet hazirlik, ogrenme notlari veya topluluk dokumantasyonu gibi daha notr ifadeler kullanilmalidir.

## Katki

### Bu depoya nasil katki verilebilir?

Duzeltme onerebilir, eksik aciklamalar ekleyebilir, iki dilli sayfa uyumunu iyilestirebilir veya pratik kurulum ve sorun giderme notlari katkisi yapabilirsiniz.

### Yeni icerik hangi tarzda olmali?

Icerik kisa, uygulanabilir, notr ve kontrol edilebilir olmalidir. Promosyon dili, desteksiz odul iddialari ve mainnet varsayimlarindan kacinilmalidir.

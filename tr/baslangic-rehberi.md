# QoreChain ile Başlangıç / Getting Started with QoreChain

QoreChain topluluk dokümantasyon merkezine hoş geldiniz. Bu rehber, yeni katılımcıların ekosistemi anlamasına ve doğru başlangıç noktasını seçmesine yardımcı olur.

## QoreChain Nedir? / What Is QoreChain?

QoreChain; kuantum sonrası güvenlik, çoklu VM uyumluluğu ve topluluk erişimine açık altyapı katılımına odaklanan bir Layer 1 blokzinciri ekosistemidir.

Ekosistem genellikle şu alanlarda tartışılır:

- kuantum sonrası kriptografi;
- EVM, CosmWasm ve SVM uyumluluğu;
- Light Node katılımı;
- topluluk dokümantasyonu ve katılım rehberleri;
- geliştirici ve operatör eğitimi.

Bu sayfa topluluk tarafından sürdürülen bir giriş rehberidir. Resmi QoreChain dokümantasyonu veya duyurularının yerini tutmaz.

## Bu Rehber Kime Yöneliktir? / Who Should Use This Guide?

| Hedef Kitle | Önerilen Başlangıç Noktası |
|---|---|
| Yeni topluluk üyesi | Önce SSS ve sözlüğü okuyun |
| Light Node operatörü | Light Node Operasyonları ve Sorun Giderme ile başlayın |
| Görev katılımcısı | Eigenstate 2 Görevleri ve Kanıt Gönderimi ile başlayın |
| Katkıda bulunan | Katkıda Bulunma Rehberi ve Stil Rehberini okuyun |
| Geliştirici | Mevcut depolar ve geliştirici notlarını inceleyin |

## Önerilen Okuma Sırası / Recommended Reading Order

1. [QoreChain SSS](./sss.md)
2. [QoreChain Terimler Sözlüğü](./terimler-sozlugu.md)
3. [QoreChain Bilgi Bankası](./bilgi-bankasi.md)
4. [Light Node Operasyonları](./light-node-operasyonlari.md)
5. [Sorun Giderme](./sorun-giderme.md)
6. [Eigenstate 2 Görevleri](./eigenstate-2-gorevleri.md)
7. [Kanıt Linki Rehberi](./kanit-linki-rehberi.md)

## Depo Yapısı / Repository Structure

| Klasör / Dosya | İçerik |
|---|---|
| `en/` | İngilizce rehberler |
| `tr/` | Türkçe rehberler |
| `LIGHTNODE_SETUP.md` | Light Node kurulum bağlantıları |
| `CONTRIBUTING.md` | Katkıda bulunma kuralları |
| `STYLE_GUIDE.md` | Yazım ve biçimlendirme standartları |
| `CHANGELOG.md` | Değişiklik geçmişi |
| `docs/` | Meta dosyalar ve içerik haritası |

## Light Node Operatörleri için Temel Gereksinimler / Basic Requirements for Light Node Operators

Light Node çalıştırmadan önce en güncel resmi talimatları inceleyin ve ortamınızın uygun olduğunu doğrulayın.

| Gereksinim | Önerilen Temel Değer |
|---|---|
| İşletim sistemi | Ubuntu 22.04+ |
| CPU | 2 çekirdek veya daha fazlası |
| RAM | 4 GB veya daha fazlası |
| Disk | 50 GB SSD veya daha fazlası |
| Docker | Kurulu |
| Docker Compose | Kurulu |
| Ağ erişimi | Güncel talimatlara göre gerekli portlar açık |

Tam operasyon rehberi için [Light Node Operasyonları](./light-node-operasyonlari.md) sayfasına bakın.

## Yaygın İlk Adımlar / Common First Steps

- Tekrarlayan sorular sormadan önce SSS'yi okuyun.
- Temel terimleri sözlükten öğrenin.
- Light Node rehberini yalnızca güncel resmi talimatları kontrol ettikten sonra kullanın.
- Ekran görüntülerini ve kanıt linklerini hassas bilgilerden arındırın.
- Özel anahtarları, seed phrase'leri, API anahtarlarını veya sunucu kimlik bilgilerini paylaşmayın.
- Mainnet, doğrulayıcı, stake ve ödülle ilgili ayrıntıları güncellemeye duyarlı bilgiler olarak değerlendirin.

## Sorun Giderme / Troubleshooting

Kurulum veya panel erişim sorunlarıyla karşılaşırsanız [Sorun Giderme Rehberi](./sorun-giderme.md) ile başlayın. Panel erişimi, container'lar, loglar, güncellemeler ve kaynak kontrolleri gibi yaygın Light Node sorunlarını kapsar.

## Katkı Yolu / Contribution Path

Topluluk katkıda bulunanları şu şekillerde yardımcı olabilir:

- belirsiz sayfaları geliştirerek;
- Türkçe ve İngilizce içerikleri çevirerek;
- güncel olmayan talimatları bildirerek;
- güvenli sorun giderme örnekleri ekleyerek;
- eksik SSS veya sözlük maddeleri önererek.

Katkıda bulunmadan önce depodaki [Katkıda Bulunma Rehberi](../CONTRIBUTING.md) ve [Stil Rehberi](../STYLE_GUIDE.md) belgelerini okuyun.

## Sorumluluk Reddi / Disclaimer

Bu, topluluk tarafından sürdürülen bir kaynaktır. Resmi QoreChain dokümantasyonunun yerini tutmaz. Kritik ağ kuralları, komutlar, stake gereksinimleri ve mainnet'e ilişkin ayrıntılar her zaman resmi kaynaklardan doğrulanmalıdır.

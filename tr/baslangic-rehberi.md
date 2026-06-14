# QoreChain'e Başlangıç Rehberi

QoreChain topluluk dokümantasyon merkezine hoş geldiniz. Bu rehber, yeni katılımcıların QoreChain ekosistemini anlamasına ve doğru başlangıç noktasını bulmasına yardımcı olur.

## QoreChain Nedir?

QoreChain, kuantum sonrası kriptografiyi temelinde barındıran bir Katman 1 blok zinciridir. EVM (Ethereum Sanal Makinesi), CosmWasm ve SVM (Solana Sanal Makinesi) ile uyumludur; geliştiricilerin tanıdık araçlarla çalışırken yeni nesil güvenlikten yararlanmasını sağlar.

Temel özellikler:
- Kuantum sonrası dirençli kriptografi
- Çoklu VM uyumluluğu (EVM / CosmWasm / SVM)
- Topluluk tarafından yönetilen ağ
- Hafif Düğüm (Light Node) katılım modeli — ağır donanım gerektirmez

## Nasıl Katılabilirim?

### Hafif Düğüm Çalıştır

Hafif Düğüm operatörleri ağın kullanılabilirliğini korumaya yardımcı olur. Gereksinimler mütevazıdır — küçük bir VPS yeterlidir.

Buradan başlayın: [Hafif Düğüm Operasyonları](./light-node-operasyonlari.md)

## Depo Yapısı

```
qorechain-guides/
├── en/          # İngilizce belgeler
├── tr/          # Türkçe belgeler
├── docs/        # Meta dosyalar (içerik haritası, çeviri durumu)
├── assets/      # Görseller ve statik dosyalar
└── .github/     # Issue şablonları, PR şablonları, Actions
```

## Ön Koşullar

Hafif Düğüm çalıştırmak için:

| Gereksinim | Minimum |
|---|---|
| İşletim Sistemi | Ubuntu 22.04+ |
| CPU | 2 çekirdek |
| RAM | 4 GB |
| Disk | 50 GB SSD |
| Docker | Kurulu |
| Docker Compose | Kurulu |
| Stake | 1000 QOR |

## Sık Sorulan Sorular

Yaygın sorular için [SSS](./sss.md) sayfasına bakın.

## Sorun Giderme

Düğüm kurulumunda sorunla karşılaşırsanız [Sorun Giderme Rehberi](./sorun-giderme.md) sayfasına bakın.

## İçerik Haritası

Mevcut tüm belgeler için [docs/content-map.md](../docs/content-map.md) sayfasına bakın.

## Sorumluluk Reddi

Bu, topluluk tarafından sürdürülen bir kaynaktır ve resmi QoreChain belgelerinin yerini almaz. Ağ üzerinde işlem yapmadan önce her zaman resmi kaynakları doğrulayın.

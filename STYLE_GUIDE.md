# QoreChain Guides Stil Rehberi / Style Guide

Bu rehber, QoreChain Guides deposundaki dokumantasyon sayfalarinin tutarli kalmasi icin hazirlanmistir.

This guide keeps documentation pages in QoreChain Guides consistent.

## Genel Ilkeler / General Principles

| Turkce | English |
|---|---|
| Adimlari kisa, acik ve uygulanabilir yazin. | Keep steps short, clear, and practical. |
| Kritik adimlarda resmi kaynaklara yonlendirin. | Point users to official sources for critical steps. |
| Komutlari dogru baglamla birlikte verin. | Give commands with the correct context. |
| Uzun paragraflar yerine tablo ve kontrol listesi kullanin. | Prefer tables and checklists over long paragraphs. |
| Tahminleri gercek bilgi gibi yazmayin. | Do not present assumptions as facts. |

## Iki Dilli Yapi / Bilingual Structure

| Sayfa Turu / Page Type | Beklenen Yapi / Expected Structure |
|---|---|
| Koke eklenen ortak dosyalar / Shared root files | Turkce ve Ingilizce birlikte olmali / Should include both Turkish and English |
| `tr/` altindaki dosyalar / Files under `tr/` | Turkce olmali / Should be Turkish |
| `en/` altindaki dosyalar / Files under `en/` | Ingilizce olmali / Should be English |
| Issue ve PR sablonlari / Issue and PR templates | Iki dilli olmali / Should be bilingual |

## Komut Yazimi / Command Style

Komutlari her zaman kod blogu icinde yazin.

Always write commands inside fenced code blocks.

```bash
docker ps
```

Komuttan once ne yaptigini, komuttan sonra ne beklenmesi gerektigini aciklayin.

Explain what the command does before it, and what the user should expect after it.

## Linkler / Links

- Depo icindeki linklerde goreli yollar kullanin.
- Use relative links for files inside the repository.
- Dis kaynaklarda resmi veya guvenilir kaynaklara oncelik verin.
- Prefer official or trusted sources for external links.

## Durum Etiketleri / Status Labels

| Durum / Status | Anlam / Meaning |
|---|---|
| Aktif / Active | Sayfa kullanima hazir / The page is ready to use |
| Hazirlaniyor / Preparing | Konu belirlenmis, icerik planlaniyor / Topic is defined and content is being planned |
| Planlandi / Planned | Konu yol haritasinda, henuz sayfa yok / Topic is on the roadmap but no page exists yet |

## Guvenlik Dili / Safety Language

Kullaniciya seed phrase, private key, API key veya benzeri gizli bilgileri paylastirmayin.

Do not ask users to share seed phrases, private keys, API keys, or similar secrets.

Kritik ag, stake veya guvenlik adimlarinda resmi QoreChain kaynaklarinin kontrol edilmesi gerektigini belirtin.

For critical network, stake, or security steps, remind users to check official QoreChain sources.

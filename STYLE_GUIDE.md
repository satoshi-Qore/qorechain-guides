# QoreChain Guides Stil Rehberi / Style Guide

Bu rehber, QoreChain Guides deposundaki dokümantasyon sayfalarının tutarlı kalması için hazırlanmıştır.

This guide keeps documentation pages in QoreChain Guides consistent.

## Genel İlkeler / General Principles

| Türkçe | English |
|---|---|
| Adımları kısa, açık ve uygulanabilir yazın. | Keep steps short, clear, and practical. |
| Kritik adımlarda resmi kaynaklara yönlendirin. | Point users to official sources for critical steps. |
| Komutları doğru bağlamla birlikte verin. | Give commands with the correct context. |
| Uzun paragraflar yerine tablo ve kontrol listesi kullanın. | Prefer tables and checklists over long paragraphs. |
| Tahminleri gerçek bilgi gibi yazmayın. | Do not present assumptions as facts. |

## İki Dilli Yapı / Bilingual Structure

| Sayfa Türü / Page Type | Beklenen Yapı / Expected Structure |
|---|---|
| Köke eklenen ortak dosyalar / Shared root files | Türkçe ve İngilizce birlikte olmalı / Should include both Turkish and English |
| `tr/` altındaki dosyalar / Files under `tr/` | Türkçe olmalı / Should be Turkish |
| `en/` altındaki dosyalar / Files under `en/` | İngilizce olmalı / Should be English |
| Issue ve PR şablonları / Issue and PR templates | İki dilli olmalı / Should be bilingual |

## Komut Yazımı / Command Style

Komutları her zaman kod bloğu içinde yazın.

Always write commands inside fenced code blocks.

```bash
docker ps
```

Komuttan önce ne yaptığını, komuttan sonra ne beklenmesi gerektiğini açıklayın.

Explain what the command does before it, and what the user should expect after it.

## Linkler / Links

- Depo içindeki linklerde göreli yollar kullanın.
- Use relative links for files inside the repository.
- Dış kaynaklarda resmi veya güvenilir kaynaklara öncelik verin.
- Prefer official or trusted sources for external links.

## Durum Etiketleri / Status Labels

| Durum / Status | Anlam / Meaning |
|---|---|
| Aktif / Active | Sayfa kullanıma hazır / The page is ready to use |
| Hazırlanıyor / Preparing | Konu belirlenmiş, içerik planlanıyor / Topic is defined and content is being planned |
| Planlandı / Planned | Konu yol haritasında, henüz sayfa yok / Topic is on the roadmap but no page exists yet |

## Güvenlik Dili / Safety Language

Kullanıcıya seed phrase, private key, API key veya benzeri gizli bilgileri paylaştırmayın.

Do not ask users to share seed phrases, private keys, API keys, or similar secrets.

Kritik ağ, stake veya güvenlik adımlarında resmi QoreChain kaynaklarının kontrol edilmesi gerektiğini belirtin.

For critical network, stake, or security steps, remind users to check official QoreChain sources.

# Content Maintenance Checklist / İçerik Bakım Kontrol Listesi

This checklist helps maintain QoreChain Guides as a reliable, bilingual, community-driven knowledge hub.

Bu kontrol listesi, QoreChain Guides deposunun güvenilir, iki dilli ve topluluk odaklı bir bilgi merkezi olarak korunmasına yardımcı olur.

## Purpose / Amaç

As the repository grows, outdated links, mismatched Turkish and English pages, stale task information, and unsupported claims can reduce trust. This checklist provides a repeatable review process for keeping pages clear, current, and safe.

Depo büyüdükçe eskiyen linkler, Türkçe ve İngilizce sayfa uyumsuzlukları, güncelliğini yitiren görev bilgileri ve desteklenmeyen iddialar güveni azaltabilir. Bu liste, sayfaları açık, güncel ve güvenli tutmak için tekrar edilebilir bir inceleme süreci sunar.

## When to Use This Checklist / Ne Zaman Kullanılır?

| Situation / Durum | Use This Checklist? / Bu Liste Kullanılsın mı? |
|---|---|
| A new guide is added / Yeni rehber eklendi | Yes / Evet |
| A page is translated / Sayfa çevrildi | Yes / Evet |
| A task requirement changes / Görev gereksinimi değişti | Yes / Evet |
| A link or command is updated / Link veya komut güncellendi | Yes / Evet |
| Mainnet-sensitive information is mentioned / Mainnet'e bağlı bilgi geçiyor | Yes / Evet |
| Only a typo is fixed / Sadece yazım hatası düzeltildi | Quick check / Kısa kontrol |

## 1. Link Review / Link Kontrolü

Check every internal and external link before merging or publishing a page.

Bir sayfa yayınlanmadan veya birleştirilmeden önce tüm iç ve dış linkleri kontrol edin.

| Check / Kontrol | Yes/No |
|---|---|
| Internal repository links open correctly / Depo içi linkler doğru açılıyor |
| Turkish and English counterpart links are valid / Türkçe ve İngilizce karşılık linkleri geçerli |
| External links point to reliable sources / Dış linkler güvenilir kaynaklara gidiyor |
| Official-source links are preferred for critical details / Kritik detaylarda resmi kaynak linkleri tercih ediliyor |
| No broken placeholder links remain / Bozuk placeholder link kalmadı |

## 2. Bilingual Alignment / İki Dilli Uyum

Turkish and English pages do not need to be word-for-word identical, but their structure should stay aligned when they describe the same topic.

Türkçe ve İngilizce sayfaların kelime kelime aynı olması gerekmez, ancak aynı konuyu anlatıyorlarsa yapı olarak uyumlu kalmaları gerekir.

| Check / Kontrol | Yes/No |
|---|---|
| Matching page exists or is planned / Karşı dilde sayfa var veya planlandı |
| Headings follow a similar structure / Başlıklar benzer yapıda ilerliyor |
| Key warnings appear in both languages / Önemli uyarılar iki dilde de var |
| Task names and category names are consistent / Görev ve kategori adları tutarlı |
| Navigation links point to both language versions where useful / Gereken yerlerde iki dil versiyonuna link veriliyor |

## 3. Mainnet-Sensitive Content / Mainnet'e Bağlı İçerik

Some content may change as QoreChain evolves. These topics should be written carefully and reviewed often.

QoreChain geliştikçe bazı içerikler değişebilir. Bu başlıklar dikkatli yazılmalı ve sık gözden geçirilmelidir.

| Topic / Konu | Maintenance Rule / Bakım Kuralı |
|---|---|
| RPC endpoints | Do not present unofficial endpoints as final / Resmi olmayan endpointleri nihai gibi sunmayın |
| Chain ID | Mark as subject to official confirmation when needed / Gerektiğinde resmi doğrulamaya bağlı olduğunu belirtin |
| Rewards and commissions | Avoid guarantees / Garanti ifadelerinden kaçının |
| Validator requirements | Point to official sources / Resmi kaynaklara yönlendirin |
| Staking rules | Avoid fixed claims unless confirmed / Doğrulanmadıkça kesin ifade kullanmayın |
| Tokenomics details | Use cautious wording and references / Dikkatli dil ve kaynak kullanın |

Recommended wording:

```text
This information should be verified against official QoreChain documentation and current announcements.
```

Önerilen ifade:

```text
Bu bilgi resmi QoreChain dokümantasyonu ve güncel duyurularla doğrulanmalıdır.
```

## 4. Safety and Privacy Review / Güvenlik ve Gizlilik Kontrolü

Community documentation should never encourage users to share sensitive information.

Topluluk dokümantasyonu kullanıcıları hassas bilgi paylaşmaya yönlendirmemelidir.

| Check / Kontrol | Yes/No |
|---|---|
| No private keys, seed phrases, or passwords are shown / Private key, seed phrase veya parola gösterilmiyor |
| Example wallet addresses are clearly placeholders / Örnek cüzdan adresleri açıkça placeholder |
| Screenshots do not reveal tokens, emails, IPs, or private dashboards / Ekran görüntüleri token, e-posta, IP veya özel panel göstermiyor |
| Proof instructions avoid exposing personal data / Kanıt yönergeleri kişisel veri paylaşımını önlüyor |
| Support instructions ask users to redact sensitive details / Destek yönergeleri hassas bilgileri gizlemeyi istiyor |

## 5. Task and Proof Review / Görev ve Kanıt Kontrolü

Eigenstate 2 and community task pages should be practical without claiming guaranteed approval.

Eigenstate 2 ve topluluk görev sayfaları pratik olmalı, ancak kesin onay vaadi vermemelidir.

| Check / Kontrol | Yes/No |
|---|---|
| Task description is clear / Görev açıklaması net |
| Proof link method is explained / Kanıt linki yöntemi açıklanmış |
| Screenshot upload limitations are handled safely / Ekran görüntüsü yükleme sınırları güvenli şekilde ele alınmış |
| Description examples are neutral and honest / Açıklama örnekleri tarafsız ve dürüst |
| No approval guarantee is implied / Onay garantisi ima edilmiyor |

## 6. Structure and Navigation Review / Yapı ve Navigasyon Kontrolü

Pages should be easy to find from the main repository entry points.

Sayfalar ana depo giriş noktalarından kolay bulunabilmelidir.

| Check / Kontrol | Yes/No |
|---|---|
| Page is linked from a relevant README or index / Sayfa ilgili README veya dizinden linklenmiş |
| Related resources are listed at the end / İlgili kaynaklar sonda listelenmiş |
| File name is lowercase with hyphens / Dosya adı küçük harf ve tireli |
| Page title clearly explains the topic / Sayfa başlığı konuyu net açıklıyor |
| Reader role is clear / Okuyucu rolü net |

## 7. Review Cadence / İnceleme Sıklığı

| Content Type / İçerik Türü | Suggested Review / Önerilen Kontrol |
|---|---|
| Root README and language landing pages | Monthly or after major structure changes / Aylık veya büyük yapı değişikliklerinden sonra |
| Light Node pages | After official technical updates / Resmi teknik güncellemelerden sonra |
| Eigenstate 2 task guides | After task list or review-flow changes / Görev listesi veya inceleme akışı değişince |
| Proof submission pages | After review-field changes / İnceleme alanı değişince |
| Troubleshooting pages | When repeated community issues appear / Toplulukta tekrar eden sorunlar çıktığında |
| Roadmap | After major content milestones / Büyük içerik kilometre taşlarından sonra |

## 8. Reviewer Notes / İnceleyen Kişi Notları

When reviewing a page, leave a short note in the pull request or issue explaining what was checked.

Bir sayfa incelenirken pull request veya issue içinde neyin kontrol edildiğini kısa not olarak yazın.

Example:

```text
Checked links, bilingual alignment, mainnet-sensitive wording, and proof privacy notes.
```

Örnek:

```text
Linkler, iki dilli uyum, mainnet'e bağlı ifadeler ve kanıt gizliliği notları kontrol edildi.
```

## Related Resources / İlgili Kaynaklar

- [Documentation Standards](./documentation-standards.md)
- [Academy Learning Paths](./academy-learning-paths.md)
- [Roadmap](../ROADMAP.md)
- [Contributing](../CONTRIBUTING.md)
- [Support](../SUPPORT.md)

## Disclaimer / Not

This checklist supports community documentation maintenance. It does not replace official QoreChain documentation, technical specifications, or announcements.

Bu kontrol listesi topluluk dokümantasyonu bakımını destekler. Resmi QoreChain dokümantasyonu, teknik özellikleri veya duyurularının yerine geçmez.

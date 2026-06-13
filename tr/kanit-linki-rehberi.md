# Kanıt Linki Rehberi

Bu rehber, QoreChain görev panelinde ekran görüntüsü yükleme alanı olmadığında kanıtın nasıl linke dönüştürülebileceğini açıklar.

Bazı görevlerde yalnızca iki alan bulunur:

- Proof link
- Describe what you did

Bu durumda ekran görüntüsü doğrudan yüklenemez. Kanıt, inceleyicinin erişebileceği herkese açık veya paylaşılabilir bir link haline getirilmelidir.

## Temel Akış

1. Görevi tamamlayın.
2. Gerekirse ekran görüntüsü alın.
3. Kanıtı herkese açık veya link ile görülebilir bir yere yükleyin.
4. Oluşan linki `proof link` alanına ekleyin.
5. `Describe what you did` alanına kısa ve net bir açıklama yazın.

## Kullanılabilecek Kanıt Linki Seçenekleri

| Seçenek | Ne Zaman Uygun? | Not |
|---|---|---|
| GitHub proof repository | Çok sayıda görevi düzenli takip etmek için | En düzenli ve teknik olarak güçlü seçeneklerden biridir |
| GitHub Gist | Tek bir görev veya kısa kanıt notu için | Basit ve hafif bir alternatiftir |
| Google Drive | Ekran görüntüsü paylaşmak için | Paylaşım ayarı `linke sahip olan görüntüleyebilir` olmalıdır |
| X veya LinkedIn paylaşımı | Sosyal görevlerde | Kanıt sosyal bağlamla uyumlu olur |
| Imgur veya benzeri görsel yükleme servisi | Sadece ekran görüntüsü linki üretmek için | Link herkese açık görünebilmelidir |
| Herkese açık Telegram kanal mesajı | Topluluk paylaşımları için | Kanal veya mesaj herkese açık olmalıdır |

## GitHub Proof Repo Yöntemi

Bu yöntem, görev kanıtlarını uzun vadeli ve düzenli tutmak isteyen kullanıcılar için uygundur.

Önerilen yapı:

```text
qorechain-task-proofs/
|-- README.md
|-- eigenstate-2/
|   |-- linkedin-follow.md
|   |-- github-follow.md
|   |-- reddit-intro.md
|-- screenshots/
    |-- linkedin-follow.png
    |-- github-follow.png
```

Her görev için kısa bir Markdown sayfası hazırlanabilir:

```md
# Follow QoreChain Association on LinkedIn

Task: Follow QoreChain Association on LinkedIn
Status: Completed
Evidence: Screenshot attached in this repository
Date: YYYY-MM-DD

I followed the QoreChain Association LinkedIn page. Since the task form does not include a screenshot upload field, I am submitting this public GitHub proof link for manual review.
```

## Google Drive Yöntemi

1. Ekran görüntüsünü Google Drive'a yükleyin.
2. Dosyaya sağ tıklayıp paylaşım ayarlarını açın.
3. Erişimi `linke sahip olan görüntüleyebilir` olarak ayarlayın.
4. Linki kopyalayıp görev panelindeki `proof link` alanına ekleyin.

Bu yöntemde linkin gizli veya erişime kapalı kalmadığından emin olun.

## Açıklama Örnekleri

Genel görevler için:

```text
I completed the requested task. Since there is no screenshot upload field, I provided a public proof link where the evidence can be reviewed manually.
```

Takip görevleri için:

```text
I followed the requested QoreChain account/page and provided a public proof link for manual review.
```

Beğeni veya etkileşim görevleri için:

```text
I completed the required engagement action and provided a public proof link showing the completed task.
```

GitHub görevleri için:

```text
I completed the requested GitHub action and provided a public GitHub link as proof for manual review.
```

## Dikkat Edilmesi Gerekenler

- Kanıt linki inceleyici tarafından açılabilmelidir.
- Özel hesap, kapalı grup veya giriş isteyen sayfalar zayıf kanıt olabilir.
- Seed phrase, private key, cüzdan gizli bilgileri, e-posta veya telefon numarası paylaşmayın.
- Gerekirse ekran görüntüsündeki hassas bilgileri kapatın.
- Kanıt açıklamasında abartılı iddia veya onay garantisi kullanmayın.

## Kısa Özet

Ekran görüntüsü yükleme alanı yoksa, kanıtı linke dönüştürün. En önemli nokta, inceleyicinin linke tıkladığında görevin yapıldığını anlayabilmesidir.

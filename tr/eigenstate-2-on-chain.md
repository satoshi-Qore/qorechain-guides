# Eigenstate 2 On-Chain Görevleri

Bu sayfa, Eigenstate 2 içindeki on-chain görevler için topluluk rehberidir.

On-chain kategori; QOR transferi, staking, delegation, governance, Light Node çalıştırma, bridge işlemleri, QOR bakiyesi ve AI araçlarına yönelik görevleri kapsar.

## Kapsam

Gözlemlenen görev yapısına göre bu kategoride 23 görev bulunur. Bu kategori, teknik ve finansal risk taşıyabileceği için diğer görevlere göre daha dikkatli ele alınmalıdır.

## Görev Türleri

| Görev Türü | Örnek | Uygun Kanıt |
|---|---|---|
| Transfer | İlk QOR işlemini gönderme | Explorer veya işlem linki |
| Delegation | En az 10 QOR delegate etme | İşlem, validator veya cüzdan kanıtı |
| Staking | Staked pozisyon oluşturma veya koruma | Explorer, panel veya cüzdan kanıtı |
| Governance | İlk proposal oyu veya proposal gönderimi | Governance/proposal linki |
| Light Node | Register and run a light node, 24 saat veya 7 gün çalışma | Node paneli, görev paneli veya uygun kanıt linki |
| Bridge | IBC üzerinden QOR bridge işlemi | Bridge veya transaction linki |
| Holding | TGE döneminde belirli QOR tutarı bulundurma | Resmi sistemin istediği kanıt |
| AI araçları | AI audit veya smart contract üretimi | Platformun oluşturduğu uygun kayıt/link |

## Güvenlik Önceliği

On-chain görevlerde amaç görev tamamlamak olsa bile güvenlik her zaman önce gelir.

Asla paylaşılmaması gereken bilgiler:

- seed phrase
- private key
- cüzdan şifresi
- doğrulama kodları
- sunucu SSH bilgileri
- API key veya token
- özel IP ve hassas node bilgileri

## İşlem Kanıtı

Bir işlem explorer üzerinde görünüyorsa en iyi kanıt genellikle işlem linkidir. Cüzdan ekran görüntüsü gerekiyorsa bakiye dışındaki hassas bilgiler kapatılmalıdır.

Kısa açıklama örneği:

```text
I completed the requested on-chain task and submitted the related transaction or explorer link for manual review.
```

## Light Node Görevleri

Light Node görevlerinde kanıt, görev panelinin ve resmi doğrulama akışının nasıl çalıştığına bağlı olabilir.

Dikkat edilmesi gerekenler:

- Node'un doğru ağda çalıştığını kontrol edin.
- Panelde sync veya status bilgisi varsa hassas verileri kapatarak kullanın.
- Log paylaşmanız gerekiyorsa özel anahtar, token veya IP bilgilerini gizleyin.
- "24 saat" veya "7 gün" gibi görevlerde süre tamamlanmadan başvuru yapmayın.

## Mainnet ve TGE Görevleri

Mainnet veya TGE ile ilişkili görevlerde acele edilmemelidir. Resmi duyuru, ağ durumu ve görev panelindeki güncel talimatlar kontrol edilmeden işlem yapılmamalıdır.

Bu rehber, finansal tavsiye vermez. On-chain işlem yapmadan önce riskleri kullanıcı kendisi değerlendirmelidir.

## Dikkat Edilecek Noktalar

- Testnet ve mainnet adreslerini karıştırmayın.
- Yanlış ağda işlem yapmayın.
- İşlem ücretlerini ve minimum tutarları kontrol edin.
- Görev paneli resmi olarak başlamadıysa beklemek daha doğru olabilir.
- İnceleme tamamlanmadan görevi onaylanmış gibi göstermeyin.

## İlgili Rehberler

- [Light Node Rehberi](./light-node/)
- [Eigenstate 2 Görevleri](./eigenstate-2-gorevleri.md)
- [Eigenstate 2 Kanıt Gönderimi](./eigenstate-2-kanit-gonderimi.md)
- [Eigenstate 2 SSS](./eigenstate-2-sss.md)

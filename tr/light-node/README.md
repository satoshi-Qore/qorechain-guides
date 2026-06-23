# Light Node Rehberi — Buradan Başla

> **Ağ Durumu:** QoreChain şu an mainnet öncesi aşamadadır. RPC endpoint'leri, Chain ID, blok ödülleri ve komisyon oranları gibi değerler, mainnet lansmanında resmi dokümantasyonda yayınlanacaktır. Üçüncü taraf kaynaklara güvenmeyiniz.

Bu rehber, QoreChain Light Node çalıştırmak için ihtiyacınız olan her şeyi kapsar — sunucu hazırlığından günlük operasyonlara ve sorun çözmeye kadar.

---

## Kapsam

Bu rehber şunları kapsar:

- Sunucu seçimi ve hazırlığı
- Docker tabanlı Light Node kurulumu
- Servis yönetimi ve sağlık kontrolleri
- Log takibi ve tanılama
- Yaygın sorunlar ve çözümleri

Bu rehber; validator node kurulumu, staking veya governance katılımını **kapsamaz**.

---

## Başlamadan Önce

Şunlara sahip olduğunuzdan emin olun:

- Minimum gereksinimleri karşılayan bir VPS veya sunucu (Bölüm 01'e bakınız)
- Sunucuya SSH erişimi
- Temel Linux komut satırı bilgisi
- Docker bilgisi yardımcı olur ancak zorunlu değildir — tüm komutlar verilmektedir

---

## Kurulum Akışı

Bölümleri sırayla takip edin:

| Adım | Dosya | Açıklama |
|------|-------|----------|
| 1 | [Sunucu Hazırlığı](./01-sunucu-hazirligi.md) | İşletim sistemi, güvenlik duvarı, kullanıcı ayarları |
| 2 | [Docker Kurulumu](./02-docker-kurulumu.md) | Docker kurulumu ve yapılandırması |
| 3 | [Light Node Kurulumu](./03-light-node-kurulumu.md) | Image çekme, yapılandırma, node başlatma |
| 4 | [İzleme](./04-izleme.md) | Sağlık kontrolleri, panel erişimi, metrikler |
| 5 | [Sorun Giderme](./05-sorun-giderme.md) | Yaygın hatalar ve çözümler |

---

## Günlük Kontroller

Node'unuz çalışmaya başladıktan sonra her gün kontrol edin:

```bash
# Servis durumunu kontrol et
docker ps | grep qorechain

# Son logları gör (son 50 satır)
docker logs --tail 50 qorechain-lightnode-sx

# Sync durumunu kontrol et (RPC etkinse)
curl -s http://localhost:<RPC_PORT>/status | jq .result.sync_info
```

> `<RPC_PORT>` yerine node yapılandırmanızda tanımlanan portu kullanın.

---

## Log Takibi ve Sorun Giderme

Bir sorun fark ederseniz loglarla başlayın:

```bash
# Canlı logları takip et
docker logs -f qorechain-lightnode-sx

# Container yeniden başlatma sayısını kontrol et
docker inspect qorechain-lightnode-sx | grep RestartCount
```

Sistematik sorun giderme için [Bölüm 05 — Sorun Giderme](./05-sorun-giderme.md) sayfasına bakınız.

---

## Görev Kanıtı / Task Notu

Çalışan bir node kanıtı sunmanız gerekiyorsa (kampanya veya görev için):

- Container'ın çalıştığını gösteren `docker ps` ekran görüntüsü
- İzleme paneli ekran görüntüsü (Bölüm 04'e bakınız)
- Blok senkronizasyon ilerlemesini gösteren log çıktısı

---

## Resmi Kaynaklar

Yapılandırma değerlerini her zaman resmi QoreChain kaynaklarından doğrulayın:

- **Web sitesi:** [qorechain.io](https://qorechain.io)
- **GitHub:** [github.com/QoreChain](https://github.com/QoreChain)
- **Discord:** Resmi duyurular kanalı

> ⚠️ Belirli değerler (RPC URL, Chain ID, genesis dosyası URL'si, ödül oranları) mainnet öncesinde değişebileceğinden bu rehbere sabit olarak yazılmamıştır. Her zaman en güncel resmi değerleri kullanınız.

---

## Sorumluluk Reddi

Bu, topluluk tarafından sürdürülen bir kaynaktır. Resmi QoreChain dokümantasyonunun yerini almaz. Devam etmeden önce kritik detayları her zaman resmi kaynaklardan doğrulayın.

# QoreChain Light Node Setup / Light Node Kurulumu

This page is a short bilingual entry point for QoreChain Light Node setup and operation notes.

Bu sayfa, QoreChain Light Node kurulum ve operasyon notları için kısa iki dilli bir giriş sayfasıdır.

## Full Guides / Tam Rehberler

| Language / Dil | Guide / Rehber |
|---|---|
| Türkçe / Turkish | [Light Node Operasyonları](./tr/light-node-operasyonlari.md) |
| English / İngilizce | [Light Node Operations](./en/light-node-operations.md) |

## Requirements / Gereksinimler

| English | Türkçe |
|---|---|
| VPS or dedicated server, Ubuntu 22.04 recommended | Ubuntu 22.04 önerilen VPS veya dedicated server |
| Docker | Docker |
| Docker Compose | Docker Compose |
| 1000 QOR stake | 1000 QOR stake |
| Stable internet connection | Stabil internet bağlantısı |
| Basic terminal access | Temel terminal erişimi |

## Basic Setup / Temel Kurulum

Download the Light Node files.

Light Node dosyalarını indirin.

```bash
git clone https://github.com/qorechain/qorechain-lightnode.git
cd qorechain-lightnode
```

Start the services.

Servisleri başlatın.

```bash
docker compose up -d
```

## Service Check / Servis Kontrolü

Check running containers.

Çalışan container durumunu kontrol edin.

```bash
docker ps
```

Expected services / Beklenen servisler:

- qorechain-lightnode-sx
- qorechain-lightnode-ux

## Panel Access / Panel Erişimi

Open the panel in your browser.

Paneli tarayıcıda açın.

```text
http://YOUR_SERVER_IP:8420
```

Replace `YOUR_SERVER_IP` with your own server IP address.

`YOUR_SERVER_IP` alanını kendi sunucu IP adresinizle değiştirin.

## Logs / Loglar

Check the main service logs.

Ana servis loglarını kontrol edin.

```bash
docker logs qorechain-lightnode-sx
```

Follow logs live.

Logları canlı takip edin.

```bash
docker logs -f qorechain-lightnode-sx
```

## Restart / Yeniden Başlatma

Restart the services.

Servisleri yeniden başlatın.

```bash
docker compose restart
```

## Troubleshooting / Sorun Giderme

| Issue / Durum | Check / Kontrol | Action / Aksiyon |
|---|---|---|
| Panel does not open / Panel açılmıyor | Server IP and port / Sunucu IP ve port | Check `docker ps` and firewall settings / `docker ps` ve firewall ayarlarını kontrol edin |
| Service is not visible / Servis görünmüyor | Container list / Container listesi | Run `docker compose up -d` again / `docker compose up -d` komutunu tekrar çalıştırın |
| Logs show errors / Loglarda hata var | SX service logs / SX servis logları | Note the error and check again after restarting / Hatayı not alın ve yeniden başlatarak tekrar kontrol edin |
| Node does not respond / Node yanıt vermiyor | Server resources / Sunucu kaynakları | Check CPU, RAM, and disk usage / CPU, RAM ve disk durumunu kontrol edin |

## Note / Not

This page is a quick reference. For the maintained operation flow, use the full Turkish or English guide linked above.

Bu sayfa hızlı referans niteliğindedir. Güncel operasyon akışı için yukarıda bağlanan tam Türkçe veya İngilizce rehberi kullanın.

This repository does not replace official QoreChain documentation. Official sources and current announcements should be checked for critical steps.

Bu depo resmi QoreChain dokümantasyonunun yerine geçmez. Kritik adımlarda resmi kaynaklar ve güncel duyurular kontrol edilmelidir.

# QoreChain Light Node Setup / Light Node Kurulumu

This page is a short bilingual entry point for QoreChain Light Node setup and operation notes.

Bu sayfa, QoreChain Light Node kurulum ve operasyon notlari icin kisa iki dilli bir giris sayfasidir.

## Full Guides / Tam Rehberler

| Language / Dil | Guide / Rehber |
|---|---|
| Turkce / Turkish | [Light Node Operasyonlari](./tr/light-node-operasyonlari.md) |
| English / Ingilizce | [Light Node Operations](./en/light-node-operations.md) |

## Requirements / Gereksinimler

| English | Turkce |
|---|---|
| VPS or dedicated server, Ubuntu 22.04 recommended | Ubuntu 22.04 onerilen VPS veya dedicated server |
| Docker | Docker |
| Docker Compose | Docker Compose |
| 1000 QOR stake | 1000 QOR stake |
| Stable internet connection | Stabil internet baglantisi |
| Basic terminal access | Temel terminal erisimi |

## Basic Setup / Temel Kurulum

Download the Light Node files.

Light Node dosyalarini indirin.

```bash
git clone https://github.com/qorechain/qorechain-lightnode.git
cd qorechain-lightnode
```

Start the services.

Servisleri baslatin.

```bash
docker compose up -d
```

## Service Check / Servis Kontrolu

Check running containers.

Calisan container durumunu kontrol edin.

```bash
docker ps
```

Expected services / Beklenen servisler:

- qorechain-lightnode-sx
- qorechain-lightnode-ux

## Panel Access / Panel Erisimi

Open the panel in your browser.

Paneli tarayicida acin.

```text
http://YOUR_SERVER_IP:8420
```

Replace `YOUR_SERVER_IP` with your own server IP address.

`YOUR_SERVER_IP` alanini kendi sunucu IP adresinizle degistirin.

## Logs / Loglar

Check the main service logs.

Ana servis loglarini kontrol edin.

```bash
docker logs qorechain-lightnode-sx
```

Follow logs live.

Loglari canli takip edin.

```bash
docker logs -f qorechain-lightnode-sx
```

## Restart / Yeniden Baslatma

Restart the services.

Servisleri yeniden baslatin.

```bash
docker compose restart
```

## Troubleshooting / Sorun Giderme

| Issue / Durum | Check / Kontrol | Action / Aksiyon |
|---|---|---|
| Panel does not open / Panel acilmiyor | Server IP and port / Sunucu IP ve port | Check `docker ps` and firewall settings / `docker ps` ve firewall ayarlarini kontrol edin |
| Service is not visible / Servis gorunmuyor | Container list / Container listesi | Run `docker compose up -d` again / `docker compose up -d` komutunu tekrar calistirin |
| Logs show errors / Loglarda hata var | SX service logs / SX servis loglari | Note the error and check again after restart / Hatayi not alin ve yeniden baslatma sonrasi tekrar kontrol edin |
| Node does not respond / Node yanit vermiyor | Server resources / Sunucu kaynaklari | Check CPU, RAM, and disk usage / CPU, RAM ve disk durumunu kontrol edin |

## Note / Not

This page is a quick reference. For the maintained operation flow, use the full Turkish or English guide linked above.

Bu sayfa hizli referans niteligindedir. Guncel operasyon akisi icin yukarida baglanan tam Turkce veya Ingilizce rehberi kullanin.

This repository does not replace official QoreChain documentation. Official sources and current announcements should be checked for critical steps.

Bu depo resmi QoreChain dokumantasyonunun yerine gecmez. Kritik adimlarda resmi kaynaklar ve guncel duyurular kontrol edilmelidir.

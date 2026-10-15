# Flipper Zero ile Wi-Fi Kimlik Bilgisi Toplama Tespiti

**Flipper Zero / BadUSB senaryolarında Windows üzerinde yapılan Wi-Fi şifre sızdırma saldırılarının tespiti ve önlenmesi üzerine eğitim amaçlı bir analiz.**

![demo](assets/demo.gif)
<!-- assets/demo.gif — projeyi en iyi anlatan görsel veya kısa ekran kaydı (10 MB altı önerilir) -->

Bu proje, saldırganların `netsh` komutuyla Wi-Fi profillerini düz metin parola ile dışa aktarmasını nasıl tespit edebileceğinizi ve buna karşı nasıl önlem alabileceğinizi gösterir. Amaç saldırı yapmak değil, bu tür saldırıları **Windows Olay Günlüğü (Event Viewer)** üzerinden fark etmektir.

> ⚠️ **Uyarı:** Bu depo yalnızca **eğitim ve savunma amaçlıdır**. Aktif şifre çalma veya veri sızdırma kodu içermez. İzinsiz veri toplama yasadışıdır.

---

## Özet

| | |
|---|---|
| **Problem** | BadUSB / Flipper Zero gibi cihazlarla Windows'ta Wi-Fi şifrelerinin `netsh wlan export profile key=clear` komutuyla düz metin olarak dışa aktarılıp sızdırılması |
| **Yöntem** | Windows Olay Günlüğü'nde ilgili süreç ve komut satırı olaylarının (Event ID 4688 vb.) izlenmesi ve korelasyonu |
| **Simülasyon / donanım** | Flipper Zero (BadUSB modülü) + Windows test makinesi |
| **Makale** | [paper/proje-adi.pdf](paper/proje-adi.pdf) *(varsa buraya makale/rapor bağlantısı)* |

### Sistem mimarisi

![mimari](assets/architecture.png)
<!-- assets/architecture.png — saldırı akışı: Flipper Zero → BadUSB payload → netsh export → dışarı veri gönderimi → log tespiti -->

---

## Seçilmiş sonuçlar

### Sonuç 1: Tespit edilen olay günlüğü kayıtları
*Event ID 4688 ile `netsh.exe` sürecinin ve şüpheli komut satırı argümanlarının yakalanması.*

![sonuc1](plots/sonuc_1.png)

### Sonuç 2: Payload çalıştırma süresi / başarı oranı
*Farklı payload varyantlarının çalışma süresi ve tespit edilme oranı karşılaştırması.*

| grafik A | grafik B |
|---|---|
| ![a](plots/sonuc_2a.png) | ![b](plots/sonuc_2b.png) |

### Sonuç 3: Alınan önlemlerin etkisi
*Önerilen log/politika önlemleri uygulandıktan sonra tespit süresindeki iyileşme.*

![sonuc3](plots/sonuc_3.png)

*Tüm şekiller `plots/` klasöründe.*

---

## Kurulum

### Gereksinimler
- Windows 10/11 (test ortamı)
- Flipper Zero + BadUSB (Bad Kb / DuckyScript) modülü
- (Varsa) Python 3.x — log analiz betikleri için

### Adımlar
```bash
git clone https://github.com/Nasuhii/flipperzero-wifi-stealer-withusingwebhook.git
cd flipperzero-wifi-stealer-withusingwebhook
# gerekiyorsa:
python3 -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
```

## Kullanım

### Payload / tespit betiğini çalıştırma
```bash
python scripts/check_install.py
```

**Beklenen çıktı:**
```
Event ID 4688 taraması: 3 şüpheli netsh çağrısı bulundu
Özet: tespit oranı %100
```

### Sonuçları yeniden üretme

| Şekil | Komut |
|---|---|
| sonuc_1.png | `python scripts/plot_1.py` |
| sonuc_2.png | `python scripts/plot_2.py` |
| sonuc_3.png | `python scripts/plot_3.py` |

---

## Proje yapısı

```
flipperzero-wifi-stealer-withusingwebhook/
├── assets/                        # README görselleri (demo.gif, architecture.png)
├── configs/                       # ayar dosyaları
├── payloadforturkishusers.txt     # Flipper Zero BadUSB payload (eğitim amaçlı, Türkçe kullanıcılar için)
├── scripts/                       # log analiz / tespit betikleri
├── plots/                         # sonuç grafikleri
├── paper/                         # makale/rapor (varsa)
├── requirements.txt
└── README.md
```

---

## Atıf, lisans, iletişim

```bibtex
@misc{flipperzero_wifi_detection_2026,
  title   = {Flipper Zero ile Wi-Fi Kimlik Bilgisi Toplama Tespiti},
  author  = {Nasuhi},
  year    = {2026},
  howpublished = {\url{https://github.com/Nasuhii/flipperzero-wifi-stealer-withusingwebhook}}
}
```

**Lisans:** MIT (veya tercih ettiğiniz lisans)
**İletişim:** GitHub üzerinden issue açabilirsiniz.

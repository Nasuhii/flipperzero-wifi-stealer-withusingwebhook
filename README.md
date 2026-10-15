# Flipper Zero ile Wi-Fi Kimlik Bilgisi Toplama Tespiti

**Flipper Zero / BadUSB üzerinden Windows'ta çalıştırılan bir Wi-Fi şifre dışa aktarma payload'ı ve bunun nasıl tespit edilebileceğine dair eğitim amaçlı not.**

Bu repo, `netsh wlan export profile key=clear` komutunu kullanarak Wi-Fi şifrelerini düz metin olarak dışa aktaran bir BadUSB payload'ı içerir. Amaç, bu tür bir payload'ın Windows Olay Günlüğü (Event Viewer) üzerinden nasıl fark edilebileceğini göstermektir.

> ⚠️ **Uyarı:** Bu depo yalnızca **eğitim ve savunma amaçlıdır**. Payload, izinsiz kullanıldığında yasadışıdır ve sorumluluk kullanıcıya aittir.

---

## Özet

| | |
|---|---|
| **Problem** | BadUSB (Flipper Zero) ile Windows'a takılan bir cihazın, kullanıcı fark etmeden `netsh` komutuyla Wi-Fi şifrelerini düz metin olarak dışa aktarması |
| **Yöntem** | `payloadforturkishusers.txt` içindeki DuckyScript payload'ının çalıştırdığı komutların, Windows Olay Günlüğü'nde (Event ID 4688, `netsh.exe` süreç oluşturma) tespit edilmesi |

---

## Kullanım

1. `payloadforturkishusers.txt` dosyasını Flipper Zero'nun BadUSB (Bad Kb) modülüne yükleyin.
2. Hedef Windows makinesinde Flipper Zero'yu USB olarak takın ve payload'ı çalıştırın.
3. Tespit için Windows makinesinde **Event Viewer → Windows Logs → Security** kısmından **Event ID 4688** kayıtlarını filtreleyip komut satırında `netsh.exe` ve `wlan export profile` geçen süreçleri arayın.

---

## Proje yapısı

```
flipperzero-wifi-stealer-withusingwebhook/
├── payloadforturkishusers.txt   # Flipper Zero BadUSB payload (DuckyScript)
└── README.md
```

---

## Lisans, iletişim

**Lisans:** MIT
**İletişim:** GitHub üzerinden issue açabilirsiniz.

# 🧰 DFIR Tools – Checklist Installazione e Utilizzo

Questa lista tiene traccia degli strumenti forensi che uso o tengo pronti, suddivisi per contesto operativo. Lo stato di utilizzo dipende dal caso e dal tipo di analisi.

---

## 🖥️ Strumenti per il PC LIVE (target)

> Da eseguire da USB o supporto esterno. Non installare sul sistema target.

| Tool                   | Funzione                         |
|------------------------|----------------------------------|
| FTK Imager             | Acquisizione disco e RAM         |
| Magnet RAM Capture     | Acquisizione memoria volatile    |
| KAPE (solo acquisizione) | Raccolta artefatti mirata     |
| Velociraptor (agent)   | Raccolta remota artefatti        |

---

## 💻 Strumenti installati sul PC di analisi

> Usati per analizzare immagini, RAM, artefatti e generare report.

| Tool                      | Funzione principale               |
|---------------------------|-----------------------------------|
| Autopsy                   | Analisi immagini disco, carving   |
| Volatility                | Analisi RAM                       |
| Registry Recon            | Analisi avanzata del registro     |
| KAPE (analisi)            | Parsing artefatti raccolti        |
| Redline                   | Analisi host e timeline           |
| Arsenal Image Mounter     | Montaggio immagini `.E01`         |
| CyberChef                 | Decodifica e analisi stringhe     |
| Wireshark                 | Analisi traffico di rete          |

---

>Documento curato da **Diego Bonatti**  
Portfolio tecnico: [GitHub](https://github.com/Arkanah)
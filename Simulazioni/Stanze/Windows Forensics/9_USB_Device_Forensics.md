# External Devices/USB device forensics


## 🧩 Device Identification
Le seguenti chiavi tengono traccia dei **dispositivi collegati** in particolare:

- **`SYSTEM\CurrentControlSet\Enum\USBSTOR`**  
Questa chiave registra **dispositivi di archiviazione USB** (chiavette, hard disk esterni, ecc.) che sono stati collegati almeno una volta al sistema.

- **`SYSTEM\CurrentControlSet\Enum\USB`**  
Questa chiave è più generale: registra **tutti i dispositivi USB**, non solo quelli di archiviazione.


>[!NOTE]
In entrambe le chiavi troviamo informazioni come:
**Nome del produttore**, **Modello del dispositivo**, **Numero di serie**, **Data/ora prima connessione**...

---

## ⏳ First/Last Times

Similmente questo registro di chiavi tiene traccia della **prima** volta che un dispositivo è **stato connesso**, l'**ultima** volta che è **stato connesso** e l'**ultima volta** che è stato **rimosso**.  

- `SYSTEM\CurrentControlSet\Enum\USBSTOR\Ven_Prod_Version\USBSerial#\Properties\{83da6326-97a6-4088-9453-a19231573b29}\####`

>[!NOTE]
>Tra parentesi graffe troviamo l'ID del dispositivo.  
>Il campo `####` può essere sostituito con:
>- 0064	➜ First Connection time
>- 0066	➜ Last Connection time
>- 0067	➜ Last removal time

---
## 💿 USB device Volume Name:

La chiave `SOFTWARE\Microsoft\Windows Portable Devices\Devices` contiene informazioni sui **dispositivi portatili USB** collegati al sistema, come smartphone, fotocamere digitali, lettori MP3 e altri dispositivi MTP/PTP.

>[!NOTE]
A differenza di USBSTOR, questa chiave si concentra su dispositivi **non necessariamente visti come unità disco**, ma comunque connessi via USB.

 

---

🔗 [TryHackMe – Windows Forensics 1 (modulo 9)](https://tryhackme.com/room/windowsforensics1)

---

>Documento curato da **Diego Bonatti**  
Portfolio tecnico: [GitHub](https://github.com/diego-bonatti)
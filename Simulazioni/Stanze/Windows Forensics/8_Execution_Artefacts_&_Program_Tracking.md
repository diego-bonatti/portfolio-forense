
# Prove dell'esecuzione di file

## 👤 UserAssist
>La chiave **`UserAssist`** registra le **applicazioni lanciate dall’utente** tramite **Windows Explorer**, ad esempio:

- Doppio clic su un programma
- Avvio da Start Menu
- Esecuzione da barra di ricerca

e quindi fornisce le informazioni su:

- i programmi eseguiti 
- il timestamp dell'esecuzione 
- il numero di volte che sono stati eseguiti.

>[!NOTE]
>I programmi eseguiti tramite **command line** non sono presenti
>in queste chiavi di UserAssist

### Dove si trova UserAssist:
`NTUSER.DAT\Software\Microsoft\Windows\Currentversion\Explorer\UserAssist\{GUID}\Count`
All’interno sono presenti più sottochiavi identificate da GUID, ognuna contenente una lista di elementi eseguiti.

### 🧠 Campi UserAssist – Significato forense

| Campo         | Significato                                                                 | Utilità forense                                      |
|---------------|------------------------------------------------------------------------------|------------------------------------------------------|
| **Run Counter** | Numero di volte che l’elemento è stato eseguito                             | Indica la **frequenza d’uso** di un’app o file (indica l'esecuzione dell'app o file)      |
| **Focus Count** | Quante volte la finestra è stata portata in primo piano                    | Mostra **interazione attiva** con l’app              |
| **Focus Time**  | Tempo totale (in millisecondi) in cui la finestra è rimasta attiva         | Aiuta a capire **quanto tempo l’utente ha usato** quell’app |

### ✅ In sintesi 
La chiave UserAssist è un artefatto fondamentale per ricostruire quali programmi sono stati eseguiti dall’utente,
con timestamp, frequenza e durata.
È utile per identificare attività sospette, software non autorizzato, o comportamenti abituali.

---

## 🧩 ShimCache (AppCompatCache) – Tracce di eseguibili visti dal sistema

**ShimCache**, noto anche come **AppCompatCache**, è un artefatto del registro che registra **eseguibili visti o potenzialmente eseguiti** dal sistema operativo.  
È utilizzato da Windows per gestire la compatibilità delle applicazioni, ma ha un **alto valore forense**.

---

### 📁 Posizione nel registro


`SYSTEM\CurrentControlSet\Control\Session Manager\AppCompatCache`  
Si trova nell’hive SYSTEM, quindi è valido per l’intero sistema, non specifico per un singolo utente.

>[!NOTE]
>I dati vengono scritti al riavvio o spegnimento del sistema, non in tempo reale.  
>Il timestamp lì indica la data/ora di ultima modifica del file, non di esecuzione del file!

Non garantisce la certezza dell’esecuzione, ma la presenza e visibilità del file

---

### 📒 Note
Registry Explorer ci genererà un output non leggibile di questo artefatto, per poterlo leggere dobbiamo utilizzare: **`AppCompatCache Parser Utility`**:

- Esempio di comando:  
`AppCompatCacheParser.exe --csv <path to save output> -f <path to SYSTEM hive for data parsing> -c <control set to parse>`

Il parametro `-c` permette di specificare **quale configurazione del sistema si vuole analizzare**.
Di solito si usa `-c 1`, ma verificare cercando in:
- `SYSTEM\Select\Current`

L'output può essere letto utilizzando **EZviewer** o altri tools di Eric Zimmerman.

---

## 📒 Amcache

**AmCache** è un artefatto del registro che registra **dettagli sui file eseguibili lanciati** sul sistema.  
È stato introdotto con Windows 8 e successivi, ed è uno dei metodi più affidabili per confermare l’**esecuzione di un’applicazione**.

- `C:\Windows\appcompat\Programs\Amcache.hve`

Informazioni riguardo agli ultimi programmi eseguiti possono essere trovare nell'hive:

- `Amcache.hve\Root\File\{Volume GUID}\`

>[!NOTE]
 AmCache salva gli **SHA1 hashes** dei programmi che sono stati eseguiti
---

## 🧩 BAM/DAM:


### 🪟 BAM
BAM sta per **Background Activity Moderator**.
È un componente di Windows introdotto con Windows 10 per gestire il consumo energetico delle app in background.  
### 🎯 Obiettivo tecnico
- Ottimizzare la durata della batteria
- Limitare l’attività delle app non in primo piano
- Monitorare quali app vengono eseguite e quando

`SYSTEM\CurrentControlSet\Services\bam\UserSettings\{SID}`

>SID sta per Security Identifier.  
È un identificatore univoco assegnato da Windows a ogni account utente, gruppo o entità di sicurezza.

### 🪟 DAM
DAM è un componente di Windows introdotto con Windows 10, progettato per monitorare e moderare l’attività delle **applicazioni desktop tradizionali** (non UWP).  
Il suo scopo originario è legato all’ottimizzazione energetica.

`SYSTEM\CurrentControlSet\Services\dam\UserSettings\{SID}`


>[!NOTE]
>BAM/DAM **non registrano esecuzioni da unità esterne** o condivisioni di rete.  
>Questa posizione contiene informazioni sui programmi eseguiti di recente, inclusi il **percorso completo** e la **data/ora dell’ultima esecuzione**.

---
🔗 [TryHackMe – Windows Forensics 1 (modulo 8)](https://tryhackme.com/room/windowsforensics1)

---

>📄Documento curato da **Diego Bonatti**  
💻Portfolio tecnico: [GitHub](https://github.com/diego-bonatti)  
📬Contatto: diego.bonatti.fdi@gmail.com
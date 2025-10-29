
# 🧠 Windows Forensics – Dove Cercare Cosa (Attività Utente e Sistema)

| Cosa vuoi sapere                        | Dove cercare / Tipo artefatto                                               | Percorso / File / Hive                                                  | Strumenti consigliati                      |
|----------------------------------------|------------------------------------------------------------------------------|-------------------------------------------------------------------------|-------------------------------------------|
| 🚀 Programmi eseguiti di recente        | Prefetch                                                                    | `C:\Windows\Prefetch\*.pf`                                              | PECmd, KAPE                                |
|                                        | UserAssist                                                                  | `NTUSER.DAT\...\Explorer\UserAssist`                                    | Registry Explorer, UserAssist              |
|                                        | Amcache                                                                     | `C:\Windows\AppCompat\Programs\Amcache.hve`                             | AmcacheParser                              |
|                                        | ShimCache / AppCompatCache                                                  | `SYSTEM\...\AppCompatCache`                                             | AppCompatCacheParser                       |
| 📂 File aperti dall’utente             | Jump Lists                                                                  | `%AppData%\Microsoft\Windows\Recent\AutomaticDestinations\*.ms`        | JLECmd                                     |
|                                        | RecentDocs                                                                  | `NTUSER.DAT\...\Explorer\RecentDocs`                                    | Registry Explorer                          |
|                                        | MRUList (Open/Save dialogs)                                                | `NTUSER.DAT\...\ComDlg32\OpenSavePidlMRU`                               | Registry Explorer                          |
| 🗑️ File cancellati                     | Recycle Bin                                                                 | `$Recycle.Bin`                                                          | RecycleBin parser, KAPE                    |
|                                        | USN Journal                                                                 | `\$Extend\$UsnJrnl` (NTFS)                                              | MFTECmd, Plaso                             |
| 🔌 Dispositivi USB collegati           | USBSTOR + MountedDevices                                                    | `SYSTEM\CurrentControlSet\Enum\USBSTOR` + `MountedDevices`              | USBDeview, Registry Explorer               |
| 📁 Cartelle esplorate dall’utente      | ShellBags                                                                   | `NTUSER.DAT\...\Shell\BagMRU`                                           | ShellBags Explorer, Registry Explorer      |
| 🧭 Attività utente nel tempo           | Windows Timeline                                                            | `ActivitiesCache.db`                                                    | Timeline Explorer, KAPE                    |
| 🧪 Programmi installati                | Uninstall keys                                                              | `SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall`                   | Registry Explorer                          |
|                                        | Amcache                                                                     | `Amcache.hve`                                                           | AmcacheParser                              |
| 👤 Login e logout                      | Security log (event log)                                                    | `Security.evtx`                                                         | Event Log Explorer, Plaso                  |
|                                        | SAM + SYSTEM                                                                | `SAM\Users` + `SYSTEM\...\ProfileList`                                  | Registry Explorer                          |
| 🌐 Connessioni di rete attive (RAM)    | Volatile memory (live capture)                                              | RAM dump                                                                | Volatility, Rekall                         |
| 🧠 Processi attivi (RAM)               | Volatile memory                                                             | RAM dump                                                                | Volatility (`pslist`, `psscan`)            |
| 🧨 File eseguito anche se cancellato   | Prefetch + Amcache + ShimCache                                              | `.pf`, `Amcache.hve`, `AppCompatCache`                                  | PECmd, AmcacheParser, AppCompatCacheParser |
| 🌐 Attività browser                    | WebCache                                                                    | `WebCacheV01.dat`                                                       | WebCacheV01 parser, KAPE                   |
| 🧭 Timeline completa di eventi         | Event logs + Timeline Explorer                                              | `.evtx` + CSV da KAPE                                                   | Plaso, Timeline Explorer                   |






# 📋 Tabella Registri Windows

| Tipo di informazione            | Hive / Percorso Registro                                                                 |
|----------------------------------|------------------------------------------------------------------------------------------|
| 🖥️ Versione e build di Windows   | `SOFTWARE\Microsoft\Windows NT\CurrentVersion`                                          |
| 💻 Nome del computer             | `SYSTEM\CurrentControlSet\Control\ComputerName\ComputerName`                            |
| 🌍 Fuso orario                   | `SYSTEM\CurrentControlSet\Control\TimeZoneInformation`                                  |
| 📡 Interfacce di rete            | `SYSTEM\CurrentControlSet\Services\Tcpip\Parameters\Interfaces\{GUID}`                  |
| 📶 Reti conosciute               | `SOFTWARE\Microsoft\Windows NT\CurrentVersion\NetworkList\Profiles\{GUID}`             |
| 🚀 Programmi in avvio automatico|  `SOFTWARE\Microsoft\Windows\CurrentVersion\Run`  `NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Run`
|                                  |                               |
| 🧩 Servizi attivi                | `SYSTEM\CurrentControlSet\Services`                                                     |
| 👤 Profili utente                | `SOFTWARE\Microsoft\Windows NT\CurrentVersion\ProfileList\{SID}`                        |
| 🔐 Account locali                | `SAM\Domains\Account\Users`                                                             |
| 🧠 UserAssist (GUI usage)        | `NTUSER.DAT\Software\Microsoft\Windows\CurrentVersion\Explorer\UserAssist`              |
| 📂 Jump Lists                    | File `.automaticDestinations-ms` e `.customDestinations-ms` in `%AppData%\Microsoft\Windows\Recent\AutomaticDestinations` |
| 🧬 Prefetch                      | File `.pf` in `C:\Windows\Prefetch`                                                     |
| 🔍 Amcache                       | `C:\Windows\AppCompat\Programs\Amcache.hve`                                             |
| 🌐 Cronologia browser (Edge/IE) | `WebCacheV01.dat` in `C:\Users\<user>\AppData\Local\Microsoft\Windows\WebCache`         |
| 🧭 Windows Timeline              | `ActivitiesCache.db` in `C:\Users\<user>\AppData\Local\ConnectedDevicesPlatform`        |

---

## 🧪 Note tecniche

- `CurrentControlSet` è un alias dinamico → punta a `ControlSet001` o `ControlSet002` in base al boot
- I file `.DAT` (NTUSER.DAT, SYSTEM, SOFTWARE, ecc.) sono gli hive principali
- I file `.LOG1`, `.LOG2`, `.blf`, `.regtrans-ms` contengono modifiche non ancora committate
- Alcuni artefatti (Jump Lists, Prefetch, Amcache) **non sono nel registro**, ma sono comunque fondamentali

---

## 📦 Suggerimenti per acquisizione

- Usa **KAPE** per raccogliere questi artefatti in modo mirato
- Analizza con:
  - `Registry Explorer` per hive e log
  - `RECmd`, `RegRipper` per parsing e report
  - `Timeline Explorer` per visualizzare CSV

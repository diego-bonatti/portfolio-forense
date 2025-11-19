
# Caso Stanza KAPE

Organization X has an Acceptable Use Policy for their Portable Devices, including Laptops.  
 This policy forbids users from connecting removable or Network drives, installing software from unknown locations, and connecting to unknown networks.   
 It looks like one of the users has violated this policy.   
 Can you help Organization X find out if the user violated the Acceptable Use Policy on their device?   

---

Estratto **KapeTriage** e **Registry Hives**, consultato USBSTORE nell'hive: SYSTEM

![alt](Screenshots/Serial_Numbers_USBSTOR_Reg_Exp.png)

1C6F654E59A3B0C179D366AE è il serial number

---

- Controllo Amcache, cerco il path degli eseguibili: Amcache_UnassociatedFileEntries.csv (non ho trovato nulla di rilevante).
- Controllo: ShimCache (AppCompatCache) SYSTEM\CurrentControlSet\Control\Session Manager\AppCompatCache   
- Controllo Prefetch (non ho trovato nulla di rilevante)


>[!NOTE]
I **Jump Lists** registrano file aperti con applicazioni, anche se eseguiti da unità di rete. Se l’utente ha lanciato il setup da Z:\Installers, quella voce sarà nei Jump Lists.  
In Automatic Destinations

![alt](Screenshots/Acquisizione_task_2.png)

Analizzando le Jump Lists in AutomaticDestinations.csv, tramite EzViewer ho trovato:

![alt](Screenshots/Jump_lists_automaticDest.png)


## Domanda 3

Quando il programma: `CHROMESETUP.EXE` è stato eseguito?

>Dal poster guida di **SANS** nella categoria **Program Execution**:    
![alt](Screenshots/User_Assist.png)

Analizzo quindi il registro e infatti trovo:

![alt](Screenshots/UserAssist_Reg_Exp.png)



## Domanda 4

Che cosa è stato cercato dalla **barra di ricerca** dello **START menu**?  

>Dal poster guida di **SANS** nella categoria **Deleted File or File Knowledge**:  
>![alt](Screenshots/WordWheelQuery.png)


Analizzo quindi il registro e trovo:

![alt](Screenshots/WordWeelQuery_Reg_Exp.png)

è stato cercato quindi *RunWallpaperSetup.cmd*


## Domanda 5

Quando si è connesso alla prima volta alla **Network 3**?

>Dal poster guida di **SANS** nella categoria **Network Activity/Physical Location**:  
![alt](Screenshots/Network_History.png)


Analizzo quindi il registro e noto:

![alt](Screenshots/Network_History_Reg_Exp.png)


## Domanda 6
Come si chiama l'unità USB da cui è stato installato KAPE?

Ho trovato i nomi delle USB collegate: D, E, in `SYSTEM\MountedDevices`

![alt](Screenshots/Lettere_USB.png)

![alt](Screenshots/Serial_Numbers_USBSTOR_Reg_Exp.png)



Analizzo le Jump Lists: (-d directory)
```powershell
JLECmd.exe -d "C:\Users\THM-4n6\Desktop\output_target\C\Users\THM-4n6\AppData\Roaming\Microsoft\Windows\Recent\AutomaticDestinations" --csv "C:\Users\THM-4n6\Desktop\toolsout"
```

![alt](Screenshots/Jump_Lists_KAPE.png)

---

>📄Documento curato da **Diego Bonatti**  
💻Portfolio tecnico: [GitHub](https://github.com/diego-bonatti)  
📬Contatto: diego.bonatti.fdi@gmail.com
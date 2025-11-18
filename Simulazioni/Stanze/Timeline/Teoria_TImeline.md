

# Timeline

## Terminologia

- **`Timestamp`**: indica quando un evento si è **verificato**.
- **`File System Structure`**
- **`MACB`**: **Modified**, **Accessed**, **Changed**, **Birth**.
- **`Event Sequencing`**: eventi **ordinati** in base al loro timestamp.
- **`Time Synchronization`**: timestamp devono essere convertiti nella **timezone** preferita.
- **`Time Carving`**: **ricostruzione** di artefatti eliminati tramite carving.
- **`Temporal Correlation`**: combinazione di più timestamp da più risorse per comprendere meglio l'incidente.


### Tipi di Timeline

- **`Quick Timeline`**: fornisce una panoramica generale degli eventi.
- **`Super Timeline`**: più dettagliata.
- **`Mini Timeline`**: simile alla quick ma è lo zoom di un periodo che ci interessa.


## Artifact Acquisition & Processing 

- **`Logs`**: conservano **attività**, variazioni del sistema e attività insolite.
- **`File System and Metadata`**: dettagli riguardo ai files (**MACB**)
- **`Network Traffic`**: tutti i dati che attraversano la rete, analizzato per identificare attività insolite.
- **`Mount Points`**: posizioni nel File System che contengono altri dati che possono essere analizzati.
- **`Temp Locations`**: directory temporanee che contengono artefatti.
- **`Deleted data from bin`**: anche i files eliminati possono contenere informazioni importanti.

## Integrità e Sicurezza dei dati

>L'integrità dei data viene garantita dalla copia **forense**, perchè dopo che è stata effettuata la copia, viene verificato l'**hash**.  
>Viene utilizzata anche la **Chain Of Custody**, che indica, chi detiene la prova, chi l'ha individuata, come l'ha estratta.  
Quindi verificare i dati con l'hash assicura che i dati non sono stati manipolati e sono legittimi.

>[!NOTE]
`Plaso` è un programma che ci permette di creare Super Timeline, assieme ad `Autopsy`, tra i due Plaso eccelle, ma Autopsy alla fine ha più funzionalità ed è un buon tool che svolge molti più compiti.



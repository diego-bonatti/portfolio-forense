
# Utilizzo di KAPE

Programma per estrarre artefatti da dispositivi live, molto più veloce
che aspettare l'imaging completo del disco.

- Estrae artefatti che ci interessano (grazie ai **target**)
- Processa gli artefatti (grazie ai **moduli**) 

## Come avviene la copia

La lista di file selezionata dalla categoria target viene processata,
cercando di copiare più files possibile (tutti quelli non **bloccati dall'OS**).  
I files di cui la copia è stata bloccata dall'OS entrano in un'altra coda, dove vengono copiati usando l'accesso diretto ai bit del disco (parliamo quindi di **RAW Copy)**

![alt](Screenshots/Procedura_KAPE.png)


## 🎯 Target Options

Rappresentano gli artefatti che devono essere **collezionati da un sistema o da un'immagine** e poi **copiati** nella destinazione che abbiamo specificato.

>[!NOTE]
> I targets in KAPE sono definiti con l'estensione `.tkape`.  
> Contiene informazioni sull'artefatto che vogliamo acquisire 

---

### Compound Targets

>È l'**insieme di più piccoli targets**.  
Questo insieme ci semplifica l'acquisizione, rendendola più veloce e più efficace rispetto all'acquisire uno alla volta questi targets.

Esempii di Compound Targets:

- `!BasicCollection`
- `!SANS_triage`
- `KAPEtriage`

!Disabled e !Local sono altre directory che svolgono funzioni sui targets.

- Contiene targets che non voglio che appaiano nella lista di Targets attivi

- Targets che non voglio che vengano sincronizzati con la repository di KAPE su Github

















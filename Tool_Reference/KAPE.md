
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
























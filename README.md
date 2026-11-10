# MovPacAI
## Contesto
Sviluppo di una App Android per movimentazione pacchi di una ricevitoria.
La ricevitoria offre questi servizi ai clienti in convenzione con PuntoPoste e potenzialmente con altri spedizionieri
- ARRIVI Un cliente che deve ricevere un pacco perchè acquistato su Amazon, Vinted, Subito o su altre piattaforme può scegliere che il pacco gli venga recapitato presso il PuntoPoste. Si presenterà dall'esercente con un codice per il ritiro e lo preleverà
- PARTENZE Un cliente che deve spedire un pacco per vendita su Vinted, Subito o altre piattaforme o per reso Amazon può portarlo presso il PuntoPoste per la spedizione opportutamente corredato di etichetta (cartacea o digitale). L'esercente provvederà alal presa in carico e successivamente alla consegna ai corrieri di spedizione.

| | | | GIACENZA | | |  | 
| -- | -- | -- | -- | -- | -- | -- |
| Il cliente porta un pacco da spedire | >> | Registrazione <br> Presa in carico | PARTENZE | Registrazione <br> Uscita | >> | Consegna al corriere |
| Il corriere porta un pacco da consegnare | >> | Registrazione <br> Presa in carico | ARRIVI | Registrazione <br> Uscita | >> | Consegna al cliente |

Diversi gestori da gestire

| Servizio Spedizione | PATENZE | ARRIVI | |
| -------------- | --- | --- | --- |
| Poste          | X | X | Da implementare |
| Inpost         |   |   | Dismesso        |
| Bartolini      |   |   | Possibile futuro nuovo servizio |
| ecc            |   |   | Possibile futuro nuovo servizio |
| Pacco cortesia | X | X | Pacco fatto arrivare all'indirizzo dell'esercizio commerciale ma non gestito ufficialmente |

## Funzionalità APP
### Funzioni base operatore
- L'APP deve leggere con la telecamera dello smartphone i barcode e i qrcode stampati sulla etichetta di arrivo o partenza e registrare i campi su un database (anche un semplice foglio CSV o excel o sheet Google)
- Il database contiene questi campi
- L'APP deve permettere un rapido accesso all'elenco dei pacchi in GIACENZA. Un pacco è in giacenza se è attualmente presso l'esercizio commerciale in quanto
  - va consegnato al cliente destinatario (ARRIVI)
  - va consegnato al corriere per la spedizione (PARTEBZE)
- L'APP permette l'edit dei campi registrati con telecamera per integrazionio correzioni; permette altresì, previa conferma, la cancellazione di un pacco
- L'APP permette la funzione di uscita con valorizzazionr automatica di data e ora di un pacco che vuol dire consegna al cliente o al corriere
- 
  
### Funzioni nuove
Come descritto 

- Diminuire il più possibile numero di click che l'operatore deve eseguire. Esempio ora per dichiarare l'uscita di un pacco bisogna arrivare all'elenco, selezionare un pacco e poi cliccare sull'icona di uscita

### Altro
- Ogni scansione o modifica manuale tramite App va prima salvata in locale e poi sincronizzata in background con il cloud
- Il database presente sul cloud deve essere giornalmente backuppato e archiviato con una retention configurabile ma indicativamente di 15 giorni

## Architettura
- L'APP è sviluppata per sistema operativo Android
- Per maggior resilenza il database degli Arrivi e Partenza ossia l'elenco dei dati letti dalle etichette o inseriti / modificati dall'esercente deve risiedere su una piattaforma cloud


## Suggerimenti
Quelli che seguono sono suggerimenti per quanto è stato fatto e ricercato fino ad ora ma non sono assolutamente vincolanti. Scegli la soluzione più idonea, che sia semplice ma dia un risultato buono in stabilità e aspetto grafico.

### Scelte framework
- Sviluppo in Kotline
- Archiviazione su Firestore

### Versione pregressa
Una prima versione funzionante dell'App è stata già realizzata  con AppSheet + GoogleSheet.
Di seguito si descrive tale app, si veda [AppSheet](AppSheet/) per relativi screenshot

L'App ha tre menù principali (Primary Navigation)
| Menù | Descrizione | Screenshot |
| --- | --- | --- |
| Giacenza | Visualizza un grafico a barre indicante le quantità di pacchi in magazzino ossia presenti presso l'esercizio commerciale; il grafico è raggruppato per servizio(all'epoca PuntoPoste e Inpost e per tipologia di pacco: Arrivo (da dare al cliente), Partenza (da dare al corriere) | [Giacenze1.jpg](AppSheet/Giacenze1.jpg) |
| ^        | Cliccando su una barra si accede all'elenco dei pacchi in giacenza per quel servizio e tipo | [Giacenze2.jpg](AppSheet/Giacenze2.jpg) |
| ^        | Selezionando un pacco si può procedere con EDIT dei campi, con CANCELLAZIONE o con la funzoine veloce USCITA | [Giacenze3.jpg](AppSheet/Giacenze3.jpg) |
-  Visualizza
- Riepilogo
- Archivio

  


# MovPacAI
## Contesto
Sviluppo di una App Android per movimentazione pacchi di una ricevitoria.
La ricevitoria offre questi servizi ai clienti in convenzione con PuntoPoste e potenzialmente con altri spedizionieri
- ARRIVI Un cliente che deve ricevere un pacco perchè acquistato su Amazon, Vinted, Subito o su altre piattaforme può scegliere che il pacco gli venga recapitato presso il PuntoPoste. Si presenterà dall'esercente con un codice per il ritiro e lo preleverà
- PARTENZE Un cliente che deve spedire un pacco per vendita su Vinted, Subito o altre piattaforme o per reso Amazon può portarlo presso il PuntoPoste per la spedizione opportutamente corredato di etichetta (cartacea o digitale). L'esercente provvederà alla presa in carico e successivamente alla consegna ai corrieri di spedizione.
- un pacco che è ancora presso la ricevitoria di dice in GIACENZA, tale pacco
  - verrà consegnato al cliente destinatario se è un ARRIVO
  - verrà consegnato al corriere/postino se è una PARTENZA
  - in entrambi i casi fino a quando non viene consegnato ha il campo "Data Uscita" non valorizzato

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

| Campo | Tipologia | Descrizione |
| ----- | --------- | ----------- |
| Tipo  | Ref       | puntamento ad altra tabella di tipi pacco: es "Poste Arrivi", "Poste Partenza". "InPost Arrivi", ... |
| Codice | Text | stringa alfanumerica che rappresenta il codice del pacco secondo il gestore del servizio | 
| Data Arrivo | Date | data in cui il pacco è entrato in ricevitoria tramite l'operazione di "scan e registrazione " |
| Da          | Text | chi ha consegnato il pacco in ricevitoria: nome comune "postino" o "corriere" per gli ARRIVI; nome della persona che spedisce per le PARTENZE |
| Data Arrivo | Date | data in cui il pacco esce dalla ricevitoria tramite l'operazione di "uscita" |
| A           | Text | destinatario del pacco: nome del cliente che deve ricevere il pacco per gli ARRIVI; nome del destinatario della spedizione per le PARTENZE |
| Note        | Text | eventuali altri note inserite dall'esercente |

(è possibile che il database effettivo contenga anche una chiave primaria univoca per record nascosta alel visualizzazioni)

- L'APP deve permettere un rapido accesso all'elenco dei pacchi in GIACENZA. Un pacco è in giacenza se è attualmente presso l'esercizio commerciale in quanto
  - va consegnato al cliente destinatario (ARRIVI)
  - va consegnato al corriere per la spedizione (PARTENZE)
- L'APP permette l'edit dei campi registrati con telecamera per integrazionio correzioni; permette altresì, previa conferma, la cancellazione di un pacco
- L'APP permette la funzione di uscita con valorizzazione automatica di data e ora di un pacco che vuol dire consegna al cliente o al corriere
- 
  
### Funzioni nuove
Lo sviluppo dell'APP può considerare le funzionalità del prototipo fatto con AppSheet, vedi [Versione pregressa](#versione-pregressa), apportando però almeno le seguenti migliorie

**Scan Ingresso/Uscite** 
Attualmente la funzione di scan serve solo per le registrazioni pacco in arrivo nella ricevitoria con identificazoine automatica del Codice letto da abr-code. Si vuole che:
- 

**Razionalizzazione**
- Razionalizzare i menù: le funzioni Giacenze e Archivio sostanzialmente accedono alla stessa base dati mostrando uno i pacchi ancora in giacenza per cui non è stata fatta la chiusura ed uno la totalità dei pacchi. Valutare l'unificazione dei due menù con
  - possibilità di filtro veloce per passare da Giacenze (record con data_chiusura null) a Archivio (tutti)
  - default di visualizzazione impostato su Giacenze dato che sono i pacchi che l'esercente deve ancora lavorare
- Diminuire il più possibile numero di click che l'operatore deve eseguire. Esempio ora per dichiarare l'uscita di un pacco bisogna arrivare all'elenco, selezionare un pacco e poi cliccare sull'icona di uscita
- Attualmente la funzione di scan (solo per le entrate) è fruibile dal menù Giacenze. Potrebbe essere portata in primo piano sulla schermata di default dell'App con pulsanti chiari, grandi e accessibili e affiancata dalla funzione di uscita tramite scan.

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
- Giacenze
- Riepilogo
- Archivio

e tre menù secondari (non in primo piano visibili ma accessibili da "..." in alto della finestra
- Statistiche
- Statistiche trimestrali
- About
  
| Menù | Descrizione | Screenshot |
| --------- | --- | --- |
| Giacenza  | Visualizza un grafico a barre indicante le quantità di pacchi in magazzino ossia presenti presso l'esercizio commerciale; il grafico è raggruppato per servizio (all'epoca PuntoPoste e Inpost e per tipologia di pacco: Arrivo (da dare al cliente), Partenza (da dare al corriere) | [Giacenze1.jpg](AppSheet/Giacenze1.jpg) |
| ^         | Cliccando su una barra si accede all'elenco dei pacchi in giacenza per quel servizio e tipo | [Giacenze2.jpg](AppSheet/Giacenze2.jpg) |
| ^         | Selezionando un pacco si può procedere con EDIT dei campi, con CANCELLAZIONE o con la funzoine veloce USCITA | [Giacenze3.jpg](AppSheet/Giacenze3.jpg) | 
| Riepilogo | Mostra per ciascun tipologia (es "Poste Arrivi", "Poste PArtenze", "Inpost Arrivi", ..) il totale dei pacchi registrati tramite l'app e il totale dei pacchi in giacenza | [Riepilogo1.jpg](AppSheet/Riepilogo1.jpg) | 
| Archivio  | Funzione simile a Giacenze ma mostra tutti i pacchi piuttosto che solo le Giacenze. Parte da un menù riepilogativo e poi permette l'accesso alla lista dei pacchi e al dettaglio | [Archivio1.jpg](AppSheet/Archivio1.jpg) [Archivio2.jpg](AppSheet/Archivio2.jpg)  |
| ^         | Dal dettaglio di un pacco è possibile Modifica, Cancellazione del record o operazione di Uscita se il pacco è tra quelli ancora in giacenza | [Archivio3.jpg](AppSheet/Archivio3.jpg)  |
| Statistiche |
| Statistiche trimestrali |
| About | Informazioni sull'app |

  
## Alternative Commerciali
Valuta queste alternative di APP per prendere idee

https://www.track-pod.com/blog/free-barcode-scanner-app/


# MovPacAI
## Contesto
Sviluppo di una App Android per movimentazione pacchi di una ricevitoria.
La ricevitoria offre questi servizi ai clienti in convenzione con PuntoPoste e potenzialmente con altri spedizionieri
- ARRIVI Un cliente che deve ricevere un pacco perchè acquistato su Amazon, Vinted, Subito o su altre piattaforme può scegliere che il pacco gli venga recapitato presso il PuntoPoste. Si presenterà dall'esercente con un codice per il ritiro e lo preleverà
- PARTENZE Un cliente che deve spedire un pacco per vendita su Vinted, Subito o altre piattaforme o per reso Amazon può portarlo presso il PuntoPoste per la spedizione opportutamente corredato di etichetta (cartacea o digitale). L'esercente provvederà alla presa in carico e successivamente alla consegna ai corrieri di spedizione.

- un pacco che è ancora presso la ricevitoria di dice in GIACENZA, tale pacco:
  - verrà consegnato al cliente destinatario se è un ARRIVO
  - verrà consegnato al corriere/postino se è una PARTENZA
  - in entrambi i casi fino a quando non viene consegnato ha il campo "Data Uscita" non valorizzato
- la registrazione ufficiale della consegna di un pacco (ARRIVI) o di una presa in carico per la spedizione (PARTENZE) avviene sui sistemi proprietari dei vari servi di di spedizione. Questa app deve servire solo come database interno dell'esercente e è separata dagli altri sistemi di gestione dei pacchi.

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
| Pacco cortesia | X | X | Pacco di tipo ARRIVI fatto arrivare all'indirizzo dell'esercizio commerciale ma non gestito ufficialmente. Questo si verifica se nell'etichetta non compare esplicitamente il punto di ritiro dell'esercente (esempio "PuntoPoste Tabaccheria N. 1660 ....") |

## Architettura
- L'APP è sviluppata per sistema operativo Android
- Per maggior resilenza il database degli Arrivi e Partenze ossia l'elenco dei dati letti dalle etichette o inseriti / modificati dall'esercente deve risiedere su una piattaforma cloud

## Funzionalità APP
### Login
- L'app sarà usata da una sola persona proprietario di una sola ricevitoria
- Non ci deve essere login sull'app

### Funzioni base operatore
- Leggere con la telecamera dello smartphone i barcode e i qrcode stampati sulla etichetta di arrivo o partenza e registrare i campi su un database (anche un semplice foglio CSV o excel o sheet Google)
- Il database contiene questi campi

| Campo | Tipologia | Descrizione |
| ----- | --------- | ----------- |
| TipoSpedizione | Ref | puntamento ad altra tabella di tipi spedizione: es "Poste Arrivi", "Poste Partenze". "InPost Arrivi", ... |
| Codice | Text | stringa alfanumerica che rappresenta il codice del pacco secondo il gestore del servizio | 
| Marketplace | Text | se rilevabile indica la piattaforma per cui si sta usando il servizio di Spedizione: Amazon, Vinted, Subito, ... |
| Data Arrivo | Date | data in cui il pacco è entrato in ricevitoria tramite l'operazione di "scan e registrazione " |
| Da          | Text | chi ha consegnato il pacco in ricevitoria: vuoto per gli ARRIVI; nome della persona che spedisce per le PARTENZE |
| Data Uscita | Date | data in cui il pacco esce dalla ricevitoria tramite l'operazione di "uscita" |
| A           | Text | destinatario del pacco: nome del cliente che deve ricevere il pacco per gli ARRIVI; nome del destinatario della spedizione per le PARTENZE |
| Note        | Text | eventuali altri note inserite dall'esercente |

- Non ci sono altri dati da registrare: no documento, no firma cliente, ...
- Gestire l'elenco dei pacchi in GIACENZA. Un pacco è in giacenza se è attualmente presso l'esercizio commerciale in quanto
  - va consegnato al cliente destinatario (ARRIVI)
  - va consegnato al corriere per la spedizione (PARTENZE)
- Gestire l'elenco completo dei pacchi gestiti, sia in giacenza che già usciti
- Permettere la modifica dei campi (sia registrati con telecamera che inseriti manualmente) per integrazioni o correzioni; permettere altresì, previa conferma, la cancellazione di un pacco
- Permettere la funzione di uscita con valorizzazione automatica di data e ora di un pacco che vuol dire consegna al cliente o al corriere. Anche il pacco registrato come "uscito" deve essere modificabile annullando, se occorre, la data di uscita
- Avere dashboard riepilogative con numero di pacchi gestiti e numero pacchi in giacenza per tipologia di servizio. Avere inoltre dashboard o grafici di andamento temporale sia su base mensile che trimestrale, indicare nei grafici le quantità di pacchi gestite per servizio (Poste, Inpost).
  
### Funzioni nuove
Per lo sviluppo dell'APP considerare le funzionalità del prototipo fatto con AppSheet, vedi [Versione pregressa](#versione-pregressa), apportando però almeno le seguenti migliorie

#### Scan Ingresso/Uscite
Attualmente la funzione di scan serve solo per le registrazioni pacco in arrivo nella ricevitoria con identificazoine automatica del Codice letto da bar-code. Si vuole che:
- La fotocamera possa leggere, oltre ai bar-code con il Codice, anche i QRCode, dove presenti, che riportano maggiori informazioni (es mittente, destinatario, ..). Con i dati letti si valorizzano i campi di un record che va confermato dall'operatore previa eventuale aggiunta di informazioni.
- La fotocamera sia usata anche per la funzione di uscita. Quindi un pacco può uscire in due modi:
  - consultando elenco si accede al dettaglio del pacco e si usa la funzione "Uscita" che valorizza la "Data uscita" e quindi di fatto toglie il pacco dalle giacenze
  - dalla schermata principale con la funzoine "Uscita Pacchi", si attiva la telecamera con cui si inquadra l'etichetta, il sistema identifica il record nella base dati delle giacenze e valorizza l'uscita. Se il pacco non viene trovato un messaggio di errore segnala il fatto.
- se possibile, valutandolo dal set di training e dalle prove che effettuerò, riconoscere in automatico con scan dell'etichetta
  - se si tratta di ARRIVO o PARTENZA
  - Marketplace
- Lo scan per ingresso o uscita valorizza i campi del database a secondo di quanto ha letto (codice e dati anagrafici per ingressi, data per le uscite) e i campi così modificati vengono mostrati all'operatore in una "schermata di modifica" per una conferma (tasto OK o Salva); tuttavia dalla "schermata di modifica" deve essere possibile rieseguire lo scan con nuova valorizzazione dei campi. Questa funzione è necessaria e importante perchè le etichette riportano più codici a barre e più qrcode quindi può capitare di aver inquadrato quello errato o quello incompleto che riporta meno dati
- Un pacco registrato come già entrato (scan o inserimento manuale + conferma esplicita operatore) non può essere di nuovo scansionato per l'ingresso; se ciò avviene il sistema avvisa dell'errore e del duplicato; stessa cosa per l'operazione di uscita che può essere fatta solo una volta a meno di modifiche del record che cancellino "data uscita"
 
#### Razionalizzazione
- Razionalizzare i menù: le funzioni Giacenze e Archivio sostanzialmente accedono alla stessa base dati mostrando uno i pacchi ancora in giacenza per cui non è stata fatta la chiusura ed uno la totalità dei pacchi. Valutare l'unificazione dei due menù con
  - possibilità di filtro veloce per passare da Giacenze (record con data_chiusura null) a Archivio (tutti)
  - default di visualizzazione impostato su Giacenze dato che sono i pacchi che l'esercente deve ancora lavorare
- Diminuire il più possibile numero di click che l'operatore deve eseguire. Esempio ora per dichiarare l'uscita di un pacco bisogna arrivare all'elenco, selezionare un pacco e poi cliccare sull'icona di uscita
- Posizionare in primo piano nella schermata home le funzioni più utilizzate come "scan per Entrate Pacchi") e "scan per "Uscita Pacchi". Usare pulsanti chiari, grandi e accessibili.

#### Elenchi
- Permettere la selezione multipla di più pacchi su cui applicare la funzione di Uscita (cliente prende tre pacchi di propria proprietà e non ho usato la funzione di uscita tramite scan del  code; allora vado in elenco, selezono tutti e tre i pacchi e con un asola operazoine faccio l'uscita)
- Permettere dall'elenco la cancellazione di un record (un pacco) senza dover accedere al dettaglio di quel pacco
- Permettere filtri tramite casella di ricerca globale, se possibile integrato con riconoscitore vocale di Google
- Permettere l'edit anche del campo codice (non previsto su versione attuale perchè usato come chiave primaria)
- Permettere ordinamento almeno per alfabetico ordini e cronologico
- Nelle date mostrare sia giorno che ora
- In cima a tutti gli elenchi indicare sempre il numero di record totali della vista con gli attuali filtri
- Evidenziare con colori o icone diverse i pacchi in base al Marketplace
  
#### Statistiche
- permettere i grafici di statistica (mensili o trimestrali) sia per la totalità (come è ora) che per le sole giacenze
- se si prevedono grafici (barre, torte, ..) indicare sempre negli elementi grafici anche i valori assoluti delle quantità riportate
- ogni grafico deve essere anche fruibile in forma tabellare

#### Open Discussion
Da verificare, esaminando anche i dati di training che fornirò, la corretta interpretazione di mittente e destinatario tramite scan dei qrcode

Esempi

| use case | Mittente Etichetta | Destinatario Etichetta | Mittente sul DB | Destinatario sul DB | TipoSpedizione sul DB | Marketplace sul DB | Note |
| -------- | ------------------ | ---------------------- | --------------- | ------------------- | ------------------- | ----------------- | ---- |
| Acquisto Amazon ricevuto in tabaccheria tramite Poste | MXP <b> Strada Dogana 45 <br> Milano | Pierluigi Pierini <br> Punto poste Tabaccheria 1660 <br> Via Raffaele Battistini 123 <br> Roma | | Pierluigi Pierini | PosteArrivi | Amazon | |
| Acquisto Amazon mandato per cortesia dell'esercente al suo indirizzo tramite Poste | MXP <b> Strada Dogana 45 <br> Milano | Pierluigi Pierini <br> Via Raffaele Battistini 123 <br> Roma | | Pierluigi Pierini | Altro | Amazon | non rientra nei servizi della ricevitoria e non viene fatturato, classificarlo come Altro |
| Spedizione Vinted dalla ricevitoria via Poste | Pierluigi Pierini <br> Via Raffaele Battistini 123 <br> Roma | Guglielmo Marconi  <br> Punto poste Tabaccheria 2850 <br> Via Porrettana, 1320 Casalecchio (BO) | Pierluigi Pierini | Guglielmo Marconi | PostePartenze | Vinted | pacco in partenza |

- Se per la corretta identificazione delle etichette è necessario conoscere i dati della ricevitoria che usa l'App permettene la configurazione in un apposito menù di amministrazione

### Altri requisiti architetturali
- Ogni scansione o modifica manuale tramite App va prima salvata in locale e poi sincronizzata in background con il cloud
- Inserisci funzione di export record filtrati in CSV
- Il database presente sul cloud deve essere giornalmente backuppato e archiviato con una retention configurabile (default 15 giorni). Non voglio piani a pagamento per cui se il piano free non offre backup trova altre soluzioni come la lettura, conversione in CSV e archiviazione su drive.

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

tre menù secondari (non in primo piano visibili ma accessibili da "..." in alto della finestra
- Statistiche
- Statistiche trimestrali
- About

alcune funzioni fruibili tramite "pulsanti azione"
- "+" = aggiungi pacco
- icona del camion = uscita pacco
- cancella record
- edit record
  
| Menù | Descrizione | Screenshot |
| --------- | --- | --- |
| Giacenza  | Visualizza un grafico a barre indicante le quantità di pacchi in magazzino ossia presenti presso l'esercizio commerciale; il grafico è raggruppato per servizio (all'epoca PuntoPoste e Inpost e per tipologia di pacco: Arrivo (da dare al cliente), Partenza (da dare al corriere) | [Giacenze1.jpg](AppSheet/Giacenze1.jpg) |
| ^         | Cliccando su una barra si accede all'elenco dei pacchi in giacenza per quel servizio e tipo | [Giacenze2.jpg](AppSheet/Giacenze2.jpg) |
| ^         | Selezionando un pacco si può procedere con EDIT dei campi, con CANCELLAZIONE o con la funzoine veloce USCITA | [Giacenze3.jpg](AppSheet/Giacenze3.jpg) | 
| Riepilogo | Mostra per ciascun TipoSpedizione (es "Poste Arrivi", "Poste Partenze", "Inpost Arrivi", ..) il totale dei pacchi registrati tramite l'app e il totale dei pacchi in giacenza | [Riepilogo1.jpg](AppSheet/Riepilogo1.jpg) | 
| Archivio  | Funzione simile a Giacenze ma mostra tutti i pacchi piuttosto che solo le Giacenze. Parte da un menù riepilogativo e poi permette l'accesso alla lista dei pacchi e al dettaglio | [Archivio1.jpg](AppSheet/Archivio1.jpg) [Archivio2.jpg](AppSheet/Archivio2.jpg)  |
| ^         | Dal dettaglio di un pacco è possibile Modifica, Cancellazione del record o operazione di Uscita se il pacco è tra quelli ancora in giacenza | [Archivio3.jpg](AppSheet/Archivio3.jpg)  |
| Statistiche | Rappresenta su grafico i totali pacchi raggruppati per mese; con click si accede al dettaglio del mese con grafico a barre diviso per TipoSpedizione; ancora click e si accede all'elenco dei pacchi per il mese e il TipoSpedizione selezionati  | [Statistiche1.jpg](AppSheet/Statistiche1.jpg) [Statistiche2.jpg](AppSheet/Statistiche2.jpg) [Statistiche3.jpg](AppSheet/Statistiche3.jpg) |
| Uscite trimestrali | Come Statistiche ma con raggruppamento del primo grafico per trimestri dell'anno piuttosto che per mesi | [UsciteTrim11.jpg](AppSheet/UsciteTrim1.jpg) [UsciteTrim12.jpg](AppSheet/UsciteTrim2.jpg) |
| About | Informazioni sull'app |  [About1.jpg](AppSheet/About1.jpg)  About2.jpg](AppSheet/About2.jpg) |
| "+" = aggiungi pacco | L'icona "+" apre la schermata di inserimento e modifica di un record, premendo l'icona "qrcode" il valore di Codice viene letto dallo scan | [Aggiungi1.jpg](AppSheet/Aggiungi1.jpg) [Aggiungi2.jpg](AppSheet/Aggiungi2.jpg)  |
icona del camion = uscita pacco | Una volta selezionato il record con l'icona "camion" si fa l'uscita del pacco | [Uscita1.jpg](AppSheet/Uscita1.jpg) [Uscita2.jpg](AppSheet/Uscita2.jpg) |

NOTA: Per i raggruppamenti per data fa fede la "Data uscita" del pacco

## Attivazione e distribuzione app
- L'App può essere distribuita tramite APK da installare senza Play Store
- In una seconda fare faremo la migrazione dei dati di Google Sheet su nuovo database Firebase
  
## Alternative Commerciali
Valuta queste alternative di APP per prendere idee

https://www.track-pod.com/blog/free-barcode-scanner-app/


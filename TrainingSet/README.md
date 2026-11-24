
# Training Set

Convenzione del nome dei files con barcode e QRCode usati per training

Il nome file è composto da 6 campi separati dal carattere "_" (underscore)
Quella che segue è la legenda dei vari campi, se un valore non è noto viene inserita la lettere "X"


| Campo1 | Campo2 | Campo3 | Campo4 | Campo5 | Campo6 | Campo7 |
| ------- | ------- | ------- | ------- | ------- | ------- | ------- |
| Sequenziale identificativo del file | Modalità di acquisizione: <br>**S** = Scan <br>**F** = File etichetta originaria fornita dal MarketPlace <br> **P** = Picture foto delel etichette| Tipo Servizio <br>- Poste<br>- InPost<br>- ...| - Arrivi<br>- Partenze | MarketPlace<br>- amazon<br>- Vinted<br>- ... | Se pacco inserenti i servizi da fatturare della ricevitoria<br>**R** = Ricevitoria<br>**A** = Altro | Per alcuni sample viene fornito nel nome file il **Codice** da memorizzare sulla base dati come identificativo del pacco |

gli scan sono stati presi con "Fax e scanner di Windows" e seguenti opzioni
- ritaglio manuale della sola areaa interessata
- Profilo = Documento
- Colore = Scala di Grigi
- Formato = TIF
- Risoluzione DPI = 300


La seguente riporta i valori corretti letti a mano dalle etichette

| File     | Servizio Spedizione |  Tipo     | Marketplace | gestione in Ricev 1660 | Codice                    |  Mittente         | Destinatario        |
| ----     | ------------------- | --------- | ----------- | ---------------------- | ------------------------- |  ---------------- | ------------------- |
| 01_S_... | Poste               | Arrivi    |             | SI                     | RTZF239C63802010          |                   | PIERLUIGI PIERINI   | 
| 02_S_... |                     |           | Amazon      | NO (Altro cortesia)    | IT3482510720              |                   | Maurizio Di Gravio  |
| 03_S_... |                     |           |             | NO (Altro cortesia)    | IT2657547993              |                   | Pierluigi Pierini   |
| 04_F_... | Poste               | Partenze  | Vinted      | SI                     | RTZ1UW1WEZAKC8S6          | PIERLUIGI PIERINI | FRANCESCO PICOZZI   |
| 05_F_... | Poste               | Partenze  | Vinted      | SI                     | 1UW1WEZAKB6JL             | PIERLUIGI PIERINI | VLOCKERS C/O MADRID |
| 06_F_... | Poste               | Partenze  | Vinted      | SI                     | RTZ1UW1WEZAKB5VK          | PIERLUIGI PIERINI | AUGUSTA CAMERONI    |
| 07_F_... | InPost              | Partenze  | Subito      | SI                     | 820159547623875031481519  | Pierluigi Pierini | Enrico Zenesini     |
| 08_S_... | Poste               | Arrivi    | Amazon      | SI                     | RTZF239C65118791          |                   | PIERLUIGI PIERINI   |
| 09_P_... | Poste               | Arrivi    | Vinted      | SI                     | RTZ1UW1WEZAQAF3K          | ANNA PIRRO        | FRANCESCA MARINI    |
| 10_P_... | Poste               | Arrivi    | Vinted      | SI                     | RTZ1UW1WEZAPIG3Z          | MAURIZIO ZATTA    | VITTORIA MARADEI    |
| 11_P_... | Poste               | Arrivi    | Vinted      | SI                     | RTZ1UW1WEZAOJBCL          | Federica Micheli  | Federica Ferrera    |
| 12_P_... | Poste               | Arrivi    | Amazon      | SI                     | RTZF259D92964515          |                   | PAOLO FIOCCHETTI    |
| 13_P_... | Poste               | Arrivi    | Amazon      | SI                     | RTZF259D93030815          |                   | SUSANNA CAROLINA    |
| 14_P_... | Poste               | Arrivi    | Zalando     | SI                     | RTZ1P73C70979183          |                   | Leilani Jane Sebastian |
| 15_P_... | Poste               | Partenze  | Zalando     | SI                     | RVE1UW1OT5AAZ3AV          | Anna Veit         | Zalando Italy Srl   |
| 16_P_... | Poste               | Partenze  |             | SI                     | RTZ1UW1WEZAQYIV1          | Alessio Monottoli | Daniele Valenzano   |
| 17_P_... | Poste               | Partenze  |             | SI                     | JF70059193217             | carmela attina    | Amazon SORT         |
| 18_P_... | Poste               | Partenze  |             | SI                     | RTZ1UW1WEZAQXLUF          | Federica Falessi  | Sandy Ganlath       |
| 19_P_... | Poste               | Arrivi    | Amazon      | SI                     | RTZF259D90377978          |                   | PIERLUIGI PIERINI   |
| 20_P_... | Poste               | Arrivi    | Amazon      | SI                     | RTZF239C65118791          |                   | PIERLUIGI PIERINI   |
| 21_P_... | Poste               | Arrivi    | Amazon      | SI                     | RTZF238D92083019          |                   | PIERLUIGI PIERINI   |

I pacchi in arrivo presso "ricevitoria 1660" hanno l'indicazione della ricevitoria nell'etichetta

I pacchi in partenza tramite "ricevitoria 1660" non hanno l'indicazione della ricevitoria perchè il cliente li porta arbitrariamente per la spedizione; alcune etichette in partwnza sono quindi marcate come afferenti alla ricevitoria solo perchè le ho prese presso l'esercizio

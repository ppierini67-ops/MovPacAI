
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
| File     | Tipo Servizio   |   |   DA FINIRE ......                         |
| ----     | -----------     | ---- | -----------------                        |
| 01_S_... | Poste           | Arrivi      | _X_R_RTZF239C63802010.tif                    |
| 02_S_... | <non lo so>     | <non lo so> | _Amazon_A_IT3482510720.tif                   |
| 03_S_... | <non lo so >    | <non lo so> |_X_A_IT2657547993.tif                        |
| 04_F_... | Poste_Partenze  | _Vinted_R_RTZ1UW1WEZAKC8S6.pdf               |
| 05_F_... | Poste_Partenze  | _Vinted_R_1UW1WEZAKB6JL.pdf                  |
| 06_F_... | Poste_Partenze  | _Vinted_R_RTZ1UW1WEZAKB5VK.pdf               |
| 07_F_... | InPost_Partenze | _Subito_R_820159547623875031481519.pdf       |
| 08_S_... | Poste_Arrivi    | _Amazon_R_RTZF239C65118791.tif               |
| 09_P_... | Poste_Arrivi    | _Vinted_R_RTZ1UW1WEZAQAF3K.jpg               |
| 10_P_... | Poste_Arrivi    | _Vinted_R_RTZ1UW1WEZAPIG3Z.jpg               |
| 11_P_... | Poste_Arrivi    | _Vinted_R_RTZ1UW1WEZAOJBCL.jpg               |
| 12_P_... | Poste_Arrivi    | _Amazon_R_RTZF259D92964515.jpg               |
| 13_P_... | Poste_Arrivi    | _Amazon_R_RTZF259D93030815.jpg               |
| 14_P_... | Poste_Arrivi    | _Zalando_RTZ1P73C70979183.jpg                |
| 15_P_... | Poste_Partenze  | _Zalando_R_RVE1UW1OT5AAZ3AV.jpg              |
| 16_P_... | Poste_Partenze  | _X_R_RTZ1UW1WEZAQYIV1.jpg                    |
| 17_P_... | Poste_Partenze  | _X_R_JF70059193217.jpg                       |
| 18_P_... | Poste_Partenze  | _X_R_RTZ1UW1WEZAQXLUF.jpg                    |
| 19_P_... | Arrivi_Amazon   | _R_RTZF259D90377978.jpg                      |
| 20_P_... | Arrivi_Amazon   | _R_RTZF239C65118791.jpg                      |
| 21_P_... | Arrivi_Amazon   | _R_RTZF238D92083019.jpg                      |


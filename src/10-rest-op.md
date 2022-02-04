# Operazioni REST

Lato server, le operazioni REST sono solitamente associate ad operazioni che avvengono all'interno di un database.

Ricordiamo che, quando interagiamo con un qualsiasi database, i diversi comandi rientrano all'interno delle operazioni cosiddette **CRUD**: **C**reate, **R**ead, **U**pdate e **D**elete.

I database SQL e le chiamate HTTP usano strategie diverse per eseguire queste operazioni. Di seguito una tabella riassuntiva di confronto.

| Operazione  | SQL | HTTP/REST |
|---|---|---|
| Create |INSERT|POST (o PUT)|
| Read  |SELECT|GET|
| Update  |UPDATE|PUT / PATCH|
| Delete  |DELETE|DELETE|

Di seguito vediamo in dettaglio alcune operazioni HTTP/REST. 

Ricordiamo anche che, per effettuare una qualsiasi operazione, bisogna preliminarmente identificare **l'URL** della risorsa, ad esempio `/users/27` oppure `/events`. Per identificare la risorsa, è necessario consultare la documentazione delle API.

## Selezione della risorsa
Per leggere il valore di una risorsa, usiamo l'URL della risorsa stessa ed effettuiamo la richiesta HTTP con il metodo GET. Ci si aspetta che il database non cambi stato dopo questa chiamata.

> Eccezioni a questa regola potrebbero essere quando vogliamo salvare alcune informazioni di analisi d'utilizzo del sito, In questo caso, una chiamata GET aumenterà comunque un contatore di visite, modificando di fatto lo stato del server.


## Modifica di una risorsa
Per modificare la risorsa `POST` e `PUT` in base al tipo di operazione che vogliamo eseguire. `POST` di solito si usa quando voglio creare una nuova risorsa, mentre `PUT` quando la voglio modificare. In realtà, la distinzione tra questi due metodi è più sottile, come mostrato di seguito.

### Idempotenza
Per capire bene la differenza tra `POST` e `PUT`, dobbiamo introdurre il concetto di idempotenza. Un comando si chiama _idempotente_ se "_richieste ripetute identiche devono portare al medesimo stato dei dati sul server_". Pensate ad esempio ad una `UPDATE` in SQL. Se chiamate più volte UPDATE con gli stessi parametri, le chiamate successive alla prima non avranno effetto sulla riga da aggiornare. Pensate ora alla INSERT. Se chiamate più volte INSERT con gli stessi parametri, ipotizzando un'assegnazione automatica della chiave primaria, ad ogni chiamata il database andrà ad aggiungere una nuova riga.

La stessa cosa per le chiamate HTTP.

`PUT` è idempotente: facendo più richieste identiche, il DB viene modificato solo la prima volta.

`POST` non è idempotente: facendo più richieste identiche, ad ogni chiamata verrà aggiunta una nuova risorsa e creata una chiave primaria per noi.

Nella pratica, questo significa che quando uso `PUT` devo passare anche la chiave primaria dell'elemento da creare o aggiornare, mentre con `POST` non devo fornire la chiave primaria, perché verrà creata dal server.

Approfondimento sul concetto di idempotenza [qui]( http://blog.loris.tissino.it/2013/06/http-rest-e-api.html).

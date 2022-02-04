# REST API

La parola "API" (Application Program Interface) è riferita al generico concetto di _definizione_ un'interfaccia tra due applicazioni software. Nell'ambito web, le API sono particolarmente importanti perché definiscono il modo con cui client e server comunicano tra di loro. Delle API definite bene, permettono di dividere in modo proficuo il lavoro tra gli sviluppatori front-end e back-end, facilitano l'integrazioni di servizi di terze parti, la scalabilità e la manutenibilità del codice, etc.

Esistono diversi approcci per definire delle API. L'approccio web attualmente più usato si chiama "REST" ed è quello che analizzeremo in questo corso.

> Un alternativa alle REST API sono le [SOAP API](https://it.wikipedia.org/wiki/SOAP), in cui uso sempre uno stesso URL e la specifica risorsa viene selezionata all'interno del body della richiesta HTTP attraverso un documento XML. Questo tipo di approccio però non si coniuga bene con il funzionamento dei browser e del web in generale, rendendo impossibile ad esempio creare bookmarks, condividere link o navigare indietro nella cronologia delle pagine visitate. In generale quindi, se non ci sono esigenze particolari, è sempre consigliato usare il paradigma REST.

## Caratteristiche distintive delle REST API
REST è l'acronimo di [Representational State Transfer](https://it.wikipedia.org/wiki/Representational_state_transfer). Proposto per la prima volta nel 2000 da Roy Fielding (USA), prevede i seguenti concetti fondamentali:

- Risorse con URL auto-descrittivi

Gli URL devono essere il più possibile chiari per l'utente e contenere le informazioni necessarie al server per processare la richiesta. Ad esempio, dall'URL `https://en.wikipedia.org/wiki/Representational_state_transfer#Uniform_interface` è chiaro cosa sto chiedendo al server, anche senza dover cliccare sul link stesso.

- Utilizzo esplicito dei metodi HTTP

Ogni risorsa (URL) può essere associato ad azioni diverse usando metodi HTTP diversi. Ad esempio, usando il metodo `GET` posso leggere una risorsa, con `PUT` posso modificarla, con `DELETE` posso cancellarla, etc.

- Comunicazione senza stato

La comunicazione senza stato (_stateless_) è qualcosa che pervade il web e forse è uno dei suoi tratti più caratteristici e di successo. In pratica, significa che ogni richiesta è indipendente dalle altre e il server non tiene traccia direttamente della successione delle chiamate. Un'associazione tra queste può essere fatto indirettamente tramite cookies o chiavi di sessione, ma il server non tiene aperto un thread, processo o canale tra una chiamata HTTP e la successiva.


## REST & MVC
Lato server, ogni richiesta HTTP è associata ad un azione (cioè un metodo o una funzione). Le azioni sono richiamabili direttamente nella barra degli indirizzi del browser o indirettamente da una ancora in un link. I parametri che vengono passati alla funzione sono anch’essi nella forma analoga a quella degli altri path, cioè un elenco di parametri separati da `/` oppure alla fine del path dopo il `?`. Ad es. `calcolatrice/somma/3/4/` (oppure `calcolatrice/somma?a=3&b=4`) esegue la somma di due numeri forniti come parametro. L'abbinamento tra HTTP e azione avviene nel "routing" dell'applicazione, nel nostro caso in `index.php`.


# Schema logico

Una volta che siamo soddisfatti con lo schema concettuale, possiamo passare a convertirlo nello schema logico che poi potrà essere implementato nel DBMS.

Per fare questo passaggio, ci sono alcune regole che dobbiamo seguire.

## Entità ed attributi

Per le entità valgono le seguenti regole:
- ogni entità diventa una tabella
- le tabelle si rappresentano con la sintassi `nometabella()`
- il nome delle entità diventa il nome della tabella, _convertito al plurale_ e con la lettera minuscola (es. Utente diventa utenti)
- ogni attributo diventa un'attributo della tabella
- se la chiave primaria è `id`, si aggiunge il nome della tabella (al singolare), ad esempio `id_utente`
- le chiavi primarie sono <ins>sottolineate</ins>

Riprendendo l'esempio del capitolo precedente:

utenti(<ins>id_utente</ins>,nome,cognome)
eventi(<ins>id_evento</ins>,titolo, costo)

Queste tabelle ancora non sono complete perché mancano le chiavi esterne, che vedremo nel prossimo paragrafo.

## Relazioni
Per le relazioni valgono le seguenti regole:
- per le relazioni uno a molti (una molteplicità ha cardinalità massima `1`, l'altra `n`), si aggiunge una chiave esterna nel lato "uno" della relazione
- per le relazioni molti a molti (entrambe le molteplicità della relazione hanno cardinalità massima `n`), si crea una nuova tabella associativa, che contiene come attributi le chiavi esterne verso le due relazioni; bisogna anche aggiungere un vincolo di unicità della coppia di chiavi esterne
- per le relazioni uno a uno (entrambe le molteplicità hanno cardinalità massima `1`), si può procedere in diversi modi:
 - le due tabelle possono diventare un'unica tabella che contiene gli attributi di entrambe le tabelle
 - se non si vuole creare un'unica entità, si procede come nel caso delle relazioni molti a molti
- per le chiavi esterne si usa il _corsivo_

Completando l'esempio di prima:
utenti(<ins>id_utente</ins>,nome,cognome)
eventi(<ins>id_evento</ins>,titolo, costo, _organizzatore_)
partecipanti(<ins>id_utente</ins>,<ins>id_evento</ins>)


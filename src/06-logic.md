# Schema logico

Una volta che siamo soddisfatti con lo schema concettuale, possiamo passare a convertirlo nello schema logico che poi potrà essere implementato nel DBMS.

Per fare questo passaggio, ci sono alcune regole che dobbiamo seguire.

## Entità ed attributi

Per le entità valgono le seguenti regole:
- ogni entità diventa una tabella
- le tabelle si rappresentano con la sintassi `nometabella(lista attributi)`
- il nome dell'entità diventa il nome della tabella, _convertito al plurale_ e con la lettera minuscola (es. Utente diventa utenti)
- ogni attributo dell'entità diventa un'attributo della tabella
- se la chiave primaria è `id`, si aggiunge il nome della tabella al singolare, ad esempio `id_utente`
- le chiavi primarie sono <ins>sottolineate</ins>

Riprendendo l'esempio del capitolo precedente:

- utenti(<ins>id_utente</ins>,nome,cognome)
- eventi(<ins>id_evento</ins>,titolo, costo)

Queste tabelle ancora non sono complete perché mancano le chiavi esterne, che vedremo nel prossimo paragrafo.

## Relazioni
Per le relazioni valgono le seguenti regole:
- per le relazioni uno a molti si aggiunge una chiave esterna nel lato "uno" della relazione
- per le relazioni molti a molti, si crea una nuova tabella associativa, che contiene come attributi le chiavi esterne verso le due relazioni; bisogna anche aggiungere un vincolo di unicità della coppia di chiavi esterne
- per le relazioni uno a uno si può procedere in diversi modi:
    - le due tabelle possono diventare un'unica tabella che contiene tutti gli attributi
    - se non si vuole creare un'unica tabella, si procede come nel caso delle relazioni uno a molti, scegliendo come entità che ha la chiave esterna quella più dipendente dall'altra (es. dettagli_utente dipende concettualmente da utente e quindi andrà a contenere la chiave esterna)
- per le chiavi esterne si usa il _corsivo_

Completando l'esempio di prima, la relazione è n-n, quindi aggiungo una tabella associativa in cui la coppia:

- utenti(<ins>id_utente</ins>, nome, cognome)
- eventi(<ins>id_evento</ins>, titolo, costo, _organizzatore_)
- partecipanti(_<ins>id_utente</ins>_, _<ins>id_evento</ins>_)


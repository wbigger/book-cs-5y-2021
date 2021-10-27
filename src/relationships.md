# Relazioni tra tabelle

Due tabelle possono avere dei riferimenti tra loro di tipo diverso, che affronteremo in questo capitolo.

# Uno a uno (one-to-one)
È il caso in cui una riga di una tabella si associa ad una ed una sola riga di un'altra tabella.

Questo tipo di relazione si ha di solito quando abbiamo una tabella di dettagli. Pensiamo ad esempio ad un'applicazione in cui salviamo nei database i dettagli di un utente.

```sql
create table utenti (
    utente_id int primary key auto_increment,
    nome varchar(100),
    cognome varchar(100),
);
create table dettagli_utente (
    utente_id int,
    indirizzo varchar(100),
    telefono varchar(30),
    foreign key(utente_id) references utenti(utente_id)
);
```
In questo caso, ogni dettaglio si riferisce ad uno ed un solo utente, ed ogni utente ha uno es un solo dettaglio.

Per interrogare il database:
```sql
select u.cognome,d.indirizzo
from dettagli_utente as d
join utenti as u
    using(utente_id);
```
Da notare che in questa `select` ho usato `using` anziché `on` perché le colonne con la chiave esterna e la chiave primaria avevano lo stesso nome (`utente_id`).

Qualcuno potrebbe pensare che la tabella `dettagli_utente` potrebbe essere fusa con la tabella `utenti`, cioè potremmo semplicemente aggiungere le colonne `indirizzo` e `telefono` ad `utenti`. Ottima osservazione! In effetti, alcune volte conviene farlo, altre volte no. Bisogna prendere in considerazione:
- quanto spesso utilizzo i dettagli: se li uso raramente, conviene tenerli in una tabella separata
- quanto sono grandi le tabelle: se la tabelle sono grandi, conviene tenerle separate
- se hanno privilegi di accesso diversi: se la tabella dettagli ha dei vincoli di accesso più stringenti (ad esempio perché contiene dei dati sensibili), conviene tenerli in una tabella separata.

# Uno a molti (one-to-many)
E' il caso in cui una riga di una tabella può avere un riferimento da più righe di un'altra tabella.

Pensiamo al caso degli eventi e dell'organizzatore dell'evento. Ogni evento, ha uno ed un solo utente organizzatore, mentre un utente può organizzare vari eventi.

```sql
create table utenti (
    utente_id int primary key auto_increment,
    nome varchar(100),
    cognome varchar(100),
)
create table eventi (
    evento_id int primary key auto_increment,
    titolo varchar(100),
    organizzatore int,
    foreign key(organizzatore) references utenti(utente_id)
)
```

Interrogazione:
```sql
select e.titolo,u.cognome
from eventi as e
join utenti as u
    on e.organizzatore=u.utente_id;
```


## Molti a molti (many-to-many)
È il caso in cui una riga di una tabella può riferirsi a più righe di un'altra tabella e viceversa. 

Pensiamo ad esempio al caso dei partecipanti ad un evento. Ogni evento può avere più eventi partecipanti, ed ogni utente può partecipare a più eventi.

Non esiste in SQL un modo semplice di esprimere questa relazione. Per sua natura infatti, ogni colonna può avere solo un valore, non è possibile mettere una lista di valori all'interno della colonna.

> In teoria si potrebbe avere una colonna `varchar` con all'interno più valori, ad esempio più numeri di telefono separati da virgola. Questa sarebbe una convenzione personale dello sviluppatore, non qualcosa di gestito nativamente dal database, ed è fortemente sconsigliato. In ogni caso, quando un database non ha effettivamente colonne con più valori, si dice che è in _prima forma normale_.

Per rappresentare una relazione molti a molti dobbiamo necessariamente usare una nuova tabella, che conterrà solo chiavi esterne che fanno riferimento alle tabelle che devono essere associate. Questa tabella prende il nome di _tabella associativa_ (junction table).

```sql
create table utenti (
    utente_id int primary key auto_increment,
    nome varchar(100),
    cognome varchar(100),
);
create table eventi (
    evento_id int primary key auto_increment,
    titolo varchar(100),
);
create table partecipanti (
    evento_id int,
    utente_id int,
    foreign key(evento_id) references eventi(evento_id),
    foreign key(utente_id) references utenti(utente_id),
);
```

A questo punto, per poter fare un'interrogazione, dovrò mettere due `join` concatenate:
```sql
select e.titolo,
        u.nome as nome_partecipante,
        u.cognome as cognome_partecipanti
from partecipanti as p
join eventi as e
    using(evento_id)
join utenti as u
    using (utente_id);
```
# Cheat Sheet

## Tipi dati

| Tipo | Limiti | Byte |
|-|:-:|:-:| 
| __char(__*n_caratteri*__)__ | __0__ ≤ *n_caratteri* ≤ __255__ | __1-255__ |
| __varchar(__*n_caratteri*__)__ | __0__ ≤ *n_caratteri* ≤ __255__ | __1-255__ |
| __tinyint__ | __-128__ ≤ *valore* ≤ __127__ | __1__ | 
| __int__ | __-2·10⁹__ ≤ *valore* ≤ __2·10⁹__ | __4__ | 
| __bigint__ | __-2·10⁶³__ ≤ *valore* ≤ __2·10⁶³__ | __8__ | 

## Nota sulle lettere maiuscole e minuscole
Il linguaggio SQL non fa distinzione tra maiuscole e minuscole. Questo ha portato a diversi stili di scrittura dei comandi, tutti sintatticamente validi. 

Chi usa le lettere maiuscole ritiene che sia più chiaro e facile distinguere le keyword dal resto dei comandi.

Chi usa le lettere minuscole lo ritiene più in linea con la sintassi degli attuali linguaggi di programmazione, considerando che spesso si usano degli editor che si occupano di evidenziare le parole chiavi.

Personalmente preferisco usare le lettere minuscole, ma se usate le maiuscole va bene lo stesso. L'importante è che presa una scelta, siate coerenti con la scelta fatta (almeno all'interno della stessa query!!).

## Convenzioni sui nomi
Seguiamo le seguenti convenzioni:
- per i nomi delle tabelle, usiamo il plurale (es. `utenti`)
- se possibile, per le tabelle usare un nome collettivo (es. `personale` invece di `dipendenti`)
- per i nomi delle colonne, usiamo il singolare (es. `nome`)
- per le chiavi primarie, usiamo il nome della tabella al singolare seguito da `_id` (es. `utente_id`)


## Data Definition Language (DDL)
Il Data Definition Language (DDL) è la parte del linguaggio SQL che si occupa di creare, modificare o eliminare elementi nella _schema logico_ del database. In altre parole, contiene i comandi per creare o modificare databases e tabelle. Le parole chiave usate nel DDL sono:
- __create__ per creare elementi
- __alter__ per modificare elementi
- __drop__ per eliminare elementi

###
**show databases;**<br>
*Elenca tutti i database del DBMS*

<details closed> 
<summary>Esempi</summary>

```sql
show databases;
```
</details>


###
**show tables;**<br>
*Elenca tutte le tabelle nel database*
<details closed> 
<summary>Esempi</summary>

```sql
show tables;
```
</details>

###
**use** _nome_database_**;**<br>
*Seleziona un database*
<details closed> 
<summary>Esempi</summary>

```sql
use calendario;
```
```sql
use bar;
```
</details>



### CREATE
**create table** *nome_tabella* __(__*nome_colonna* *tipo* __,__ *nome_colonna2* *tipo*__);__<br>
*Crea una tabella all'interno del database*
<details closed> 
<summary>Esempi</summary>

```sql
create table eventi (titolo varchar(255), data int);
```
```sql
create table studenti (nome varchar(100), cognome varchar(100), eta int unsigned);
```
</details>

###
**primary key**<br>
*Indica una o più colonne che identificano in modo univoco una riga. In italiano: chiave primaria.*
<details closed> 
<summary>Esempi</summary>

```sql
create table cittadini (codice_fiscale char(16) primary key, nome varchar(255));
```
```sql
create table utenti (username varchar(50) primary key, password varchar(255));
```
```sql
create table telefoni (modello char(10) primary key, disponibilita int);
```
</details>

###
**auto_increment**<br>
*Incrementa il valore di una colonna ogni volta che viene aggiunta una riga*
<details closed> 
<summary>Esempi</summary>

```sql
create table prodotti (id int primary key auto_increment, nome varchar(255));
```
</details>


###
**foreign key** <br>
*Crea un riferimento ad una chiave primaria di un'altra tabella. In italiano: chiave esterna.*

Spesso le tabelle hanno dei riferimenti le une con le altre. Pensiamo ad esempio alle tabelle "eventi" e "utenti". Ogni evento ha un organizzatore (uno solo), quindi vorremmo poter inserire questa informazione nel nostro database. Per fare questa operazione abbiamo bisogno di una chiave esterna.

<details closed> 
<summary>Esempi</summary>

```sql
create table eventi (
    titolo varchar(100),
    evento_id int auto_increment,
    organizzatore int,
    foreign key (organizzatore) references utenti(utente_id)
);
```
Nel momento in cui si inserisce un nuovo evento, il DBMS controlla che l'organizzatore sia un utente esistente; in caso contrario rifiuta l'inserimento.
</details>

### DROP
**DROP TABLE** *nome_tabella*__;__<br>
*Elimina una tabella dal database*
<details closed> 
<summary>Esempi</summary>

```sql
drop table prodotti;
```
```sql
drop table utenti;
```
```sql
drop table studenti;
```
</details>



### ALTER
**alter table** *nome_tabella* **rename to** *nuovo_nome_tabella*__;__<br>
*Cambia il nome di una tabella*
<details closed> 
<summary>Esempi</summary>

```sql
alter table utenti rename studenti;
```
```sql
alter table ata rename personale_ata ;
```
</details>
	



### RENAME
**rename table** *nome_tabella* **to** *nuovo_nome_tabella*__,__ *nome_tabella_2* **to** *nuovo_nome* etc...__;__<br>
*Cambia il nome di una o più tabelle (funziona solo in MySQL)*
<details closed> 
<summary>Esempi</summary>

```sql
rename table utenti to professori;
```
```sql
rename table ny_times to pubblicazioni_ny_times, the_guardian to pubblicazioni_the_guardian;
```
</details>
	


## Data Manipulation Language
Il Data Manipulation Language (DML) è la parte del linguaggio SQL che serve per modificare, aggiornare e cancellare il _contenuto_ delle tabelle, senza alternarne però lo schema logico. Si compone prevalentemente di:
- __insert__ per inserire una nuova riga in una tabella
- __update__ per aggiornare una o più colonne di una riga
- __delete__ per cancellare una o più righe

### INSERT
**insert into** *nome_tabella* __(__*nome_colonna*, *nome_colonna2...*__)__ **values** __(__*valore*, *valore2...*__);__<br>
*Inserisce una riga nella tabella*
<details closed> 
<summary>Esempi</summary>

```sql
insert into studenti (nome, cognome) values ('mario', 'rossi');
```
```sql
insert into targhe (targa) values ('ab123cd');
```
```sql
insert into prodotti (nome, costo, disponibilita) values ('acqua', 0.50);
```
</details>



### UPDATE
**update** *nome_tabella* **set** __(__*nome_colonna* = *valore*, *nome_colonna2* = *valore*, *...*__)__ **where** *condizione*;<br>
*modifica una riga o più righe nella tabella*
<details closed> 
<summary>esempi</summary>

```sql
update studenti set nome='claudio' where cognome='rossi';
```
</details>

### DELETE
**delete from** *nome_tabella* **where** *condizione*;<br>
*elimina una o più righe nella tabella*
<details closed> 
<summary>esempi</summary>

```sql
delete from studenti where cognome='rossi';
```
</details>


## Data Query Language
Il Data Query Language (DQL) è la parte del linguaggio SQL che serve per interrogare il database. Si compone essenzialmente del comando __select__ con tutte le sue diverse forme e clausole.

### SELECT
**select** *nome_colonna*, *nome_colonna2...* **from** *nome_tabella*__;__<br>
*Seleziona (filtrando) dati da una tabella*
<details closed> 
<summary>Esempi</summary>

```sql
select nome, cognome from dipendenti;
```
```sql
select costo from merendine;
```
```sql
select * from video -- "*" significa "tutte le colonne";
```
L'asterisco (_star_ in inglese) è da usare esclusivamente in fase di debug o nei rari casi in cui serva effettivamente avere tutte le colonne per eseguire qualche tipo di indagine. Nella pratica, in un'applicazione bisogna sempre selezionare le colonne che poi effettivamente saranno usate nel resto del codice, per aumentare le prestazioni ed evitare errori di vario genere.
</details>

### WHERE
**where** *condizione*__;__<br>
*where introduce una o più condizioni per filtrare le righe*
<details closed> 
<summary>Esempi</summary>

```sql
select nome, cognome from cittadini where regione='lazio';
```
```sql
select nome, indirizzo from hotel where costo < 150.00 and stanze_libere > 2;
```
```sql
select nome, iban from libri where review between 3 and 5;
```
</details>
	
### ORDER BY
**order by** *colonna1,colonna2,...* [asc|desc]__;__<br>
*order by ordina i risultati in base ad una colonna; si possono ordinare i risultati in ordine crescente (`asc`, default) o decrescente (`desc`). si possono specificare più colonne in sequenza, in questo caso ordinerà prima per la colonna1, poi per la colonna2, etc.

<details closed> 
<summary>Esempi</summary>

```sql
select nome, cognome
from cittadini
order by cognome;
```
```sql
select nome, cognome
from cittadini
order by cognome,nome,età desc;
```
</details>

### JOIN
Finora abbiamo trattato interrogazioni con una sola tabella. Molto spesso, tuttavia, serve fare interrogazioni su più tabelle contemporaneamente. Riprendiamo l'esempio della tabella `eventi` e la tabella `utenti`, e che ogni evento abbia esattamente un organizzatore. 

Per fare interrogazioni su più tabelle, si usa la clausola **join**.

Vediamo come si crea un'interrogazione con la join. Si comincia sempre con il comando **select**. Dopo aver specificato come al solito le colonne che vogliamo selezionare, usiamo:
1. la clausola **from** con **la tabella che contiene la chiave esterna**
2. quindi aggiungiamo la clausola **join** con **la tabella a cui fa riferimento la chiave esterna**
3. aggiungiamo infine la keyword **on** con la condizione sulle chiavi che si vogliono unire

Quando usiamo colonne da più tabelle, è bene specificare sempre anche la tabella quando richiamiamo una colonna, usando la notazione punto, ad esempio `eventi.organizzatore`.

> Se non ci sono conflitti tra i nomi delle colonne, non sarebbe necessario specificare la tabella; tuttavia è una buona pratica diffusa e consolidata specificare sempre la tabella.

> Tecnicamente, si può partire da una qualsiasi tabella, non solo quella con le chiavi esterne. Però per convenzione partiamo da quella, in modo da darci un'ordine mentale.

> Se e solo se la colonna con la chiave esterna ha lo stesso nome della colonna con la chiave primaria, posso usare la clausola `using` anziché `on`. Questo è particolarmente utile nelle tabelle associative, che vedremo in seguito.

<details closed> 
<summary>Esempi</summary>

```sql
select eventi.titolo, utenti.nome, utenti.cognome
from eventi
join utenti on eventi.organizzatore=utenti.utente_id;
```

</details>

La clausola `join` può essere usata insieme alle clausole `where` o `order by` per filtrare ed organizzare ulteriormente i risultati.

<details closed> 
<summary>Esempi</summary>

```sql
select eventi.titolo, eventi.costo, utenti.nome, utenti.cognome
from eventi
join utenti on eventi.organizzatore=utenti.utente_id
where eventi.costo > 0
order by utenti.cognome asc;
```
</details>

### AS
Come si può intuire dalle ultime query, le richieste complesse possono diventare anche molto lunghe. Per questo motivo è possibile abbreviare i nomi delle tabelle o delle colonne con il comando `as`.

Attenzione ad alcune cose in particolare:
- a volte l'alias viene utilizzato prima di essere definito, questo può sembrare contro-intuitivo ma è il comportamento normale
- per convenzione, l'alias delle tabelle è il primo carattere della tabella; se ci dovessero essere più tabelle che iniziano con lo stesso nome, si possono usare le prime due lettere oppure un numero incrementale (es. `s1`,`s2`, etc.)

<details closed> 
<summary>Esempi</summary>

```sql
-- comando as per rinominare le tabelle
select e.titolo, e.costo, u.nome, u.cognome
from eventi as e 
join utenti as u on e.organizzatore=u.utente_id
where e.costo > 0 
order by u.cognome asc;
```

```sql
-- comando as per rinominare le colonne
-- in questo caso la tabella risultante avrà nelle colonne i nuovi nomi degli alias
select e.titolo as titolo_evento,
    u.nome as nome_organizzatore,
    u.cognome as cognome_organizzatore
from eventi as e 
join utenti as u on e.organizzatore=u.utente_id
where e.costo > 0 
order by u.cognome asc;
```
</details> 

# Drop table if exists
In fase di sviluppo, può essere utile fare il drop delle tabelle e ricrearle da capo, invece di modificarle. Se si fa il drop di una tabella che non esiste, però, SQL ci ritorna un errore; questo è particolarmente fastidioso quando scriviamo uno script. Per evitare questo problema esiste il drop condizionato all'esistenza effettiva della tabella.

<detail closed>
```sql
drop table if exists utenti;
```
</detail>

### On delete
Cosa succede se cancelliamo una riga che è un riferimento in un'altra tabella? Consideriamo ad esempio che ho diversi eventi organizzati da Mario Rossi. Ad un certo punto, cancello l'utente Mario Rossi. Cosa succede a tutti gli eventi organizzati da lui?

Esistono varie strategie, essenzialmente:
- se la chiave esterna è facoltativa, si può sostituire con NULL
- cancello la riga con la chiave esterna

<detail closed>

```sql
create table eventi (
    -- ...
    -- se viene cancellato l'organizzatore, nell'evento viene impostato a NULL
    foreign key(organizzatore) references utenti(utente_id) ON DELETE SET NULL
```

```sql
create table eventi (
    -- ...
    -- se viene cancellato l'organizzatore, viene cancellato anche l'evento
    foreign key(organizzatore) references utenti(utente_id) ON DELETE CASCADE
```

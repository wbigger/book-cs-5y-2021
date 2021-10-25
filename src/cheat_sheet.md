# Cheat Sheet

## Tipi dati

| Tipo | Limiti | Byte |
|-|:-:|:-:| 
| __CHAR(__*n_caratteri*__)__ | __0__ ≤ *n_caratteri* ≤ __255__ | __1-255__ |
| __VARCHAR(__*n_caratteri*__)__ | __0__ ≤ *n_caratteri* ≤ __255__ | __1-255__ |
| __TINYINT__ | __-128__ ≤ *valore* ≤ __127__ | __1__ | 
| __INT__ | __-2·10⁹__ ≤ *valore* ≤ __2·10⁹__ | __4__ | 
| __BIGINT__ | __-2·10⁶³__ ≤ *valore* ≤ __2·10⁶³__ | __8__ | 

## Nota sulle lettere maiuscole e minuscole
Il linguaggio SQL non fa distinzione tra maiuscole e minuscole. Questo ha portato a diversi stili di scrittura dei comandi, tutti sintatticamente validi. 

Chi usa le lettere maiuscole ritiene che sia più chiaro e facile distinguere le keyword dal resto dei comandi.

Chi usa le lettere minuscole lo ritiene più in linea con la sintassi degli attuali linguaggi di programmazione, considerando che spesso si usano degli editor che si occupano di evidenziare le parole chiavi.

Personalmente preferisco usare le lettere minuscole, ma se usate le maiuscole va bene lo stesso. L'importante è che presa una scelta, siate coerenti con la scelta fatta (almeno all'interno della stessa query!!).


## Data Definition Language (DDL)
Il Data Definition Language (DDL) è la parte del linguaggio SQL che si occupa di creare, modificare o eliminare elementi nella _schema logico_ del database. In altre parole, contiene i comandi per creare o modificare databases e tabelle. Le parole chiave usate nel DDL sono:
- __CREATE__ per creare elementi
- __ALTER__ per modificare elementi
- __DROP__ per eliminare elementi


###
**SHOW DATABASES;**<br>
*Elenca tutti i database del DBMS*

<details closed> 
<summary>Esempi</summary>

```sql
SHOW DATABASES;
```
</details>


###
**SHOW TABLES;**<br>
*Elenca tutte le tabelle nel database*
<details closed> 
<summary>Esempi</summary>

```sql
SHOW TABLES;
```
</details>

###
**USE** _nome_database_**;**<br>
*Seleziona un database*
<details closed> 
<summary>Esempi</summary>

```sql
USE calendario;
```
```sql
USE bar;
```
</details>



###
**CREATE TABLE** *nome_tabella* __(__*nome_colonna* *tipo* __,__ *nome_colonna2* *tipo*__);__<br>
*Crea una tabella all'interno del database*
<details closed> 
<summary>Esempi</summary>

```sql
CREATE TABLE eventi (titolo varchar(255), data int);
```
```sql
CREATE TABLE studenti (nome varchar(100), cognome varchar(100), eta int unsigned);
```
</details>

###
**PRIMARY KEY**<br>
*Indica una o più colonne che identificano in modo univoco una riga*
<details closed> 
<summary>Esempi</summary>

```sql
CREATE TABLE cittadini (codicefiscale char(16) PRIMARY KEY, nome varchar(255));
```
```sql
CREATE TABLE utenti (username varchar(50) PRIMARY KEY, password varchar(255));
```
```sql
CREATE TABLE telefoni (modello char(10) PRIMARY KEY, disponibilita int);
```
</details>




###
**AUTO_INCREMENT**<br>
*Incrementa il valore di una colonna ogni volta che viene aggiunta una riga*
<details closed> 
<summary>Esempi</summary>

```sql
CREATE TABLE prodotti (id int PRIMARY KEY AUTO_INCREMENT, nome varchar(255));
```
</details>




###
**DROP TABLE** *nome_tabella*__;__<br>
*Elimina una tabella dal database*
<details closed> 
<summary>Esempi</summary>

```sql
DROP TABLE prodotti;
```
```sql
DROP TABLE utenti;
```
```sql
DROP TABLE studenti;
```
</details>



###
**ALTER TABLE** *nome_tabella* **RENAME TO** *nuovo_nome_tabella*__;__<br>
*Cambia il nome di una tabella*
<details closed> 
<summary>Esempi</summary>

```sql
ALTER TABLE utenti RENAME studenti;
```
```sql
ALTER TABLE ata RENAME personale_ata ;
```
</details>
	



###
**RENAME TABLE** *nome_tabella* **TO** *nuovo_nome_tabella*__,__ *nome_tabella_2* **TO** *nuovo_nome* etc...__;__<br>
*Cambia il nome di una o più tabelle (funziona solo in MySQL)*
<details closed> 
<summary>Esempi</summary>

```sql
RENAME TABLE utenti TO professori;
```
```sql
RENAME TABLE ny_times TO pubblicazioni_ny_times, the_guardian TO pubblicazioni_the_guardian;
```
</details>
	


## Data Manipulation Language
Il Data Manipulation Language (DML) è la parte del linguaggio SQL che serve per modificare, aggiornare e cancellare il _contenuto_ delle tabelle, senza alternarne però lo schema logico. Si compone prevalentemente di:
- __INSERT__ per inserire una nuova riga in una tabella
- __UPDATE__ per aggiornare una o più colonne di una riga
- __DELETE__ per cancellare una o più righe

###
**INSERT INTO** *nome_tabella* __(__*nome_colonna*, *nome_colonna2...*__)__ **VALUES** __(__*valore*, *valore2...*__);__<br>
*Inserisce una riga nella tabella*
<details closed> 
<summary>Esempi</summary>

```sql
INSERT INTO studenti (nome, cognome) VALUES ('Mario', 'Rossi');
```
```sql
INSERT INTO targhe (targa) VALUES ('AB123CD');
```
```sql
INSERT INTO prodotti (nome, costo, disponibilita) VALUES ('Acqua', 0.50);
```
</details>



###
**UPDATE** *nome_tabella* **SET** __(__*nome_colonna* = *valore*, *nome_colonna2* = *valore*, *...*__)__ **WHERE** *condizione*;<br>
*Modifica una riga o più righe nella tabella*
<details closed> 
<summary>Esempi</summary>

```sql
UPDATE studenti SET (nome='Claudio') WHERE cognome='Rossi';
```
</details>

###
**DELETE** FROM *nome_tabella* **WHERE** *condizione*;<br>
*Elimina una o più righe nella tabella*
<details closed> 
<summary>Esempi</summary>

```sql
DELETE FROM studenti WHERE cognome='Rossi';
```
</details>


## Data Query Language
Il Data Query Language (DQL) è la parte del linguaggio SQL che serve per interrogare il database. Si compone essenzialmente del comando __SELECT__ con tutte le sue diverse forme e clausole.

###
**SELECT** *nome_colonna*, *nome_colonna2...* **FROM** *nome_tabella*__;__<br>
*Seleziona (filtrando) dati da una tabella*
<details closed> 
<summary>Esempi</summary>

```sql
SELECT nome, cognome FROM dipendenti;
```
```sql
SELECT costo FROM merendine;
```
```sql
SELECT * FROM video -- "*" significa "tutte le colonne";
```
L'asterisco (_star_ in inglese) è da usare esclusivamente in fase di debug o nei rari casi in cui serva effettivamente avere tutte le colonne per eseguire qualche tipo di indagine. Nella pratica, in un'applicazione bisogna sempre selezionare le colonne che poi effettivamente saranno usate nel resto del codice, per aumentare le prestazioni ed evitare errori di vario genere.
</details>

###
**WHERE** *condizione*__;__<br>
*WHERE introduce una o più condizioni per filtrare le righe*
<details closed> 
<summary>Esempi</summary>

```sql
SELECT nome, cognome FROM cittadini WHERE regione='Lazio';
```
```sql
SELECT nome, indirizzo FROM hotel WHERE costo < 150.00 AND stanze_libere > 2;
```
```sql
SELECT nome, iban FROM libri WHERE review BETWEEN 3 AND 5;
```
</details>
	

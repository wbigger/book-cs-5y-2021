# Cheat Sheet

## Tipi dati

| Tipo | Limiti | Byte |
|-|:-:|:-:| 
| __CHAR(__*n_caratteri*__)__ | __0__ ≤ *n_caratteri* ≤ __255__ | __1-255__ |
| __VARCHAR(__*n_caratteri*__)__ | __0__ ≤ *n_caratteri* ≤ __255__ | __1-255__ |
| __TINYINT__ | __-128__ ≤ *valore* ≤ __127__ | __1__ | 
| __INT__ | __-2·10⁹__ ≤ *valore* ≤ __2·10⁹__ | __4__ | 
| __BIGINT__ | __-2·10⁶³__ ≤ *valore* ≤ __2·10⁶³__ | __8__ | 

## Query

<br>
<span class="font-md">

**SHOW DATABASES;**

</span>

<span class="description">

*Elenca tutti i database del DBMS*

</span>

<details closed> 
<summary>Esempi</summary>

```sql
SHOW DATABASES;
```
</details>
<br>
<br>


<span class="font-md">

**SHOW TABLES**__;__

</span>

<span class="description">

*Elenca tutte le tabelle nel database*

</span>

<details closed> 
<summary>Esempi</summary>

```sql
SHOW TABLES;
```
</details>
<br>
<br>


<span class="font-md">

**USE** *nome_database*__;__

</span>

<span class="description">

*Seleziona un database*

</span>

<details closed> 
<summary>Esempi</summary>

```sql
USE calendario;
```
```sql
USE bar;
```
</details>
<br>
<br>


<span class="font-md">

**CREATE TABLE** *nome_tabella* __(__*nome_colonna* *tipo* __,__ *nome_colonna2* *tipo*__);__

</span>

<span class="description">

*Crea una tabella all'interno del database*

</span>

<details closed> 
<summary>Esempi</summary>

```sql
CREATE TABLE eventi (titolo varchar(255), data int);
```
```sql
CREATE TABLE studenti (nome varchar(100), cognome varchar(100), eta int unsigned);
```

</details>
<br>
<br>


<span class="font-md">

**PRIMARY KEY**

</span>

<span class="description">

*Indica una o più colonne che identificano in modo univoco una riga*

</span>

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
<br>
<br>



<span class="font-md">

**AUTO_INCREMENT**

</span>

<span class="description">

*Incrementa il valore di una colonna ogni volta che viene aggiunta una riga*

</span>

<details closed> 
<summary>Esempi</summary>

```sql
CREATE TABLE prodotti (id int PRIMARY KEY AUTO_INCREMENT, nome varchar(255));
```
</details>
<br>
<br>


<span class="font-md">

**DROP TABLE** *nome_tabella*__;__

</span>

<span class="description">

*Elimina una tabella dal database*

</span>

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
<br>
<br>


<span class="font-md">

**INSERT INTO** *nome_tabella* __(__*nome_colonna*, *nome_colonna2...*__)__ **VALUES** __(__*valore*, *valore2...*__);__

</span>

<span class="description">

*Inserisce una entry (riga) nella tabella*

</span>

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
<br>
<br>


<span class="font-md">

**SELECT** *nome_colonna*, *nome_colonna2...* **FROM** *nome_tabella*__;__

</span>

<span class="description">

*Seleziona (filtrando) dati da una tabella*

</span>

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
</details>
<br>
<br>


<span class="font-md">

**WHERE** *condizione*__;__

</span>

<span class="description">

*WHERE introduce una o più condizioni per filtrare le entry*

</span>

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
<br>	
<br>
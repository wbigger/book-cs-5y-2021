# Cheat Sheet

## Tipi dati

| Tipo | Limiti | Byte |
||::|::| 
| __CHAR(__*n_caratteri*__)__ | __0__ ≤ *n_caratteri* ≤ __255__ | __1-255__ |
| __VARCHAR(__*n_caratteri*__)__ | __0__ ≤ *n_caratteri* ≤ __255__ | __1-255__ |
| __TINYINT__ | __-128__ ≤ *valore* ≤ __127__ | __1__ | 
| __INT__ | __-2·10⁹__ ≤ *valore* ≤ __2·10⁹__ | __4__ | 
| __BIGINT__ | __-2·10⁶³__ ≤ *valore* ≤ __2·10⁶³__ | __8__ | 

## Comandi
<hr>
<span class="font-md">

**SHOW DATABASES;**

</span>

Elenca tutti i database del **DBMS**
<details closed> 
<summary>Esempi</summary>

```sql
SHOW DATABASES;
```
</details>
<hr>


<span class="font-md">

**SHOW TABLES**__;__

</span>

Elenca tutte le tabelle nel database
<details closed> 
<summary>Esempi</summary>

```sql
SHOW TABLES;
```
</details>
<hr>


<span class="font-md">

**USE** *nome_database*__;__

</span>

Seleziona un database
<details closed> 
<summary>Esempi</summary>

```sql
USE calendario;
```
```sql
USE bar;
```
</details>
<hr>


<span class="font-md">

**CREATE TABLE** *nome_tabella* __(__*nome_colonna* *tipo*__,__ *nome_colonna2* *tipo*__);__

</span>

Crea una tabella all'interno del database
<details closed> 
<summary>Esempi</summary>

```sql
CREATE TABLE eventi (titolo varchar(255), data int);
```
```sql
CREATE TABLE studenti (nome varchar(100), cognome varchar(100), eta int unsigned);
```
</details>
<hr>


<span class="font-md">

**DROP TABLE** *nome_tabella*__;__

</span>

Elimina una tabella dal database
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
<hr>
# Raccolta dei requisiti

La creazione e manutenzione di un database è qualcosa di molto complesso (soprattutto per i DB relazionali come SQL), quindi conviene bisogna fare un'attenta progettazione iniziale per ridurre al minimo le modifiche in fase esecutiva.

## Colloquio con il committente (customer)

Per cominciare a progettare il database, bisogna raccogliere prima di tutto i requisiti dagli _stakeholder_. Gli stakeholder sono "chiunque c'entri" con il progetto, quindi il committente, gli utenti finali, eventuali sistemisti, norme e regolamenti, etc.

Nel nostro caso, per semplicità, consideriamo solo il colloquio con il committente, che dal nostro punto di vista possiamo anche chiamare _cliente_.

> Nell'agile/scrum, il colloquio è un compito che svolge il Product Owner.

Durante il colloquio, dovrete cercare di raccogliere informazioni a riguardo:
- cosa ci si aspetti che faccia il servizio, in poche parole
- chi saranno gli utilizzatori del servizio (amministratori, impiegati, utenti finali, etc.)
- quanti sono gli utenti attesi che usufruiranno del servizio, per ogni tipologia (10 utenti finali al giorno? 100? 1000? quanti impiegati?)
- quali operazioni deve svolgere ogni tipologia utente
- quante volte ogni tipologia di utente svolge una certa operazione (es. accesso al sito, prenotazione, like su un elemento, etc.)

Diamo inoltre i seguenti suggerimenti:
- lasciate parlare liberamente il vostro interlocutore, non interrompetelo troppo di frequente
- se l'interlocutore sta evidentemente divagando, riportatelo sul progetto cone delle domande su argomenti specifici di interesse
- non fate domande troppo tecniche, siete voi che dovete saper gestire i dettagli implementativi, non lui
- non esitate a chiedere il perché di una certa affermazione, anche se a volte la risposta può sembrare scontata, a volte non lo è

Alcuni consigli su come scrivere gli appunti:
- usate sempre un verbo e non solo sostantivi negli appunti

```txt
lista prenotazioni --> controllare lista prenotazioni
```

- cercate sempre di mettere il soggetto al verbo, soprattutto se non è ovvio

```txt
controllare lista prenotazioni --> l'amministratore deve poter controllare la lista prenotazioni
```

- quando possibile cercate di mettere il perché di un certo appunto

```txt
l'amministratore deve poter controllare la lista prenotazioni --> l'amministratore deve poter controllare la lista prenotazioni per fare rendicontazione giornaliera
```

In generale, cercate di prendere appunti in forma discorsiva, non come semplice elenco puntato.

Soprattutto se il colloquio è in presenza, si consiglia inoltre di prendere appunti su un foglio di carta, per mettere a maggior agio l'interlocutore, fare disegni e diagrammi, sottolineare o aggiungere note facilmente ad appunti già presi.

## Analisi degli appunti
Una volta raccolti gli appunti, si passa all'analisi.

Anche in questo caso, vediamo un metodo semplice per analizzare i dati
- cerchiare le parole (o metterle in grassetto se il file è digitale)
- sottolineare i verbi
- se necessario, farsi un dizionarietto con gli eventuali sinonimi. Ad esempio, il committente potrebbe aver parlato di "cliente", "ragazzo", "compratore" riferendosi alla stessa tipologia di utente.









# Spreadsheets cheatsheet

Ho usato una espressione regolare per rimuovere tutto, 
`=REGEXREPLACE(A1; ".+(?:<)([a-zA-Z]+)\.([a-zA-Z]+)([0-9])?\@sns.it>,"; "$1\.$2$3@sns.it")`
e ho usato il sito [regex101](https://regex101.com) per realizzarla.

`=IF(ISNA(VLOOKUP(A2;'Risposte del modulo 1'!$B$2:$B$64;1;FALSE));"NO";"sì")`
questa invece l'ho usata per dire: c'è un'occorrenza e allora stampa "sì" oppure "NO".
Inoltre ho che se uso il simbolo del dollaro come in `$B$4`, la casella `B4` della formula non cambia con la compilazione automatica di sheets ma cambiano le altre cose; invece `A2` cambia con la casella.

`=COUNTIFS(intervallo condizione; criterio; [intervallo2; criterio;...])`
Per dirgli che vuoi che la casella sia diversa da qualcosa, devi usare `"<>string"` o `"<>"&cell`.
Ricordati che gli intervalli per le condizioni devono avere la stessa dimensione.

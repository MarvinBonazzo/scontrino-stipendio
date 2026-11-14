# Wrapped dello stipendio: istruzioni per Claude Code

Versione "a storie" (stile Spotify Wrapped) dello Scontrino delle tasse, pensata per ragazzi delle medie e superiori.
È il gemello del "Wrapped dello Stato" (Scontrino pubblico): stesso stile, stessi colori, stessa navigazione.

## File
- `index.html`: pagina unica e autosufficiente (HTML + CSS + JS inline). Unica risorsa esterna: Google Fonts (Archivo, Space Mono).

## Come funziona
- Prima schermata: si sceglie un lavoro (Barista 1.400 €, Infermiera 2.000 €, Programmatrice 3.000 € lordi al mese) oppure si scrive il proprio lordo mensile.
- `build(nome, lordo)` calcola tutto e riempie le schermate. Poi si va avanti toccando a destra e indietro toccando a sinistra.
- I personaggi sono nell'array `WHO`. Sono esempi, non medie statistiche: se li cambi, lascia la nota "Stipendi di esempio".

## Calcolo (non modificarlo senza motivo)
La funzione `calc()` e le sue funzioni di supporto (`detrazioneLavoro`, `irpefLorda`) sono copiate identiche da `../index.html` (lo Scontrino delle tasse).
Se cambiano le regole fiscali, aggiorna prima lo Scontrino delle tasse e poi ricopia qui le stesse funzioni.
- Regole 2026 per un dipendente: contributi azienda 30% (media), INPS 9,19%, IRPEF 23/33/43% con scaglioni 28.000 e 50.000 €, detrazioni, taglio del cuneo, trattamento integrativo.
- 13 mensilità (`MENS`).
- Cifre mensili arrotondate come nell'originale, così somme e differenze tornano all'euro.

## Schermate e dati
| Schermata | Dato |
| --- | --- |
| Costo per l'azienda | lordo + contributi azienda + TFR |
| Netto e "fette di pizza" | netto ÷ costo × 10 |
| Dove va la pizza | netto, contributi azienda, contributi tuoi, IRPEF, TFR |
| INPS | contributi azienda + tuoi; spiega che pagano le pensioni di oggi |
| Scalini IRPEF | evidenzia lo scaglione del reddito imponibile |
| IRPEF al mese | IRPEF meno taglio del cuneo |
| Dove vanno i soldi del suo lavoro | contributi azienda + tuoi + IRPEF (`d.pub`), divisi secondo la spesa pubblica 2024 (Eurostat COFOG, milioni di euro, array `COFOG`: le stesse 13 voci e gli stessi nomi del Wrapped dello Stato, stessi numeri di `SPESA` in `../index.html`). Euro interi che sommano esattamente `d.pub` |
| Perché anche i contributi | contributi 2024 (278 mld) contro pensioni 2024 (360 mld) |
| Lo Stato spende più di quanto incassa | `d.extra` = `d.pub` × (spesa ÷ entrate 2024 − 1); debito 50.343 € a testa (Banca d'Italia, fine 2024 ÷ residenti ISTAT) |
| Giorno di "liberazione" | (contributi azienda + tuoi + IRPEF) ÷ costo × 365, contato dal 1° gennaio |
| Le tasse che non si vedono | IVA 6,75 € e accise 4,60 € al giorno per residente (stesse cifre del Wrapped dello Stato), addizionali solo spiegate |
| Scontrino finale | busta paga riga per riga + dove finiscono contributi e IRPEF + parte presa in prestito; link al Wrapped dello Stato |

## Parole spiegate (glossario)
Ogni parola tecnica (IRPEF, TFR, INPS, lordo, netto, detrazioni…) si può toccare e apre un cartoncino in basso con la spiegazione.
- Le spiegazioni sono nell'oggetto `GLOSS` (chiave → [titolo, testo]): una o due frasi, senza altre parole difficili dentro.
- Nel markup: `<u data-w="chiave">parola</u>`. Nelle frasi create in JS: `W("chiave","parola")`.
- `prep()` rende le parole toccabili anche da tastiera (Invio). Va richiamata dopo aver creato nuovo testo (già fatto in `build`).
- Se aggiungi una parola tecnica nuova, aggiungi anche la sua voce in `GLOSS`.

## Regole di testo
- Si dà sempre del tu, con rispetto: anche quando si sceglie un lavoro di esempio, chi legge è "tu" ("il tuo netto", "paghi").
- Diretto, senza addolcire: "Pensioni" e "anziani", non "nonni"; "Sussidi e assistenza", non "aiuti a chi ha bisogno". I nomi delle 13 voci sono gli stessi del Wrapped dello Stato.
- Linguaggio per un ragazzo di 12-14 anni, con una metafora o un esempio pratico per ogni concetto.
- Nessuna sigla o parola tecnica senza spiegazione: o si spiega nella frase, o si rende toccabile con il glossario.
- Solo informazioni utili, niente curiosità fini a sé stesse. Tono neutro, nessun giudizio politico.
- Dire sempre cosa semplifica: niente addizionali regionali e comunali, nessun familiare a carico, contributi azienda come media.

## Cose da sistemare
- Pulsante per esportare lo scontrino finale come immagine da condividere.

## Fine della storia
Sotto lo scontrino finale: "Prova un altro lavoro", poi i link alle due pagine complete ("Scontrino dello stipendio", "Scontrino dello Stato") e il bottone "Fonti, calcoli e numeri interi". Il pannello `#info` si riempie in `build()`: il conto di un anno per lo stipendio scelto (ogni valore arrotondato una volta sola, così le somme tornano), le regole fiscali usate, la spesa pubblica 2024 in euro interi, le formule e i link alle fonti. Se cambi le regole in `calc()`, aggiorna anche il testo delle regole nel pannello.

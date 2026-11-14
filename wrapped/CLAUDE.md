# Wrapped dello stipendio: istruzioni per Claude Code

Versione "a storie" (stile Spotify Wrapped) dello Scontrino delle tasse, pensata per ragazzi delle medie e superiori.
È il gemello del "Wrapped dello Stato" (Scontrino pubblico): stesso stile, stessi colori, stessa navigazione.

## File
- `index.html`: pagina unica e autosufficiente (HTML + CSS + JS inline). Unica risorsa esterna: Google Fonts (Archivo, Space Mono).

## Come funziona
- Prima schermata: si sceglie un personaggio (Barista 1.400 €, Infermiera 2.000 €, Programmatrice 3.000 € lordi al mese) oppure si scrive il proprio lordo mensile.
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
| Dove va l'IRPEF | IRPEF divisa secondo la spesa pubblica 2024 (Eurostat COFOG, punti di PIL, array `COFOG`) |
| Giorno di "liberazione" | (contributi azienda + tuoi + IRPEF) ÷ costo × 365, contato dal 1° gennaio |
| Scontrino finale | busta paga riga per riga + dove finisce l'IRPEF |

## Parole spiegate (glossario)
Ogni parola tecnica (IRPEF, TFR, INPS, lordo, netto, detrazioni…) si può toccare e apre un cartoncino in basso con la spiegazione.
- Le spiegazioni sono nell'oggetto `GLOSS` (chiave → [titolo, testo]): una o due frasi, senza altre parole difficili dentro.
- Nel markup: `<u data-w="chiave">parola</u>`. Nelle frasi create in JS: `W("chiave","parola")`.
- `prep()` rende le parole toccabili anche da tastiera (Invio). Va richiamata dopo aver creato nuovo testo (già fatto in `build`).
- Se aggiungi una parola tecnica nuova, aggiungi anche la sua voce in `GLOSS`.

## Regole di testo
- Linguaggio per un ragazzo di 12-14 anni, con una metafora o un esempio pratico per ogni concetto.
- Nessuna sigla o parola tecnica senza spiegazione: o si spiega nella frase, o si rende toccabile con il glossario.
- Solo informazioni utili, niente curiosità fini a sé stesse. Tono neutro, nessun giudizio politico.
- Dire sempre cosa semplifica: niente addizionali regionali e comunali, nessun familiare a carico, contributi azienda come media.

## Cose da sistemare
- Con "Tu" (lordo scritto a mano) i testi restano in terza persona ("il suo lavoro"). Va aggiunta la seconda persona.
- Pulsante per esportare lo scontrino finale come immagine da condividere.
- Collegare i due Wrapped: alla fine di questo, un link al Wrapped dello Stato e viceversa.

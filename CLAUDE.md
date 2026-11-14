# Scontrino dello Stipendio

Il tuo stipendio raccontato a storie, una schermata alla volta, per ragazzi delle medie e delle superiori: quanto costa il tuo lavoro all'azienda, quanto ti arriva, quanto va a INPS e IRPEF e cosa si paga con quei soldi. Finisce con la busta paga stampata come uno scontrino.

Progetto gemello dello **Scontrino dello Stato** (repo `scontrino-pubblico`): stesso stile, stessi colori, stessa navigazione, stessi dati. Questo mostra cosa paghi tu; quello quanti soldi arrivano allo Stato, da dove e come vengono spesi. Si linkano a vicenda.

La parola "Wrapped" non si usa: i due progetti si chiamano Scontrino dello Stipendio e Scontrino dello Stato.

## File
- `index.html`: pagina unica e autosufficiente (HTML + CSS + JS inline). Unica risorsa esterna: Google Fonts (Archivo, Space Mono). Si apre anche con un doppio clic.

## Come funziona
- Prima schermata: si sceglie un lavoro (Barista 1.400 €, Infermiera 2.000 €, Programmatrice 3.000 € lordi al mese) oppure si scrive il proprio lordo mensile.
- `build(nome, lordo)` calcola tutto e riempie le schermate. Poi si va avanti toccando a destra e indietro toccando a sinistra (o con le frecce).
- I lavori di esempio sono nell'array `WHO`. Sono esempi, non medie statistiche: se li cambi, lascia la nota "Stipendi di esempio".

## Calcolo (non modificarlo senza motivo)
`calc()` con `detrazioneLavoro` e `irpefLorda`:
- Regole 2026 per un dipendente: contributi azienda 30% (media), INPS 9,19% + 1% oltre 56.224 €, IRPEF 23/33/43% con scaglioni 28.000 e 50.000 €, detrazione per lavoro dipendente, ulteriore detrazione, taglio del cuneo, trattamento integrativo. TFR = lordo ÷ 13,5.
- 13 mensilità (`MENS`).
- Cifre mensili arrotondate una volta sola, così somme e differenze tornano all'euro.

## Schermate e dati
| Schermata | Dato |
| --- | --- |
| Costo per l'azienda | lordo + contributi azienda + TFR |
| Netto | netto ÷ costo × 10 (le "fette di pizza", solo come esempio) |
| Dove vanno i tuoi soldi | netto, contributi azienda, contributi tuoi, IRPEF, TFR |
| INPS | contributi azienda + tuoi; pagano le pensioni di oggi |
| Scalini IRPEF | evidenzia lo scaglione del reddito imponibile |
| IRPEF al mese | IRPEF meno taglio del cuneo |
| Cosa pagano i tuoi soldi | contributi + IRPEF (`d.pub`), divisi come la spesa pubblica 2024 (Eurostat COFOG, milioni di euro, array `COFOG`). Euro interi che sommano esattamente `d.pub` |
| Perché anche i contributi | contributi 2024 (278 mld) contro pensioni 2024 (360 mld) |
| Lo Stato spende più di quanto incassa | `d.extra` = `d.pub` × (spesa ÷ entrate 2024 − 1); debito 50.343 € a testa |
| Giorno di "liberazione" | (contributi + IRPEF) ÷ costo × 365, contato dal 1° gennaio |
| Le tasse che non si vedono | IVA 6,75 € e accise 4,60 € al giorno per residente, addizionali solo spiegate |
| Scontrino finale | busta paga riga per riga + dove finiscono contributi e IRPEF + parte presa in prestito |

**Stessi numeri dello Scontrino dello Stato**: le 13 voci di `COFOG` (nomi e milioni), `ENTRATE_TOT`, IVA, accise e residenti devono restare uguali all'array `V` e agli altri dati di `scontrino-pubblico/index.html`. Se cambi un dato, cambialo in tutti e due.

## Fine della storia
Sotto lo scontrino finale: "Prova un altro lavoro", poi il link "Scontrino dello Stato" e il bottone "Fonti, calcoli e numeri interi". Il pannello `#info` si riempie in `build()`: il conto di un anno per lo stipendio scelto (ogni valore arrotondato una volta sola), le regole fiscali usate, la spesa pubblica 2024 in euro interi, le formule e i link alle fonti. Se cambi le regole in `calc()`, aggiorna anche il testo delle regole nel pannello.

## Parole spiegate (glossario)
Ogni parola tecnica (IRPEF, TFR, INPS, lordo, netto, detrazioni…) si può toccare e apre un cartoncino in basso con la spiegazione.
- Le spiegazioni sono nell'oggetto `GLOSS` (chiave → [titolo, testo]): una o due frasi, senza altre parole difficili dentro.
- Nel markup: `<u data-w="chiave">parola</u>`. Nelle frasi create in JS: `W("chiave","parola")`.
- `prep()` rende le parole toccabili anche da tastiera. Va richiamata dopo aver creato nuovo testo (già fatto in `build`).

## Regole di testo
- Si dà sempre del tu, con rispetto: anche con un lavoro di esempio, chi legge è "tu" ("il tuo netto", "paghi").
- Diretto, senza addolcire: "Pensioni" e "anziani", non "nonni"; "Sussidi e assistenza", non "aiuti a chi ha bisogno".
- Linguaggio per un ragazzo di 12-14 anni, con una metafora o un esempio pratico per ogni concetto.
- Nessuna sigla o parola tecnica senza spiegazione: o nella frase, o toccabile con il glossario.
- Solo dati ufficiali, nessuna stima. Tono neutro, nessun giudizio politico.
- Dire sempre cosa semplifica: niente addizionali, nessun familiare a carico, contributi azienda come media.

## Come lavorare con Marvin
- Scrivere in italiano, risposte dirette e brevi.
- Spiegare i concetti tecnici con un'analogia e un esempio pratico.
- Le richieste sono spesso brevi: fare esattamente quella modifica, senza riscrivere il resto.
- Se chiede solo una spiegazione, non modificare i file.

## Idee per i prossimi passi
- Pulsante per esportare lo scontrino finale come immagine da condividere.

# Scontrino delle tasse

Scrivi il tuo stipendio lordo e scopri quanto costa davvero il tuo lavoro, quanto va all'INPS, quanto in IRPEF, quanto arriva sul tuo conto e dove finiscono le tue imposte. Mostrato come uno scontrino che si stampa.

### 👉 [Apri lo scontrino](https://marvinbonazzo.github.io/scontrino-stipendio/)

Per ragazzi: **[Il Wrapped del tuo stipendio](https://marvinbonazzo.github.io/scontrino-stipendio/wrapped/)**, lo stesso conto raccontato a storie, una schermata alla volta.

Progetto gemello: **[Scontrino pubblico](https://marvinbonazzo.github.io/scontrino-pubblico/)**, che mostra quanto spende il settore pubblico per ogni residente, in Italia e in ognuno dei circa 7.900 Comuni ([codice](https://github.com/MarvinBonazzo/scontrino-pubblico)).

---

## Cosa fa

1. **Scrivi il lordo mensile** che vedi in busta paga e quante mensilità prendi (13 con la tredicesima, 14 con la quattordicesima).
2. **Lo scontrino si stampa.** Un'animazione mostra i passaggi del calcolo uno alla volta.
3. **Vedi il risultato:**
   - quanto spende l'azienda per te ogni mese, che è più del tuo lordo;
   - una barra "Ogni euro" che divide quel costo tra contributi dell'azienda, TFR, contributi tuoi, IRPEF e netto;
   - **Dove vanno le tue imposte**: la tua IRPEF divisa tra pensioni, sanità, scuola, interessi sul debito e le altre voci, nella stessa proporzione in cui lo Stato ha speso nel 2024;
   - **Voce per voce**: ogni riga si apre e mostra il conto fatto, con i numeri veri.

Un esempio: con 2.000 € lordi al mese, lo scontrino ti mostra quanto in più paga l'azienda sopra quei 2.000 €, quanto ti tolgono INPS e IRPEF, e quanti euro della tua IRPEF vanno alle pensioni o alla sanità.

## Come fa i conti

Il calcolo segue le regole di legge per un lavoratore dipendente nel 2026. Ogni passaggio è scritto in chiaro nella pagina.

| Passaggio | Regola |
| --- | --- |
| Contributi dell'azienda | 30% del lordo, pagati dall'azienda sopra il tuo stipendio |
| TFR | lordo annuo ÷ 13,5, messo da parte ogni anno |
| Contributi tuoi (INPS) | 9,19% del lordo, più l'1% sulla parte sopra 56.224 € l'anno |
| IRPEF 2026 | 23% fino a 28.000 €, 33% da 28.000 a 50.000 €, 43% oltre |
| Detrazioni | detrazione per lavoro dipendente e ulteriore detrazione fino a 1.000 € (tra 20.000 e 40.000 € di reddito) |
| Taglio del cuneo | somma esente da tasse fino a 20.000 € di reddito (7,1%, 5,3% o 4,8% secondo la fascia) |
| Trattamento integrativo | 1.200 € l'anno per i redditi fino a 15.000 €, quando spetta |
| Dove vanno le imposte | IRPEF divisa secondo la spesa pubblica italiana 2024 per funzione (Eurostat, classificazione COFOG) |

Tutto il calcolo avviene nel tuo browser. Lo stipendio che scrivi non viene salvato né mandato a nessuno: la pagina non ha account e non ha statistiche o tracciamento. L'unica cosa che scarica da fuori sono i caratteri, da Google Fonts.

## Perché ti puoi fidare

**Regole pubbliche, non opinioni.** Aliquote, scaglioni, detrazioni e taglio del cuneo sono quelli scritti nella legge di bilancio e nelle regole INPS. L'unico valore medio è il 30% dei contributi dell'azienda, e la pagina lo dice.

**Dati ufficiali per la spesa.** La divisione delle imposte usa i conti pubblici che l'ISTAT manda a **Eurostat**, l'ufficio statistico dell'Unione europea, con le stesse regole per tutti i Paesi UE. È il 2024 perché è l'ultimo anno con la spesa divisa per voce: il 2025 uscirà a inizio 2027.

**Il codice è aperto.** Tutto è in un solo file, [`index.html`](index.html). Puoi leggere ogni formula e rifare i conti con una calcolatrice.

**Ogni numero si spiega.** Nella sezione "Voce per voce" ogni cifra mostra da dove viene: quale percentuale, applicata a quale importo.

## Cosa lo scontrino semplifica

Per restare chiaro, lo scontrino fa alcune scelte. Le dice apertamente:

- **I contributi dell'azienda sono un valore medio (30%).** Il valore esatto cambia un po' in base al settore e a quanti dipendenti ha l'azienda.
- **Non conta le addizionali regionali e comunali all'IRPEF**, che cambiano da Comune a Comune.
- **Considera un dipendente senza familiari a carico** e senza altri redditi o detrazioni personali (spese mediche, mutuo…).
- **Le tue tasse non hanno un'etichetta.** Lo Stato non usa la tua IRPEF per una spesa precisa: la divisione mostra come sarebbe ripartita se seguisse la spesa pubblica totale.

Per sapere il tuo netto esatto fa fede la busta paga.

## Vedere la pagina sul tuo computer

Basta aprire `index.html` con un doppio clic: la pagina non carica altri file.

## File

| File | A cosa serve |
| --- | --- |
| `index.html` | La pagina completa: stile, testi, calcoli e dati della spesa pubblica. |
| `wrapped/` | Il Wrapped dello stipendio: lo stesso calcolo raccontato a storie, per ragazzi delle medie e superiori. Regole in `wrapped/CLAUDE.md`. |

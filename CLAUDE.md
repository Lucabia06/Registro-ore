# Registro Ore – istruzioni per le modifiche

App web (PWA) per registrare le ore di lavoro, pubblicata con GitHub Pages dal branch `main`.
Ogni modifica unita in `main` viene pubblicata automaticamente.

## Struttura
- `index.html` – tutta l'app (HTML, CSS e JavaScript in un unico file, nessuna dipendenza esterna, nessun build).
- `sw.js` – service worker per l'uso offline e gli aggiornamenti.
- `manifest.webmanifest`, `icon-*.png`, `apple-touch-icon.png` – installazione come app.

## Regole da rispettare
- Mantieni tutto in `index.html`, senza framework, librerie da CDN o passaggi di build.
- L'interfaccia è in italiano.
- **Non rompere i dati salvati.** Non rinominare né cambiare il formato di queste chiavi di localStorage:
  `registroOre.v1` (voci), `registroOre.todos`, `registroOre.colors`, `registroOre.colorsU`,
  `registroOre.tomb`, `registroOre.sync`, `registroOre.ai`, `registroOre.calBy`, `registroOre.goals` (obiettivi).
  Se servono nuovi campi, aggiungili come facoltativi e gestisci i dati vecchi che non li hanno.
- **Sincronizzazione:** ogni voce e ogni elemento da fare ha `id` e `u` (ultima modifica); le eliminazioni
  finiscono in `tomb`. Salva sempre con `save()`, `saveT()`, `saveG()` (obiettivi) e `saveC()`, che aggiornano questi valori e
  avviano la sincronizzazione. Non scrivere direttamente in localStorage per voci, lista da fare o colori.
- Dopo ogni modifica a `index.html`, aumenta di uno il numero di versione in `sw.js`
  (`const CACHE='registro-ore-vN'`) e, con lo stesso numero, `const APP_VERSION=N` in `index.html`:
  così le app installate si aggiornano e il menu mostra la versione giusta.
- L'app deve restare comoda su smartphone (larghezza 360–430 px): niente scorrimento orizzontale della pagina,
  campi di input almeno da 16 px su mobile, area toccabile adeguata. Rispetta il tema chiaro e scuro
  (variabili CSS in `:root`).
- Non inserire mai chiavi API, token o dati personali nei file del repository: è pubblico.

## Prima di consegnare
- Controlla che non ci siano errori JavaScript in console.
- Verifica la pagina sia a larghezza desktop sia a larghezza smartphone.

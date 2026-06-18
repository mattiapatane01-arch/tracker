# 📒 LEARNINGS — cosa ho imparato di Claude Code, giorno per giorno

> Regola: a fine di ogni sessione, 2-3 righe sul concetto del giorno. Se non lo so spiegare in 2 righe, non l'ho capito.
>
> Formato: **G N (data)** — concetto · cosa ho costruito · una cosa che NON mi era chiara.

---

**G1 (12/06)** — separazione config/stato: `data.json` contiene la struttura (task, milestone, label), `localStorage` contiene lo stato che cambia ogni giorno (checkbox spuntate, valori contatori). Il sito legge il JSON con `fetch()` e costruisce tutto l'HTML dinamicamente — niente hardcoded. Da chiarire: perché `fetch()` non funziona aprendo il file direttamente (serve un server locale anche solo per sviluppo).

**G2 (13-14/06)** — parametrizzare una funzione: `render(data)` → `render(data, day)` permette di mostrare qualsiasi giorno senza cambiare logica. Lezione nascosta: il browser casha i file statici — `fetch('data.json?v='+Date.now())` forza sempre la versione aggiornata. Bug reale trovato: `new Date().toISOString()` restituisce UTC, non ora locale — in Australia sfasava le date di un giorno. Fix: costruire la data con `getFullYear/getMonth/getDate` (ora locale). La catch di una Promise prende QUALSIASI errore nella chain, non solo errori di rete — messaggio generico = debugging cieco.

**G3 (14/06)** — il `CLAUDE.md` è il "cervello" che l'AI legge a ogni nuova sessione: io riparto senza memoria, lui no. Deve dire tre cose: cos'è il progetto, le regole dure (vincoli da non rompere mai), la forma dei dati. Non si scrive una volta: si MANTIENE — a fine sessione aggiorno solo lo "Stato" e le decisioni durature, non i dettagli del giorno. Trappola da evitare (mio pattern overengineering): denso ma CORTO, ogni riga si deve guadagnare il posto, un file lungo nasconde la regola importante. Cosa ho fatto oggi: confrontato la struttura `data.json` descritta nel CLAUDE.md con quella reale → trovato che il blocco `meta` non era documentato, aggiunto. Da chiarire: come decidere il confine tra "decisione duratura" (va nel CLAUDE.md) e "dettaglio di sessione" (va nel journal/non si scrive).

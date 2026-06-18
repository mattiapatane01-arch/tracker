# 📒 LEARNINGS — cosa ho imparato di Claude Code, giorno per giorno

> Regola: a fine di ogni sessione, 2-3 righe sul concetto del giorno. Se non lo so spiegare in 2 righe, non l'ho capito.
>
> Formato: **G N (data)** — concetto · cosa ho costruito · una cosa che NON mi era chiara.

---

**G1 (12/06)** — separazione config/stato: `data.json` contiene la struttura (task, milestone, label), `localStorage` contiene lo stato che cambia ogni giorno (checkbox spuntate, valori contatori). Il sito legge il JSON con `fetch()` e costruisce tutto l'HTML dinamicamente — niente hardcoded. Da chiarire: perché `fetch()` non funziona aprendo il file direttamente (serve un server locale anche solo per sviluppo).

**G2 (13-14/06)** — parametrizzare una funzione: `render(data)` → `render(data, day)` permette di mostrare qualsiasi giorno senza cambiare logica. Lezione nascosta: il browser casha i file statici — `fetch('data.json?v='+Date.now())` forza sempre la versione aggiornata. Bug reale trovato: `new Date().toISOString()` restituisce UTC, non ora locale — in Australia sfasava le date di un giorno. Fix: costruire la data con `getFullYear/getMonth/getDate` (ora locale). La catch di una Promise prende QUALSIASI errore nella chain, non solo errori di rete — messaggio generico = debugging cieco.

**G3 (14/06)** — il `CLAUDE.md` è il "cervello" che l'AI legge a ogni nuova sessione: io riparto senza memoria, lui no. Deve dire tre cose: cos'è il progetto, le regole dure (vincoli da non rompere mai), la forma dei dati. Non si scrive una volta: si MANTIENE — a fine sessione aggiorno solo lo "Stato" e le decisioni durature, non i dettagli del giorno. Trappola da evitare (mio pattern overengineering): denso ma CORTO, ogni riga si deve guadagnare il posto, un file lungo nasconde la regola importante. Cosa ho fatto oggi: confrontato la struttura `data.json` descritta nel CLAUDE.md con quella reale → trovato che il blocco `meta` non era documentato, aggiunto. Da chiarire: come decidere il confine tra "decisione duratura" (va nel CLAUDE.md) e "dettaglio di sessione" (va nel journal/non si scrive).

**G4-G5 (18/06)** — git è la **rete di sicurezza** che ti fa lavorare veloce: un commit = un salvataggio del videogioco, da lì puoi rompere tutto e tornare indietro con un comando. È questo che permette di andare "da pro", non il battere più in fretta. Due strumenti diversi: **git+GitHub** = magazzino versionato per QUALSIASI progetto (anche tool Python/trading, da tenere privati); **GitHub Pages** = mette online SOLO i siti statici (HTML/CSS/JS). Deploy fatto senza Netlify (bloccato): repo pubblico su GitHub → Pages → online. Flusso di update da ricordare: **modifico `data.json` → `git add` → `git commit` → `git push` → il sito si aggiorna da solo**. Concetto chiave del "diventare bravo": i piccoli passi non si saltano, diventano automatici — un pro legge le diff in 5 secondi, non le ignora. Da chiarire: cos'è esattamente un branch e quando me ne servirà più di uno (`main`).

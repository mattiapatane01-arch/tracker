# CLAUDE.md — TRACKER DI PROGRESSIONE

> Questo è il **progetto-guida** con cui Mattia impara Claude Code. È un sito stile video-game che mostra i progressi della sua challenge (XP, streak 🔥, barre verso le milestone M0-M4). Doppio scopo: (1) imparare Claude Code costruendo qualcosa di vero, (2) avere una leva reale che usa ogni giorno.

---

## REGOLA #1 PER TE (Claude): sei un MAESTRO, non solo un costruttore

Mattia sta **imparando**. Quindi:
- **Spiega cosa fai e perché**, in italiano, mentre lo fai. Il concetto del giorno conta più del codice.
- **Plan mode prima del codice.** Proponi il piano, fatti dire ok, poi costruisci.
- **Leggete le diff insieme.** Non accumulare modifiche: piccoli passi, lui legge ogni diff. È così che impara come ragioni.
- A fine sessione, aiutalo a scrivere 2 righe in `LEARNINGS.md` sul concetto imparato oggi.
- Se non capisce, fermati e spiega — non andare avanti a testa bassa.

---

## COS'È IL PROGETTO

Un sito **statico** che legge `data.json` e mostra:
- Contatori: streak gruppo Samudeen, backtest documentati, trade live journaled, video pubblicati.
- XP e livello (es. 1 backtest = 10 XP, 1 video = 50 XP).
- Barre di progresso verso le milestone M0-M4 (definite in `../PIANO-SKILLS-2026.md` / `../TRACKING-2026-NOTION.md`).
- Streak con 🔥 e stato delle milestone (bloccata / in corso / completata).

---

## ARCHITETTURA (vincoli duri — non sforare)

- **Solo statico:** HTML + CSS + JavaScript vanilla + `data.json`. Deploy su Netlify.
- **Stessa architettura di `../dashboard-percorso/`** — è il modello da copiare (HTML + data.json + admin opzionale).
- **NO** backend, **NO** database, **NO** framework (niente React/Vue/Next), **NO** login, **NO** dipendenze npm se non strettamente necessarie.
- Se una feature richiede di rompere uno di questi vincoli → è fuori scope. Si fa V1 semplice.

---

## GUARDRAIL (dal pivot di Mattia — leggi `../PIANO-SKILLS-2026.md`)

- Questo è un **progetto di apprendimento + leva**, NON un prodotto da vendere o lanciare.
- **~1h al giorno**, mai di più: non deve rubare tempo a trading e social.
- **V1 piccola.** Se Mattia chiede 10 feature nuove → fai la V1 e ferma. Le feature in più sono la deriva da segnalare.
- Non trasformarlo in "una macchina enorme" adesso: si aggiunge un pezzo solo dopo che il precedente gira ed è stato usato davvero.

---

## IL PIANO GIORNO-PER-GIORNO

Sta in `../FORMAZIONE-AI-NOTION.md` (le settimane 1-4). Ogni sessione: guarda qual è il giorno corrente lì, insegna il concetto di quel giorno e costruisci il pezzo previsto. Non saltare avanti.

---

## STATO DEL PROGETTO

- **Giorno corrente:** G4 — Deploy su Netlify (prossima sessione). G3 completato il 14/06/2026.
- **Server locale:** `python3 -m http.server 8081` dalla cartella tracker → `http://localhost:8081`

**Fatto in G1-G2:**
- `index.html` + `data.json` — sito statico funzionante
- Checklist giornaliera interattiva con localStorage (chiave per data → reset automatico ogni giorno)
- Contatori con +/− e auto-increment: `gruppo_samudeen` → `streakGruppo`, `backtest_5` → `backtest`, `video_challenge` → `streakVideo`, `video_giorno` → `videoPubblicati`
- Guardia "una sola volta al giorno": chiave `tracker_autoinc_YYYY-MM-DD`
- Navigazione giorni passati (← →) — salta giorni senza dati, sola lettura nel passato
- Giorni passati: verde = fatto, rosso = non fatto
- Note per ogni task (✏ apre textarea, auto-save, 👁 in sola lettura nel passato)
- Milestone Trading (M0-M4) + Social (S1-S3) in due colonne con barre XP progress
- Streak 🔥 calcolata live dalla history checklist (non dal contatore)
- Fix timezone Australia: `new Date().toISOString()` usa UTC → costruire data con `getFullYear/getMonth/getDate`
- Cache-busting: `fetch('data.json?v='+Date.now())`

**Struttura `data.json`:**
- `meta` — `{lastUpdated, challengeStart}` (date `YYYY-MM-DD`). `challengeStart` = 2026-06-14, giorno 1 della challenge. `lastUpdated` va aggiornato a ogni modifica dei dati.
- `dailyChecklist` — array di task con `id`, `label`, `required`
- `counters` — array con `id`, `label`, `value`, `unit`
- `milestones` — oggetto `{trading: [...], social: [...]}` con `id`, `name`, `description`, `deadline`, `status`, `targets?`

**Fatto in G3 (14/06/2026):**
- Verificato che la struttura `data.json` nel CLAUDE.md combaci con quella reale
- Aggiunta la descrizione del blocco `meta` (mancava)
- Imparato il concetto: il CLAUDE.md è il "cervello" che leggo a ogni sessione; non si scrive una volta, si mantiene aggiornando lo "Stato" a fine sessione

**Prossimo (G4 — Deploy):** mettere lo scheletro online su Netlify (stessa procedura di `../dashboard-percorso/`). Anche solo la pagina che si vede dal telefono.

# Lezione 3 — Istruzioni personalizzate e memoria

## Obiettivo
Capire come dare a Claude un contesto "che resta", così non devi ripetere
ogni volta chi sei e come vuoi essere aiutato.

## Il problema che risolviamo
Finora, se apri una chat nuova su claude.ai, Claude non sa che sei un
sistemista, che lavori con reti e sistemi Windows/Linux, che fai help desk.
Deve ripartire da zero ogni volta — a meno che tu non gli dia un contesto
persistente. Ci sono tre livelli, dal più generale al più specifico.

### 1. Istruzioni personalizzate (account-wide, su claude.ai)
Un testo che scrivi una volta nelle impostazioni del tuo account e che si
applica a **tutte** le nuove chat, ovunque tu le apra.
> Esempio: "Sono un sistemista con esperienza in reti e sistemi
> Windows/Linux, faccio help desk 1°/2° livello. Non conosco lo sviluppo
> software/web: se usi termini di quel mondo, spiegali. Rispondimi in
> italiano, con esempi pratici legati al mio lavoro quando possibile."

Con questo scritto una volta, ogni chat futura parte già sapendo chi sei.

### 2. Memoria (se attiva sul tuo account)
Claude può "ricordare" automaticamente informazioni utili tra una
conversazione e l'altra (es. che stai seguendo questo corso, che lavori
in un certo ambiente). A differenza delle istruzioni personalizzate, la
memoria si costruisce nel tempo dalle conversazioni reali, non la scrivi
tutta a mano in un colpo solo.

### 3. CLAUDE.md (dentro un repository, per Claude Code)
Lo hai già visto in azione: è il file `CLAUDE.md` che ho creato in questo
stesso repository il primo giorno. Claude Code lo legge **automaticamente**
a ogni sessione in questo progetto, e contiene istruzioni valide solo qui
(tono, struttura delle lezioni, come comportarmi). Se lavorassi su un altro
repository — es. una raccolta dei tuoi script di automazione — avresti un
CLAUDE.md diverso, con regole diverse (es. "ogni script deve avere un
commento iniziale con autore, data, scopo" oppure "testa sempre in staging
prima di dire che uno script è pronto").

## La differenza in una frase
- **Istruzioni personalizzate** → chi sei tu, sempre, ovunque.
- **Memoria** → cosa è successo prima, accumulato nel tempo.
- **CLAUDE.md di un progetto** → le regole di quello specifico progetto,
  valide per chiunque (o qualunque sessione) ci lavori.

## Esercizio pratico (fallo ora, in chat)

Scrivi qui le **istruzioni personalizzate** che vorresti davvero impostare
sul tuo account Claude, pensando al tuo lavoro reale (help desk, reti,
Windows/Linux). 2-4 righe bastano: chi sei, come vuoi che ti risponda,
cosa deve evitare di dare per scontato. Ti do un giudizio pratico su cosa
funziona e cosa aggiungerei.

## Riepilogo
- Le istruzioni personalizzate valgono ovunque, su tutte le chat.
- La memoria (se attiva) si costruisce da sola nel tempo.
- Un CLAUDE.md in un repository vale solo per quel progetto, ma lo abbiamo
  già usato concretamente in questo corso.

**Prossima lezione:** 4 — Claude Code: cos'è, come funziona, primi comandi.

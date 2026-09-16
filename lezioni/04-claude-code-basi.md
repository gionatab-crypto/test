# Lezione 4 — Claude Code: cos'è, come funziona, primi comandi

## Obiettivo
Capire cosa succede davvero "dietro le quinte" quando usi Claude Code (quello
che stiamo usando in questo corso), e i concetti base per usarlo con sicurezza.

## Cos'è Claude Code, in pratica
Non è solo una chat: è un ambiente in cui Claude lavora dentro una **cartella
reale** (nel nostro caso, questo repository) con accesso a file, terminale
e git. Puoi pensarlo così:

> È come avere un collega che si siede al tuo PC, con una cartella di script
> aperta. Gli chiedi qualcosa in linguaggio naturale ("controlla se questo
> script ha errori", "aggiungi un controllo sullo spazio disco"), e lui:
> legge i file veri, li modifica, prova i comandi nel terminale, e — se
> vuoi — salva tutto con git. A differenza di un collega, però, ti chiede
> il permesso prima di fare qualcosa di rischioso.

## I concetti base

- **Sessione** — una conversazione con Claude Code legata a una cartella di
  lavoro specifica (qui, il repository `test`). Ogni sessione "vede" solo
  quella cartella, non l'intero tuo computer.
- **Strumenti** — Claude Code non "scrive testo su cosa farebbe": esegue
  azioni vere tramite strumenti dedicati. Alcuni esempi: leggere un file,
  modificarne una parte, cercare una parola in tutti i file, lanciare un
  comando da terminale (bash/PowerShell). Ogni volta che nella nostra chat
  hai visto un blocco con scritto "Read", "Edit", "Bash" ecc. — quello è
  Claude che usa uno strumento specifico, non che "immagina" un risultato.
- **Permessi** — prima di eseguire azioni che modificano qualcosa (scrivere
  un file, lanciare un comando, fare un commit), Claude Code chiede la tua
  approvazione (a meno che tu non gli dia più libertà esplicitamente). Tu
  resti sempre il responsabile finale di cosa viene eseguito.
- **CLAUDE.md** — lo hai già visto: il file di istruzioni che Claude legge
  automaticamente all'inizio di ogni sessione in un repository, con le
  regole specifiche di quel progetto.
- **Git integrato** — Claude Code sa lavorare con git: creare branch, fare
  commit, aprire pull request. In questo corso, ogni lezione completata
  viene salvata con un commit — l'hai visto succedere ad ogni lezione finora.

## Dove si usa
Claude Code esiste come riga di comando sul tuo PC, ma anche via web/app
(claude.ai/code) — come stiamo facendo ora, in un ambiente cloud isolato e
già pronto, senza installare nulla.

## Esercizio pratico (fallo ora, in chat)

Ora tocca a te dare un comando reale. Scegli **una** di queste richieste (o
inventane una simile) e scrivimela in linguaggio naturale, come faresti con
un collega:

1. "Dimmi quanti commit abbiamo fatto finora in questo corso"
2. "Cerca in tutte le lezioni dove ho scritto la parola 'firewall' (o
   un'altra parola a tua scelta)"
3. "Mostrami l'elenco dei file nella cartella lezioni"

Dopo la tua richiesta, la eseguo davvero e ti spiego quale strumento ho
usato (e perché quello e non un altro).

## Esercizio svolto (esempio reale)

Richiesta: "Mostrami l'elenco dei file nella cartella lezioni".

Strumento usato: **Glob**, con pattern `lezioni/*.md` → ha restituito i 4
file di lezione esistenti, ordinati. Glob è lo strumento dedicato a
"trova file per nome/pattern" — preferito a un comando shell generico
(`ls`/`dir`) quando la richiesta è solo di elencare o cercare file, mentre
Bash resta riservato ad azioni più "attive" (eseguire comandi, script, git).

## Riepilogo
- Claude Code lavora dentro una cartella reale, con strumenti veri (leggere,
  modificare, eseguire comandi, git).
- Ti chiede il permesso prima di azioni rischiose: tu resti al comando.
- CLAUDE.md dà le regole del progetto, valide per ogni sessione futura.

**Prossima lezione:** 5 — Esplorare un progetto/repository con Claude.

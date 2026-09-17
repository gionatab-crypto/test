# Lezione 5 — Esplorare un progetto/repository con Claude

## Obiettivo
Imparare a farti aiutare da Claude per orientarti velocemente in una cartella
di file che non conosci — script ereditati da un collega, configurazioni
senza documentazione, un repository nuovo — senza dover aprire tutto a mano.

## La situazione tipica da sistemista
Ti capita spesso: erediti una cartella di script di automazione da un
collega andato via, senza una riga di documentazione. Prima, l'unico modo
era aprirli uno per uno e leggerli tutti. Con Claude Code puoi farti
guidare, come faresti chiedendo aiuto a chi li ha scritti — solo che qui
Claude "legge" i file al posto tuo e ti riassume quello che trova.

## Gli strumenti dell'esplorazione

- **Glob** — trova file per nome/pattern (l'hai già visto ieri: "mostrami i
  file nella cartella lezioni").
- **Grep** — cerca una parola o un pattern **dentro** il contenuto dei file,
  anche su tante cartelle insieme. Es: "in quali script viene usato
  l'indirizzo IP del DNS secondario?" → Grep cerca quella stringa in tutti
  i file e ti dice dove si trova.
- **Read** — apre e legge un file specifico per intero, quando vuoi capirlo
  a fondo (non solo trovarlo).

La combinazione tipica: prima **Glob** (cosa c'è?), poi **Grep** (dove si
parla di X?), infine **Read** (fammi vedere questo file nel dettaglio).

## Il consiglio pratico: parti largo, poi scendi nei dettagli
Non chiedere subito "spiegami la riga 47 dello script X" se non sai
nemmeno cosa contiene la cartella. Fai al contrario:
1. "Dammi un riepilogo di cosa c'è in questa cartella"
2. "Di questi, quale si occupa di [backup / firewall / utenti AD]?"
3. "Aprimi quello specifico e spiegamelo passo passo"

Esattamente come faresti con un collega che conosce l'ambiente: prima il
quadro generale, poi il dettaglio su cui ti serve davvero concentrarti.

## Esercizio pratico (fallo ora, in chat)

Proviamo un'esplorazione vera su questo stesso repository. Scegli una di
queste richieste (o una simile):

1. "Cerca in tutte le lezioni ogni punto in cui è citato 'CLAUDE.md'"
   (vediamo Grep in azione su più file insieme)
2. "Fammi un riepilogo di cosa contiene CORSO.md, senza leggerlo io"
3. "Cerca in quali lezioni ho parlato di 'PowerShell'"

Dopo la tua richiesta, la eseguo ed ti spiego quale strumento ho usato.

## Riepilogo
- Glob trova file, Grep cerca dentro i file, Read legge un file per intero.
- Esplora sempre dal generale al particolare, come con un collega nuovo.
- Questo approccio ti fa risparmiare ore quando eredit script/config senza
  documentazione.

**Prossima lezione:** 6 — Automatizzare script (PowerShell/Bash) con Claude.

# Lezione 1 — Come "parlare" con Claude: prompting efficace

## Obiettivo
Capire cosa rende una richiesta a Claude (o a qualsiasi AI) efficace, e scrivere
la tua prima richiesta "da professionista" su un caso reale di help desk.

## Perché è importante
Claude non "indovina" cosa vuoi: risponde a quello che scrivi. Un sistemista è
abituato a essere preciso con i comandi (un typo in PowerShell rompe lo script);
con l'AI vale lo stesso principio, ma la "sintassi" è il linguaggio naturale.
Una richiesta vaga = risposta generica. Una richiesta con contesto = risposta
utile e pronta all'uso.

## I 4 ingredienti di un buon prompt

1. **Contesto** — cosa stai facendo, in che ambiente, per chi.
   > ❌ "Scrivimi uno script per i log"
   > ✅ "Sono un sistemista, ho un server Windows Server 2019. Mi serve uno
   > script PowerShell che legga l'Event Viewer e mi elenchi gli errori delle
   > ultime 24 ore nel log di sistema."

2. **Obiettivo chiaro** — cosa vuoi ottenere, non solo il "materiale grezzo".
   > ✅ "...voglio un file CSV con Data, Livello, ID Evento, Descrizione, da
   > allegare a un ticket."

3. **Vincoli e formato** — cosa deve rispettare la risposta (lunghezza,
   linguaggio, compatibilità).
   > ✅ "Deve funzionare senza moduli esterni, solo PowerShell nativo
   > (compatibile con PowerShell 5.1)."

4. **Esempio o caso concreto** (se ce l'hai) — aiuta moltissimo.
   > ✅ "Esempio di riga che voglio ottenere: 2026-09-10 08:12, Error, 41,
   > Kernel-Power"

## Un trucco da sistemista: pensa al prompt come a un ticket ben scritto

Quando apri un ticket a un collega più esperto, non scrivi "non funziona".
Scrivi: cosa hai provato, che errore vedi, che sistema è, cosa ti aspetti.
Lo stesso identico approccio rende Claude molto più utile — perché è
esattamente l'informazione che servirebbe anche a un collega umano.

## Errori comuni da evitare
- **Prompt troppo corti su task complessi**: se il task ha più step, elencali.
- **Dare per scontato il contesto**: Claude non sa che lavori in un dominio
  Active Directory con 200 utenti a meno che tu non lo dica.
- **Non correggere**: se la prima risposta non va bene, non ricominciare da
  zero — rispondi dicendo cosa correggere ("va bene ma aggiungi anche l'IP
  del client" è un prompt valido tanto quanto il primo).

## Esercizio pratico (fallo ora, in chat)

Pensa a un compito reale che affronti spesso nel tuo lavoro di help desk
(es: reset password, controllo spazio disco, diagnosi problemi di rete,
riavvio di un servizio, verifica backup...).

Scrivi qui in chat un prompt che chiederesti a Claude per farti aiutare in
quel compito, usando i 4 ingredienti sopra. Non preoccuparti di essere
perfetto: te lo miglioro insieme dopo che lo scrivi.

## Esercizio svolto (esempio reale)

Compito scelto: controllo spazio libero su disco di sistema di più server
(Windows + Linux, accesso RDP/SSH, nessuna orchestrazione centralizzata)
prima di una finestra di aggiornamenti.

❌ Prompt iniziale: *"Devo controllare lo spazio libero del disco di sistema
di tutti i server prima di effettuare gli aggiornamenti per essere sicuro
che sia sufficiente"* — è un buon **obiettivo**, ma senza contesto tecnico,
soglia né formato è ancora un titolo di ticket, non un prompt completo.

✅ Prompt arricchito: *"Sono un sistemista, gestisco server Windows e Linux
a cui accedo via RDP/SSH (nessuna orchestrazione centralizzata tipo
Ansible/WinRM). Prima di ogni finestra di aggiornamento devo verificare che
il disco di sistema (C: su Windows, / su Linux) abbia più di 5 GB liberi.
Voglio due script da eseguire localmente su ciascun server — uno PowerShell
(nativo, no moduli esterni) e uno Bash — che controllino lo spazio libero e
aggiungano una riga a un file CSV condiviso con: data/ora, nome server, GB
liberi, esito (OK o ATTENZIONE se sotto soglia). Voglio poterli lanciare sia
a mano sia pianificarli con Attività Pianificata/cron."*

**Lezione imparata:** parole come "automatico" o "sufficiente" sono
ambigue — vanno chiarite nel prompt (append vs overwrite? soglia fissa o
percentuale? esecuzione manuale o pianificata?) prima di ottenere la
risposta, non dopo averla corretta due volte.

## Riepilogo
- Un buon prompt = contesto + obiettivo + vincoli + esempio (se possibile).
- Pensa al prompt come a un ticket ben documentato.
- Le parole ambigue (automatico, sufficiente, veloce...) vanno chiarite subito.
- Puoi sempre correggere Claude in corsa, non serve ripartire da zero.

**Prossima lezione:** 2 — Chat vs Progetti vs Claude Code: quale strumento
per quale compito.

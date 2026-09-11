# Lezione 2 — Chat vs Progetti vs Claude Code: quale strumento per quale compito

## Obiettivo
Capire le tre modalità principali con cui si usa Claude nella pratica, e
imparare a scegliere quella giusta per ogni tipo di compito.

## Le tre modalità

### 1. Chat normale (claude.ai)
Una conversazione singola, senza memoria di altre conversazioni. Nessun
accesso a file o sistemi reali: Claude vede solo quello che scrivi tu.
**Ottima per:** domande veloci, spiegazioni, bozze di testo, brainstorming,
un aiuto una tantum che esaurisci in pochi messaggi.

> Esempio: "Spiegami la differenza tra un firewall stateful e stateless"
> → chat semplice, non serve altro.

### 2. Progetti (Projects, su claude.ai)
Un "contenitore" di conversazioni che condividono lo stesso contesto:
istruzioni fisse (es. "rispondimi sempre in italiano, stile tecnico
sintetico") e file di riferimento che carichi una volta (es. uno schema di
rete, un elenco di server, una policy aziendale). Ogni nuova chat dentro
quel progetto "eredita" tutto questo, senza che tu debba ripeterlo.
**Ottimo per:** lavori ricorrenti sullo stesso argomento nel tempo — es. la
documentazione IT aziendale, dove ogni pagina deve rispettare lo stesso
stile e riferirsi agli stessi materiali.

### 3. Claude Code (quello che stai usando ora)
Non è solo una chat: gira in un ambiente con accesso reale a file, terminale
e git. Può leggere e modificare file veri, eseguire comandi, creare
script, fare commit. Non "ti spiega" come fare una cosa: **la fa**, dentro
un progetto/repository reale (come stiamo facendo con questo corso).
**Ottimo per:** lavorare su codice, script, configurazioni, automazioni —
qualsiasi cosa che debba diventare un file reale, testato, versionato.

## Come scegliere in pratica

| Ti serve... | Usa |
|---|---|
| Una risposta/spiegazione una tantum | Chat |
| Un lavoro ricorrente sullo stesso tema, con contesto fisso da riusare | Progetto |
| Modificare/creare file veri, script, automazioni, versionare con git | Claude Code |

Non sono in competizione: spesso si usano insieme. Es: usi un Progetto per
tenere la documentazione IT aggiornata nel tempo, e Claude Code quando devi
scrivere o correggere davvero gli script citati in quella documentazione.

## Esercizio pratico (fallo ora, in chat)

Ti propongo 3 scenari. Per ciascuno dimmi quale strumento useresti
(Chat / Progetto / Claude Code) e perché in una riga:

**A.** Un utente ti scrive un ticket confuso, devi rispondergli chiedendo
chiarimenti in modo professionale. Una volta sola, non si ripeterà.

**B.** Stai curando da mesi la wiki interna con le procedure IT: ogni volta
che scrivi una nuova pagina deve rispettare lo stesso stile, la stessa
struttura, e riferirsi allo stesso elenco di server che hai già caricato.

**C.** Hai una cartella con 15 script di automazione per il backup: vuoi
che vengano rivisti, corretti e versionati con git.

## Riepilogo
- Chat: aiuto veloce, una tantum, nessun contesto persistente.
- Progetto: lavoro ricorrente con contesto/file fissi da riusare.
- Claude Code: quando serve toccare file veri, eseguire comandi, versionare.

**Prossima lezione:** 3 — Istruzioni personalizzate e memoria.

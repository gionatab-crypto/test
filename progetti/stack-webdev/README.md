# Stack webdev (Portainer)

Stack Docker per ospitare siti web, basato sul riferimento che hai passato
ma adattato alle tue risposte:

- Progetto: **chiaradiluna-webdev** (WordPress), più un ambiente Apache/PHP
  condiviso e riusabile per altri progetti futuri (uno per cartella sotto
  `sites/`).
- Uso: **sito reale**, non solo laboratorio → sotto trovi una checklist di
  sicurezza da seguire prima di andare online.
- Immagine "webdev": PHP + Apache **standard** (nessuna estensione o tool
  particolare richiesto), quindi niente build di un'immagine custom.
- Porte: confermate 8091 (webdev), 8092 (chiaradiluna-webdev), 8093 (phpMyAdmin).
- Davanti c'è un reverse proxy già presente in Portainer: **Nginx Proxy
  Manager (NPM) + CrowdSec**.

> **Nota sui limiti di questa sessione:** io (Claude) lavoro qui dentro solo
> su questo repository Git, in un ambiente isolato. Non ho accesso al tuo
> Portainer, al tuo browser o al tuo server reale — non posso entrare io
> stesso in NPM a configurare i Proxy Host. Ti preparo i file e le
> istruzioni passo-passo, i click nell'interfaccia web li fai tu (o me li
> descrivi e ti guido).

## Cosa ho cambiato rispetto al tuo riferimento e perché

1. **`webdev-custom:latest` → `php:8.3-apache`** (immagine ufficiale).
   Il tuo riferimento usava un'immagine custom da costruire, ma mi hai detto
   che ti basta PHP + Apache standard. L'immagine ufficiale fa lo stesso
   lavoro (stesso comando `a2enmod vhost_alias rewrite && apache2-foreground`
   che avevi già nel riferimento) senza doverti preoccupare di costruire e
   mantenere un'immagine Docker tua. Se in futuro ti servirà qualcosa di
   speciale (es. un'estensione PHP non inclusa), allora ha senso passare a
   un'immagine custom — te lo faccio io quando serve.

2. **Password come variabili (`${...}`) invece che scritte nel file.**
   Il file `docker-compose.yml` NON contiene più password in chiaro: usa
   segnaposto tipo `${DB_ROOT_PASSWORD}`. Il valore vero lo imposti in
   Portainer (sezione "Environment variables" quando crei lo stack), non nel
   file. Motivo: questo repository finisce su Git — se le password fossero
   scritte nel file, chiunque avesse accesso al repository (o alla cronologia
   Git) le vedrebbe. Questo vale sempre, ma soprattutto ora che mi hai detto
   che il sito sarà reale.

3. **Progetto WordPress rinominato `chiaradiluna-webdev`** (nome reale che mi
   hai dato): `container_name`, il percorso del volume dei file WordPress
   (`chiaradiluna-webdev-data`) e le porte sono coerenti con questo nome.

4. **`vhost.conf` per l'ambiente condiviso `webdev`** (vedi sotto): l'ho
   scritto io perché nel tuo riferimento veniva solo montato ma non fornito.

## Come funziona l'ambiente condiviso "webdev" (per progetti futuri)

Il container `webdev` serve **più siti dalla stessa porta (8091)**, uno per
sottocartella di `/var/www/sites/`, usando il modulo Apache `vhost_alias`:

- Cartella `sites/progetto1/` → raggiungibile con `Host: progetto1.tuodominio.it`
- Cartella `sites/progetto2/` → raggiungibile con `Host: progetto2.tuodominio.it`

Questo funziona così: Apache guarda l'intestazione `Host` della richiesta e
usa la prima parola prima del punto come nome cartella (`VirtualDocumentRoot
/var/www/sites/%1`). Per farlo funzionare davvero ti servono, per ogni nuovo
progetto:

1. Una cartella `sites/<nome-progetto>/` sul server, con dentro i file PHP.
2. Un sottodominio (`<nome-progetto>.tuodominio.it`) che punta al server.
3. Se hai (o metterai) un reverse proxy davanti (consigliato per HTTPS, vedi
   sotto), il proxy deve inoltrare quel sottodominio al container `webdev`
   sulla porta 8091 **mantenendo l'header Host originale**.

Questo è esattamente il meccanismo pensato per il pannello di
amministrazione che vuoi costruire in futuro: creare un progetto = creare
una cartella sotto `sites/` (+ il sottodominio). Quando arriviamo a quella
lezione/esercizio possiamo costruire il pannello insieme.

## Limite da sapere su MariaDB

L'immagine `mariadb` crea **un solo database e un solo utente** in modo
automatico, leggendo `MYSQL_DATABASE`/`MYSQL_USER`/`MYSQL_PASSWORD` **solo la
prima volta** che il volume è vuoto. Se in futuro aggiungi un secondo sito
che ha bisogno di un proprio database (es. un secondo WordPress), dovrai
creare il nuovo database/utente a mano da phpMyAdmin (con l'utente root),
oppure dirmelo e aggiorniamo lo stack con uno script di init dedicato.

## Come usarlo in Portainer

1. Copia sul server i file di questa cartella (o clona il repo) in un
   percorso stabile, es. `/data/compose/webdev-manual/` (stesso percorso
   usato nei volumi del `docker-compose.yml` — se vuoi un percorso diverso,
   aggiorna i volumi di conseguenza).
2. In Portainer: **Stacks → Add stack**.
3. Dai un nome allo stack (es. `webdev`).
4. Incolla il contenuto di `docker-compose.yml` nell'editor web (oppure usa
   "Upload" caricando il file).
5. Nella sezione **Environment variables** dello stack, aggiungi (con i tuoi
   valori veri, non quelli di esempio):
   - `DB_ROOT_PASSWORD`
   - `WP_DB_NAME`
   - `WP_DB_USER`
   - `WP_DB_PASSWORD`
6. **Deploy the stack**.
7. Prima del primo avvio, crea sul server le cartelle usate dai volumi:
   `/data/compose/webdev-manual/{apache-config,sites,chiaradiluna-webdev-data}`
   e copia dentro `apache-config/` il file `vhost.conf` di questa cartella.

## Collegare Nginx Proxy Manager (NPM) + CrowdSec

Hai già NPM in Portainer, quindi questo stack **non deve gestire HTTPS da
solo**: resta in HTTP sulle porte 8091-8093, e ci pensa NPM davanti.

Per ogni servizio raggiungibile da internet, in NPM vai su
**Proxy Hosts → Add Proxy Host** e crea una voce così:

| Servizio | Domain Names | Forward Hostname/IP | Forward Port |
|---|---|---|---|
| WordPress chiaradiluna | `chiaradiluna.tuodominio.it` | IP del server Docker (o `localhost` se NPM gira sullo stesso host) | `8092` |
| Ambiente condiviso webdev | `progetto1.tuodominio.it`, `progetto2.tuodominio.it`, ... (uno per ogni cartella in `sites/`) | IP del server Docker | `8091` |
| phpMyAdmin (sconsigliato pubblico, vedi checklist) | eventualmente solo su rete interna/VPN | IP del server Docker | `8093` |

Cose a cui stare attento in NPM per questo stack:

- **Websockets support**: non serve (né WordPress né i siti PHP semplici lo
  richiedono), lascialo pure disattivato.
- **SSL**: attiva "Request a new SSL Certificate" (Let's Encrypt) e "Force
  SSL" per ogni Proxy Host che va online davvero.
- **CrowdSec**: se l'hai collegato come bouncer su NPM (plugin/proxy),
  funziona automaticamente su tutto il traffico che passa dai Proxy Host
  sopra: non serve configurazione aggiuntiva in questo stack.
- L'header `Host` deve arrivare intatto al container `webdev` perché
  `vhost.conf` lo usa per scegliere la cartella giusta sotto `sites/`: NPM
  lo fa di default, non c'è nulla da cambiare.

**Nota su un'opzione più sicura (facoltativa, non necessaria ora):** invece
di raggiungere i container tramite `IP-del-server:porta`, NPM potrebbe
collegarsi direttamente ai container sulla stessa rete Docker (senza
pubblicare le porte 8091-8093 sull'host). Serve però il nome della rete
Docker usata dallo stack di NPM in Portainer (Portainer → Stacks → stack di
NPM → Containers → Networks). Se me lo dai, aggiorno lo stack per collegarlo
a quella rete come `external: true` e togliamo le porte pubbliche — utile
soprattutto per phpMyAdmin.

## Checklist sicurezza (sito reale, non laboratorio)

- [ ] **Password uniche e robuste**, diverse da quelle di esempio, inserite
      solo nelle Environment variables di Portainer (mai nel file YAML).
- [ ] **phpMyAdmin pubblico (porta 8093) è un rischio** su un sito reale:
      valuta di togliere la riga `ports: - "8093:80"` e raggiungerlo solo
      via VPN/tunnel, oppure mettilo dietro autenticazione aggiuntiva sul
      reverse proxy. Ne parliamo con calma quando vuoi.
- [ ] **HTTPS**: questo stack espone solo HTTP sulle porte 8091-8093.
      Per un sito reale serve un certificato — di solito si mette un
      reverse proxy davanti (es. Nginx Proxy Manager, Traefik, Caddy) che
      gestisce HTTPS e poi inoltra il traffico a questi container. Dimmi se
      ne hai già uno sul server e ti aiuto a collegarlo.
- [ ] **Backup**: i dati veri stanno nei volumi (`mariadb-webdev-data`) e
      nelle cartelle montate (`chiaradiluna-webdev-data`, `sites/`). Vanno
      backuppati regolarmente: è un esercizio che possiamo fare insieme
      quando arriviamo alla parte di automazioni/script.
- [ ] **Aggiornamenti immagini**: `mariadb:11`, `wordpress:latest`,
      `phpmyadmin:latest`, `php:8.3-apache` vanno tenute aggiornate nel
      tempo (specie `latest`, che cambia versione da sola ad ogni pull).

## Prossimo passo

Quando crei i Proxy Host in NPM, dimmi i domini reali che stai usando (es.
`chiaradiluna.tuodominio.it`) così aggiorno gli esempi. Se vuoi anche la
versione "solo rete interna" (niente porte pubbliche), dammi il nome della
rete Docker di NPM e la preparo.

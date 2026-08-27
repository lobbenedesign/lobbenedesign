### Ciao, sono Giuseppe 👋

Costruisco software full-stack — backend fintech, tooling per agenti AI, sistemi a basso livello — spesso con assistenza AI pesante nel processo. Non nascondo questo fatto: qui sotto trovi solo progetti dove test reali e CI reale dimostrano che il codice funziona, non descrizioni che lo dichiarano e basta.

Il resto del mio profilo contiene molti altri progetti personali/sperimentali, a vari stadi di completezza — questi sono quelli su cui ho investito per portarli a uno standard verificabile.

---

#### 🏦 [psd3-open-banking-gw](https://github.com/lobbenedesign/psd3-open-banking-gw)
Gateway open banking PSD3/PSR con consent lifecycle e permission dashboard React.

- **91 test reali**, 93.57% / 91.15% di copertura
- CI su GitHub Actions verificata verde
- La CI era realmente rossa per un conflitto di dipendenze ESLint — l'ho trovato e corretto, poi riverificato verde con una run reale (non solo "dovrebbe funzionare")

#### 🧾 [invoice-to-catalog](https://github.com/lobbenedesign/invoice-to-catalog)
Trasforma fatture fornitore in schede prodotto pronte per l'e-commerce, con tracciamento provenienza/confidence per ogni campo estratto, e pubblicazione reale su 6 canali (WooCommerce, Shopify, Magento, PrestaShop, Amazon, eBay).

- **360 test reali** (324 + 36), tutti passanti
- Il numero dichiarato nel README corrisponde esattamente a quello verificato eseguendo la suite
- Integrazioni HTTP reali con i 6 canali, non mock

#### 🩺 [codedoctor-swe](https://github.com/lobbenedesign/codedoctor-swe)
Diagnosi bug da stack trace reale o issue in linguaggio naturale, patch tramite AST TypeScript reale (o LLM locale per modifiche multi-file), verifica eseguendo i test reali del progetto target, dispatch come branch git + commit locale.

- **35 test reali**, 0 fallimenti, CI verde
- Il loop agentico di retry è onesto: se una patch non risolve il bug entro il budget di tentativi, dichiara fallimento invece di simulare un successo
- Nessuna dipendenza da servizi live (Ollama, GitHub API) nei test automatizzati — tutto verificabile da chiunque cloni il repo

#### ⚡ [nexcache-VERAM3.3](https://github.com/lobbenedesign/nexcache-VERAM3.3)
Fork di Redis in C con motore di storage custom, moduli caricabili (vector search HNSW, CRDT, timeseries) e probe hardware runtime per SVE2/AVX.

- **~443 test reali** verificati (tag `-slow -cluster`), 0 fallimenti, CI verde
- Benchmark reale contro Redis 8.0.1 stock: **parità (~100%) senza pipelining**; sotto pipelining profondo un gap reale rimane (57-64% su SET, 70-82% su GET a seconda dell'hardware) — dichiarato onestamente nel README con un'issue GitHub dedicata, non nascosto
- Ha trovato e corretto un bug reale (8 thread "worker" in busy-spin permanente, ~350% CPU anche a server inattivo, zero chiamanti nel codebase) — la vecchia misura falsata da questo bug resta nel README, in una sezione dedicata, invece di essere cancellata

#### 💻 [claude-local-studio](https://github.com/lobbenedesign/claude-local-studio)
Web Studio locale per Claude Code: 24 provider LLM cloud + Ollama, repo map con AST reale (TypeScript Compiler API + tree-sitter), diff-apply reale su file, ensemble multi-modello.

- Da un monolite (`server.ts`, 4.721 righe) a 20 moduli in `src/`, verificato con `tsc --noEmit` + `bun build` a ogni singolo passo di estrazione — non solo alla fine
- **9 test reali** (server vero, richieste HTTP vere) + CI su GitHub Actions verde
- Autenticazione locale (token + cookie) verificata dal vivo: 401 senza token, 401 con token sbagliato, redirect+cookie con token corretto
- Packaging reale: `.app`/`.dmg` per macOS via `bun build --compile`, verificato lanciando il binario compilato fuori dalla cartella del repository

#### ⚙️ [nexus-local-engine](https://github.com/lobbenedesign/nexus-local-engine)
Router locale multi-engine per LLM (Ollama verificato, altri runtime rilevati onestamente se assenti), gestione modelli, cache risposte, routing per complessità.

- **13 test reali** + CI verde
- Autenticazione locale aggiunta (non c'era): senza, chiunque raggiungesse la porta poteva cancellare modelli Ollama installati o avviare download arbitrari
- Packaging `.app`/`.dmg` per macOS: durante la preparazione ho trovato un bug reale nella risoluzione dei path in un binario compilato (scriveva silenziosamente i propri file di configurazione dentro la cartella sorgente del progetto invece che accanto a sé) — corretto e riverificato lanciando il binario al di fuori del repository

#### 📄 [document-intelligence-rag](https://github.com/lobbenedesign/document-intelligence-rag)
RAG su documenti bancari con citazione obbligatoria e rifiuto esplicito quando la risposta non è supportata dai documenti.

- **60 test reali**, 97.15% di copertura, CI verde
- Progettato per non rispondere "a caso": ogni risposta cita la fonte o dichiara esplicitamente di non saperlo

#### 💬 [transaction-intelligence-agent](https://github.com/lobbenedesign/transaction-intelligence-agent)
Agente LLM con tool-calling per analisi transazionale conversazionale.

- **63 test reali**, 96% di copertura, CI verde
- Verificato dal vivo con tool-calling reale su Ollama locale (non solo test unitari mockati)

#### 🏖️ [beach-manager-app](https://github.com/lobbenedesign/beach-manager-app) · [beach-booking-app](https://github.com/lobbenedesign/beach-booking-app) · [beach-manager-electron](https://github.com/lobbenedesign/beach-manager-electron)
Piattaforma di prenotazione per stabilimenti balneari, nata da un'esperienza professionale reale (Cocobuk) — tre app distinte per tre pubblici: gestionale web per l'operatore, app cliente per la prenotazione, client desktop Electron per lo staff.

- **64 + 50 + 29 = 143 test reali**, tutti passanti, CI verde su tutti e tre i repo
- beach-booking-app e beach-manager-app erano stati pubblicati per errore come repository identici — differenziati sul serio: l'uno lato cliente, l'altro lato gestore, non solo rinominati
- Bug reali trovati e corretti durante il lavoro di verifica: test flaky legati alla data corrente, dipendenze CI rotte, non funzionalità applicativa

#### 🏄 [surf-cad-electron](https://github.com/lobbenedesign/surf-cad-electron)
App desktop React/Three.js/Electron per il design e la modellazione 3D di tavole da surf: editor 2D completo, loft 3D live, modulo pinne, export STL/DXF/G-code.

- **31 test reali** (geometria Bezier/Catmull-Rom, fit least-squares di curve digitalizzate, calcolo peso tavola) + CI verde
- **8 bug reali di reattività React trovati e corretti** (`react-hooks/refs`): due erano solo tecnicismi del linter (assegnare l'ultimo valore a un ref nel corpo del render, spostato in un `useEffect`), ma due erano bug funzionali veri — lo stile del cursore durante il drag (editor design, mappa pinne) leggeva un ref direttamente nel render, che non pianifica un re-render, quindi il cursore "grabbing" non si aggiornava in modo affidabile all'inizio/fine del trascinamento

---

*Tutti i numeri sopra sono stati verificati eseguendo realmente le rispettive test suite (o, per nexcache-VERAM3.3, anche un benchmark indipendente su hardware diverso da quello del README), non riportati dai README dei progetti senza controllo.*

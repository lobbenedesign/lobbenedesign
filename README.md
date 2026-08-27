### Ciao, sono Giuseppe 👋

Costruisco software full-stack — backend fintech, tooling per agenti AI, sistemi a basso livello — spesso con assistenza AI pesante nel processo. Non nascondo questo fatto: qui sotto trovi solo progetti dove test reali e CI reale dimostrano che il codice funziona, non descrizioni che lo dichiarano e basta.

Il resto del mio profilo contiene molti altri progetti personali/sperimentali, a vari stadi di completezza — questi quattro sono quelli su cui ho investito per portarli a uno standard verificabile.

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

---

*Tutti i numeri sopra sono stati verificati eseguendo realmente le rispettive test suite (o, per nexcache-VERAM3.3, anche un benchmark indipendente su hardware diverso da quello del README), non riportati dai README dei progetti senza controllo.*

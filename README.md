# cti.al — sito statico (Hugo + PaperMod)

Replica strutturale di [moltenbit.net](https://moltenbit.net/): generatore **Hugo**,
tema **PaperMod**, hosting gratuito su **GitHub Pages** con dominio personalizzato
`cti.al`. Stesse sezioni (Home, Posts, Disclosures, Tags, Search, Contact), stesso
font, stessa struttura; contenuti propri.

Il tema è incluso nella cartella `themes/PaperMod/` (licenza MIT): non c'è nulla da
installare, basta caricare e funziona.

---

## Struttura del progetto

```
.
├── .github/workflows/hugo.yml        # build + deploy automatici su GitHub Pages
├── hugo.toml                         # configurazione del sito (baseURL, menu, output…)
├── content/
│   ├── _index.md                     #   home (elenco dei post, come moltenbit)
│   ├── posts/                        #   articoli / write-up
│   │   ├── zammad-ssti-rce-ai-agent-cve-2026-34724.md
│   │   ├── zammad-ssrf-webhooks-cve-2026-34719.md
│   │   └── zammad-data-uri-xss-cve-2026-34718.md
│   ├── disclosures/_index.md         #   tabella delle disclosure (CVE, GHSA, post)
│   ├── contact.md                    #   pagina contatti (+ chiave PGP)
│   └── search.md                     #   pagina di ricerca
├── assets/css/extended/custom.css    # font del codice + footer social icons
├── layouts/_partials/footer.html     # footer con sole social icons (come moltenbit)
├── static/CNAME                      # contiene "cti.al"
├── static/pgp.asc                    # chiave PGP pubblica (k0x1c@proton.me)
└── themes/PaperMod/                   # il tema (incluso)
```

---

## Pubblicazione su GitHub Pages

Il repository è `github.com/k0x1c/cti-site`. Ad ogni `push` sul branch `main` il
workflow `.github/workflows/hugo.yml` compila il sito e lo pubblica.

Una sola configurazione iniziale, su GitHub:
**Settings → Pages → Build and deployment → Source → GitHub Actions.**

Lo stato del deploy è nella tab **Actions**. Il primo build richiede 1–2 minuti.

---

## Dominio `cti.al`

Il file `static/CNAME` (contiene `cti.al`) mantiene il dominio impostato ad ogni
deploy — **non rimuoverlo**.

Su GitHub: **Settings → Pages → Custom domain → `cti.al` → Save**, poi spunta
**Enforce HTTPS**.

Sul registrar, `cti.al` è un dominio *apex*: servono i record A verso GitHub Pages.

```
A   @   185.199.108.153
A   @   185.199.109.153
A   @   185.199.110.153
A   @   185.199.111.153
```

(Opzionale IPv6 con record AAAA su `@`:
`2606:50c0:8000::153`, `…8001::153`, `…8002::153`, `…8003::153`.)

---

## Aggiungere un post

Crea un file `.md` in `content/posts/`:

```markdown
---
title: "Titolo"
date: 2026-06-01
author: "k0x1c"
tags: ["cybersecurity"]
description: "Riassunto breve."
ShowToc: true
---

Contenuto in **Markdown**.
```

Per aggiungere una voce alle **Disclosures**, aggiungi una riga alla tabella in
`content/disclosures/_index.md` (colonne: CVE / ID, Product, Summary, Severity, Date,
References — con i link a NVD, all'advisory GHSA e al post).

`commit` + `push` → il sito si ricompila da solo.

---

## Anteprima in locale (opzionale)

Serve **Hugo extended ≥ 0.146**.

- Windows: `winget install Hugo.Hugo.Extended`
- macOS: `brew install hugo`
- Linux: binario/`.deb` "extended" da <https://github.com/gohugoio/hugo/releases>

```bash
hugo server
```

Apri <http://localhost:1313>.

---

## Note

- Tema PaperMod incluso (MIT). Per aggiornarlo, sostituisci `themes/PaperMod/` con una
  versione più recente dal repository ufficiale.
- L'accento cromatico segue il default di PaperMod (dark) per restare visivamente
  identico al sito di riferimento. Per un accento personalizzato basta modificare
  `assets/css/extended/custom.css`.

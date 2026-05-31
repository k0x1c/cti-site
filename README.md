# cti.al — sito statico (Hugo + Congo)

Replica strutturale di moltenbit.net: **Hugo** come generatore di siti statici e il
tema **Congo**. Hosting **gratuito** su **GitHub Pages**, con dominio personalizzato
`cti.al`. Nessun costo di hosting.

Il tema è già incluso nella cartella `themes/congo/` (non devi installare nulla):
clona/carica e funziona.

---

## 1. Struttura del progetto

```
.
├── .github/workflows/hugo.yml   # build + deploy automatici su GitHub Pages
├── config/_default/             # configurazione del sito
│   ├── hugo.toml                #   baseURL, output, tassonomie
│   ├── params.toml              #   opzioni tema (colori, ricerca, footer…)
│   ├── menus.en.toml            #   voci del menu in alto
│   ├── languages.en.toml        #   titolo, autore, link social
│   └── markup.toml              #   impostazioni Markdown (necessarie al tema)
├── content/                     # i tuoi contenuti (Markdown)
│   ├── _index.md                #   home
│   ├── posts/                   #   articoli
│   ├── disclosures/             #   sezione disclosures
│   └── contact.md               #   pagina contatti
├── static/CNAME                 # contiene "cti.al" (dominio personalizzato)
├── assets/                      # immagini/asset personalizzati (opzionale)
└── themes/congo/                # il tema (già incluso)
```

---

## 2. Pubblicazione su GitHub Pages (passo passo)

1. Crea un nuovo repository su GitHub (es. `cti-site`). Può essere pubblico o privato.
2. Carica questi file nel repository. Da terminale:
   ```bash
   git init
   git add .
   git commit -m "Initial site"
   git branch -M main
   git remote add origin https://github.com/TUO-UTENTE/cti-site.git
   git push -u origin main
   ```
   In alternativa puoi trascinare i file nell'interfaccia web di GitHub ("Add file → Upload files").
3. Nel repository vai su **Settings → Pages**.
4. Sotto **Build and deployment → Source**, scegli **GitHub Actions**.
5. Fatto: ad ogni `push` sul branch `main`, il workflow `.github/workflows/hugo.yml`
   compila il sito e lo pubblica. Lo stato lo vedi nella tab **Actions**.

Il primo deploy richiede 1–2 minuti. Il sito sarà raggiungibile su
`https://TUO-UTENTE.github.io/cti-site/` finché non colleghi il dominio (passo 3).

---

## 3. Collegare il dominio `cti.al`

### 3a. Su GitHub
**Settings → Pages → Custom domain** → scrivi `cti.al` → **Save**.
Poi spunta **Enforce HTTPS** (potrebbe diventare disponibile dopo qualche minuto,
una volta emesso il certificato).

### 3b. Sul tuo registrar (dove hai comprato cti.al)
`cti.al` è un dominio *apex* (senza sottodominio), quindi servono i **record A**.
Crea questi 4 record A (Nome/Host `@`, valori = IP di GitHub Pages):

```
A   @   185.199.108.153
A   @   185.199.109.153
A   @   185.199.110.153
A   @   185.199.111.153
```

(Opzionale, per IPv6, aggiungi anche i record AAAA su `@`:)

```
AAAA  @  2606:50c0:8000::153
AAAA  @  2606:50c0:8001::153
AAAA  @  2606:50c0:8002::153
AAAA  @  2606:50c0:8003::153
```

(Opzionale, per far funzionare anche `www.cti.al`:)

```
CNAME  www  TUO-UTENTE.github.io
```

La propagazione DNS può richiedere da pochi minuti fino a 24 ore. Verifica con:
```bash
dig cti.al +noall +answer -t A
```
Devono comparire i 4 IP sopra. Questi IP sono quelli ufficiali correnti di GitHub
Pages — se in futuro non funzionasse, ricontrolla la pagina "Managing a custom
domain" nella documentazione GitHub.

> Il file `static/CNAME` (contiene `cti.al`) fa sì che il dominio resti impostato ad
> ogni deploy. Non rimuoverlo.

---

## 4. Aggiungere un articolo

Crea un file `.md` in `content/posts/`, ad esempio `content/posts/mio-articolo.md`:

```markdown
---
title: "Titolo dell'articolo"
date: 2026-06-01
description: "Breve descrizione che compare nella lista e nei meta."
tags: ["tag1", "tag2"]
---

Il contenuto in **Markdown**.
```

Fai `commit` e `push`: il sito si ricompila da solo.
Le sezioni `posts` e `disclosures` funzionano allo stesso modo (un file `.md` per pagina).

---

## 5. Personalizzazione rapida

- **Titolo del sito e link social**: `config/_default/languages.en.toml`
  (modifica `title`, e gli URL `bluesky` / `mastodon` / `github`).
- **Voci del menu**: `config/_default/menus.en.toml`.
- **Colori / aspetto**: `config/_default/params.toml`
  - `colorScheme` — `slate` (grigio, impostato di default), oppure `congo`, `ocean`,
    `sapphire`, `fire`, `cherry`, `avocado`.
  - `defaultAppearance` — `dark` o `light`; `autoSwitchAppearance` segue il sistema.
- Tutte le opzioni del tema sono documentate qui:
  https://jpanther.github.io/congo/docs/configuration/

---

## 6. Anteprima in locale (opzionale)

Serve **Hugo (versione extended ≥ 0.146)**. Installazione:
- macOS: `brew install hugo`
- Windows: `winget install Hugo.Hugo.Extended`
- Linux: scarica il `.deb`/binario "extended" da https://github.com/gohugoio/hugo/releases

Poi, nella cartella del progetto:
```bash
hugo server
```
Apri http://localhost:1313 . Il sito si aggiorna in tempo reale mentre modifichi i file.

---

## Note

- Il tema Congo è incluso (licenza MIT). Per aggiornarlo in futuro puoi sostituire la
  cartella `themes/congo/` con una versione più recente dal repository ufficiale.
- I contenuti in `content/posts/` sono esempi: sostituiscili con i tuoi.

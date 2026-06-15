# Veebipood

Veebipood on Node.js ja Express.js põhine REST API rakendus, mis võimaldab kasutajatel sisse logida, vaadata tooteid, otsida tooteid kategooriate järgi ning luua ja hallata tellimusi.

Kõik andmed hoitakse rakenduse töö ajal mälus, eraldi andmebaasi ei kasutata.

## Tehnoloogiad

* Node.js
* Express.js
* JavaScript
* CORS
* REST API
* GitHub Actions
* HTML (lihtne kasutajaliides)

## Käivitamine

### Paigalda sõltuvused

```bash
npm install
```

### Käivita server

```bash
npm start
```

või

```bash
node src/server.js
```

Server käivitub aadressil:

```text
http://localhost:3000
```

### Käivita automaattestid

```bash
npm test
```

või

```bash
node src/test.js
```

## Testikasutajad

| Kasutajanimi | Parool | Nimi          |
| ------------ | ------ | ------------- |
| mari         | 1234   | Mari Maasikas |
| jaan         | 1234   | Jaan Jansen   |

## Teadaolevad vead

Rakenduses oli kaks viga, mis tuli parandada:

1. `src/routes/products.js` – toodete otsing kasutas valet andmekogu.
2. `src/routes/orders.js` – tellimuse algne staatus oli vale.

## API endpointid

### Kasutajad

| Meetod | URL               | Kirjeldus                               |
| ------ | ----------------- | --------------------------------------- |
| POST   | /api/users/signup | Uue kasutaja registreerimine            |
| POST   | /api/users/login  | Kasutaja sisselogimine                  |
| POST   | /api/users/logout | Kasutaja väljalogimine                  |
| GET    | /api/users/me     | Sisselogitud kasutaja andmete vaatamine |

### Tooted

| Meetod | URL                         | Kirjeldus                           |
| ------ | --------------------------- | ----------------------------------- |
| GET    | /api/products               | Kõigi toodete nimekiri              |
| GET    | /api/products/:id           | Toote vaatamine ID järgi            |
| GET    | /api/products/search        | Toodete otsimine nime järgi         |
| GET    | /api/products/categories    | Kõigi kategooriate nimekiri         |
| GET    | /api/products/category/:cat | Kindla kategooria toodete vaatamine |

### Tellimused

| Meetod | URL                    | Kirjeldus                                  |
| ------ | ---------------------- | ------------------------------------------ |
| POST   | /api/orders            | Uue tellimuse loomine                      |
| GET    | /api/orders            | Kõigi tellimuste vaatamine                 |
| GET    | /api/orders/me         | Sisselogitud kasutaja tellimuste vaatamine |
| GET    | /api/orders/:id        | Tellimuse vaatamine ID järgi               |
| PATCH  | /api/orders/:id/status | Tellimuse staatuse muutmine                |

### Statistika

| Meetod | URL        | Kirjeldus               |
| ------ | ---------- | ----------------------- |
| GET    | /api/stats | Rakenduse statistika    |
| GET    | /health    | Serveri tervisekontroll |

## Arhitektuur

Rakendus kasutab kihilist (Layered Architecture) arhitektuuri.

Struktuur:

* `server.js` – rakenduse käivitamine ja marsruutide ühendamine.
* `routes/` – API endpointide loogika.
* `data.js` – andmete hoidmine mälus.
* `public/` – staatilised failid.

Selline arhitektuur muudab koodi lihtsamini loetavaks, testitavaks ja hooldatavaks.

## GitHub Actions

GitHub Actions käivitub automaatselt iga push'i ja pull request'i korral.

Automaatne töövoog:

1. Laetakse projekt GitHubist.
2. Paigaldatakse sõltuvused (`npm install`).
3. Käivitatakse rakendus.
4. Käivitatakse automaattestid (`npm test`).
5. Kontrollitakse, et kõik testid läbiksid edukalt.

See aitab tagada koodi kvaliteedi ning avastada vead enne muudatuste ühendamist põhiharusse.

## Arhitektuuri analüüs

### Millist arhitektuuri rakendus kasutab?

Rakendus kasutab **monoliitset klient-server arhitektuuri**.

See tähendab, et kogu serveri loogika töötab ühes Node.js rakenduses ning klient saadab serverile päringuid API kaudu.

### Mille põhjal sellisele järeldusele jõudsin?

Seda on näha projekti struktuurist.

* `server.js` käivitab kogu rakenduse.
* Kaustas `routes` on erinevad API osad (kasutajad, tooted, tellimused).
* Kõik andmed asuvad ühes failis `data.js`.
* Kõik osad töötavad koos ühes rakenduses.

Rakendus ei ole jagatud eraldi teenusteks, seega on tegemist monoliitse lahendusega.

### Miks on see arhitektuur siin hea valik?

See projekt on suhteliselt väike ja lihtne.

Monoliitset rakendust on:

* lihtne arendada;
* lihtne testida;
* lihtne käivitada;
* lihtne parandada, kui tekivad vead.

Õppeprojekti jaoks on see kõige mugavam lahendus.

### Millist arhitektuuri kasutaksin siis, kui rakendusel oleks 1 miljon kasutajat?

Sellisel juhul kasutaksin **mikroteenuste arhitektuuri**.

Näiteks oleks eraldi teenused:

* kasutajate jaoks;
* toodete jaoks;
* tellimuste jaoks.

Nii saaks iga teenust eraldi uuendada ja vajadusel rohkem servereid lisada.

See muudaks süsteemi kiiremaks, töökindlamaks ja paremini skaleeritavaks suure kasutajate arvu korral.


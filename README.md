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

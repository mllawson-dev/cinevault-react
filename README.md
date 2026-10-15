# CineVault

A film-discovery and watchlist app: browse curated collections or search the OMDb catalogue, read a film's details, and save it to a watchlist without creating an account.

**[Live site](https://cinevault-mll.vercel.app/)** · **[Case study](https://www.mll-creativeeng.com/case-studies/cinevault/)**

CineVault started as my final project for the Frontend Simplified React course. I then rebuilt it on Vite and refined the interface, data handling and accessibility for my portfolio.

## Engineering

- **Server-side API key.** The browser calls `/api/movies`; `server/movies.mjs` adds the OMDb key on the server, so no credential ships to the client. The same handler runs as a Vercel function (`api/movies.js`) and as Vite dev middleware.
- **Resilient requests.** Inputs are validated, upstream calls time out, identical concurrent requests are shared, and responses are cached for five minutes.
- **Superseded searches are cancelled.** Collection enrichment runs four requests at a time and keeps the films that succeed if others fail.
- **State.** React Context separates discovery, watchlist and theme. Watchlist and theme persist in the browser, with an in-memory fallback.
- **Accessible dialogs.** Native `<dialog>` elements contain focus and return it to the control that opened them.

## Quality checks

```sh
npm test        # Node test runner: 8 server and data tests
npm run build
```

## Run locally

Requires Node 22.12+ and a free [OMDb API key](https://www.omdbapi.com/apikey.aspx).

```sh
npm ci
cp .env.example .env.local   # then add your key to OMDB_API_KEY
npm start                    # http://127.0.0.1:4181/
```

To deploy on Vercel, set `OMDB_API_KEY` as an environment variable (no `VITE_` prefix).

## Scope

Film data and posters come from OMDb. CineVault is not affiliated with IMDb or any streaming service. There are no accounts or cross-device sync; trailer links open YouTube searches.

---

Designed and built by **Michael L. Lawson**, design engineer and creative developer · [mll-creativeeng.com](https://www.mll-creativeeng.com) · [LinkedIn](https://www.linkedin.com/in/michael-lawson-a7707924)

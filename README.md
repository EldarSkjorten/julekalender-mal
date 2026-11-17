# Julekalender (mal)

Nettside med 24 luker. Hver luke har en kort tekst og knapper til Apple Music og Spotify (tom lenke skjuler knappen).
Ren HTML, CSS og JavaScript. Ingen innlogging for mottakerne, ingen sporing og ingen byggesteg.

## Lag din egen kalender

1. Trykk **Use this template → Create a new repository** øverst på denne siden, og velg **Private**. Tekstene dine blir personlige, og et offentlig prosjekt kan leses av alle.
2. Følg [`docs/oppsett.md`](docs/oppsett.md) én gang: publisering og innstillingene i editoren.
3. Hver jul: følg [`docs/veiledning.md`](docs/veiledning.md).

⚠️ Året står i `site/data/days.json` (feltet `year`), ikke i koden. Er det feil eller mangler, står lukene låst.

## Mapper

| Mappe        | Innhold                                                          |
| ------------ | ---------------------------------------------------------------- |
| `site/`      | Selve kalenderen. **Bare denne mappen publiseres.**              |
| `site/data/` | `days.json`: året, tekster og lenker for de 24 lukene            |
| `editor/`    | Redigeringssiden. Åpnes lokalt, publiseres aldri.                |
| `arkiv/`     | Arkivkopier av tidligere kalendere (`days-ÅÅÅÅ.json`). Publiseres ikke. |
| `docs/`      | Veiledning (`veiledning.md`) og engangsoppsett (`oppsett.md`). Publiseres ikke. |

## Slik åpnes og låses lukene

Tider i norsk tid. For en kalender med `"year": 2026` (eksempel):

| Dato                       | Hva skjer                                                  |
| -------------------------- | ---------------------------------------------------------- |
| Før 1. desember 2026       | Alt er låst                                                |
| 1.–24. desember 2026       | Luke n åpnes når datoen er n. desember                     |
| 25. desember – 31. januar  | Alle åpnede luker er fortsatt åpne                         |
| Fra 1. februar 2027        | Alt er låst igjen, med melding om at kalenderen er stengt  |
| Desember 2027 og senere    | Fortsatt låst, fordi dette er 2026-kalenderen              |

## Testmodus

Legg til `?test` i adressen, for eksempel `.../?test`. Alle luker åpnes, en oransje markør viser at du er i testmodus og hvilket år kalenderen er satt til,
og en rød advarsel vises hvis året i `days.json` mangler eller ikke passer med dagens dato.

## Format på `days.json`

```json
{ "year": 2026, "title": "…", "subtitle": "…", "info": "…", "days": [ { "title": "", "text": "", "apple": "", "spotify": "" } ] }
```

- `title` er overskriften (tom gir «Julekalender»), `subtitle` står under den (tom skjules), `info` vises bak «i»-knappen (tom skjuler knappen).
- Hver luke har `title`, `text`, `apple` og `spotify`. Tom streng i `apple` eller `spotify` skjuler knappen. Er luketittelen tom, vises «N. desember».
- Ukjente felt bevares av editoren, så formatet kan utvides.

## Lisens

Koden: MIT, se [`LICENSE`](LICENSE). Fonten Mountains of Christmas (Tart Workshop): Apache 2.0, se `site/fonts/LICENSE-font.txt`.

# Engangsoppsett

Dette gjør du **én gang**, før kalenderen tas i bruk. Etterpå trenger du bare [veiledningen](veiledning.md) hver jul.

> [!NOTE]
> **Vercel og Domeneshop er bare eksempler.** Andre tjenester for statiske nettsider og andre domeneleverandører fungerer også. Det viktige er at bare mappen `site/` publiseres.

> [!WARNING]
> Menyer og knapper hos GitHub, Vercel og domeneleverandøren kan ha endret navn siden dette ble skrevet. Følg det som står på skjermen, og bruk denne siden som fremgangsmåte.

## Innhold

1. [Hva du trenger](#1-hva-du-trenger)
2. [Ditt eget prosjekt på GitHub](#2-ditt-eget-prosjekt-på-github)
3. [Publisering med Vercel](#3-publisering-med-vercel)
4. [Tilpass editoren](#4-tilpass-editoren)
5. [Eget domene (valgfritt)](#5-eget-domene-valgfritt)
6. [Sikkerhet](#6-sikkerhet)
7. [Kostnad og grenser](#7-kostnad-og-grenser)
8. [Flere kalendere](#8-flere-kalendere)

## 1. Hva du trenger

- En konto på **GitHub** (gratis). Der ligger prosjektet, og der bytter du innholdet hvert år.
- En tjeneste som **publiserer** kalenderen på en nettadresse. Her beskrives **Vercel** (gratis for personlig bruk), som henter filene fra GitHub av seg selv. Kalenderen er vanlige filer uten byggesteg, så andre tjenester for statiske nettsider fungerer også.
- Eventuelt et **eget domene**. Uten det får kalenderen en adresse som slutter på `.vercel.app`.

## 2. Ditt eget prosjekt på GitHub

1. Lag et nytt prosjekt (repo) på GitHub med filene fra denne kalenderen. Kommer du fra en mal, trykker du **Use this template** eller kopierer mappene `site`, `editor`, `docs` og `arkiv` inn i et nytt prosjekt.
2. **Gjør prosjektet privat** hvis tekstene dine er personlige. Et offentlig prosjekt kan leses av alle, også historikken.
3. Slå på tofaktor (to-trinns innlogging) på GitHub-kontoen: **Settings → Password and authentication**.

> [!NOTE]
> Kalenderen bruker ingen passord eller nøkler, så det er ingenting hemmelig i filene. Det private gjelder bare tekstene dine.

## 3. Publisering med Vercel

1. Gå til **vercel.com** og logg inn med GitHub-kontoen.
2. Velg **Add New… → Project**.
3. Under **Import Git Repository** finner du prosjektet ditt. Står det ikke der, velger du å justere GitHub-tilgangen og gir Vercel tilgang til akkurat dette prosjektet («Only select repositories»).
4. Under **Configure Project** setter du:
   - **Project Name:** for eksempel `julekalender`. Det blir en del av testadressen.
   - **Framework Preset:** `Other`.
   - **Root Directory:** trykk **Edit** og velg `site`. **Dette er viktig:** da publiseres bare mappen `site/`, og aldri editoren, veiledningen eller arkivet.
   - **Build Command** og **Output Directory:** la stå tomme. Kalenderen trenger ingen bygging.
5. Trykk **Deploy**. Etter omtrent et halvt minutt får du en adresse som slutter på `.vercel.app`. Det er **testadressen**. Åpne den med `?test` på slutten.
6. Kontroller i prosjektet hos Vercel at **Settings → Git → Production Branch** er `main`, og at **Settings → General → Root Directory** er `site`.

Fra nå av oppdateres kalenderen av seg selv hver gang `main` endres på GitHub.

**Dette kan du hoppe over** på siden Vercel viser etter publiseringen:

- **Make your agent a Vercel expert:** en ferdig tekst som limes inn i et kodeverktøy. Kalenderen trenger ikke det, og det gir et verktøy mer tilgang til Vercel-kontoen enn nødvendig.
- **Enable Speed Insights:** legger til måling av besøkende. Kalenderen har bevisst ingen sporing.
- **Add Domain:** det gjør du først i [kapittel 5](#5-eget-domene-valgfritt), når testadressen virker.

## 4. Tilpass editoren

Øverst i skriptet i `editor/index.html` er det noen få innstillinger, under overskriften **Innstillinger**. Du kan endre dem rett på GitHub: åpne filen, trykk blyanten, endre teksten mellom de enkle anførselstegnene, og trykk **Commit changes**.

| Innstilling | Hva den gjør | Eksempel |
| --- | --- | --- |
| `GITHUB_REPO` | Ditt prosjekt på GitHub. Gir editoren lenker rett til `days.json`, til arkivmappen og til denne veiledningen. Tom gir ingen GitHub-lenker. | `'brukernavn/julekalender'` |
| `CALENDAR_URL` | Adressen til den publiserte kalenderen, med `/` til slutt. Gir lenka **kalenderen i testmodus** i editoren. | `'https://jul.eksempel.no/'` |
| `GREETING_NAME` | Navnet i en liten hilsen i editoren. Tom gir en hilsen uten navn. | `'Kari'` |
| `DEVICE_NOTE` | Viser en melding om at editoren er laget for datamaskin når den åpnes på mobil eller nettbrett. | `true` |

I kalenderen (`site/index.html`) kan du velge stjernestøvet som vises når kalenderen åpnes: `STARDUST_DEFAULT` er `'stjerne'`, `'punkter'` eller `'av'`.

Etter en endring laster du ned editoren på nytt (se [veiledningen](veiledning.md#hent-editoren-til-maskinen-din)).

## 5. Eget domene (valgfritt)

Gjøres når testadressen virker. Eksempelet bruker underadressen `jul.eksempel.no` og domeneleverandøren Domeneshop. Hos andre leverandører heter menyene noe annet, men stegene er de samme.

1. **Hos Vercel:** åpne prosjektet, velg **Domains** (eller Settings → Domains) og trykk **Add Existing**. Du eier allerede domenet, så velg ikke «Buy». Skriv hele underadressen, for eksempel `jul.eksempel.no`, og la den høre til **Production**.
2. Vercel viser «Invalid Configuration» og en oppføring under fanen **DNS Records**: type **CNAME**, navn `jul` og en lang verdi som er unik for prosjektet. Kopier verdien med kopieringsikonet, ikke ved å skrive den av. Fanen **Vercel DNS** handler om å flytte hele domenet til Vercel, og skal ikke brukes.
3. **Hos domeneleverandøren** (Domeneshop: logg inn, **Mine domener**, velg domenet og fanen **DNS-pekere**): se på oppføringene som står der fra før, for eksempel for e-post, og **ikke endre eller slett noe**.
4. Legg til en ny oppføring med vertsnavn `jul` og verdien fra Vercel. Hos Domeneshop skriver du i den ledige linja nederst og trykker det grønne plusset, og en CNAME lages av seg selv. Slutter verdien på et punktum og leverandøren avviser det, tar du bort punktumet. Etterpå skal verdien i listen **ikke** ha ditt eget domene bakerst.
5. **Tilbake hos Vercel:** trykk **Refresh** ved domenet. Når det står at oppsettet er gyldig, er adressen klar. Det tar fra noen minutter til noen timer. Sikker forbindelse (https) ordnes automatisk.
6. Sett den nye adressen i `CALENDAR_URL` i editoren ([kapittel 4](#4-tilpass-editoren)).

> [!NOTE]
> **Hvorfor en underadresse (`jul.eksempel.no`) og ikke en mappe (`eksempel.no/jul`)?** I en nettadresse er `eksempel.no` hvilken tjener som svarer, og `/jul` er hvilken side den viser. Hos domeneleverandøren styrer du bare navnet, så en underadresse trenger bare én DNS-oppføring. En mappe krever at hele domenet ligger hos en tjeneste som sender `/jul` videre til kalenderen, eller et webhotell. Kalenderen virker også fra en mappe, så det kan gjøres senere.

## 6. Sikkerhet

- Tofaktor på GitHub, Vercel og hos domeneleverandøren.
- Bare `site/` publiseres (Root Directory i [kapittel 3](#3-publisering-med-vercel)).
- Kalenderen har ingen innlogging, ingen cookies og ingen sporing, og fonten ligger i selve siden. Den henter ingenting fra andre tjenester når noen åpner den. Apple og Spotify kontaktes først når en mottaker trykker på knappene.
- Adressen er åpen for alle som har lenka, og siden ber søkemotorer om ikke å vise den. Del lenka bare med dem den er til.

## 7. Kostnad og grenser

- Vercels gratisplan («Hobby») koster ingenting og er til personlig, ikke-kommersiell bruk.
- Grensene gjelder hele kontoen, ikke hvert prosjekt. Da dette ble skrevet var de 100 GB overføring og 1 million forespørsler i måneden, 200 prosjekter, 50 domener per prosjekt og 100 publiseringer i døgnet. En kalender bruker en liten brøkdel av dette.
- Overskrides en grense, blir du ikke belastet, men tjenesten pauses i inntil 30 dager. Sjekk **Usage** hos Vercel av og til.
- Et eget domene koster det domeneleverandøren tar.

## 8. Flere kalendere

Skal du lage en kalender til noen andre, lager du et eget, nytt prosjekt på GitHub med de samme mappene, og følger denne siden på nytt for det prosjektet. Tittel, undertekst, info-tekst og alle luker endrer du i editoren. Husk å endre innstillingene i [kapittel 4](#4-tilpass-editoren).

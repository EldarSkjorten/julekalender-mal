# Veiledning for julekalenderen

Steg for steg, for deg som lager kalenderen hver jul. Du trenger ikke kunne programmering.

> [!IMPORTANT]
> **Første gang?** Kalenderen må settes opp én gang før den kan brukes: et prosjekt på GitHub, en tjeneste som publiserer den, og eventuelt et eget domene. Det står i [Engangsoppsett](oppsett.md). Denne veiledningen er for det du gjør hvert år etter det.

**Fargeboksene:** blå er forklaring, grønn er tips, gul er noe du bør passe på, og lilla er noe du må vite først.

## Innhold

1. [Oversikt: hva er hva?](#1-oversikt-hva-er-hva)
2. [Hver jul: lag kalenderen](#2-hver-jul-lag-kalenderen)
3. [Legg filen ut, slik at kalenderen oppdateres](#3-legg-filen-ut-slik-at-kalenderen-oppdateres)
4. [Test før du deler lenka](#4-test-før-du-deler-lenka)
5. [Neste år: gjenbruk, arkiv og tidligere versjoner](#5-neste-år-gjenbruk-arkiv-og-tidligere-versjoner)
6. [Hvis noe går galt](#6-hvis-noe-går-galt)
7. [Ordliste](#7-ordliste)

## 1. Oversikt: hva er hva?

Prosjektet har tre deler du trenger å kjenne til:

- **Editoren** (`editor/index.html`): verkstedet ditt. Her skriver du tekstene og legger inn lenkene. Den åpnes på din egen maskin og publiseres aldri.
- **Kalenderen** (mappen `site/`): det mottakerne ser. Dette er det eneste som legges ut på nettet.
- **Innholdet** (`site/data/days.json`): én fil som binder de to sammen. Editoren lager den, og kalenderen leser den. Den inneholder kalenderåret, tittel, undertekst, info-tekst og alle 24 luker.

**Veien fra editor til mottaker:** Editoren → `days.json` → prosjektet på GitHub → publiseringstjenesten (for eksempel Vercel) → nettadressen → mottakerne.

**To filnavn å kjenne til:**

- `days.json` er filen kalenderen bruker. Den skal **alltid** hete akkurat det, uten årstall, ellers finner ikke kalenderen den.
- `days-ÅÅÅÅ.json` (for eksempel med årstallet for i år) er en **arkivkopi** med samme innhold. Årstallet i navnet gjør at du kan ta vare på flere år side om side. Den brukes ikke av kalenderen. Se [kapittel 5](#5-neste-år-gjenbruk-arkiv-og-tidligere-versjoner).

Alt du skriver i editoren lagres automatisk som utkast i nettleseren din. Først når du eksporterer og legger filen ut, ser mottakerne det.

> [!NOTE]
> **Hvorfor kan ikke editoren lagre rett til kalenderen?** En nettside kan av sikkerhetsgrunner ikke skrive til filer på maskinen din eller endre noe på nettet på egen hånd. Det er også en bevisst sperre her: editoren skal aldri kunne endre den publiserte kalenderen. Derfor er det et lite mellomsteg, som veiledningen tar deg gjennom.

## 2. Hver jul: lag kalenderen

> [!NOTE]
> **Bruk en datamaskin.** Editoren er laget for Mac eller PC. På mobil og nettbrett kan den åpnes, men det er ikke testet ordentlig: utkastet lagres bare i den nettleseren du bruker, og filer og nedlasting er tungvint. Selve kalenderen virker fint på alle enheter.

### Hent editoren til maskinen din

Editoren ligger i prosjektet ditt på GitHub. Den må ligge på maskinen din for å kunne åpnes. Velg én av måtene:

- **Last ned som ZIP (enklest):** åpne prosjektet på github.com, trykk den grønne knappen **Code** og velg **Download ZIP**. Dobbeltklikk ZIP-filen for å pakke den ut. Har editoren blitt oppdatert siden sist, laster du ned på nytt på samme måte.
- **GitHub Desktop (hvis du bruker det):** første gang velger du **File → Clone Repository…**, finner prosjektet og velger en mappe. Senere trykker du **Fetch origin** og så **Pull origin**, så har du alltid nyeste versjon i samme mappe.

> [!WARNING]
> **Utkastet ligger i nettleseren, ikke i mappen.** I noen nettlesere er det også knyttet til hvor filen ligger. Bruk derfor samme nettleser, og pakk ut en ny ZIP til samme sted som den gamle (erstatt mappen), så finner editoren utkastet igjen. Er du usikker, eksporterer du før du bytter, og bruker <kbd>Importer</kbd> etterpå.

### Lag kalenderen

1. **Åpne editoren.** I mappen fra ZIP-filen eller GitHub Desktop åpner du mappen `editor` og dobbeltklikker på `index.html`. Den åpnes i nettleseren (Safari, Chrome, Edge eller Firefox). Lag gjerne et bokmerke.

2. **Sjekk kalenderåret.** Feltet **Kalenderår** øverst bestemmer når lukene åpnes: luke 1 åpnes 1. desember det året, og alle luker står åpne til og med 31. januar året etter.
   Editoren regner ut hvilket år dagens dato hører til: fra 1. februar til 31. desember er det inneværende år, og i januar er det fjorårets (den kalenderen står fortsatt åpen). Er utkastet ditt laget for et **annet** år enn dette, for eksempel når du åpner fjorårets utkast en ny høst, kommer det opp en oransje boks med to valg:
   - <kbd>Bruk nåværende innhold som utgangspunkt for neste kalender</kbd>: beholder alt og bytter bare året. Passer når mye skal være som før.
   - <kbd>Start ny, tom kalender</kbd>: tømmer alle luker og bytter året. Tittel, undertekst og info-tekst beholdes. Passer når alt skal byttes ut.

   Begge kan angres rett etterpå. Lager du kalenderen samme år som utkastet gjelder, for eksempel første gang, kommer ingen boks. Da sjekker du bare at året stemmer.

3. **Fyll ut «Om kalenderen».** Tittel (tom gir «Julekalender»), undertekst, og info-tekst som vises bak «i»-knappen. Rett under tittel og undertekst ser du hvordan toppen av kalenderen blir. Tom undertekst skjules, og tom info-tekst skjuler «i»-knappen. <kbd>Forhåndsvis info</kbd> viser info-vinduet.

4. **Fyll ut lukene.** For hver luke skriver du en tekst og limer inn lenker til Apple Music og Spotify. Lenkene kontrolleres mens du skriver, og låtnavnet vises når det lar seg slå opp. Er en lenke tom, skjules knappen i kalenderen. Hver luke får en status:
   - **Tom**: ingenting skrevet.
   - **Påbegynt**: noe er skrevet, men tekst eller lenke mangler.
   - **Klar**: tekst og minst én lenke uten feil.
   - **Sjekk**: noe bør ses på, for eksempel en lenke til feil type, to ulike låter, eller samme låt i to luker.

   Rutene øverst viser alle 24 og hopper til luka. Rødt betyr at en lenke ikke kan virke. Oransje betyr at du bør sjekke selv.

   **Slik kan tekstene se ut:** en tom linje gir nytt avsnitt, og et vanlig linjeskift gir ny linje i samme avsnitt. Emoji virker. I tillegg kan du bruke enkel formatering:

   | Du skriver | Det blir |
   | --- | --- |
   | `**fet skrift**` | **fet skrift** |
   | `*kursiv*` | *kursiv* |
   | `[les mer](https://eksempel.no/side)` | en lenke med teksten «les mer» |
   | `https://eksempel.no/side` | adressen som klikkbar lenke |

   Lenker åpnes i en ny fane, og bare adresser som starter med `http://` eller `https://` blir lenker. Annen kode i teksten vises bare som tekst. Lenkene til musikken legger du fortsatt i lenkefeltene, så blir de knapper. Det samme gjelder info-teksten, og <kbd>Forhåndsvis</kbd> viser hvordan det blir.

5. **Forhåndsvis.** Trykk <kbd>Forhåndsvis</kbd> på en luke for å se den slik mottakeren ser den.

6. **Eksporter.** Trykk <kbd>Eksporter days.json</kbd> øverst til høyre. Vinduet sier hva som eventuelt mangler, og du velger hvordan filen skal videre (se [kapittel 3](#3-legg-filen-ut-slik-at-kalenderen-oppdateres)):
   - <kbd>Kopier innholdet</kbd>: kopierer hele filen, til å lime inn på GitHub (enklest).
   - <kbd>Last ned begge filene</kbd>: laster ned `days.json` og arkivkopien `days-ÅÅÅÅ.json`.
   - <kbd>Bare days.json</kbd> og <kbd>Bare arkivkopi</kbd>: hver for seg.

> [!TIP]
> Utkastet ligger igjen i editoren mellom øktene. Har du bare noen få endringer, åpner du editoren, endrer dem og eksporterer på nytt. Eksporter gjerne innimellom mens du jobber, så har du en kopi i en fil.

## 3. Legg filen ut, slik at kalenderen oppdateres

Kalenderen leser `site/data/days.json` i prosjektet på GitHub. Skal innholdet endres, må den filen byttes ut der. Når den er byttet, publiserer publiseringstjenesten (for eksempel Vercel) den nye versjonen av seg selv, vanligvis i løpet av ett minutt.

### Måte A: direkte på GitHubs nettsider (enklest, ingen programmer)

1. I editoren: trykk <kbd>Eksporter days.json</kbd>, deretter <kbd>Kopier innholdet</kbd>.
2. Trykk lenka **days.json på GitHub** i eksportvinduet. Du må være logget inn på GitHub. (Uten lenka: åpne `site/data/days.json` i prosjektet ditt på github.com og trykk blyanten for å redigere.)
3. Klikk inni tekstfeltet, merk alt (<kbd>Cmd</kbd>+<kbd>A</kbd> på Mac, <kbd>Ctrl</kbd>+<kbd>A</kbd> på Windows) og lim inn (<kbd>Cmd</kbd>+<kbd>V</kbd> eller <kbd>Ctrl</kbd>+<kbd>V</kbd>). Nå er den gamle teksten byttet ut.
4. Trykk den grønne knappen **Commit changes…** øverst til høyre. Skriv gjerne en kort beskrivelse, for eksempel «Ny kalender». Velg **Commit directly to the main branch** og trykk **Commit changes**.
5. Vent et minutt og gå videre til [testing](#4-test-før-du-deler-lenka).

> [!TIP]
> **Trygg variant:** i punkt 4 kan du i stedet velge **Create a new branch** og trykke **Propose changes**. Vercel lager da en egen testadresse for denne versjonen (den kan bare åpnes når du er logget inn på Vercel). Du tester der, og trykker **Merge pull request** på GitHub når du er fornøyd. Først da blir den publisert for mottakerne.

### Måte B: fra prosjektmappen på maskinen (GitHub Desktop)

1. Hent nyeste versjon først: **Fetch origin**, så **Pull origin**.
2. I editoren: <kbd>Eksporter days.json</kbd>, <kbd>Last ned begge filene</kbd>.
3. Flytt `days.json` fra Nedlastinger til `site/data/` i prosjektmappen og velg å erstatte den gamle.
4. Legg gjerne arkivkopien `days-ÅÅÅÅ.json` i mappen `arkiv/` (se [kapittel 5](#5-neste-år-gjenbruk-arkiv-og-tidligere-versjoner)).
5. I GitHub Desktop: skriv en kort beskrivelse, trykk **Commit to main**, så **Push origin**.

## 4. Test før du deler lenka

1. Åpne kalenderens adresse med `?test` på slutten, for eksempel `https://jul.eksempel.no/?test`. Lenka **kalenderen i testmodus** i editoren («Slik lager du kalenderen for et nytt år», steg 4) gjør det for deg.
2. Øverst vises en oransje markør: **TESTMODUS – alle luker er åpne nå · kalender for ÅÅÅÅ**. Sjekk at året stemmer. Stemmer det ikke med dagens dato, kommer en rød advarsel.
3. Trykk deg gjennom lukene: er teksten riktig, og åpner knappene riktig låt? Gjør det gjerne også på telefonen.
4. Åpne adressen **uten** `?test`. Før 1. desember skal alle luker være låst, med meldingen «Velkommen tilbake 1. desember». Det er slik mottakerne ser den.
5. Er alt i orden, deler du lenka **uten** `?test`.

> [!NOTE]
> **Kalenderen kan ikke åpnes ved å dobbeltklikke på filen.** Editoren virker når du dobbeltklikker på den, men selve kalenderen må ligge på en nettadresse for å kunne lese `days.json`. Test den derfor der den er publisert. Åpner du den likevel fra mappen, står det en forklaring øverst i stedet for kalenderen.

> [!NOTE]
> **Editoren endrer ikke kalenderen av seg selv.** Kalenderen endres først når `days.json` er byttet ut på GitHub ([kapittel 3](#3-legg-filen-ut-slik-at-kalenderen-oppdateres)). Vil du se hvordan en luke og toppen blir før du publiserer, bruker du <kbd>Forhåndsvis</kbd> på luka og forhåndsvisningen under «Om kalenderen».

<details>
<summary><b>Valgfritt: se hele kalenderen på din egen maskin, uten å publisere</b></summary>

Legg den eksporterte `days.json` i `site/data/` i din lokale kopi (den erstatter den som ligger der), og start en liten lokal nettjener fra mappen `site`. Det endrer ikke GitHub eller den publiserte kalenderen.

- **Mac:** åpne Terminal, skriv `cd ` (med mellomrom), dra mappen `site` inn i vinduet og trykk Enter. Skriv deretter `python3 -m http.server 8000` og trykk Enter. Mac-en kan spørre om å installere kommandolinjeverktøy første gang.
- **Windows:** åpne PowerShell i mappen `site` (høyreklikk i mappen mens du holder Shift) og skriv `py -m http.server 8000`. Det krever at Python er installert.
- Åpne `http://localhost:8000/?test` i nettleseren. Stopp nettjeneren med <kbd>Ctrl</kbd>+<kbd>C</kbd>.

Dette er ikke prøvd på alle maskiner. Fungerer det ikke, er det enklest å teste på den publiserte adressen.

</details>

## 5. Neste år: gjenbruk, arkiv og tidligere versjoner

### Bygge videre eller starte tomt

Når du åpner editoren en ny høst, ligger fjorårets utkast der fortsatt, og den oransje boksen spør hva du vil (se steg 2 i [kapittel 2](#2-hver-jul-lag-kalenderen)):

- **Bygge videre** (<kbd>Bruk nåværende innhold som utgangspunkt for neste kalender</kbd>) når mye skal være som før, for eksempel tittel, info-tekst eller noen av tekstene.
- **Starte tomt** (<kbd>Start ny, tom kalender</kbd>) når lukene skal fylles på nytt. Tittel, undertekst og info-tekst beholdes.
- Vil du tømme absolutt alt, også tittel og info-tekst, bruker du <kbd>Tøm hele kalenderen …</kbd> øverst i editoren. Året beholdes.

Alle tre spør først, og kan angres rett etterpå.

### Hvis utkastet er borte

Utkastet forsvinner hvis nettleserdata tømmes, eller hvis du bytter maskin eller nettleser. Trykk da <kbd>Importer</kbd> og velg en arkivkopi (`days-ÅÅÅÅ.json`) eller en `days.json` du har lastet ned. <kbd>?</kbd> ved siden av <kbd>Importer</kbd> forklarer knappen. Har du ingen fil, finner du den publiserte utgaven på GitHub (se under).

### Arkivkopier (valgfritt, gjør du selv)

En arkivkopi er filen `days-ÅÅÅÅ.json`, som lastes ned sammen med `days.json` når du eksporterer. Den har samme innhold, men årstallet i navnet gjør at årene kan ligge side om side og er lette å finne igjen. Kalenderen bruker den ikke.

Prosjektet har en mappe `arkiv/` til slike kopier. Eksportvinduet i editoren har en lenke som åpner opplastingen til den mappen på GitHub (velg filen og trykk **Commit changes**). Mappen publiseres ikke.

> [!WARNING]
> Arkivkopiene inneholder tekstene dine. Legg dem ikke i et offentlig prosjekt.

### Tidligere versjoner på GitHub (skjer av seg selv)

Dette er en funksjon i GitHub, ikke i kalenderen: hver gang `site/data/days.json` endres på GitHub, tar GitHub vare på den forrige utgaven. Åpne filen på github.com og velg **History** for å se alle utgavene og hente fram en gammel. Det skjer av seg selv, men utgavene er ordnet etter dato og ikke etter kalenderår, så arkivkopiene er enklere å finne fram i.

## 6. Hvis noe går galt

**Kalenderen viser «Oisann, det er noe feil her»**
Filen `days.json` mangler, er ødelagt, eller mangler året. Åpne kalenderen med `?test`: den røde advarselen forteller hva som er galt. Eksporter på nytt fra editoren og legg filen ut igjen.

**Alle luker er låst, men det er desember**
Året i `days.json` er feil. Sjekk feltet **Kalenderår** i editoren og eksporter på nytt. En kalender åpner bare lukene i desember det året den er laget for.

**Endringen vises ikke**
Vent et par minutter. Last siden på nytt med <kbd>Cmd</kbd>+<kbd>Shift</kbd>+<kbd>R</kbd> (Mac) eller <kbd>Ctrl</kbd>+<kbd>F5</kbd> (Windows). Sjekk hos publiseringstjenesten (hos Vercel: **Deployments**) at den siste publiseringen er ferdig.

**Lenkekontrollen i editoren viser ikke låtnavn**
Det er ikke en feil. Oppslagene hos Apple og Spotify virker ikke alltid, og da står det «Fikk ikke hentet navnet». Trykk **Åpne ↗** for å sjekke lenka selv. Kontrollen av selve lenka virker uansett.

**Nettleseren lastet bare ned én av to filer**
Nettleseren kan ha blokkert nummer to. Trykk <kbd>Bare arkivkopi</kbd>. Safari spør «Vil du tillate nedlastinger?» første gang: velg **Tillat**. Ombestemmer du deg, finner du det under **Safari → Innstillinger → Nettsteder → Nedlastinger**.

**Jeg har mistet utkastet i editoren**
Se [Hvis utkastet er borte](#hvis-utkastet-er-borte).

**Jeg publiserte noe feil**
Åpne `site/data/days.json` på GitHub, velg **History**, finn forrige utgave og lim den inn igjen som i kapittel 3. Eller importer den i editoren og eksporter på nytt.

## 7. Ordliste

- **Repo:** prosjektmappen din på GitHub, med alle filene og hele historikken.
- **Commit:** å lagre en endring på GitHub, med en kort beskrivelse.
- **Gren (branch):** en parallell kopi av prosjektet, brukt til å prøve noe uten å endre det som er publisert. Hovedgrenen heter `main`.
- **Publisering (deploy):** å legge ut en ny versjon av siden. Publiseringstjenesten (for eksempel Vercel) gjør det av seg selv etter hver endring i `main`.
- **Publiseringstjeneste (hosting):** tjenesten som viser nettsiden din på internett. For eksempel Vercel.
- **DNS og CNAME:** adresseoppføringer som sier hvor et domene peker. En CNAME kan føre for eksempel `jul.eksempel.no` til publiseringstjenesten.
- **JSON:** filformatet `days.json` bruker: ren tekst med faste felter. Du trenger ikke åpne den, men den kan leses i en tekstleser.

---

Denne veiledningen ligger i mappen `docs/` og publiseres ikke sammen med kalenderen.

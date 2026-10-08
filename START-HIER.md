# Green Saturday — openen in VS Code

Dit is de volledige broncode van het conceptprototype, inclusief app, styling, QR-scanner, API en databaseschema. Het is React/TypeScript met Vinext; er is geen los HTML-bestand dat je met Live Server kunt openen.

## Starten

1. Installeer Node.js 22.13 of hoger en VS Code.
2. Pak de ZIP uit. Open de map green-saturday-app in VS Code (File > Open Folder).
3. Open Terminal > New Terminal. Voer achtereenvolgens uit:

```sh
npx pnpm@11.25.0 install --frozen-lockfile
npm run build
node --import ./scripts/sites-env.mjs ./node_modules/wrangler/bin/wrangler.js d1 execute DB --local --config dist/server/wrangler.json --persist-to .wrangler/state --file drizzle/0000_clean_dreaming_celestial.sql
npm run dev
```

Open de localhost-URL die in de terminal verschijnt (standaard http://localhost:5173).
De databaseopdracht is alleen nodig bij de eerste installatie van deze database. De melding 'table already exists' betekent dat de tabellen al zijn aangemaakt; voer de opdracht dan niet opnieuw uit.

Als PowerShell npm.ps1 blokkeert, kies Command Prompt als terminalprofiel in VS Code.

## Later opnieuw starten

```sh
npm run dev
```

Stop met Ctrl+C. Je lokale gegevens staan in .wrangler/state en blijven bewaard. De online deelnemersgegevens worden niet meegeleverd of gewijzigd; lokaal gebruik je een aparte database.

## Waar verander ik iets?

- app/page.tsx: alle schermen, navigatie, knoppen en QR-scanner.
- app/globals.css: kleuren, lettergroottes en mobiele opmaak.
- lib/program.ts: voorbeeldworkshops en puntendoel.
- app/api/demo/route.ts: opslaan, inschrijven, toekennen van punten en boomtickets.
- db/schema.ts: databasetabellen.
- drizzle/: SQL om de tabellen aan te maken.
- app/layout.tsx: paginatitel en taal.
- public/favicon.svg: icoontje in het browsertabblad.

Let op: het prototype heeft 100 punten op meerdere plekken in de interface en API. Als je het spaardoel wijzigt, zoek projectbreed naar 100 en werk de relevante teksten en berekeningen bij.

## Testen

Maak een fictieve deelnemer, schrijf in voor alle drie workshops, wissel naar Organisatie en bevestig elke workshop via de persoonlijke QR-code of de testknop. Bij 100 punten verschijnt automatisch één boomticket. Dubbele bevestigingen leveren geen extra punten op.

De camera heeft browsertoestemming nodig. Camera werkt doorgaans op localhost of HTTPS; een telefoon die een onbeveiligd lokaal IP-adres opent krijgt mogelijk geen cameratoegang. De handmatige code-invoer blijft beschikbaar.

## Grenzen van deze versie

Dit is een conceptprototype met vrij wisselbare demodeelnemers en rollen. Het is niet geschikt voor echte persoonsgegevens of een publiek evenement zonder beveiligde medewerkers- en deelnemersaccounts. De boomtickets en locaties zijn demonstraties. Er is geen bevestigde gemeentelijke plantgarantie.

De oorspronkelijke versie heeft een geslaagde TypeScript-controle en productiebuild. De databasebeveiliging tegen dubbele punten en dubbele tickets is gecontroleerd. Installatie op jouw Windows-computer en camerascans op jouw telefoon zijn nog niet getest.

De ZIP bevat geen node_modules, database-inhoud, API-sleutels of inloggegevens. De benodigde pakketten worden bij installatie gedownload. Wijzigingen in VS Code veranderen de online versie niet automatisch.

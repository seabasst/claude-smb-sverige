---
name: moms-redovisning
description: Förbereder svensk momsdeklaration för aktuell momsperiod genom att hämta transaktioner ur Bokio, validera momskoder mot BAS-kontoplan, stämma av mot kontoutdrag, generera underlag för Skatteverkets eTjänst och flagga felaktiga eller saknade momskodningar. Använd den här skillen när användaren nämner "moms", "momsredovisning", "momsperiod", "momsdeklaration", "skattedeklaration", "moms till Skatteverket", "stäm av moms", "momskontroll", eller pratar om kvartalsvis eller månatlig momsperiod. Trigga också på meningar som "vad ska jag betala i moms", "är det moms snart", "förbered momsen", "kolla momsen för Q1/Q2/Q3/Q4". Skillen täcker både månads-, kvartals- och årsmoms, samt utgående moms (försäljning) och ingående moms (inköp) på samtliga svenska momssatser (25 %, 12 %, 6 %, 0 %).
---

# Moms-redovisning för svenska småföretag

Det här är en av de mest värdefulla återkommande uppgifterna för en svensk småföretagare. Felmoms är dyrt: rättning kostar tid, försenad inbetalning kostar ränta, och fel som upptäcks vid revision kan bli rejäla efterhandsbeskattningar.

## När skillen ska köras

- Användaren ber om momsförberedelse för en specifik period
- Användaren frågar "vad blir momsen" eller "hur mycket ska jag betala"
- Det är inom 14 dagar innan momsdeklarationens deadline
- Användaren laddar upp ett Bokio-export och vill ha hjälp att förstå

## Förutsättningar

- **Bokio MCP** måste vara installerad och autentiserad. Verifiera detta först.
- Om Bokio MCP saknas, säg det tydligt och hänvisa till `INSTALLATION.md`.

## Workflow

### Steg 1: Bekräfta period och bolag

Fråga om något är oklart:

- Vilket bolag (om användaren har flera i Bokio)?
- Vilken momsperiod (månad, kvartal, år)?
- Vilken specifik period (t.ex. Q1 2026, januari 2026, helår 2025)?

Är användaren osäker, kolla Bokios `companySettings` eller motsvarande för att se vilken momsperiod bolaget är registrerat för.

### Steg 2: Hämta data från Bokio

Använd Bokio MCP för att hämta:

- Alla bokföringsverifikat i perioden
- Konton enligt BAS-kontoplan, särskilt:
  - **2610–2627** (utgående moms)
  - **2640–2647** (ingående moms)
  - **3001–3199** (försäljning Sverige)
  - **3105, 3106** (EU-försäljning av varor)
  - **3308** (försäljning till tredje land)
  - **4056, 4515** (omvänd skattskyldighet)

Ta även med saldon från föregående periods avstämning för att se om något öppet finns kvar.

### Steg 3: Sammanställ momsunderlag

Räkna ihop per ruta i Skatteverkets blankett (momsdeklaration):

**Försäljning som beskattas:**
- Ruta 05: Momspliktig försäljning eller egna uttag exklusive moms
- Ruta 06: Momspliktig försäljning där köparen är skattskyldig
- Ruta 07: Inköp av varor från annat EU-land
- Ruta 08: Inköp av tjänster från annat EU-land

**Utgående moms:**
- Ruta 10: Utgående moms 25 %
- Ruta 11: Utgående moms 12 %
- Ruta 12: Utgående moms 6 %

**Ingående moms:**
- Ruta 48: Ingående moms att dra av

**EU och tredje land:**
- Ruta 35: Försäljning av varor till annat EU-land
- Ruta 38: Försäljning av tjänster till annat EU-land
- Ruta 39: Försäljning som inte är skattskyldig

Slutsumma: **Moms att betala eller få tillbaka** (ruta 49).

### Steg 4: Validera och flagga

Innan resultatet presenteras, kör dessa kontroller:

| Kontroll | Vad du letar efter | Åtgärd |
|----------|---------------------|--------|
| Felaktig momskod | 25 % på resor (ska vara 6/12), 6 % på konsulttjänster (ska vara 25) | Flagga verifikat, föreslå rättning |
| Saknad moms | Försäljningsverifikat utan motkontering på 2610-konto | Flagga som "kolla manuellt" |
| Obalans | Ingående + utgående går inte ihop med 1630 (skattekonto) | Kräv manuell granskning |
| Omvänd skattskyldighet | Bygg- och städtjänster missade omvänd moms | Flagga och hänvisa till § |
| EU utan VAT-validering | Försäljning ruta 35/38 utan VIES-validerat VAT-nr | Föreslå körning av `periodisk-sammanstallning` |

### Steg 5: Presentera resultat

Använd den här strukturen i svaret:

```
📋 MOMSREDOVISNING [period]
Bolag: [namn] (org.nr [xxx])
Momsperiod: [månad/kvartal/år]
Deadline: [datum]

═══════════════════════════════
SAMMANFATTNING
═══════════════════════════════
Utgående moms:      XX XXX kr
Ingående moms:    - XX XXX kr
───────────────────────────────
Att betala/få tillbaka: XX XXX kr

═══════════════════════════════
DETALJER PER RUTA
═══════════════════════════════
[Tabell med alla relevanta rutor]

═══════════════════════════════
⚠️  ATT KONTROLLERA INNAN INLÄMNING
═══════════════════════════════
1. [Konkret flagga med verifikatnummer]
2. [Konkret flagga med verifikatnummer]
...

═══════════════════════════════
NÄSTA STEG
═══════════════════════════════
□ Granska flaggade verifikat ovan
□ Logga in på Skatteverkets eTjänst
□ Fyll i siffrorna enligt rutorna ovan
□ Betala till bankgiro 5050-1055 senast [datum]
```

### Steg 6: Aldrig deklarera automatiskt

Skatteverket har ingen publik API för momsinlämning som tillåter tredjepart att skicka in deklarationer för svenska bolag utan e-leg. **Försök aldrig automatisera själva inlämningen.** Skillens jobb slutar vid att producera underlaget. Användaren tar det manuellt till Skatteverkets eTjänst.

## Periodicitet och deadlines

Bolagets momsperiod styrs av omsättningen:

- **< 1 MSEK:** Årsmoms, deadline 26:e i andra månaden efter räkenskapsårets slut
- **1–40 MSEK:** Kvartalsmoms, deadline 12:e i andra månaden efter perioden
- **> 40 MSEK:** Månadsmoms, deadline 26:e i andra månaden efter perioden

Verifiera alltid genom att fråga eller kolla i Bokio innan du antar.

## Vanliga felkällor

**Reverse charge på utländska tjänster:** Köp av Google Ads, AWS, Stripe-avgifter från utländska leverantörer kräver omvänd skattskyldighet. Saldot på 4535/4545 ska matcha utgående och ingående moms.

**Privata uttag och förmåner:** Kontrollera om något bokförts på 2898 eller 7385 som skulle krävt momskoning.

**Korrigeringar från föregående period:** Bokio behåller öppna saldon. Om föregående periods skatte­konto inte är nollat, fråga om det ska tas med.

## Output-format

Om användaren ber om Excel: generera `.xlsx` med en flik per ruta och en sammanställningsflik. Annars presentera direkt i chatten.

## Referenser

- [Skatteverket: Momsdeklaration](https://www.skatteverket.se/foretag/skatterochavdrag/moms/redovisamomsen.4.18e1b10334ebe8bc8000843.html)
- `references/moms-regler.md` (i det här repot)

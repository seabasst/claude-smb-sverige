# Momsregler för svenska SMB — referens

> ⚠️ **Verifiera mot Skatteverket innan användning i produktion.** Regler kan ändras.

## Momssatser

| Sats | Vad det omfattar |
|------|-------------------|
| **25 %** | Standardsats. De flesta varor och tjänster |
| **12 %** | Livsmedel, restaurang- och cateringtjänster, hotell |
| **6 %** | Böcker, tidningar, kollektivtrafik, idrottsevenemang, kulturella tjänster |
| **0 %** | Export, EU-försäljning till momsregistrerade köpare, vissa sjukvårdstjänster |

## Momsperioder

Periodicitet bestäms av omsättning:

| Omsättning | Period | Deadline |
|-----------|--------|----------|
| < 1 MSEK | Helår | 26:e i andra månaden efter räkenskapsårets slut |
| 1–40 MSEK | Kvartal | 12:e i andra månaden efter kvartalet |
| > 40 MSEK | Månad | 26:e i andra månaden efter månaden |

Standardperiod är kvartal. Företag kan ansöka om månadsmoms (för att kunna få återbetalning snabbare) eller årsmoms (för att förenkla).

## Rutor i momsdeklarationen

### Försäljning som beskattas

| Ruta | Vad |
|------|-----|
| 05 | Momspliktig försäljning eller egna uttag, exkl. moms |
| 06 | Momspliktig försäljning där köparen är skattskyldig |
| 07 | Inköp av varor från annat EU-land |
| 08 | Inköp av tjänster från annat EU-land |
| 09 | Beskattningsunderlag vid inköp av tjänster från utlandet |

### Utgående moms

| Ruta | Vad |
|------|-----|
| 10 | Utgående moms 25 % |
| 11 | Utgående moms 12 % |
| 12 | Utgående moms 6 % |
| 30 | Utgående moms på inköp från EU |
| 31 | Utgående moms på inköp av tjänster från utlandet |
| 32 | Utgående moms vid omvänd skattskyldighet |

### Ingående moms

| Ruta | Vad |
|------|-----|
| 48 | Ingående moms att dra av |

### Övrig försäljning

| Ruta | Vad |
|------|-----|
| 35 | Försäljning av varor till annat EU-land |
| 36 | Försäljning av varor utanför EU |
| 38 | Försäljning av tjänster till EU-land |
| 39 | Annan försäljning, inte momspliktig |
| 41 | Försäljning där köparen är skattskyldig (byggtjänster m.m.) |

### Slutruta

| Ruta | Vad |
|------|-----|
| 49 | **Moms att betala eller få tillbaka** |

## Omvänd skattskyldighet

Omvänd skattskyldighet innebär att köparen, inte säljaren, betalar moms. Gäller bland annat:

- **Byggtjänster** mellan byggbolag (B2B)
- **Städtjänster** sedan 2021
- **Mobiltelefoner, surfplattor, datorer** över 50 000 kr per faktura
- **El och gas** vid handel mellan registrerade bolag
- **Tjänster från utlandet** (köparen redovisar moms i Sverige)

Säljaren noterar "Omvänd skattskyldighet enligt 1 kap. 2 § första stycket 4 b mervärdesskattelagen" på fakturan. Köparen bokför både utgående (ruta 30/31/32) och ingående moms (ruta 48) på samma belopp.

## EU-handel

### Försäljning till momsregistrerade köpare i EU

- 0 % moms (vid varor) eller omvänd skattskyldighet (vid tjänster)
- Köparens VAT-nummer **måste** vara validerat mot VIES
- Rapporteras i ruta 35 (varor) eller 38 (tjänster)
- Ska också med i **periodisk sammanställning** (kvartalsvis)

### Försäljning till privatpersoner i EU (B2C)

- Tröskel 10 000 EUR per år för all distansförsäljning till EU sammanlagt
- Under tröskel: svensk moms
- Över tröskel: registrera i **OSS-systemet** (One-Stop-Shop) och betala moms i köparens land

### Köp från EU

- Säljaren tar inte ut moms (om du anger ditt VAT-nummer)
- Du bokför både utgående och ingående moms i Sverige (omvänd skattskyldighet)

## Faktureringsregler

Svensk faktura ska innehålla:

- Faktura-/serieidentifikation
- Fakturadatum
- Säljarens namn, adress, organisationsnummer, momsregistreringsnummer
- Köparens namn och adress (vid belopp över 4 000 kr inkl. moms)
- Köparens momsregistreringsnummer (vid omvänd skattskyldighet eller EU-handel)
- Vad som sålts (varuslag, mängd, tjänst)
- Datum för leverans eller tjänsteutförande
- Beskattningsunderlag per momssats
- Tillämpad momssats
- Momsbelopp
- Vid omvänd skattskyldighet: hänvisning till bestämmelse
- Vid F-skatt: "Innehar F-skattsedel"

## Faktureringskrav vid små belopp

Förenklad faktura tillåts under 4 000 kr inkl. moms:

- Datum
- Säljare
- Vad som sålts
- Momsbelopp eller -sats

## Inbetalning

- **Bankgiro:** 5050-1055 (Skatteverkets skattekonto)
- **OCR:** Företagets organisationsnummer + period
- Pengar betalas in på skattekontot

## Konton i Bokio (BAS)

| Konto | Namn |
|-------|------|
| 2610 | Utgående moms 25 % |
| 2611 | Utgående moms försäljning Sverige 25 % |
| 2615 | Utgående moms 25 % omvänd skattskyldighet |
| 2620 | Utgående moms 12 % |
| 2630 | Utgående moms 6 % |
| 2640 | Ingående moms |
| 2641 | Ingående moms 25 % |
| 2645 | Ingående moms utländsk leverantör |
| 2650 | Redovisningskonto för moms |

## Datakällor

- [Skatteverket: Moms](https://www.skatteverket.se/foretag/skatterochavdrag/moms.4.18e1b10334ebe8bc8000841.html)
- [Mervärdesskattelagen (2023:200)](https://www.riksdagen.se/sv/dokument-och-lagar/dokument/svensk-forfattningssamling/mervardesskattelag-2023200_sfs-2023-200/)

## Versionering

| Version | Datum | Notering |
|---------|-------|----------|
| 2026.1 | Januari 2026 | Initial version |

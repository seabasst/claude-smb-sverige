---
name: f-skatt-bolagskontroll
description: Verifierar nya leverantörer, kunder eller samarbetspartners genom att kontrollera F-skattestatus hos Skatteverket, registreringsdata hos Bolagsverket, och eventuella betalningsanmärkningar via tillgängliga källor. Skydd mot att betala till bolag som tappat F-skatt (vilket gör dig skyldig för deras skatter och avgifter), bolag i likvidation, eller fiktiva bolag. Använd den här skillen när användaren nämner "F-skatt", "F-skattsedel", "kolla bolag", "verifiera leverantör", "kolla nytt bolag", "är de seriösa", "kan jag lita på detta bolag", "leverantörskontroll", "vendor verification", "due diligence på bolag". Trigga också på "kolla att de har F-skatt", "är de momsregistrerade", "finns bolaget på riktigt", "ny kund/leverantör". Skillen ska köras innan första betalningen till en ny leverantör eller innan stort uppdrag startas med ny kund.
---

# F-skatt och bolagskontroll

Snabbt och billigt att kolla — dyrt att låta bli. Om du betalar en faktura till en leverantör som inte har F-skatt blir du skyldig för deras skatter och arbetsgivaravgifter. Bolag som gått i konkurs eller likvidation kan fakturera ändå om ingen kollar.

## När skillen ska köras

- Innan första betalningen till en ny leverantör
- Innan stort åtagande tas med ny kund (där kreditrisk finns)
- Vid offert eller ramavtalsförhandling
- När användaren misstänker att något inte stämmer med ett bolag
- Som rutin innan F-skatt verifieras varje årsskifte för aktiva leverantörer

## Förutsättningar

Skillen kan i grundläge använda offentliga webbsidor:

- **Skatteverket:** F-skattregistret via [skatteverket.se](https://sso.skatteverket.se/fa/UppgifterOmFoeretag.do)
- **Bolagsverket:** Allmänna uppgifter via [bolagsverket.se](https://www.bolagsverket.se)
- **Allabolag.se** eller **Hitta.se** för basinformation

För djupare kontroll: integration med UC (Upplysningscentralen) eller Creditsafe (kräver konto).

## Workflow

### Steg 1: Samla in information om bolaget

Be användaren om eller hämta från Bokio leverantörsregister:

- **Organisationsnummer** (10 siffror, format XXXXXX-XXXX)
- **Bolagsnamn**
- **Påstått VAT-nummer** (om de fakturerar från Sverige)

Om organisationsnummer saknas: be om det. Inga kontroller går att göra utan.

### Steg 2: Validera organisationsnummer

Kontrollera att org.nr är formatmässigt korrekt:

- 10 siffror
- För aktiebolag: börjar med 55
- För handelsbolag/kommanditbolag: börjar med 916 eller 969
- För ekonomisk förening: börjar med 716 eller 769
- För enskild firma: ofta personnumret (10 siffror utan sekel)
- Kontrollsiffra: använd Luhn-algoritm (sista siffran ska stämma)

### Steg 3: F-skattkontroll (kritisk)

Sök upp bolaget i Skatteverkets F-skattregister:

- **Har bolaget F-skatt?** Ja/Nej
- **Har bolaget momsregistrering?** Ja/Nej (krävs för momsavdrag på fakturor)
- **Är bolaget registrerat som arbetsgivare?** (relevant om du köper konsulttjänster)

> **VIKTIGT:** Om bolaget inte har F-skatt och du betalar utan att göra skatteavdrag, blir du som köpare ansvarig för deras inkomstskatt och arbetsgivaravgifter. Detta är den största risken vid uteblivna kontroller.

### Steg 4: Bolagsstatus

Kontrollera Bolagsverket eller allabolag.se:

| Status | Vad det betyder | Åtgärd |
|--------|------------------|--------|
| Aktivt | Normalt | Fortsätt |
| Likvidation | Bolaget håller på att avvecklas | Stort kreditflaggning |
| Konkurs | Bolaget kan inte betala | Avbryt samarbete |
| Avregistrerat | Bolaget existerar inte längre | Avbryt |
| Vilande | Inga aktiva transaktioner | Fråga varför de fakturerar |

Kolla också:

- **Registreringsdatum** (bolag yngre än 6 månader = extra granskning)
- **Säte** (matchar uppgivna adressen?)
- **Verksamhetsbeskrivning** (rimlig för det de fakturerar?)
- **Styrelse** (kända personer, kopplingar till andra bolag?)

### Steg 5: Verksamhetskontroll

För högre belopp eller känsliga affärer:

- Senast inlämnad årsredovisning (Bolagsverket)
- Omsättning enligt senaste bokslut
- Antal anställda
- Eventuella betalningsanmärkningar (kräver UC-konto)
- Revisor (har de revisor om de är skyldiga att ha det?)

### Steg 6: Presentera resultat

```
🔍 BOLAGSKONTROLL
Bolag: [namn]
Org.nr: [xxxxxx-xxxx]
Datum för kontroll: [datum]

═══════════════════════════════
RESULTAT
═══════════════════════════════
✅ / ⚠️ / ❌ F-skatt: [status]
✅ / ⚠️ / ❌ Moms: [status]
✅ / ⚠️ / ❌ Arbetsgivare: [status]
✅ / ⚠️ / ❌ Bolagsstatus: [status]
✅ / ⚠️ / ❌ Registrerat sedan: [datum]

═══════════════════════════════
OM BOLAGET
═══════════════════════════════
Säte: [stad]
Verksamhet: [beskrivning]
Senaste bokslut: [datum]
Omsättning: [belopp]
Antal anställda: [antal]
Styrelse: [namn]

═══════════════════════════════
SAMMANTAGEN BEDÖMNING
═══════════════════════════════
[GRÖN: Säkert att göra affär med | GUL: Gör affär men granska faktura noga | RÖD: Avbryt eller kräv förskott]

═══════════════════════════════
EVENTUELLA VARNINGAR
═══════════════════════════════
- [Konkret varning om något]

═══════════════════════════════
NÄSTA STEG
═══════════════════════════════
□ [Beroende på resultat]
□ Lägg in bolaget i Bokio leverantörsregister
□ Spara denna kontroll som dokumentation
```

### Steg 7: Spara dokumentation

Förslå att användaren sparar resultatet:

- I Bokio under leverantörens dokument
- Som PDF i bolagets arkiv
- I CRM (HubSpot, Pipedrive)

Detta är bra dokumentation om Skatteverket ifrågasätter någon transaktion senare.

## Specialfall

### Utländska bolag

F-skattregistret täcker inte utländska bolag. För EU-bolag:

- Validera VAT-nummer via [VIES](https://ec.europa.eu/taxation_customs/vies/)
- Kontrollera om de har svensk filial registrerad
- Kräv förskott eller använd escrow för stora belopp

### Enskilda firmor

Personnummer som org.nr. Risken är att personen själv går i personlig konkurs.

- Kolla F-skatt på personen
- Färre offentliga uppgifter än för AB

### Nystartade bolag

Bolag under 6 månader:

- Ingen historik
- Hög andel "katalog-bolag" som köps färdiga
- Be om referenser

### Kommunala och statliga organ

Behöver vanligtvis inte kontrolleras lika hårt, men:

- Verifiera att fakturan kommer från rätt organisationsnummer
- Stora upphandlingar har egna rutiner

## Återkommande kontroll

Föreslå att F-skattstatus på aktiva leverantörer kontrolleras minst:

- En gång per år (kring årsskiftet)
- Innan stora utbetalningar (> 100 000 kr)
- Om något känns konstigt (förändrad fakturaadress, ny bankgiro, etc.)

Denna skill kan köras i batch på hela leverantörsregistret från Bokio.

## Vanliga fallgropar

- **Antaganden:** Bara för att bolaget hade F-skatt i fjol betyder inte att de har det idag
- **Likalydande namn:** Två bolag kan ha snarlika namn med olika org.nr — verifiera alltid på siffrorna
- **Fakturasplittring:** Bolag som tappat F-skatt kan fortsätta fakturera utan att meddela
- **Mellanmän:** Vissa bolag fakturerar via mellanhandsbolag för att dölja problem — kolla alltid det fakturerande bolaget

## Referenser

- [Skatteverkets F-skattregister](https://sso.skatteverket.se/fa/UppgifterOmFoeretag.do)
- [Bolagsverket](https://www.bolagsverket.se)
- [VIES (EU VAT-validering)](https://ec.europa.eu/taxation_customs/vies/)
- [Allabolag.se](https://www.allabolag.se)

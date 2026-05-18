# Inkasso- och påminnelseregler — svensk referens

> ⚠️ **Verifiera mot aktuell lagstiftning. Vid tvist: rådfråga jurist.**

## Lagstöd

- **Räntelagen (1975:635):** Reglerar dröjsmålsränta
- **Inkassolagen (1974:182):** Reglerar yrkesmässig inkassoverksamhet
- **Lag (1981:739) om ersättning för inkassokostnader m.m.:** Reglerar avgifter

## Dröjsmålsränta

### Räntesats

Dröjsmålsränta = **Riksbankens referensränta + 8 procentenheter**

Riksbankens referensränta fastställs varje halvår (1 januari och 1 juli).

Aktuell sats: kontrollera på [Riksbanken.se](https://www.riksbank.se/sv/statistik/sok-rantor--valutakurser/forklaring-till-serierna/referensrantan/) innan användning.

### När ränta får tas ut

**Företag (B2B):**
- Ränta löper från förfallodag automatiskt om förfallodag avtalats
- Om förfallodag inte avtalats: 30 dagar efter att fakturan skickats

**Privatpersoner (B2C):**
- Ränta löper från 30 dagar efter att krav skickats om inget annat avtalats
- Skäl: Konsumentskyddet, kunden behöver chans att betala

### Beräkningsformel

```
Ränta = (Belopp × (Referensränta + 8%) × Antal dagar förfallen) / 365
```

Exempel: Faktura 10 000 kr, förfallen 30 dagar, referensränta 2 %:

```
Ränta = (10 000 × (2 % + 8 %) × 30) / 365
     = (10 000 × 0,10 × 30) / 365
     = 82,19 kr
```

## Påminnelseavgift

### Belopp

**Max 60 kr** per påminnelse enligt lag (1981:739).

### Villkor

För att få ta ut påminnelseavgift krävs:

- Det är avtalat (skrivet i avtal eller på fakturan)
- Skälig betalningsfrist har getts (vanligtvis 8 dagar)
- Endast en avgift per faktura

Om inget avtalats om påminnelseavgift: **avgift får inte tas ut**.

## Inkassokostnader

### Eget inkassokrav

Vid hantering i egen regi: **max 180 kr** för inkassokrav.

Krav: dokumenterat krav som följer Datainspektionens (numera IMY) god inkassosed.

### Inkassobolag

Om ett professionellt inkassobolag tar över ärendet, gäller deras prislista enligt:

- Inkassoföreläggande hos Kronofogden: 380 kr (statlig avgift)
- Inkassobolagets handläggning: varierar, ofta provision på huvudbeloppet
- Eventuella förlikningskostnader

## Inkassoflöde (branschpraxis)

```
Dag 0:    Fakturadatum
Dag 30:   Förfallodag (vanligen)
Dag 31-37: Vänlig påminnelse (frivillig)
Dag 38:   Formell påminnelse #1
           - 60 kr påminnelseavgift
           - Ränta börjar synas tydligt på krav
           - 8 dagars frist
Dag 46:   Sista påminnelse / inkassovarning
           - Tydlig varning om att inkasso skickas
           - 8 dagars frist
Dag 54:   Inkassokrav
           - 180 kr inkassoavgift
           - Sista chans innan Kronofogden
           - 8 dagars frist
Dag 62:   Ansökan om betalningsföreläggande hos Kronofogden
           - 380 kr statlig avgift
           - Risk för betalningsanmärkning för gäldenären
```

## Datainspektionens (IMY) krav på god inkassosed

Vid all yrkesmässig inkasso gäller:

1. Klart och tydligt formulerat krav
2. Inga hot eller olämpliga påtryckningar
3. Specifikation av belopp (huvudbelopp, ränta, avgifter)
4. Information om var och hur betalning ska göras
5. Skälig frist för betalning
6. Information om vad som händer om kravet inte betalas

## Bestridanden

Om kunden bestrider fakturan **innan inkasso**:

- Stoppa inkassoprocessen omedelbart
- Inkasso får inte fortsätta vid tvist
- Hantera tvisten genom förlikning eller domstol
- Kronofogden tar inte upp bestridda ärenden — då måste tvistemål väckas hos tingsrätt

Om kunden bestrider **efter** att Kronofogden fått ärendet:

- Ärendet flyttas till tingsrätt om kreditgivaren vill fortsätta
- Detta är dyrt och tar tid — ofta bättre att förhandla

## Konton i Bokio (BAS)

| Konto | Vad |
|-------|------|
| 1510 | Kundfordringar |
| 1519 | Nedskrivning av kundfordringar |
| 3992 | Erhållna räntor från kunder |
| 3991 | Erhållna påminnelseavgifter |
| 6350 | Förluster på kundfordringar |

## Datakällor

- [Räntelagen (1975:635)](https://www.riksdagen.se/sv/dokument-och-lagar/dokument/svensk-forfattningssamling/rantelag-1975635_sfs-1975-635/)
- [Inkassolagen (1974:182)](https://www.riksdagen.se/sv/dokument-och-lagar/dokument/svensk-forfattningssamling/inkassolag-1974182_sfs-1974-182/)
- [Lag (1981:739) om ersättning för inkassokostnader](https://www.riksdagen.se/sv/dokument-och-lagar/dokument/svensk-forfattningssamling/lag-1981739-om-ersattning-for-inkassokostnader_sfs-1981-739/)
- [IMY: God inkassosed](https://www.imy.se/verksamhet/inkasso/)
- [Kronofogden](https://www.kronofogden.se)

## Versionering

| Version | Datum | Notering |
|---------|-------|----------|
| 2026.1 | Januari 2026 | Initial version |

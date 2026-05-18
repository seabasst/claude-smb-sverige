---
name: sie4-export-revisor
description: Exporterar bokföringen från Bokio i SIE4-format (svensk standard för bokföringsdataöverföring) och paketerar för att skickas till revisor eller redovisningskonsult. Inkluderar verifikat, kontoplan, balanslista och eventuella bilagor. Använd den här skillen när användaren nämner "SIE4", "SIE-fil", "exportera till revisor", "skicka till revisor", "redovisningskonsult", "årsbokslut", "revision", "extern revisor". Trigga också på "vad ska jag skicka till revisorn", "kan du paketera bokföringen", "färdigställ för revision".
---

# SIE4-export till revisor

## Status: STUB — bidra gärna

Skillen ska:

1. Exportera SIE4-fil från Bokio för vald period
2. Validera filen mot SIE4-standarden (BAS Intressentförenings spec)
3. Paketera tillsammans med:
   - Kontoutdrag från bank
   - Skattekontoutdrag
   - Eventuella inventarielistor
   - Förteckning över öppna fakturor (kund + leverantör)
4. Generera följebrev till revisor med:
   - Periodens nyckeltal
   - Frågor och oklarheter som identifierats
   - Kontaktuppgifter
5. Komprimera till .zip för enkel överföring

## TODO

- [ ] Definiera exakt Bokio MCP-anrop för SIE4-export
- [ ] Lägga till validering av SIE4-syntax
- [ ] Mall för följebrev (företagsanpassad)
- [ ] Stöd för Visma och Fortnox SIE4-format också
- [ ] Säker överföring (kryptering eller länk istället för bilaga)

## Referenser

- [SIE-format specifikation](https://sie.se/format/)
- [BAS Intressentförening](https://www.bas.se)

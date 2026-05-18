---
name: manadsbokslut-bokio
description: Genomför månadsbokslut i Bokio: stämmer av bankkontot mot bokföringen, identifierar oavstämda transaktioner, kontrollerar att periodens intäkter och kostnader är korrekt bokförda, beräknar resultatet, genererar en plain-english P&L och balansrapport, samt flaggar saker som behöver åtgärdas innan månaden låses. Använd den här skillen när användaren nämner "månadsbokslut", "stäm av månaden", "stäng månaden", "boka klart månaden", "close the month", "resultatrapport för månaden", "P&L för månaden", "balansrapport", "avstämning Bokio". Trigga också på "hur gick månaden", "vad gjorde vi förra månaden", "kolla att bokföringen stämmer", "är allt bokfört". Skillen ska köras månadsvis och utgör grunden för momsredovisning, AGI och kvartalsuppföljning.
---

# Månadsbokslut i Bokio

Månadsbokslutet är fundamentet allt annat står på. Om månaden inte är stängd ordentligt blir momsen fel, kassaflödet ser konstigt ut, och årsbokslutet blir en mardröm.

## När skillen ska köras

- Inom första veckan efter månadens slut
- Innan momsredovisning eller AGI körs (de förlitar sig på korrekt bokfört underlag)
- När användaren ber om resultatrapport eller "kolla månaden"
- När bank- eller Stripe-saldot inte stämmer med Bokio

## Förutsättningar

- **Bokio MCP** installerad och autentiserad
- Bankkontotransaktioner importerade till Bokio (via filimport eller bankkoppling)
- Eventuella Stripe/Klarna/Swish-rapporter tillgängliga

## Workflow

### Steg 1: Bekräfta period och bolag

Fråga om något är oklart:

- Vilken månad?
- Är det första gången månaden granskas, eller en omstämning?
- Finns det åtgärder från föregående månads bokslut som behöver kontrolleras?

### Steg 2: Avstämning av bankkonto

Hämta från Bokio:

- Saldot på konto **1930** (bank) per sista i månaden
- Saldot enligt det fysiska bankkontot per samma datum (be användaren om bankutdrag eller kolla i bankkoppling)

Räkna ut:

```
Avvikelse = Bokio 1930 - Bank-saldo
```

| Avvikelse | Tolkning |
|-----------|----------|
| 0 kr | Perfekt avstämning |
| Positiv | Bokfört men inte i banken (eller missade insättningar) |
| Negativ | I banken men inte bokfört |

Om avvikelse ≠ 0, hitta orsaken:

- Oavstämda transaktioner i Bokio
- In/utbetalningar runt månadsskiftet (vanligaste orsaken: kortavgift bokad i Bokio men inte clearad i banken ännu)
- Saknade kvitton eller fakturor

### Steg 3: Kontrollera periodens transaktioner

Gå igenom i Bokio:

**Intäkter:**
- Är alla fakturor som skickades i månaden bokförda? Räkna mot Bokios fakturamodul
- Saknas några försäljningar (Swish, kontant, Stripe utan automatisk koppling)?
- Är periodisering korrekt för fakturor som täcker flera månader?

**Kostnader:**
- Är alla kvitton inscannade och kontoförda?
- Finns leverantörsfakturor som tagits emot men inte bokförts?
- Är kortköp på företagskort matchade med kvitton?

**Skatter och avgifter:**
- Är arbetsgivaravgifter bokförda för månaden (även om de betalas nästa månad)?
- Är moms bokförd löpande på 2610/2640?

**Periodiska kostnader:**
- Hyror, prenumerationer, försäkringar — är de bokförda?

### Steg 4: Specialavstämningar

| Konto | Vad det är | Vad du kontrollerar |
|-------|-----------|----------------------|
| **1510** Kundfordringar | Obetalda fakturor | Saldot ska matcha summan av öppna fakturor i Bokio |
| **1630** Skattekonto | Saldot vs Skatteverkets eTjänst | Ska överensstämma. Om inte: skattekontot kanske rörts |
| **1930** Bank | Bankkontot | Ska matcha banksaldot |
| **2440** Leverantörsskulder | Obetalda lev.fakturor | Saldot = summan av öppna leverantörsfakturor |
| **2610/2640** Moms | Periodens momsrörelser | Ska matcha summa moms ut/in på försäljnings- och inköpsverifikat |
| **2710** Personalskatt | Avdragen skatt | Saldot ska matcha den AGI som ska deklareras |
| **2730** Arbetsgivaravgifter | Beräknade avgifter | Saldot = aktuell månads avgifter |

### Steg 5: Generera P&L och balansrapport

Använd Bokio MCP för att hämta:

- Resultatrapport för månaden
- Balansrapport per sista i månaden

Presentera i klartext, inte bara siffror. Exempel:

```
📊 MÅNADSBOKSLUT [månad år]
Bolag: [namn] (org.nr [xxx])

═══════════════════════════════
RESULTAT I KORTHET
═══════════════════════════════
Intäkter:         XXX XXX kr (jmf föreg månad: +X %)
Rörelsens kostnader: XXX XXX kr (jmf föreg: -X %)
───────────────────────────────
RESULTAT:         XX XXX kr

Marginal: XX %
Året hittills (YTD): X XXX XXX kr

═══════════════════════════════
TOPP 5 KOSTNADER
═══════════════════════════════
1. [Kategori]: XX XXX kr
2. [Kategori]: XX XXX kr
...

═══════════════════════════════
BALANS PER [sista datum]
═══════════════════════════════
Bank:                 XXX XXX kr
Kundfordringar:        XX XXX kr
Leverantörsskulder:   - XX XXX kr
Skattekonto:            X XXX kr
Eget kapital:         XXX XXX kr

═══════════════════════════════
⚠️  ATT ÅTGÄRDA INNAN MÅNADEN STÄNGS
═══════════════════════════════
1. [Konkret post med belopp och åtgärd]
2. ...
```

### Steg 6: Flagga avvikelser

Räkna jämförelse mot föregående månad och jämför med samma månad föregående år (om data finns):

| Avvikelse | Trösklar |
|-----------|----------|
| Intäkter ± 30 % | Fråga om det är normalt |
| Enskild kostnadskategori ± 50 % | Flagga för granskning |
| Helt nya konton används | Fråga varför, kanske felkodning |
| Negativ balans på normalt positivt konto | Flagga som potentiellt fel |

### Steg 7: Föreslå nästa steg

```
═══════════════════════════════
NÄSTA STEG
═══════════════════════════════
□ Åtgärda flaggade poster (se ovan)
□ Stämma av momsrörelser → kör `moms-redovisning`
□ Kontrollera lönedata → kör `agi-arbetsgivardeklaration`
□ Generera SIE4 för revisor om slutet på kvartal → kör `sie4-export-revisor`
□ Lås månaden i Bokio (när allt är åtgärdat)
```

## Periodisering

För svenska SMB enligt K2/K3-regelverket: periodisera bara väsentliga poster. För skill-paketet räknar vi periodisering som väsentlig om:

- Belopp > 5 000 kr och avser mer än 1 månad framåt
- Hyra som betalats i förskott
- Försäkringar betalda för ett år
- Större licensavgifter

Mindre belopp får tas direkt på resultatet enligt väsentlighetsprincipen.

## Vanliga felkällor

- **Stripe/Klarna-avgifter:** Bokio matchar inte alltid avgifter automatiskt. Kontrollera konto 6570 vs faktiska avgifter
- **Privata uttag:** Bokade på fel konto (2393 istället för 2898) eller missade helt
- **Företagskort:** Köp utan kvitto eller felkoddade till privat
- **Bilförmån:** Glöms ofta att bokföras månatligen, kommer som ihåg först vid årsbokslut
- **Förseningsavgifter:** Bokas på 6991 men borde ofta gå till 7510 om de gäller skatt/avgifter

## Referenser

- `references/bokio-mcp-tools.md` (för specifika MCP-anrop)
- [Bokföringsnämnden K2-regelverket](https://www.bfn.se/sv/redovisningsregler/k-regelverk/k2)

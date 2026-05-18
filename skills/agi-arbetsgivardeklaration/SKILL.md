---
name: agi-arbetsgivardeklaration
description: Förbereder och sammanställer arbetsgivardeklaration på individnivå (AGI) för månatlig inlämning till Skatteverket. Hämtar löneunderlag från Bokio, kontrollerar att arbetsgivaravgifter, skatteavdrag, förmåner och ersättningar är korrekt bokförda per anställd, och producerar både totalsumman för betalning och AGI-XML-underlag. Använd den här skillen när användaren nämner "AGI", "arbetsgivardeklaration", "lönerapport till Skatteverket", "betala arbetsgivaravgifter", "skatteavdrag anställda", "deklarera löner", "AGI på individnivå", eller pratar om månadens lönerapportering. Trigga också på "vad ska jag betala till Skatteverket den 12:e", "hur mycket är arbetsgivaravgifter", "kolla lönerna inför Skatteverkets deadline". Skillen täcker både vanliga anställda, fåmansbolagsägare, förmånsbeskattning och engångsutbetalningar.
---

# AGI — Arbetsgivardeklaration på individnivå

Sedan 2019 ska alla arbetsgivare i Sverige rapportera löner på individnivå varje månad. Det är AGI:n. Den ska in senast den 12:e i månaden efter utbetalningsmånaden (17:e för stora företag), och samtidigt ska arbetsgivaravgifter och skatteavdrag betalas till skattekontot.

Felaktig AGI leder till föreläggande och i värsta fall förseningsavgift på 1 250 kr per individ.

## När skillen ska köras

- Användaren nämner AGI, arbetsgivardeklaration eller månadsrapportering
- Det är mellan 1:a och 12:e i månaden (deadline närmar sig)
- Användaren har precis kört en lönekörning i Bokio
- Användaren undrar "vad ska jag betala till Skatteverket"

## Förutsättningar

- **Bokio MCP** installerad och autentiserad
- Lönekörningen för aktuell månad är genomförd i Bokio
- Användaren har angett vilken månad det gäller (utbetalningsmånaden, inte rapporteringsmånaden)

## Workflow

### Steg 1: Identifiera period och anställda

Fråga eller hämta från Bokio:

- Vilken utbetalningsmånad? (AGI:n rapporterar den månad lönen *betalades*, inte när den intjänades)
- Hur många anställda har haft utbetalning?
- Finns det engångsutbetalningar (bonus, semesterersättning, retroaktiv lön)?

### Steg 2: Hämta löneunderlag från Bokio

Per anställd, hämta:

- **Bruttolön** (kontant ersättning)
- **Förmåner** (bilförmån, kost, bostad, etc.)
- **Avdragen preliminär skatt** (A-skatt)
- **Arbetsgivaravgifter** beräknade på bruttolön + skattepliktiga förmåner
- **Andra avdrag** (jobbskatteavdrag, fackavgift)
- **Identifierare:** personnummer (krypterat hanterat), namn, anställningsnummer

Konton att kontrollera i Bokio (BAS):

- **7010, 7210** Löner till anställda
- **7220, 7240** Löner till företagsledare (fåmansbolag)
- **7385** Kostnader för fri bostad / förmåner
- **7510, 7515** Arbetsgivaravgifter
- **2710** Personalskatt
- **2730** Arbetsgivaravgifter att betala

### Steg 3: Räkna arbetsgivaravgifter

**Standardprocentsats 2026:** 31,42 % (på lön + skattepliktiga förmåner)

Undantag som kan gälla:

| Kategori | Sats | Villkor |
|----------|------|---------|
| Personer födda 1938–1958 | 10,21 % | Endast ålderspensionsavgift |
| Personer födda 1959–1962 | 23,75 % | Reducerad sats |
| Ungdomar 15–18 år | 10,21 % | På lön upp till 25 000 kr/mån |
| FoU-personal | -10 % | Forskningsavdrag enligt särskild regel |

Verifiera datumen i `references/arbetsgivaravgifter-2026.md` — satserna kan ändras årligen.

### Steg 4: Validera och flagga

Innan output, kontrollera:

| Kontroll | Vad du letar efter | Åtgärd |
|----------|---------------------|--------|
| Skatteavdrag rimligt | A-skatt ska vara ~30 % av brutto, inte 0 eller över 50 | Flagga |
| Förmåner bokförda | Bilförmån, friskvård över 5 000 kr, bostadsförmån | Kontrollera kodning |
| Personnummer komplett | 12 siffror, kontrollsiffra korrekt | Flagga |
| Avgift matchar konto | Beräknad avgift ≈ saldot på 2730 | Flagga avvikelser > 100 kr |
| Engångsskatt | Bonus över 1 PBB ska ha engångsskatt, inte tabellskatt | Kontrollera |

### Steg 5: Presentera resultat

```
📋 ARBETSGIVARDEKLARATION (AGI) - [månad år]
Bolag: [namn] (org.nr [xxx])
Rapporteringsdatum: senast den [12:e datum]

═══════════════════════════════
SAMMANFATTNING
═══════════════════════════════
Antal anställda i AGI: [N]
Total bruttolön:        XXX XXX kr
Total förmånsvärde:      XX XXX kr
───────────────────────────────
Underlag för avgifter:  XXX XXX kr

Arbetsgivaravgifter:     XX XXX kr
Avdragen skatt (A):      XX XXX kr
───────────────────────────────
ATT BETALA TILL SKATTEKONTO: XXX XXX kr

═══════════════════════════════
PER INDIVID
═══════════════════════════════
[Tabell: Namn | PNR (maskerat) | Brutto | Förmån | Skatt | Avgift]

═══════════════════════════════
⚠️  ATT KONTROLLERA INNAN INLÄMNING
═══════════════════════════════
1. [Konkret flagga med anställd och belopp]
...

═══════════════════════════════
NÄSTA STEG
═══════════════════════════════
□ Granska flaggade poster
□ Logga in på Skatteverket eTjänst (AGI)
□ Importera underlag eller fyll i manuellt
□ Betala XXX XXX kr till bankgiro 5050-1055 senast [12:e datum]
□ Bokio: bokför betalning mot 1630 / 2710 / 2730
```

### Steg 6: AGI-XML-export (valfri)

Om användaren ber om XML-fil för upload till Skatteverket eller löneprogram:

- Skapa fil enligt Skatteverkets [AGI-format](https://www.skatteverket.se/foretag/arbetsgivare/arbetsgivardeklaration/utvecklareavlonesystem.4.41f1c61d16193087d7faf3.html)
- Namnge `AGI-[orgnr]-[YYYY-MM].xml`
- Spara i outputs-mappen, presentera filen

**Skicka aldrig in deklarationen automatiskt.** Skillens jobb slutar vid att producera underlag och XML. Användaren laddar upp eller fyller i manuellt på Skatteverkets eTjänst.

## Fåmansbolag och egen lön

Är användaren ägare i fåmansbolag och tar lön till sig själv? Då är extra kontroller relevanta:

- Tillräckligt löneunderlag för 3:12-utdelning nästa år (`k10-faman` skillen)
- Bostadsförmån vid privat boende ägt av bolaget
- Sjuklöneregler för fåmansbolagsägare

Föreslå att köra `k10-faman` om underlaget verkar marginellt för gränsbeloppet.

## Vanliga felkällor

- **Förmåner glömda:** friskvård över 5 000 kr/år, mobiltelefon med privat bruk, restaurangbesök utöver representation
- **Engångsersättning fel skatt:** retroaktiv lön eller bonus med tabellskatt istället för engångsskatt (32 %)
- **Sjuklön karensavdrag:** karensavdraget ska vara 20 % av en genomsnittlig veckolön, inte 1 dag
- **Semesterersättning vid avslut:** ska in i sista lönebeskedet och rapporteras i AGI

## Referenser

- [Skatteverket: AGI](https://www.skatteverket.se/foretag/arbetsgivare/arbetsgivardeklaration.4.361dc8c15312eff6fd1f7cf.html)
- `references/arbetsgivaravgifter-2026.md`

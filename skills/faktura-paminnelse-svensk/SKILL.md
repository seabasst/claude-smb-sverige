---
name: faktura-paminnelse-svensk
description: Hanterar fakturapåminnelser och inkasso enligt svensk lagstiftning. Identifierar förfallna fakturor i Bokio, beräknar korrekt påminnelseavgift (max 60 kr) och dröjsmålsränta (referensränta + 8 procentenheter), upprättar tröskel innan inkassoärende, och genererar utkast till påminnelsemejl, andra påminnelse, inkassovarning och slutligen inkassokrav. Använd den här skillen när användaren nämner "påminnelse", "fakturapåminnelse", "obetalda fakturor", "kunder som inte betalat", "skicka påminnelse", "inkasso", "dröjsmålsränta", "påminnelseavgift", "förfallna fakturor", "chase invoices", "krav på kund". Trigga också på "vilka kunder är sena", "vem är skyldig mig pengar", "hur mycket har jag utestående", "skicka krav på X". Skillen följer Inkassolagen och Räntelagen samt Svensk Inkassos branschpraxis.
---

# Fakturapåminnelse och inkasso enligt svensk lag

Anthropics original "invoice chaser" är gjord för USA. I Sverige finns lagstadgade gränser för påminnelseavgift, dröjsmålsränta och inkassoflöde. Den här skillen följer dem.

## När skillen ska köras

- Användaren ber om hjälp med påminnelser eller obetalda fakturor
- Användaren laddar upp lista över utestående fakturor
- Det är dag 14, 30 eller 45 efter förfallodatum (typiska påminnelsesteg)
- Användaren undrar "hur mycket har jag utestående"

## Förutsättningar

- **Bokio MCP** installerad och autentiserad
- Tydliga faktureringsvillkor i de ursprungliga fakturorna (annars går inte avgifter och ränta att kräva ut)

## Lagligt ramverk (kort version)

**Påminnelseavgift:** Max 60 kr per påminnelse. Endast om det stod i avtalet eller på fakturan att avgift tas ut vid försenad betalning. Kan endast tas ut **en gång** per faktura.

**Dröjsmålsränta:** Räntelagen § 6. Riksbankens referensränta + 8 procentenheter. Räknas från förfallodag tills betalning är gjord. *Verifiera aktuell referensränta vid körning.*

**Inkassoavgift:** Max 180 kr om inkassobolag inte är inkopplat ännu (eget inkassokrav). Om inkassobolag tar över: deras avgifter följer Datainspektionens regler.

**Tröskel innan inkasso:** Branschpraxis är 1–2 påminnelser med minst 8 dagars frist mellan, sedan inkassokrav.

Full text i `references/inkasso-regler.md`.

## Workflow

### Steg 1: Hämta utestående fakturor

Använd Bokio MCP för att lista alla obetalda fakturor. Per faktura, samla:

- Fakturanummer, datum, förfallodag
- Belopp inkl. moms
- Antal dagar förfallen
- Kundnamn, kundnummer, org.nr eller personnummer
- Tidigare påminnelser skickade (om Bokio loggar det)
- Avtalade betalningsvillkor

### Steg 2: Klassificera per åtgärdssteg

Gruppera fakturor i fyra hinkar:

| Steg | Förfallna dagar | Åtgärd |
|------|-----------------|--------|
| **Snäll påminnelse** | 1–7 | Vänligt mejl, "kanske missat" |
| **Formell påminnelse** | 8–14 | Påminnelseavgift 60 kr + ränta börjar räknas |
| **Sista påminnelse** | 15–30 | Varning om inkasso, full sammanställning |
| **Inkassokrav** | 31+ | Antingen eget krav (max 180 kr) eller överlämna till inkassobolag |

Om kunden är ett aktiebolag och beloppet är över 10 000 kr, föreslå direkt steg "Inkasso" efter dag 14 eftersom Kronofogden-process går snabbare.

### Steg 3: Räkna ränta och avgifter per faktura

För varje faktura, beräkna:

```
Dröjsmålsränta = (Belopp × (Referensränta + 8%) × Antal dagar förfallen) / 365
Påminnelseavgift = 60 kr (endast om inte tidigare uttagen)
Inkassoavgift = 180 kr (endast vid inkassokrav)

Att betala totalt = Belopp + Ränta + Avgifter
```

Visa beräkningen tydligt så användaren och kunden kan följa den.

### Steg 4: Generera mejlutkast

Använd dessa templates som bas, anpassa per kund och bolagets ton.

#### Snäll påminnelse (dag 1–7)

```
Ämne: Vänlig påminnelse: faktura [FAKTNR]

Hej [Namn],

Hoppas allt är väl! Jag ville bara påminna om faktura [FAKTNR] på 
[BELOPP] kr som hade förfallodag [DATUM]. Möjligt att den hamnat 
mellan stolarna.

Bankgiro: [BG]
OCR: [OCR]
Belopp: [BELOPP] kr

Hör av dig om något är oklart.

Vänliga hälsningar,
[Avsändare]
```

#### Formell påminnelse (dag 8–14)

```
Ämne: Påminnelse — faktura [FAKTNR] förfallen [X] dagar

Hej [Namn],

Faktura [FAKTNR] om [BELOPP] kr förföll [DATUM] och är nu [X] dagar
förfallen.

Enligt avtal och Räntelagen tillkommer:
- Påminnelseavgift: 60 kr
- Dröjsmålsränta: [BERÄKNAT BELOPP] kr (referensränta + 8 % från förfallodag)

Att betala totalt: [SUMMA] kr

Bankgiro: [BG] | OCR: [OCR]

Vänligen betala senast [NYTT DATUM, 8 dagar fram]. Om betalning 
uteblir kommer ärendet att gå vidare till inkasso, vilket innebär 
ytterligare kostnader för er.

Vänliga hälsningar,
[Avsändare]
```

#### Sista påminnelse / inkassovarning (dag 15–30)

```
Ämne: SISTA PÅMINNELSE — inkasso skickas [DATUM]

[Namn],

Faktura [FAKTNR] om [BELOPP] kr är nu [X] dagar förfallen trots 
tidigare påminnelse.

Specifikation:
Originalbelopp:        [BELOPP] kr
Påminnelseavgift:           60 kr
Dröjsmålsränta:        [RÄNTA] kr
─────────────────────────────────
Att betala:           [SUMMA] kr

Bankgiro: [BG] | OCR: [OCR]

Om full betalning inte är oss tillhanda senast [DATUM, 8 dagar fram]
överlämnar vi ärendet till inkasso. Det innebär ytterligare 180 kr 
i inkassoavgift och risk för betalningsanmärkning för er.

Vänligen kontakta oss omgående om det finns oklarheter.

[Avsändare]
```

#### Inkassokrav (dag 31+)

Detta är ett juridiskt dokument. Föreslå att antingen:

a) **Egen hantering:** Generera inkassokrav som följer Datainspektionens krav (Datainspektionens vägledning för inkasso). Belopp = original + 60 kr påminnelseavgift + 180 kr inkassoavgift + ränta.

b) **Överlämning till inkassobolag:** Föreslå Lowell, Visma Financial Solutions, eller Svea Inkasso. Förklara att inkassobolag tar provision och att kunden då får betalningsanmärkning vid utebliven betalning.

### Steg 5: Presentera resultat

```
📋 PÅMINNELSESAMMANSTÄLLNING
Bolag: [namn]
Genererad: [datum]

═══════════════════════════════
SAMMANFATTNING
═══════════════════════════════
Totalt utestående: XXX XXX kr
Antal förfallna fakturor: [N]
Snitt antal dagar förfallna: [X]

Per åtgärdssteg:
- Snäll påminnelse: [N st] = [XXX] kr
- Formell påminnelse: [N st] = [XXX] kr
- Sista påminnelse: [N st] = [XXX] kr
- Inkasso rekommenderas: [N st] = [XXX] kr

═══════════════════════════════
UTKAST GENERERADE
═══════════════════════════════
[Lista över utkast med kund + steg + belopp]

═══════════════════════════════
NÄSTA STEG
═══════════════════════════════
□ Granska varje utkast (klicka för att se)
□ Justera ton för specifika kunder om relevant
□ Skicka via valt mejlsystem
□ Logga skickade påminnelser i Bokio
□ För inkassofall: bestäm eget eller överlämna
```

### Steg 6: Skicka aldrig automatiskt

Skillen genererar utkast. Användaren granskar och skickar manuellt via sitt mejlsystem (Gmail, Outlook). Föreslå att lägga sig själv på BCC för logg.

## Specialfall

**Företagskunder med god relation:** Föreslå muntligt samtal innan formell påminnelse. Kallt påminnelsemejl kan skada långa relationer.

**Privatpersoner:** Räntelagen gäller, men inkassoflödet är mer reglerat. Räntelagen § 4 säger att privatpersoner som inte är näringsidkare bara behöver betala ränta från 30 dagar efter krav skickats, om inget avtalats. Var försiktig med automatiska räntepåslag mot konsumenter.

**Bestridda fakturor:** Om kunden har bestridit fakturan: skicka aldrig inkasso. Föreslå tvistförhandling, eventuellt ansökan om betalningsföreläggande hos Kronofogden.

**Utländska kunder:** Räntelagen och Inkassolagen gäller bara i Sverige. Föreslå att referera till avtalet och eventuellt internationell inkasso.

## Vanliga felkällor

- **Påminnelseavgift utan avtalsgrund:** Avgift kan bara tas ut om det stod i ursprungsfakturan eller avtalet
- **Dubbla påminnelseavgifter:** Endast en avgift per faktura
- **Ränta på ränta:** Beräkna ränta endast på huvudbeloppet, inte på avgifter
- **Inkasso utan föregående krav:** Datainspektionen kräver att kunden fått chans att betala innan inkasso

## Referenser

- [Räntelagen (1975:635)](https://www.riksdagen.se/sv/dokument-och-lagar/dokument/svensk-forfattningssamling/rantelag-1975635_sfs-1975-635/)
- [Inkassolagen (1974:182)](https://www.riksdagen.se/sv/dokument-och-lagar/dokument/svensk-forfattningssamling/inkassolag-1974182_sfs-1974-182/)
- [Riksbankens referensränta](https://www.riksbank.se/sv/statistik/sok-rantor--valutakurser/forklaring-till-serierna/referensrantan/)
- `references/inkasso-regler.md`

# LinkedIn-utkast för lansering

Tre olika varianter att välja mellan. Anpassa efter eget tycke.

---

## Variant A: Hyllning + komplement (rekommenderas för räckvidd)

I förra månaden lanserade Anthropic *Claude for Small Business*. 15 skills och 15 workflows som gör Claude användbar inuti QuickBooks, PayPal, HubSpot och Google Workspace. Brilliant arbete.

Som svensk småföretagare blev jag genast nyfiken. Installerade pluginet. Insåg snabbt att hälften fungerar direkt (lead-triage, content-strategy, customer-pulse, contract-review) och hälften gör inget för mig (cash-flow med QuickBooks, invoice-chase utan svensk räntelag, tax-prep utan momsperiod).

Så jag byggde en kompletterande svensk stack. Open source.

→ 11 Claude Skills för svenskt regelverk
→ Bygger på Bokio MCP
→ Täcker momsredovisning, AGI på individnivå, fakturapåminnelser med svensk räntelag, F-skattekontroll, K10 för fåmansbolag, periodisk sammanställning och mer
→ Designat att köras *parallellt* med Anthropics SMB-plugin, inte ersätta det
→ Aldrig automatisk inlämning, alltid mänsklig kontroll innan något skickas

Det här är v0.1. Sex av elva skills är stubs. Behöver hjälp av redovisningskonsulter, revisorer och utvecklare att fylla ut.

Repo: github.com/kirimedia/claude-smb-sverige

Bidra om du jobbar med svenska SMB. Ju fler ögon på regelverken, desto bättre blir det för alla.

#AI #Småföretag #Bokföring #Bokio #OpenSource

---

## Variant B: Kort och vass

Anthropic släppte *Claude for Small Business* i oktober: 15 SMB-skills inuti QuickBooks, PayPal, HubSpot.

Hälften fungerar direkt för svenska företag. Andra halvan är gjord för amerikansk skatte- och inkassolagstiftning.

Byggde en kompletterande svensk stack. Open source. 11 skills för moms, AGI, K10, F-skatt, fakturapåminnelser och annat som kräver svenskt regelverk.

Bygger på Bokio MCP. Designat att köras parallellt med Anthropics plugin.

→ github.com/kirimedia/claude-smb-sverige

---

## Variant C: Personlig + tekniskt

Spenderade helgen med Anthropics nya *Claude for Small Business*-plugin. Trevligt paket: 15 skills som täcker payroll, månadsbokslut, kampanjer, kundtjänst, kontraktsgranskning.

Strukturen är vacker. Men finanssidan är hårt knuten till QuickBooks och PayPal. För svenskt aktiebolag betyder det att fem av femton finansrelaterade skills inte fungerar utan att Bokio och Skatteverket finns med i bilden.

Så jag byggde en kompletterande stack. Samma arkitektur, svenskt regelverk:

- `moms-redovisning` (Bokio + Skatteverkets rutor)
- `agi-arbetsgivardeklaration` (månatlig AGI på individnivå)
- `faktura-paminnelse-svensk` (Räntelagen, max 60 kr påminnelseavgift, IMY-flöde)
- `f-skatt-bolagskontroll` (innan första betalningen till ny leverantör)
- `k10-faman` (3:12, gränsbelopp, sparat utdelningsutrymme)
- Och fler

Open source under MIT. Bygger ovanpå Bokio MCP. Användaren godkänner alltid innan något skickas.

Är du auktoriserad revisor, redovisningskonsult eller utvecklare som jobbar med svenska SMB? Pull requests välkomna.

→ github.com/kirimedia/claude-smb-sverige

Tack till @Anthropic för att de byggde och öppnade konceptet att börja med. Vi rekommenderar att alla användare också installerar deras officiella plugin för full täckning.

---

## Tips för att maxa LinkedIn-räckvidd

- **Posta tisdag–torsdag mellan 08–10**
- **Lägg till en bild eller carousel** med översikt av skills-tabellen (skapa screenshot av README:s tabell)
- **Tagga relevanta personer:** Bokios CEO, någon på Anthropic-teamet om du har koppling, eventuella svenska AI-personer du följer
- **Hashtags:** #AI, #Småföretag, #Bokföring, #Bokio, #OpenSource, #Sverige, #AB, #Företagande
- **Kommentera tillbaka aktivt** under första 60 minuterna efter publicering
- **Pinga några förstahandsanvändare** privat innan du postar så de kan kommentera tidigt
- **Tonalitet:** Hyllning till Anthropic + ödmjuk komplettering. Aldrig "Anthropic gjorde fel". Den positioneringen är både ärligare och mer professionellt klok eftersom du är en Anthropic-byggande byrå.

# Claude för Småföretag — Sverige 🇸🇪

> Komplement-stack till [Anthropics Claude for Small Business](https://github.com/anthropics/knowledge-work-plugins). Inspirerad av samma idé, byggd från grunden för svenska företag — med Bokio som finansiell motor och svenska regelverk som logik.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Skills](https://img.shields.io/badge/Skills-11-blue.svg)](#komplett-skill-översikt)
[![Status](https://img.shields.io/badge/Status-v0.1%20Public%20Beta-orange.svg)](#roadmap)

---

## Varför en separat stack?

I oktober 2025 lanserade Anthropic [Claude for Small Business](https://claude.com/solutions/small-business): 15 skills och 15 workflows som lägger AI inuti QuickBooks, PayPal, HubSpot, DocuSign och Google Workspace. Briljant arbete för amerikanska småföretag.

För svensk SMB stannar nyttan vid hälften. QuickBooks är marginellt här. PayPal likaså. Och inget i originalpaketet hanterar momsperiod, AGI på individnivå, arbetsgivaravgifter 31,42 %, F-skattekontroll, periodisk sammanställning, 3:12-regler eller svensk räntelag och inkassoflöde.

Det här repot fyller gapet. Det är **inte en fork** av Anthropics plugin. Det är en oberoende svensk stack med samma filosofi, skriven från grunden för Bokio och svenskt regelverk.

## Använd båda parallellt

Anthropics SMB-plugin och denna stack är kompletterande, inte konkurrerande. Installera båda.

**Använd Anthropics direkt** för universella uppgifter som inte är landsspecifika:

| Anthropic skill | Vad den gör |
|------------------|-------------|
| `lead-triage` | Prioritera HubSpot-leads med samtalslista |
| `content-strategy` | Generera content-brief från säljdata |
| `canva-creator` | Bygg kampanjmaterial i Canva |
| `customer-pulse` | Aggregera kundfeedback och teman |
| `ticket-deflector` | Drafta tonjusterade kundtjänstsvar |
| `crm-maintenance` | Hygien i HubSpot |
| `contract-review` | Plain-english avtalsgranskning |
| `job-post-builder` | Jobbannons + intervjuguide |
| `business-pulse` | Veckopuls på verksamheten |
| `smb-onboard` | Onboarding av nya kunder |

**Använd vår svenska variant** när Anthropics räcker tekniskt men logiken inte är gjord för Sverige:

| Anthropic skill | Svensk variant | Skillnad |
|-----------------|----------------|----------|
| `cash-flow-snapshot` | `kassa-prognos-30d` | Bokio + Swish/Stripe istället för QuickBooks/PayPal |
| `invoice-chase` | `faktura-paminnelse-svensk` | Räntelagen (referens + 8 %), max 60 kr påminnelseavgift, inkassoflöde enligt IMY |
| `margin-analyzer` | `marginal-analys-bas` | BAS-kontoplan istället för QuickBooks chart of accounts |
| `month-end-prep` | `manadsbokslut-bokio` | Bokio-avstämning, BAS, svenska periodiseringsregler |
| `tax-season-organizer` | `moms-redovisning` | Momsperiod istället för quarterly estimated taxes |

**Endast hos oss** — helt nya skills för specifikt svenska behov:

| Skill | Vad den gör |
|-------|-------------|
| `agi-arbetsgivardeklaration` | Månatlig AGI på individnivå till Skatteverket |
| `f-skatt-bolagskontroll` | Verifiera F-skatt och bolagsstatus hos Skatteverket/Bolagsverket |
| `sie4-export-revisor` | Paketera SIE4-fil för svensk revisor |
| `periodisk-sammanstallning` | EU-försäljning med VIES-validering |
| `k10-faman` | 3:12-räkning för fåmansbolag (gränsbelopp, sparat utdelningsutrymme) |
| `semester-berakning` | Semesterlön enligt Semesterlagen (12 %-regeln, sammalöneprincipen) |

## Komplett skill-översikt

**11 svenska skills:**

| Skill | Vad den löser | Status |
|-------|---------------|--------|
| `moms-redovisning` | Förbereder momsperiodens deklaration ur Bokio | ✅ v1 |
| `agi-arbetsgivardeklaration` | Månatlig AGI på individnivå | ✅ v1 |
| `faktura-paminnelse-svensk` | Påminnelser med lagstadgad ränta och avgifter | ✅ v1 |
| `manadsbokslut-bokio` | Avstämning, P&L, avvikelseflaggor | ✅ v1 |
| `f-skatt-bolagskontroll` | Verifiera nya leverantörer mot Skatteverket | ✅ v1 |
| `sie4-export-revisor` | SIE4-paketering till revisor | 🟡 stub |
| `periodisk-sammanstallning` | EU-försäljning, VIES-validering | 🟡 stub |
| `k10-faman` | 3:12 för fåmansbolag | 🟡 stub |
| `kassa-prognos-30d` | 30-dagars kassaflödesprognos | 🟡 stub |
| `marginal-analys-bas` | Marginalanalys på BAS-kontoplan | 🟡 stub |
| `semester-berakning` | Semesterlön, 12 %-regel, sparade dagar | 🟡 stub |

**4 referenser** med svenska regelverk uppdaterade för 2026:

- `references/arbetsgivaravgifter-2026.md`
- `references/moms-regler.md`
- `references/inkasso-regler.md`
- `references/bokio-mcp-tools.md`

## Hur det fungerar

1. **Installera [Bokio MCP](https://github.com/kirimedia/bokio-mcp)** i Claude Desktop, Code eller Cowork
2. **Installera Anthropics SMB-plugin** för de universella skillsen (`claude plugin install small-business@knowledge-work-plugins`)
3. **Kopiera vår `skills/`-mapp** till din Claude Skills-mapp
4. **Be Claude göra jobbet:** "Förbered momsperioden för Q1" eller "Skicka påminnelser på alla obetalda fakturor över 14 dagar"

Claude använder Bokio MCP för att hämta data, kör analyserna enligt skillens instruktioner, och presenterar resultatet med tydliga next steps. Du godkänner allt innan något skickas, bokförs eller deklareras.

## Snabbstart

```bash
# Klona repot
git clone https://github.com/kirimedia/claude-smb-sverige.git

# Installera Bokio MCP (förutsättning)
git clone https://github.com/kirimedia/bokio-mcp.git
cd bokio-mcp && npm install && npm run build

# Installera Anthropics SMB-plugin (för universella skills)
claude plugin marketplace add anthropics/knowledge-work-plugins
claude plugin install small-business@knowledge-work-plugins

# Kopiera svenska skills till Claude
cp -r claude-smb-sverige/skills/* ~/.claude/skills/
```

Full guide: [INSTALLATION.md](./INSTALLATION.md)

## Vem är det för?

- **Enmansaktiebolag och fåmansbolag** som vill slippa kvällsjobb med moms, lön och fakturering
- **Småföretagare med Bokio** som vill ha en assistent som faktiskt kan svensk bokföring
- **Redovisningskonsulter** som vill paketera kunduppdrag effektivare
- **Developers och AI-konsulter** som bygger AI-lösningar för svenska SMB

## Bidra

Det här är v0.1. Halva stacken är stubs. Bidrag är välkomna, särskilt om du:

- Är auktoriserad revisor eller redovisningskonsult och kan validera regelverk
- Arbetar dagligen i Bokio och vet vart skon klämmer
- Vill bygga ut stubbarna eller lägga till skills för Fortnox/Visma eEkonomi

Se [CONTRIBUTING.md](./CONTRIBUTING.md).

## Roadmap

**v0.2 (Q3 2026):** Fyll ut alla stubs. Lägg till Fortnox- och Visma eEkonomi-MCP-stöd.

**v0.3:** Swish Företag, Stripe Sverige och Klarna-integrationer. Open Banking via Tink.

**v1.0:** Production-ready stack med eval-suite, CI och svenskcertifierade flöden.

**Långsiktigt:** Lägga till "overlay-skills" som utökar Anthropics universella skills med svensk kontext, exempelvis svensk avtalsrätt-overlay på `contract-review` och LAS-overlay på `job-post-builder`.

## Attribution

Strukturen och flera koncept i den här stacken (skills + workflows + router-arkitektur, samt namnvalet och kategoriseringen av återkommande SMB-uppgifter) är inspirerade av [Anthropics Claude for Small Business plugin](https://github.com/anthropics/knowledge-work-plugins).

Detta repo är en **oberoende svensk anpassning**, inte en fork. Inget innehåll är kopierat direkt från Anthropics plugin. Alla skill-instruktioner är skrivna från grunden med svenska regelverk och Bokio som utgångspunkt.

Tack till Anthropic för att de byggde och öppnade konceptet att börja med. Vi rekommenderar att alla användare av denna stack också installerar Anthropics plugin för full täckning av universella SMB-uppgifter.

## Bakgrund

Byggd av [KiriMedia](https://kirimedia.co), en AI-native performance marketing-byrå. Vi använder stacken själva för KiriMedia AB. Skillsen är publicerade open source eftersom svenska småföretag förtjänar samma AI-fördel som amerikanska.

Frågor, feedback eller samarbete: [sebastian@kirimedia.co](mailto:sebastian@kirimedia.co)

## Licens

MIT. Använd den, modifiera den, sälj den. Vi vill bara att svenska småföretag ska få bra AI-stöd.

---

**Inte officiell Anthropic-produkt.** Det här är en oberoende svensk anpassning, byggd på Anthropics öppna Skill-format men separat från Anthropics SMB-plugin. Claude och Anthropic är varumärken som tillhör Anthropic, PBC.

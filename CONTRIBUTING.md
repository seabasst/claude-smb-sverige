# Bidra till Claude för Småföretag — Sverige

Tack för att du vill bidra. Det här repot blir bara bra om svenska redovisningskonsulter, utvecklare och småföretagare deltar.

## Vad vi behöver hjälp med

### Hög prioritet

- **Fyll ut stubbar:** Sex skills är just nu stubbar (`sie4-export-revisor`, `periodisk-sammanstallning`, `k10-faman`, `kassa-prognos-30d`, `marginal-analys-bas`, `semester-berakning`). Plocka en, bygg fullt innehåll.
- **Validering av regelverk:** Är du auktoriserad revisor, redovisningskonsult eller skattejurist? Granska skill-innehållet och flagga fel.
- **Realtests med Bokio:** Kör skillsen på din egen bokföring och rapportera vad som inte funkar.

### Medium prioritet

- **Stöd för Fortnox MCP** parallellt med Bokio
- **Stöd för Visma eEkonomi MCP**
- **Open Banking-integration** (Tink, Plaid) för realtidskassasaldon
- **Stripe Sverige MCP** för avstämning av Stripe-utbetalningar

### Lägre prioritet (men välkommet)

- Översättning till engelska för internationella användare som driver svenskt bolag
- Förbättrad output-formattering (markdown, PDF, Excel)
- Eval-suite för automatisk testning av skills

## Hur du bidrar

### Liten ändring (typo, regelverksuppdatering)

1. Forka repot
2. Skapa branch: `git checkout -b fix/litet-fix`
3. Gör ändringen
4. Commit: `git commit -m "Fix: tydligare formulering i moms-redovisning"`
5. Push och öppna PR

### Större ändring (ny skill, ny integration)

1. Öppna ett Issue först. Beskriv vad du vill bygga.
2. Vänta på diskussion och feedback (vi vill undvika dubbelarbete)
3. Forka och bygg
4. Inkludera:
   - SKILL.md enligt befintligt format
   - Eventuell `references/`-fil med relevant regelverk
   - Uppdatering av README-tabellen
5. Öppna PR

## Skill-format

Alla skills ska:

- Ha en YAML-frontmatter med `name` och `description`
- Description ska vara "pushy" så Claude triggar skillen även om användaren inte uttryckligen ber om den
- Description ska inkludera **trigger-fraser** (på svenska) som användare faktiskt skulle skriva
- Body ska följa strukturen: `När skillen ska köras` → `Förutsättningar` → `Workflow` → `Vanliga felkällor` → `Referenser`
- Aldrig automatisera **inlämning** till myndigheter eller **utskick** till kunder. Producera underlag, låt användaren godkänna.

## Tonalitet

- Direkt och resultatfokuserad
- Inga em-dashes (—). Använd vanliga bindestreck eller punkt.
- Inga onödiga floskler ("I'd be happy to help you with...")
- Svenska i skill-innehåll. Engelska i kommentarer och tekniska delar
- Aldrig referera till "uppgifter Skatteverket eller andra myndigheter inte officiellt publicerar"

## Test innan PR

Innan PR, kör skillen själv mot:

- Ditt eget Bokio-konto (om du har företag)
- Mock-data om du inte har företag

Beskriv testet i PR:n.

## Code of Conduct

Var schysst. Var saklig. Vi är här för att hjälpa svenska småföretag, inte slåss på internet.

## Frågor

Öppna ett Issue eller mejla [sebastian@kirimedia.co](mailto:sebastian@kirimedia.co).

# Bokio MCP — verktygsreferens

Referens för vilka verktyg som finns i [Bokio MCP](https://github.com/kirimedia/bokio-mcp) och vad varje skill behöver anropa.

## Förutsättning

Bokio MCP installerad och autentiserad. Se [INSTALLATION.md](../INSTALLATION.md) i repots rot.

## Tillgängliga verktyg

| Tool | Vad det gör | Vilka skills använder det |
|------|-------------|----------------------------|
| `bokio_customers_list` | Lista kunder | faktura-paminnelse, f-skatt-bolagskontroll |
| `bokio_customers_get` | Hämta en kund | faktura-paminnelse, f-skatt-bolagskontroll |
| `bokio_customers_create` | Skapa kund | (framtida) |
| `bokio_customers_update` | Uppdatera kund | (framtida) |
| `bokio_invoices_list` | Lista fakturor | faktura-paminnelse, kassa-prognos, manadsbokslut |
| `bokio_invoices_get` | Hämta en faktura | faktura-paminnelse |
| `bokio_invoices_create` | Skapa faktura | (framtida) |
| `bokio_invoices_line_items_list` | Lista fakturarader | manadsbokslut, marginal-analys |
| `bokio_journal_entries_list` | Lista bokföringsverifikat | moms-redovisning, manadsbokslut, sie4-export, marginal-analys |
| `bokio_items_list` | Lista lagerartiklar | (om relevant för bolaget) |
| `bokio_uploads_list` | Lista uppladdade filer | manadsbokslut (kvittokontroll) |
| `bokio_uploads_get` | Hämta uppladdad fil | manadsbokslut |
| `bokio_uploads_download` | Ladda ner fil | sie4-export |

## Mappning skill → tool

### moms-redovisning

```
1. bokio_journal_entries_list  (period: aktuell momsperiod)
   → filtrera på konton 2610-2627, 2640-2647, 3000-3999
2. Räkna ihop per momsruta
3. Returnera underlag
```

### agi-arbetsgivardeklaration

```
1. bokio_journal_entries_list  (period: aktuell utbetalningsmånad)
   → filtrera på konton 7010-7299, 7510-7570
2. Per anställd: hämta saldon
3. Returnera AGI-underlag
```

### faktura-paminnelse-svensk

```
1. bokio_invoices_list  (status: openOverdue)
2. För varje:
   - bokio_invoices_get (för fakturadetaljer)
   - bokio_customers_get (för kunduppgifter)
3. Räkna ränta och avgifter
4. Generera påminnelseutkast
```

### manadsbokslut-bokio

```
1. bokio_journal_entries_list  (hela månaden)
2. bokio_invoices_list  (öppna)
3. Stäm av konto för konto
4. Generera P&L och balansrapport
```

### f-skatt-bolagskontroll

```
Använder INTE Bokio MCP primärt.
Använder offentliga källor:
- Skatteverkets F-skattregister (web scraping eller API om tillgängligt)
- Bolagsverket
- VIES (för EU-VAT)

Bokio MCP används endast för:
- bokio_customers_get (om kunden redan finns i registret)
```

## Saknade verktyg

Följande verktyg finns inte i nuvarande Bokio MCP men skulle behövas för full täckning. Bidrag välkomna:

- `bokio_company_settings_get` — Bolagets inställningar (momsperiod, räkenskapsår, etc.)
- `bokio_balance_sheet_get` — Balansrapport för viss period
- `bokio_income_statement_get` — Resultatrapport för viss period
- `bokio_sie4_export` — Exportera SIE4-fil för viss period
- `bokio_employees_list` — Lista anställda
- `bokio_payroll_runs_list` — Lista lönekörningar
- `bokio_tax_account_get` — Skattekontosaldo (kräver Bokio-integration mot Skatteverket)

## Bidra med MCP-utvecklingen

Bokio MCP är öppen källkod under MIT. Pull requests välkomna på:
[https://github.com/kirimedia/bokio-mcp](https://github.com/kirimedia/bokio-mcp)

## Felsökning

### "Bokio MCP not authenticated"

```bash
cd ~/bokio-mcp
npm run auth
```

### "Company not found"

Verifiera att rätt bolag är valt i Bokio MCP-konfigurationen. Om bolagsbyte behövs:

```bash
cd ~/bokio-mcp
npm run select-company
```

### Verktyg returnerar tomma resultat

Kontrollera att perioden är korrekt formaterad (ISO 8601: `2026-01-01` till `2026-03-31`).

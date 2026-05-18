# Installation — Claude för Småföretag, Sverige

Guide för att komma igång med stacken. Tar 10–20 minuter att sätta upp.

## Förutsättningar

- En dator med macOS, Windows eller Linux
- Node.js 20 eller senare ([installation](https://nodejs.org))
- Git
- **Claude Desktop**, **Claude Code**, eller **Claude Cowork**
- Ett Bokio-konto med API-tillgång aktiverad

## Steg 1: Installera Bokio MCP

Bokio MCP är förutsättning. Du behöver den för att Claude ska kunna prata med din bokföring.

```bash
git clone https://github.com/kirimedia/bokio-mcp.git
cd bokio-mcp
npm install
npm run build
```

Konfigurera autentisering enligt repots egen guide. Du behöver Bokio API-nyckel.

## Steg 2: Klona det här repot

```bash
git clone https://github.com/kirimedia/claude-smb-sverige.git
```

## Steg 3: Installera skills

### Alternativ A: Claude Desktop

Kopiera skill-mapparna till din Claude Skills-mapp.

**macOS:**
```bash
mkdir -p ~/Library/Application\ Support/Claude/skills/
cp -r claude-smb-sverige/skills/* ~/Library/Application\ Support/Claude/skills/
```

**Windows:**
```cmd
xcopy /E claude-smb-sverige\skills %APPDATA%\Claude\skills\
```

**Linux:**
```bash
mkdir -p ~/.config/Claude/skills/
cp -r claude-smb-sverige/skills/* ~/.config/Claude/skills/
```

### Alternativ B: Claude Code

Skapa eller redigera `~/.claude/skills/` och lägg till skill-mapparna där.

```bash
mkdir -p ~/.claude/skills/
cp -r claude-smb-sverige/skills/* ~/.claude/skills/
```

### Alternativ C: Claude Cowork

I Claude Cowork: dra och släpp varje `SKILL.md`-fil till "Skills"-fliken i appen.

## Steg 4: Konfigurera Claude Desktop / Code

Lägg till Bokio MCP i din `claude_desktop_config.json` (Claude Desktop) eller `mcp.json` (Claude Code).

**Exempel:**

```json
{
  "mcpServers": {
    "bokio": {
      "command": "node",
      "args": ["/path/to/bokio-mcp/build/index.js"],
      "env": {
        "BOKIO_API_KEY": "din-api-nyckel-här",
        "BOKIO_COMPANY_ID": "ditt-bolags-id"
      }
    }
  }
}
```

Starta om Claude Desktop / Code.

## Steg 5: Verifiera installation

Öppna Claude och säg:

```
Lista alla skills du har för svenska småföretag.
```

Claude ska svara med listan över de 11 skills i den här stacken.

Säg sedan:

```
Använd Bokio MCP och visa mig de senaste fakturorna.
```

Om det fungerar är allt klart.

## Steg 6: Testa en skill

Pröva med något lågrisk:

```
Förbered en bolagskontroll för Bolagsverket org.nr 559123-4567.
```

Eller om du har en pågående momsperiod:

```
Förbered momsdeklarationen för aktuellt kvartal.
```

Granska resultatet noga. Kom ihåg att skillsen alltid producerar **underlag**, aldrig skickar in eller bokför något automatiskt.

## Felsökning

### "Skills not found"

Verifiera att skill-mapparna ligger på rätt plats och har `SKILL.md`-fil i varje mapp:

```bash
ls -la ~/.claude/skills/moms-redovisning/SKILL.md
```

### "Bokio MCP timeout"

API-nyckeln kan ha gått ut eller behöver scope:n uppdateras. Återgenerera nyckeln i Bokios inställningar.

### "Cannot read accounts"

Verifiera att Bokio MCP har rätt bolag konfigurerat. Om du har flera bolag i Bokio, sätt `BOKIO_COMPANY_ID` korrekt i konfigurationen.

## Säkerhet

- Bokio MCP körs lokalt på din maskin
- API-nycklar lagras i din miljö, inte i molnet
- Inga av skills skickar data utanför Claude
- Användaren godkänner alla utgående åtgärder

## Support

- **Bokio MCP-issues:** [github.com/kirimedia/bokio-mcp/issues](https://github.com/kirimedia/bokio-mcp/issues)
- **Skill-issues:** [github.com/kirimedia/claude-smb-sverige/issues](https://github.com/kirimedia/claude-smb-sverige/issues)
- **Övriga frågor:** [sebastian@kirimedia.co](mailto:sebastian@kirimedia.co)

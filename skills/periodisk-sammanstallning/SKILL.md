---
name: periodisk-sammanstallning
description: Sammanställer kvartalsvis periodisk sammanställning för EU-försäljning (varor och tjänster), validerar köparnas VAT-nummer mot VIES, och förbereder underlag för inlämning till Skatteverket. Använd skillen när användaren nämner "periodisk sammanställning", "EU-försäljning", "VIES", "moms EU", "kvartalsrapport EU", "OMP", "intrastat". Trigga också på "har jag sålt något till EU", "vad ska jag rapportera om EU-försäljningen".
---

# Periodisk sammanställning för EU-försäljning

## Status: STUB — bidra gärna

Skillen ska:

1. Hämta alla försäljningar bokförda på 3105, 3106, 3108 (EU-försäljning) från Bokio
2. För varje köpare:
   - Validera VAT-nummer mot VIES API
   - Verifiera att fakturan är märkt med rätt momskoder (omvänd skattskyldighet)
3. Summera per köpare och momsperiod (kvartal)
4. Generera underlag för Skatteverkets eTjänst (CSV eller XML)
5. Flagga:
   - Fakturor utan giltigt VAT-nummer på köparen
   - Försäljningar bokförda som EU men där köparen är svensk
   - Försäljningar över Intrastat-gränsen (varor, just nu 9 MSEK för utförsel)

## TODO

- [ ] VIES API-integration för automatisk validering
- [ ] Stöd för OMP (One-Stop-Shop) för digitala tjänster till privatpersoner i EU
- [ ] Intrastat-tröskelvarning
- [ ] Underlagsformat enligt Skatteverkets exakta specifikation

## Referenser

- [VIES VAT Validation](https://ec.europa.eu/taxation_customs/vies/)
- [Skatteverket: Periodisk sammanställning](https://www.skatteverket.se/foretag/skatterochavdrag/moms/periodisksammanstallning.4.18e1b10334ebe8bc8000984.html)

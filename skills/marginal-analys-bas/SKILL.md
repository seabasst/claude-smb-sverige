---
name: marginal-analys-bas
description: Räknar marginaler på företaget enligt svensk BAS-kontoplan, inklusive bruttomarginal, täckningsbidrag, EBITDA, rörelsemarginal och nettomarginal. Bryter ner kostnadsstrukturen i fasta vs rörliga och identifierar vilka kostnadskategorier som drar mest. Använd skillen när användaren nämner "marginal", "marginaler", "bruttomarginal", "lönsamhet", "är vi lönsamma", "TB", "täckningsbidrag", "EBITDA", "kostnadsanalys", "var går pengarna". Trigga också på "varför är resultatet så lågt", "kan vi öka marginalen", "analysera kostnaderna".
---

# Marginalanalys på BAS-kontoplan

## Status: STUB — bidra gärna

Skillen ska:

1. Hämta resultaträkning från Bokio för vald period
2. Klassificera kostnader enligt BAS-kontoklasser:
   - 4xxx: Material och varor (rörlig)
   - 5xxx: Övriga externa kostnader (delvis rörlig)
   - 6xxx: Övriga externa kostnader (mest fast)
   - 7xxx: Personalkostnader (semi-fast)
   - 8xxx: Finansiella poster
3. Räkna ut:
   - **Bruttomarginal** = (Omsättning - Kostnad sålda varor) / Omsättning
   - **TB1** = Omsättning - direkta rörliga kostnader
   - **TB2** = TB1 - direkt fasta kostnader
   - **EBITDA** = Resultat före räntor, skatt, av- och nedskrivningar
   - **Rörelsemarginal** = EBIT / Omsättning
   - **Nettomarginal** = Resultat efter skatt / Omsättning
4. Jämförelse:
   - Mot föregående period
   - Mot motsvarande period i fjol
   - Mot industristandard (om data finns)
5. Top-5 kostnader med procent av omsättning
6. Identifiera kostnadskategorier som "drar i sär" från historiskt mönster

## TODO

- [ ] Branschbenchmark-data för svenska SMB
- [ ] Visualisering med vattenfallsdiagram (omsättning → kostnader → resultat)
- [ ] AI-genererad "berättelse" om varför marginalen rört sig

## Referenser

- BAS-kontoplan (BAS-kontogruppen)
- `references/bas-kontoplan-2026.md`

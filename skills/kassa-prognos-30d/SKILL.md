---
name: kassa-prognos-30d
description: Bygger 30-dagars kassaflödesprognos baserat på Bokio-data: nuvarande bankposition, förväntade inbetalningar från öppna fakturor (med riskviktning per kund), kända utbetalningar (lön, hyra, moms, AGI, leverantörsfakturor), och återkommande prenumerationer. Använd skillen när användaren nämner "kassaflöde", "cashflow", "likviditet", "kassaprognos", "klarar vi månaden", "hur mycket pengar har vi", "förfaller fakturor", "vad ska vi betala". Trigga också på "klarar vi lönen", "kan jag betala momsen", "håller likviditeten".
---

# 30-dagars kassaflödesprognos

## Status: STUB — bidra gärna

Skillen ska:

1. Hämta nuvarande bankposition från Bokio (konto 1930) + Stripe/Klarna-saldon
2. Hämta öppna kundfakturor (1510) med förfallodatum
3. Riskvikta inkommande betalningar:
   - Förfallna fakturor < 30 dagar: 80 % sannolikhet
   - 30–60 dagar: 60 %
   - 60–90 dagar: 30 %
   - 90+ dagar: 10 %
   - Specifika kunder med historik: ange individuell sannolikhet
4. Lista kommande utbetalningar (säkra):
   - Lön (utbetalningsdatum)
   - Skattebetalning (moms, AGI — datum från skatteverket)
   - Hyror, prenumerationer (återkommande)
   - Leverantörsfakturor med förfallodatum
5. Generera daglig prognos i 30 dagar
6. Flagga:
   - Dagar med risk för negativ kassa
   - Buffert vs målnivå
   - Stora utbetalningar som kommer

## TODO

- [ ] Visualisering som linjediagram eller stapeldiagram
- [ ] Scenarioplanering ("vad händer om kund X betalar sent")
- [ ] Integrationsstöd för Open Banking via Tink (realtidsbalans)
- [ ] Återkommande prenumerationer från Stripe/Klarna

## Referenser

- Standardpraxis för SMB-cashflow-modellering
- Bokios fakturarapport-API

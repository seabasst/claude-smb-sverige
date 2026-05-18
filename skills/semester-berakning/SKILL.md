---
name: semester-berakning
description: Beräknar semesterlön, semesterersättning och sparade semesterdagar enligt svenska Semesterlagen (1977:480). Hanterar både 12 %-regeln (vanlig för månadslön) och sammalöneprincipen. Använd skillen när användaren nämner "semester", "semesterlön", "semesterersättning", "sparade semesterdagar", "semesterlönegrundande", "semestertillägg", "12 procent semester". Trigga också på "hur mycket semesterlön ska jag betala", "räkna semestern", "när tjänar man in semester", "vad får jag i semesterersättning vid uppsägning".
---

# Semesterberäkning enligt Semesterlagen

## Status: STUB — bidra gärna

Skillen ska:

1. Hämta från Bokio + lönesystem:
   - Intjänandeår (1 april - 31 mars) och uttagsår
   - Bruttolön under intjänandeåret
   - Antal anställningsdagar
   - Frånvaro som inte är semesterlönegrundande
   - Eventuell sparad semester från tidigare år
2. Räkna semesterdagar enligt avtal eller lag:
   - Lagminimum: 25 dagar (varav 20 sammanhängande)
   - Vanliga kollektivavtal: 25–30 dagar
3. Räkna semesterlön:
   - **12 %-regeln:** 12 % av semesterlönegrundande bruttolön
   - **Sammalöneprincipen:** ordinarie månadslön + semestertillägg om 0,43 % per dag (provanställning, kollektivavtal)
4. Sparade dagar (Semesterlagen § 18):
   - Max 25 dagar sammanlagt får sparas
   - Sparade dagar måste tas ut inom 5 år
5. Semesterersättning vid uppsägning:
   - Outtagen semesterlön ska betalas ut direkt
6. Output:
   - Bokföringsförslag på 2920 (semesterlöneskuld)
   - Förslag på lönespecifikationsrader
   - Underlag för anställdas semesterbesked

## TODO

- [ ] Hantera olika kollektivavtal (Unionen, IF Metall, Handels)
- [ ] Spara semesterhistorik per anställd
- [ ] Förmånsberäkning om semester växlas mot tjänstebil eller liknande

## Referenser

- [Semesterlagen (1977:480)](https://www.riksdagen.se/sv/dokument-och-lagar/dokument/svensk-forfattningssamling/semesterlag-1977480_sfs-1977-480/)
- Eventuellt tillämpligt kollektivavtal

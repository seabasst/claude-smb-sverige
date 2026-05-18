---
name: k10-faman
description: Beräknar gränsbelopp enligt 3:12-reglerna för fåmansbolagsägare (K10-blanketten), inklusive löneunderlagsregel (huvudregel) och förenklingsregel. Räknar både årets gränsbelopp och sparade utdelningsutrymmen från tidigare år. Använd skillen när användaren nämner "K10", "3:12", "fåmansbolag", "gränsbelopp", "utdelning", "lågbeskattad utdelning", "förenklingsregel", "huvudregel", "löneuttag fåmansbolag", "kvalificerade andelar". Trigga också på "hur mycket utdelning kan jag ta lågbeskattat", "räkna K10 för i år", "behöver jag ta mer lön".
---

# K10 och 3:12-regler för fåmansbolag

## Status: STUB — kritisk skill för enmansaktiebolag och fåmansbolag

Skillen ska:

1. Hämta från Bokio:
   - Totala kontanta löner till anställda och ägare för året
   - Ägarens egen löneuttag
   - Antal anställda
   - Bolagets utgående anskaffningsutgift för aktierna
2. Beräkna **förenklingsregeln** (Schablonbelopp):
   - 2026: cirka 217 250 kr (2,75 IBB)
   - Fördelas över antal aktier
3. Beräkna **huvudregeln** (löneunderlagsregel):
   - Lönekrav uppfyllt? (10 IBB + 5 % av total lönesumma)
   - 50 % av total kontant lönesumma
   - Plus index på anskaffningsutgift
4. Välj det högsta av de två
5. Lägg till **sparat utdelningsutrymme** från tidigare år (uppräknat med 3 % + statslåneräntan)
6. Föreslå:
   - Hur mycket utdelning som kan tas lågbeskattat (20 %)
   - Om mer löneuttag behövs detta år för att kvalificera för huvudregeln nästa år
   - Tidsplan för utdelning
7. Generera underlag för K10-blanketten

## Varför detta är kritiskt

För svenska fåmansbolagsägare är 3:12 ofta skillnaden mellan 20 % och 57 % skatt på utdelning. Att missa lönekravet ett år gör att man tappar miljonbelopp i sparat utdelningsutrymme över tid.

## TODO

- [ ] Korrekta IBB-värden för aktuellt år
- [ ] Hantering av närstående (lön till make/maka räknas inte alltid)
- [ ] Sparat utdelningsutrymme från tidigare K10-blanketter (be om input eller läs in)
- [ ] Stöd för bolag med flera ägare
- [ ] Räkneexempel som visar tröskelpunkter

## Referenser

- [Skatteverket: 3:12-reglerna](https://www.skatteverket.se/foretag/drivaforetag/famansforetag.4.18e1b10334ebe8bc80003999.html)
- [K10-blanketten](https://www.skatteverket.se/privat/etjansterochblanketter/blanketterbroschyrer/blanketter/info/2110.4.39f16f103821c58f680006807.html)

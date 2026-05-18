# Månatlig rutin — sekvens av skills

En sammanhängande rutin du kan köra första veckan i varje månad. Tar normalt 30–60 minuter och täcker det mesta av en svensk småföretagares ekonomiansvar.

## Veckoschema

### Måndag morgon

```
Kör manadsbokslut-bokio för föregående månad
```

Claude stämmer av banken, kontrollerar transaktioner, genererar P&L. Du åtgärdar eventuella flaggade poster.

### Måndag eftermiddag

```
Kör moms-redovisning för aktuell momsperiod
```

Bara om det är månad där momsperiod slutar (varje månad om månadsmoms, varje kvartal om kvartalsmoms).

### Tisdag

```
Kör agi-arbetsgivardeklaration för föregående månad
```

Om du har anställda eller tar ut egen lön. Slutförs och deklareras senast den 12:e.

### Onsdag

```
Kör faktura-paminnelse-svensk på alla obetalda fakturor
```

Claude listar förfallna fakturor med rätt åtgärdsnivå. Du granskar och skickar utkasten.

### Torsdag (kvartalsvis)

Om kvartalsslut närmar sig:

```
1. Kör periodisk-sammanstallning för EU-försäljning
2. Kör sie4-export-revisor och skicka till din revisor/redovisningskonsult
```

### Fredag (årligen, jan/feb)

Vid årsbokslut:

```
1. Kör k10-faman om du är fåmansbolagsägare
2. Förbered underlag för INK2 och K10 till deklarationen
```

## När går rutinen fel?

### Bankavstämning stämmer inte

Kör `manadsbokslut-bokio` igen och be Claude specifikt:

> Stäm av konto 1930 mot bankutdraget i bifogad fil. Lista alla skillnader.

### Moms ser konstigt ut

Kör `moms-redovisning` och be:

> Visa alla verifikat där momskoden verkar fel. Föreslå rättningar.

### Glömd löneutbetalning

Innan AGI-deadline den 12:e:

> Kör agi-arbetsgivardeklaration och flagga alla anställda med oväntade saldon.

## Före årsskifte (november–december)

```
1. f-skatt-bolagskontroll på alla aktiva leverantörer
2. Granska sparat utdelningsutrymme (k10-faman) inför nästa år
3. Förbered eventuella sista löneuttag för att kvalificera huvudregeln
```

## Anpassa rutinen

Den här mallen passar de flesta fåmansbolag med 0–5 anställda. Stora variationer:

- **Renodlat e-handelsbolag:** Lägg in Stripe-avstämning, Klarna-rapport
- **Konsultbolag:** Mindre lagerhantering, fokus på fakturering och 3:12
- **Restaurang eller butik:** Daglig kassaavstämning, swish-redovisning, personalliggare

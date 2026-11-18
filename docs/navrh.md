# Pracovní návrh

Tento text je podklad k diskusi, ne hotová specifikace. Vychází z [issue 166](https://github.com/sarsonj/rodokmen-skill/issues/166) a z [návrhu pro SOA v Třeboni](../materialy/Matriky_at_home_SOA_Trebon.pdf). Všechny ukázky dat jsou vymyšlené.

## Dva vstupy do archivu

| | Portál | Hub |
| --- | --- | --- |
| Pro koho | hlavně pro lidi | hlavně pro stroje, může ho použít i člověk |
| Co nabízí | prohlížení matrik jako dnes | text, podepsané odkazy na snímky, odevzdání přepisů |
| Ochrana | archiv ji může nastavit naplno | řízený přístup, rozsah a tempo určuje archiv |

Dnes se lidé i skripty tlačí v jednom prohlížeči a archiv se může bránit jen plošnými omezeními. Se dvěma vstupy může skripty na portálu blokovat a stroje přitom mají legální cestu.

## Podepsané odkazy

Hub snímky nepřenáší ani neukládá.

1. **Hub vydá odkaz.** Platí pro jeden snímek a krátce, nese pseudonym přispěvatele a je podepsaný klíčem, který zná jen hub a archiv.
2. **Archiv ověří podpis.** Sám, bez dotazu na hub. Neplatný nebo prošlý odkaz odmítne. Stažení bez odkazu zůstávají v běžných limitech.
3. **Přispěvatel vrátí přepis.** Pošle ho hubu. Kdo ho nevrátí, další odkaz nedostane.
4. **Hub předá výsledek.** Ověřené přepisy průběžně putují archivu.

Ověření podpisu umějí běžné webové servery, například nginx modulem `secure_link`. Zda to půjde v konkrétním archivu, musíme zjistit.

Když na straně archivu nepůjde nic nastavit, zbývají dvě náhradní cesty:

- snímky stahuje jen hub z jedné povolené adresy, v dohodnutém tempu,
- archiv předá jednorázovou kopii pilotního souboru, která se po pilotu smaže.

## Případ 1: volná kapacita

Předplatné AI má limity, které se pravidelně obnovují. Když je badatel nevyužije, jeho agent si řekne o práci.

1. Agent se ohlásí hubu.
2. Hub mu přidělí pracovní jednotku s metadaty a podepsaným odkazem. Jednotka je rezervovaná na omezenou dobu.
3. Agent snímek přečte a vrátí JSON.
4. Hub tutéž jednotku přidělí jinému agentovi, který první čtení nevidí.
5. Shodná čtení projdou, rozpory jdou k člověku.

Když agent práci nedokončí, rezervace i odkaz vyprší a jednotka se přidělí jinému.

Co může hub poslat:

```json
{
  "jednotka": "trebon/N-sv7/snimek-045",
  "odkaz": "https://archiv.example/045.jpg?podpis=...",
  "archiv": "SOA v Třeboni",
  "signatura": "matrika N, sv. 7",
  "farnost": "Vesnice",
  "roky": [1841, 1845],
  "druh": "narození",
  "jazyk": ["latina", "němčina"],
  "rezervace_do": "2026-11-12T20:00:00+01:00"
}
```

Co může agent vrátit:

```json
{
  "jednotka": "trebon/N-sv7/snimek-045",
  "cetl": "model a verze nástroje",
  "zapisy": [
    {
      "datum": "1843-03-12",
      "dum": 17,
      "dite": { "doslovne": "Joannes", "cesky": "Jan" },
      "otec": { "doslovne": "Wenzl Nowak", "cesky": "Václav Novák" },
      "jistota": 0.86
    }
  ]
}
```

## Případ 2: badatel hledá konkrétní stránku

- **Stránka je přečtená:** hub vrátí hotový text v JSON, bez snímku.
- **Stránka přečtená není:** hub vydá podepsaný odkaz a badatel musí vrátit přepis celé stránky, ne jen hledaného zápisu. Tím vzniká první čtení, druhé hub přidělí jinému agentovi. Kdo přepis nevrátí, dalším požadavkům se nevyhoví.

## Originál na vyžádání

Badatel může chtít originál i k přečtené stránce, třeba jako doklad do rodokmenu. Pokud to archiv dovolí, hub k němu vydá podepsaný odkaz, cíleně a s denním limitem. K hromadnému procházení to nevede: badatel nejdřív v textu najde, na kterých stránkách jeho předci jsou, a originál si vyžádá jen k nim.

## Kvalita

- Každý snímek čtou dva přispěvatelé nezávisle, nejlépe různými nástroji.
- Mezi úkoly se přimíchají kontrolní snímky se známým správným přepisem.
- U každého čtení je uvedený přispěvatel a nástroj, aby šlo slabší čtení najít a zopakovat.
- Rozpory rozhoduje člověk nad originálem. Archiv může kontrolovat vzorky.
- Zápis prochází stavy: přečteno strojově, shoda dvou čtení, ověřeno člověkem, potvrzeno archivem.

## Dvě vrstvy přepisu

- **Doslovná vrstva** zachycuje, co je ve snímku napsáno. Nepřepisuje se a čtení se porovnávají na ní.
- **Normalizovaná vrstva** slouží k hledání, například `Joannes` jako `Jan`.

Opravy jsou dobrovolné a ukládají se jako samostatné záznamy s autorem, takže původní čtení zůstává dohledatelné.

## Hostování hubu

| | U archivu | CESNET | Komunitní server |
| --- | --- | --- | --- |
| Práce pro IT archivu | instalace, dohled, ověřování odkazů | nastavení ověřování odkazů | nastavení ověřování odkazů |
| Náklady pro archiv | výkon vlastního serveru | žádné | žádné |
| Přepisy | přímo u archivu | průběžně předávané | průběžně předávané |
| Rozjezd | podle kapacit archivu | nejpomalejší, nejspíš s akademickým partnerem | nejrychlejší |
| Dlouhodobý provoz | archiv | instituce | závisí na komunitě |

Varianty lze kombinovat, například pilot na komunitním serveru a dlouhodobý provoz jinde. Podmínky CESNET zatím neznáme.

## Co potřebujeme od archivu

- souhlas s pilotem a jednu kontaktní osobu,
- souhlas se strojovým přístupem k pilotním svazkům přes podepsané odkazy,
- souhlas se strojovým přepisem a se zveřejněním výsledného textu.

Nepotřebujeme vývoj na straně archivu, předání dat ani zveřejnění snímků mimo jeho systém. Pokud něco nedovolí smlouvy s digitalizátory, pilot může začít u fondů, kterých se to netýká.

## Pilot

Rozsah: jedna farnost nebo menší fond, řádově stovky až nízké tisíce snímků.

1. **Dohoda:** výběr souboru, podoba souhlasu, přístup ke snímkům, místo běhu hubu, kontaktní osoby.
2. **Příprava:** formát dat, kontrolní snímky, spuštění hubu, nastavení odkazů.
3. **Zpracování:** dvojí čtení, řešení rozporů, přehled pro archiv.
4. **Vyhodnocení:** přesnost, náklady na snímek, úspora provozu, zkušenost archivu a rozhodnutí, zda pokračovat.

## Podněty k technickému řešení

Z diskuse vzešly tyto návrhy. Zatím nejsou rozhodnuté:

- IIIF pro odkazování na snímky, W3C Web Annotation pro přepisy a Linked Data pro souvislosti,
- jednotné API nebo MCP, které lze nasadit vedle systémů archivu i u jiného poskytovatele,
- `User-Agent` s kontaktem na provozovatele, odpovědi `429` a `503` a hlavičky `X-RateLimit`,
- možnost vyžádat si knihu do rychlejšího úložiště s oznámením přes webhook.

Na formát by mělo navázat nebo se s ním sladit [matriky-index](https://github.com/pe-pan/matriky-index).

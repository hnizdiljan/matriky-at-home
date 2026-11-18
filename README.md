# Matriky@home

Komunitní iniciativa, jejímž cílem je převést digitalizované matriky z českých archivů do ověřeného, prohledávatelného textu. Práci by odvedli genealogové se svými AI agenty, ale **ve spolupráci s archivy a za jejich podmínek**. Název odkazuje na projekt SETI@home.

> **Stav: začínáme.** Neběží žádný hub, neexistuje kód a žádný archiv se k návrhu zatím nezavázal. Repozitář slouží k tomu, abychom se shodli na návrhu a archivům psali jednotně.

## Proč

Lidí, kteří čtou matriky s pomocí AI, rychle přibývá. Každý z nich stahuje tytéž snímky znovu a výsledek mu zůstane v soukromém rodokmenu. Archivům to přináší hlavně zátěž serverů a starosti s dodržováním podmínek.

Když sto badatelů hledá na stejné stránce, stáhne se dnes stokrát. Tady by se stáhla dvakrát, pro dvě nezávislá čtení. Ostatní by dostali hotový text a originál by si vyžádali, jen když ho opravdu potřebují.

## Jak by to fungovalo

- **Portál pro lidi, hub pro stroje.** Archiv si nechá svůj prohlížeč matrik a může ho chránit proti robotům. Stroje dostanou vlastní řízený vstup.
- **Hub snímky nepřenáší ani neukládá.** Přispěvateli vydá podepsaný odkaz do archivu, platný krátce a jen pro jeden snímek. Archiv si podpis ověří sám a ví, že stažení patří k projektu.
- **Za snímek přepis.** Kdo dostane odkaz, vrátí přepis celé stránky. Kdo přepisy nevrací, další odkazy nedostane.
- **Dvě nezávislá čtení.** Shodná čtení projdou, rozpory rozhodne člověk nad originálem.
- **Výsledek patří i archivu.** Ověřené přepisy se průběžně vracejí archivu.

Podrobnosti jsou v [návrhu](docs/navrh.md).

## Zásady

1. O rozsahu, tempu a podmínkách rozhoduje archiv.
2. Neobcházíme ochrany archivů a nestahujeme hromadně bez jejich souhlasu.
3. Snímky matrik do tohoto repozitáře nepatří.
4. Zveřejňují se jen zápisy po uplynutí zákonných lhůt: narození 100 let, sňatky a úmrtí 75 let.
5. Každý přepsaný zápis odkazuje na konkrétní snímek v archivu. Přepis originál nenahrazuje.
6. Archivům píšeme sladěně, aby nedostávaly od každého něco jiného.

## Co tady najdete

| Soubor | Obsah |
| --- | --- |
| [docs/navrh.md](docs/navrh.md) | Pracovní návrh modelu, případy užití, kvalita, hostování a pilot |
| [docs/otevrene-otazky.md](docs/otevrene-otazky.md) | Co ještě nemáme rozhodnuté |
| [docs/kontakty-archivu.md](docs/kontakty-archivu.md) | Kdo koho oslovil a s jakým výsledkem |
| [materialy/Matriky_at_home_SOA_Trebon.pdf](materialy/Matriky_at_home_SOA_Trebon.pdf) | Grafický návrh spolupráce připravený pro SOA v Třeboni |
| [materialy/matriky_jako_text.html](materialy/matriky_jako_text.html) | Zdroj tohoto PDF |

## Nejbližší kroky

1. Sladit, co a jak říkáme archivům, a doplnit přehled kontaktů.
2. Zjistit od archivů, co je skutečně trápí a co by mohly přijmout.
3. Popsat formát přepisu a vazbu na existující standardy.
4. Připravit malou ukázku podepsaného odkazu a odevzdání přepisu.

## Jak se zapojit

Založte issue, pošlete pull request, nebo se připojte k [původní diskusi](https://github.com/sarsonj/rodokmen-skill/issues/166). Hodí se zkušenosti s archivy a jednáním s veřejnou správou, čtení starého písma, provoz serverů, návrh API i práce s AI agenty.

Pokud jste některý archiv nebo instituci oslovili, doplňte to prosím do [přehledu kontaktů](docs/kontakty-archivu.md).

## Odkud to vzešlo

Nápad vznikl v [issue 166](https://github.com/sarsonj/rodokmen-skill/issues/166) projektu [rodokmen-skill](https://github.com/sarsonj/rodokmen-skill). Důležitý kontext je v [issue 91](https://github.com/sarsonj/rodokmen-skill/issues/91), kde SOA v Třeboni vysvětlil své podmínky pro snímky v DigiArchivu.

## Licence

Licence repozitáře ani budoucích dat zatím není zvolená, viz [otevřené otázky](docs/otevrene-otazky.md).

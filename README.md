# Claude Skills Clean — ChatGPT / Claude Project README

Ez a README azt írja le, hogyan érdemes a megtisztított `claude-skills-clean` csomagot ChatGPT Projectként vagy Claude Projectként használni. A cél nem az, hogy az LLM egyszerre betöltse az összes skillt, hanem az, hogy az `index.json` alapján kiválassza a megfelelő skillt, majd csak a szükséges `SKILL.md`, `references/`, `scripts/`, `assets/` és példafájlokat használja.

## Csomag célja

A csomag egy skill-router alapú tudásbázis. A projektbe feltöltött `index.json` megmondja, milyen skillek vannak, hol találhatók, melyikhez milyen referencia- és scriptfájl tartozik. A projekt instrukciói arra kényszerítik az LLM-et, hogy a felhasználói kérés kontextusa alapján válasszon skillt, és ne olvassa be feleslegesen a teljes csomagot.

## Fő fájlok

| Fájl | Kötelező? | Funkció |
|---|---:|---|
| `claude-skills-index.json` | igen | Skill-katalógus: kategóriák, útvonalak, leírások, címkék, fájllisták. |
| `PERSONA_SKILL_LOADER_PROMPT_HU.md` | igen | Beilleszthető LLM instrukció a skillválasztáshoz és betöltéshez. |
| `claude-skills-clean.zip` | ajánlott | A tisztított forráscsomag, benne minden skill és saját kapcsolódó fájlja. |
| `README_PROJECT_SETUP_HU.md` | ajánlott | Ez az útmutató. |
| `PROJECT_UPLOAD_MANIFEST.json` | ajánlott | Gépileg olvasható feltöltési és használati manifest. |
| `CHATGPT_CLAUDE_PROJECT_INSTRUCTIONS_HU.md` | ajánlott | Rövidített, közvetlenül bemásolható projektinstrukció. |

## Skill-leltár

| Kategória | Konkrét skillek | Összes `SKILL.md` | Kategória-bundle |
|---|---:|---:|---|
| `business-growth/` | 4 | 5 | `business-growth/SKILL.md` |
| `c-level-advisor/` | 33 | 34 | `c-level-advisor/SKILL.md` |
| `engineering/` | 61 | 62 | `engineering/SKILL.md` |
| `engineering-team/` | 50 | 51 | `engineering-team/SKILL.md` |
| `finance/` | 3 | 4 | `finance/SKILL.md` |
| `marketing-skill/` | 44 | 45 | `marketing-skill/SKILL.md` |
| `product-team/` | 16 | 17 | `product-team/SKILL.md` |
| `project-management/` | 8 | 9 | `project-management/SKILL.md` |
| `ra-qm-team/` | 13 | 14 | `ra-qm-team/SKILL.md` |

Összesítés: 9 fő kategória, 241 `SKILL.md`, 9 kategória-bundle, 232 konkrét skill.

## Javasolt projektstratégia

A legmegbízhatóbb működéshez kétlépcsős használat ajánlott.

Első szint: mindig legyen feltöltve a `claude-skills-index.json` és a projektinstrukció. Ez elég a skill kiválasztásához.

Második szint: a kiválasztott skill tényleges fájljait vagy a teljes `claude-skills-clean.zip` csomagot add hozzá a projekt tudásbázisához. Ha a platform nem kezeli jól a ZIP-et vagy túl sok fájlt, akkor csak a kiválasztott skill mappáját töltsd fel külön.

## ChatGPT Project beállítás

1. Hozz létre egy új projektet, például: `Claude Skills Router`.
2. A projektfájlokhoz töltsd fel legalább ezeket:
   - `claude-skills-index.json`
   - `PERSONA_SKILL_LOADER_PROMPT_HU.md`
   - `claude-skills-clean.zip`
   - opcionálisan: `README_PROJECT_SETUP_HU.md`, `PROJECT_UPLOAD_MANIFEST.json`
3. Nyisd meg a projektbeállításokat.
4. A projektinstrukciók mezőbe illeszd be a `CHATGPT_CLAUDE_PROJECT_INSTRUCTIONS_HU.md` teljes tartalmát.
5. Indíts új beszélgetést a projekten belül, és kérj egy konkrét feladatot, például: „Tervezz RAG architektúrát egy belső dokumentumkeresőhöz.”

Megjegyzés: ha a projekt nem lát bele közvetlenül a ZIP belső fájlszerkezetébe, csomagold ki lokálisan a ZIP-et, majd töltsd fel a releváns skill mappáit vagy fájljait. Nagy csomagnál ne próbáld minden fájlt egyszerre a kontextusba kényszeríteni.

## Claude Project beállítás

1. Hozz létre egy új Claude Projectet, például: `Claude Skills Router`.
2. A Project Knowledge részbe töltsd fel:
   - `claude-skills-index.json`
   - `PERSONA_SKILL_LOADER_PROMPT_HU.md`
   - `claude-skills-clean.zip` vagy a kicsomagolt releváns skill-mappák
3. A Project Instructions mezőbe illeszd be a `CHATGPT_CLAUDE_PROJECT_INSTRUCTIONS_HU.md` tartalmát.
4. Indíts új chatet a projekten belül.
5. Teszteld egy konkrét feladattal, és ellenőrizd, hogy Claude megnevezi-e a kiválasztott skillt.

## Projektinstrukció rövid célja

A projektinstrukció ezt mondja az LLM-nek:

- Először az `index.json` alapján tájékozódjon.
- Azonosítsa a feladat domainjét.
- Válassza ki a legjobb skillt.
- Először csak a skill `SKILL.md` fájlját használja.
- Csak szükség esetén olvasson kapcsolódó referenciát, scriptet vagy assetet.
- Ne töltse be és ne próbálja egyszerre alkalmazni az egész csomagot.
- Válassza szét a skill módszertanát a friss tényadatoktól.

## Példa használat 1 — Engineering / RAG

Felhasználói kérés:

```text
Tervezz egy RAG alapú belső dokumentumkeresőt egy 200 fős cégnek. Legyen benne architektúra, komponensek, kockázatok és megvalósítási terv.
```

Elvárt LLM-működés:

1. Megkeresi az `index.json`-ban a RAG-hoz vagy keresőarchitektúrához kapcsolódó skillt.
2. Valószínűleg az `engineering/rag-architect/SKILL.md` vagy hasonló engineering skill mellett dönt.
3. Betölti a skill instrukcióit.
4. Ha kell, betölti a kapcsolódó referenciafájlokat.
5. A választ az adott skill módszertana szerint készíti el.

## Példa használat 2 — Marketing kampány

Felhasználói kérés:

```text
Készíts 2 hetes LinkedIn kampánytervet egy B2B SaaS termék indulásához. Legyen benne célcsoport, posztstruktúra, CTA és mérőszámok.
```

Elvárt LLM-működés:

1. A marketing kategóriában keres.
2. Kiválaszt egy kampány-, copywriting- vagy growth marketing skillt.
3. A `SKILL.md` alapján felépíti a kampánytervet.
4. Ha van sablon vagy asset, azt használja.

## Példa használat 3 — CFO / pénzügyi modell

Felhasználói kérés:

```text
Elemezd egy SaaS startup burn rate-jét, runway-ét és unit economics helyzetét. Adj döntési javaslatot a következő 6 hónapra.
```

Elvárt LLM-működés:

1. A `c-level-advisor/` vagy `finance/` kategóriák között keres.
2. Kiválasztja a CFO, unit economics vagy fundraising jellegű skillt.
3. Ha script van a skillhez, jelzi, hogy milyen bemeneti adat kellene a futtatáshoz.
4. Ha nincs adat, feltételezések helyett kér vagy sablont ad.

## Példa használat 4 — Projektmenedzsment

Felhasználói kérés:

```text
Készíts projekttervet egy 8 hetes webalkalmazás-fejlesztési projekthez. Szerepeljen scope, mérföldkövek, kockázatok és státuszriport sablon.
```

Elvárt LLM-működés:

1. A `project-management/` kategóriából választ skillt.
2. Betölti a projekttervezési vagy delivery skillt.
3. A kimenetet strukturált tervként adja vissza.

## Ajánlott első tesztprompt

```text
Használd a feltöltött skill-csomagot. A feladat: tervezz egy RAG-alapú dokumentumkeresőt egy 200 fős szervezetnek. Először nevezd meg, melyik skillt választottad az index alapján, majd készíts architektúrát, implementációs tervet és kockázatlistát.
```

## Hibakeresés

Ha az LLM nem talál skillt:

- Ellenőrizd, hogy a `claude-skills-index.json` tényleg fel van-e töltve.
- Kérd meg: „Olvasd el az index fájlt, és listázd a releváns skill-jelölteket.”
- Ha ZIP-et használsz, ellenőrizd, hogy a platform képes-e a ZIP belső fájljait olvasni.
- Ha nem, töltsd fel külön a kiválasztott skill mappáját vagy legalább annak `SKILL.md` fájlját.

Ha túl általános választ ad:

- Kérd meg, hogy nevezze meg a használt skill útvonalát.
- Kérd meg, hogy a `SKILL.md` instrukciói szerint dolgozzon.
- Add meg a célkimenetet: stratégia, diff, architektúra, kampányterv, sablon, elemzés stb.

Ha túl sok fájlt akar betölteni:

- Mondd neki: „Csak az indexet, a választott `SKILL.md` fájlt és a szükséges kapcsolódó fájlokat használd.”

## Korlátok

A skill-csomag módszertant, sablonokat, agentikus munkamintákat és script-segédleteket ad. Nem helyettesít friss webes kutatást, jogi tanácsadást, pénzügyi tanácsadást, orvosi tanácsadást vagy biztonsági auditot. Aktuális vagy nagy kockázatú kérdéseknél a projektnek friss forrásokat is kell kérnie vagy használnia.

## Ajánlott projektinstrukciós működés

A legjobb eredmény akkor várható, ha minden válasz elején vagy végén röviden látszik:

```text
Használt skill: <útvonal>
Indok: <miért ez illeszkedik>
További betöltött fájlok: <csak ha voltak>
```

Ha a felhasználó kifejezetten csak a végső anyagot kéri, ez a blokk elhagyható.

## Karbantartás

Ha új skilleket adsz a csomaghoz:

1. Minden skill saját mappába kerüljön.
2. Minden skillhez legyen `SKILL.md`.
3. A kapcsolódó fájlok maradjanak a skill mappáján belül.
4. Frissítsd az `index.json` fájlt.
5. Tartsd külön a fejlesztői fájlokat és a terjeszthető skill-forrásokat.

Generálva: 2026-05-03T02:09:35.966178+00:00

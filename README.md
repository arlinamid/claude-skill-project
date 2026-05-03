# Claude Skills Clean — ChatGPT / Claude

**English quick reference:** Use **`PERSONA_SKILL_LOADER_PROMPT_HU.md`** (or your own upload-based instructions) for **ChatGPT Projects** with uploaded `claude-skills-index.json` and optional ZIP. For **Claude** with a **GitHub repo** (Claude Code or repo-linked Project), use **`PERSONA_SKILL_LOADER_PROMPT_CLAUDE.md`** and paste **`CLAUDE_PROJECT_INSTRUCTIONS.md`** into Project Instructions.

Ez a README azt írja le, hogyan érdemes a megtisztított `claude-skills-clean` csomagot ChatGPT Projectként vagy Claude Projectként használni. A cél nem az, hogy az LLM egyszerre betöltse az összes skillt, hanem az, hogy az `index.json` alapján kiválassza a megfelelő skillt, majd csak a szükséges `SKILL.md`, `references/`, `scripts/`, `assets/` és példafájlokat használja.

## ChatGPT vs Claude (feltöltés vs GitHub)

| Platform | Tudás forrása | Skill-loader dokumentum |
|----------|----------------|-------------------------|
| **ChatGPT** Project | Feltöltött fájlok: `claude-skills-index.json`, opcionálisan ZIP vagy kicsomagolt mappák | `PERSONA_SKILL_LOADER_PROMPT_HU.md` |
| **Claude** (Code / Project + repo) | **GitHub-on lévő klón**: fájlok a repó útvonalain | `PERSONA_SKILL_LOADER_PROMPT_CLAUDE.md` + `CLAUDE_PROJECT_INSTRUCTIONS.md` |

A magyar **ZIP / kicsomagolás** szöveg a ChatGPT-féle feltöltős workflow-hoz illik. Claudénál a repót klónozd vagy kösd be a projektbe; az indexet és a skilleket **közvetlenül a fájlfából** olvasd, nem „ZIP feltöltés” logikával.

## Csomag célja

A csomag egy skill-router alapú tudásbázis. A **skill-katalógus** (`index.json` / `claude-skills-index.json`) megmondja, milyen skillek vannak, hol találhatók, melyikhez milyen referencia- és scriptfájl tartozik. A projekt instrukciói arra kényszerítik az LLM-et, hogy a felhasználói kérés kontextusa alapján válasszon skillt, és ne olvassa be feleslegesen a teljes csomagot.

## Fő fájlok

| Fájl | Kötelező? | Funkció |
|---|---:|---|
| `claude-skills-index.json` | igen | Skill-katalógus: kategóriák, útvonalak, leírások, címkék, fájllisták (a repó gyökerében; megegyezik a `claude-skills-clean/index.json` struktúrájával). |
| `PERSONA_SKILL_LOADER_PROMPT_HU.md` | ChatGPT-nél ajánlott | Magyar, beilleszthető instrukció feltöltött csomaghoz / ZIP-hez. |
| `PERSONA_SKILL_LOADER_PROMPT_CLAUDE.md` | Claudénél ajánlott | Angol, **GitHub / repó** alapú skillválasztás és betöltés (Claude Code, repo-kötött Project). |
| `CLAUDE_PROJECT_INSTRUCTIONS.md` | Claudénél ajánlott | Rövid szöveg a Claude **Project Instructions** mezőbe másolva. |
| `claude-skills-clean/` | igen | A tisztított forráscsomag mappája: skillek, `index.json`. |
| `README.md` | ajánlott | Ez az útmutató. |

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

**ChatGPT:** első szint — töltsd fel a `claude-skills-index.json`-t és a projektinstrukciót. Második szint — a kiválasztott skill fájljai vagy teljes ZIP; ha a ZIP belseje nem indexelt, kicsomagolva tölts fel mappákat.

**Claude + GitHub:** klónozd a repót vagy kapcsold a Projecthez; első szint — `claude-skills-clean/index.json` elérhető legyen. Második szint — a modell a repóban lévő útvonalakról olvas (nem feltétlen kell külön ZIP feltöltés).

## ChatGPT Project beállítás

1. Hozz létre egy új projektet, például: `Claude Skills Router`.
2. A projektfájlokhoz töltsd fel legalább ezeket:
   - `claude-skills-index.json`
   - `PERSONA_SKILL_LOADER_PROMPT_HU.md`
   - opcionálisan: `claude-skills-clean.zip` vagy kicsomagolt `claude-skills-clean/` részmappák
3. Nyisd meg a projektbeállításokat.
4. A projektinstrukciók mezőbe másold a **`PERSONA_SKILL_LOADER_PROMPT_HU.md`** rövid beilleszthető blokkját, vagy saját összefoglalót ugyanezen szabályokkal (index → egy skill → csak szükséges fájlok).
5. Indíts új beszélgetést a projekten belül, és kérj egy konkrét feladatot.

Megjegyzés: ha a projekt nem lát bele közvetlenül a ZIP belső fájlszerkezetébe, csomagold ki lokálisan a ZIP-et, majd töltsd fel a releváns skill mappáit vagy fájljait.

## Claude Project / Claude Code beállítás (GitHub)

1. Klónozd ezt a repót, vagy nyisd meg Claude Code-ban / kösd össze a Claude Projecttel úgy, hogy a fájlok a workspace-ben legyenek.
2. **Project Knowledge** (ha használsz feltöltést): elég lehet a `claude-skills-index.json`; sok esetben a repó már elég, és nincs szükség dupla feltöltésre.
3. A **Project Instructions** mezőbe illeszd be a **`CLAUDE_PROJECT_INSTRUCTIONS.md`** teljes tartalmát (vagy a `PERSONA_SKILL_LOADER_PROMPT_CLAUDE.md` rövid verzióját).
4. A részletes router-viselkedéshez tartsd a repóban a **`PERSONA_SKILL_LOADER_PROMPT_CLAUDE.md`** fájlt, és hivatkozz rá az instrukcióban (ahogy a `CLAUDE_PROJECT_INSTRUCTIONS.md` teszi).
5. Indíts új chatet; teszteld úgy, hogy Claude megnevezi-e a kiválasztott skill útvonalát.

## Projektinstrukció rövid célja

- Először az **index** alapján tájékozódjon.
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

(Claude + repó esetén: cseréld „feltöltött skill-csomagot” → „a repó `claude-skills-clean` katalógusát”.)

## Hibakeresés

Ha az LLM nem talál skillt:

- Ellenőrizd, hogy a `claude-skills-index.json` vagy `claude-skills-clean/index.json` elérhető-e (feltöltés vagy repó).
- Kérd meg: „Olvasd el az index fájlt, és listázd a releváns skill-jelölteket.”
- ChatGPT + ZIP: ellenőrizd, hogy a platform látja-e a ZIP belső fájljait; ha nem, tölts fel külön a skill mappát vagy `SKILL.md`-t.

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

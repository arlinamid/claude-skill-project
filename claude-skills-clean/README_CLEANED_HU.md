# Claude Skills Clean — használati útmutató

Ez a csomag a megtisztított skill-forrásokat tartalmazza. A cél az volt, hogy a ZIP-ben csak a valódi skillek és a hozzájuk közvetlenül tartozó fájlok maradjanak: `SKILL.md`, `references/`, `scripts/`, `assets/`, példák, elvárt kimenetek és egyéb skill-mappán belüli támogató fájlok.

## Tartalom röviden

- Fő kategóriák száma: 9
- Összes `SKILL.md`: 241
- Kategória-bundle skill: 9
- Konkrét, használható skill: 232

## Megtartott fő kategóriák

- `business-growth/` — 4 konkrét skill + kategória `SKILL.md`
- `c-level-advisor/` — 33 konkrét skill + kategória `SKILL.md`
- `engineering/` — 61 konkrét skill + kategória `SKILL.md`
- `engineering-team/` — 50 konkrét skill + kategória `SKILL.md`
- `finance/` — 3 konkrét skill + kategória `SKILL.md`
- `marketing-skill/` — 44 konkrét skill + kategória `SKILL.md`
- `product-team/` — 16 konkrét skill + kategória `SKILL.md`
- `project-management/` — 8 konkrét skill + kategória `SKILL.md`
- `ra-qm-team/` — 13 konkrét skill + kategória `SKILL.md`

## Eltávolított tartalmak

A tisztítás során kikerültek a fejlesztői és generált elemek: `.git/`, `.github/`, `.codex/`, `.gemini/`, `.claude/`, `.claude-plugin/`, `.codex-plugin/`, gyökérszintű dokumentációs és tesztmappák, cache-ek, `__pycache__/`, `.pytest_cache/`, `.pyc` fájlok, valamint a beágyazott generált `.zip` skill-duplikátumok.

## Hogyan keress skillt?

1. Nyisd meg az `index.json` fájlt.
2. A `summary.categories` mutatja a fő kategóriákat.
3. A `by_category` alatt kategóriánként rövid leírással látod a skilleket.
4. A `skills` tömb részletes rekordot ad minden skillhez: útvonal, `SKILL.md`, leírás, címkék, referenciafájlok, scriptfájlok, assetek és minden kapcsolódó fájl.
5. Egy LLM-nek elsőként mindig csak a kiválasztott skill `SKILL.md` fájlját érdemes betöltenie. A további fájlokat csak akkor kell olvasni, ha a skill kifejezetten hivatkozik rájuk vagy a feladat végrehajtásához szükségesek.

## Ajánlott betöltési sorrend LLM-hez

1. `index.json`
2. A kiválasztott kategória-bundle `SKILL.md`, ha útválasztási segítség kell.
3. A konkrét skill `SKILL.md` fájlja.
4. Csak a szükséges `references/`, `scripts/`, `assets/` vagy példafájlok.

## Példa

Ha a feladat RAG architektúra tervezése, az `index.json` alapján a valószínű skill:

`engineering/rag-architect/SKILL.md`

Először ezt kell betölteni, majd csak azokat a kapcsolódó referenciafájlokat, amelyeket a skill vagy a feladat ténylegesen igényel.

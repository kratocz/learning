---
name: course-sync
description: Synchronizace přehledu kurzů v tomto repu s realitou — posbírá novinky z e-mailů od robot_dreams/SKVOT, z telefonátů nahraných Plaudem a ze stránek kurzů, a promítne je do README a aktivního rozhodovacího dokumentu. Použij, když uživatel řekne "/course-sync", "aktualizuj kurzy", "synchronizuj kurzy podle e-mailů", "mrkni, co je nového od robot_dreams", nebo po telefonátu/e-mailu od obchodníka robot_dreams.
---

# course-sync

Aktualizace sekce „Kurzy, které mě nyní zajímají" v [README.md](../../../README.md) a případného aktivního rozhodovacího dokumentu `selection-*.md` podle aktuálních zdrojů. Před netriviálním rozhodováním načti skill `kodex`.

## Kroky

1. **Kontext z paměti:** přečti memory soubor `robotdreams-courses-context.md` (předplacené kurzy, obchodní kontakt, jak stahovat stránky). Zjisti z README datum „stav k …" — od něj se sbírají novinky.

2. **Sběr zdrojů (paralelně):**
   - **Gmail:** `search_threads` s dotazem na domény robotdreams.cz a l-a-b-a.cz (from i to) od data posledního stavu; vlákna čti přes `get_thread` s `messageFormat: PLAIN_TEXT`.
   - **Plaud:** `list_files` s filtrem data a dotazem „kurz"; u relevantních nahrávek čti **přepis** (`get_transcript`, blok `transaction`), ne souhrn — souhrny Plaudu mají artefakty v číslech a datech. Souhrn (`get_note`) používej jen jako mapu, co v přepisu hledat.
   - **Web:** stránky kurzů stahuj `curl -sL -A "<Chrome User-Agent>"` do scratchpadu (WebFetch dostává 403); text vytáhni z HTML (server-rendered). Katalog je stránkovaný (`/course/2`, `/course/3`…) a neúplný — viz [AGENTS.md](../../../AGENTS.md), sekce Práce se zdroji. Slug kurzu má variantu s pořadím běhu (`587-t4-…` = 4. běh kurzu 587); `tN` je registrovaný alias, jiné číslo dá 404, příští běh se neuhodne.

3. **Křížová kontrola:** termíny z různých zdrojů si často protiřečí (zastaralý web, šablonovité e-maily, přeřeky v hovoru). Každé datum se dnem v týdnu ověř výpočtem (`date`/`cal`) — den v týdnu nepočítej z hlavy. Rozpory nezahlazuj, vyznač je („e-mail říká X, telefonicky Y").

4. **Zápis:**
   - README: aktualizuj řádky kurzů v sekci „Kurzy, které mě nyní zajímají" a datum „Termíny běhů odpovídají stavu k …"; ceny do README nepatří.
   - Aktivní `selection-*.md` (existuje-li): doplň sekci „Průběh" o časovou osu nových událostí a aktualizuj dotčené tabulky a body k ověření.
   - Paměť: aktualizuj `robotdreams-courses-context.md` (stav, termíny, výsledky jednání).

5. **Kontrola před commitem:** jméno firmy, která kurzy hradí, nesmí být v žádném commitovaném souboru (hlídá i hookify pravidlo) — `git grep` přes staged obsah. Ceny a fakturační detaily patří jen do `selection-*.md`, ne do README.

6. **Commit nabídni, neprováděj** — konvenční zpráva česky (`docs: …`), push jen na výslovné přání.

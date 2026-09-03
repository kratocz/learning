# AGENTS.md

Guidance for AI coding agents working in this repository (Claude Code, Codex, Antigravity, Cursor, Copilot, …).

## Project overview

Veřejný přehled sebevzdělávání Petra Kratochvíla — absolvované kurzy, kurzy, které ho aktuálně zajímají, a doporučené YouTube kanály. Čistě obsahový repozitář (Markdown), žádný kód ani build.

## Conventions

- Obsah je česky; technické termíny a názvy kurzů zůstávají v původní podobě.
- Veškerý obsah žije v `README.md` — nezakládat další obsahové soubory, dokud README nepřeroste únosnou délku. Výjimkou jsou datované rozhodovací dokumenty (`selection-YYYY-MM-DD.md`): jednorázové analýzy k jednomu rozhodnutí, které lze po jeho provedení smazat nebo archivovat.
- Seznamy a metadata jako odrážkové seznamy (`- ` / `* `); souvislá próza bez pevných zalomení řádků uprostřed vět.
- Sekce „Absolvované kurzy" a „Kurzy, které mě nyní zajímají" jsou vědomou kopií CV na [krato.cz/cs/cv](https://krato.cz/cs/cv/) — při aktualizaci jedné strany připomenout uživateli i druhou.
- Jméno firmy, která autorovi hradí kurzy, ani jména jejích lidí **nikdy nepatří do commitovaných souborů** — psát jen „firma, která mi kurzy hradí". Před commitem zkontrolovat (`git grep` přes staged obsah).

## Práce se zdroji

- Stránky kurzů na robotdreams.cz a skvt.cz vracejí pro WebFetch/boty HTTP 403; funguje `curl -sL -A "<Chrome User-Agent>"` — stránky jsou server-rendered a program kurzu je přímo v HTML.
- Katalog robotdreams.cz/courses je stránkovaný přes `/course/2`, `/course/3`… a **není úplný**: některé kurzy (např. Projektový management v IT, Vedení IT týmů, Kubernetes, FinOps) mají funkční stránku, ale v katalogu ani v sitemapě nejsou — dostupné jsou jen přes přesný slug. „Není v katalogu" tedy neznamená „neexistuje".
- Slug kurzu robot_dreams může mít variantu s označením běhu: `587-projektovy-management-v-it` i `587-t4-projektovy-management-v-it` vedou na stejný kurz (ID 587), přičemž `t4` je pořadí běhu (t1, t2, …). Jiné číslo (`t9`) i nesmyslný slug vracejí 404, takže `tN` je registrovaný alias konkrétního běhu, ne libovolný text. Který `tN` je ten příští, uhodnout nelze — musí být vypsán.
- Termíny a ceny v e-mailech a na webu robot_dreams si často protiřečí (zastaralé stránky, šablonovité e-maily) — do README psát datum stavu a zdroj, rozpory vyznačit.

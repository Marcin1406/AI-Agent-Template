# skills/INDEX.md — opisy skilli [PROJECT NAME]

## [nazwa-skilla]
**Trigger:** "[trigger 1]", "[trigger 2]"
**Po co:** [Jedno zdanie — jaki problem rozwiązuje]
**Prompt gotowy:** tak/nie
**Plik:** [example-skill/SKILL.md](example-skill/SKILL.md)

---

## Jak dodać nowy skill

1. Skopiuj folder `example-skill/` jako template
2. Zmień `SKILL.md` (triggery, cel, proces, format)
3. Dodaj wpis do tej tabeli
4. Dodaj trigger do routing table w `CLAUDE.md`

## Anti-patterns (nigdy nie rób)
- Skill który robi 3 różne rzeczy → rozbij na 3 skille
- Skill bez konkretnego procesu krok-po-kroku → nie wiadomo kiedy skończony
- Skill > 200 linii → wydziel plik `rules/` lub `examples/`

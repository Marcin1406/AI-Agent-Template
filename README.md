# AI Agent Workspace Template

Gotowy szkielet do budowy zespołu agentów AI opartego na Claude Code.  
Metodologia: **VGM AI Agent Hub** (Mateusz Wapa).

---

## Co to jest

Struktura plików i folderów która pozwala zbudować wieloagentowy system AI do automatyzacji dowolnego procesu biznesowego. Jeden template — nieskończenie wiele zastosowań.

**Przykłady projektów zbudowanych na tym szkielecie:**
- Automatyzacja Print on Demand (sprzedaż na 5 platformach)
- Agencja contentowa (research → pisanie → publikacja)
- Obsługa klienta (triaging → odpowiedź → eskalacja)
- Analiza inwestycyjna (screening → fundamenty → ryzyko → decyzja)
- Freelance PM (brief → wycena → wykonanie → rozliczenie)

---

## Struktura

```
/
├── CLAUDE.md          ← SUPERVISOR — mózg systemu, routing table
├── MEMORY.md          ← wiedza projektowa (rotuje z projektem)
├── USER.md            ← stały profil użytkownika
├── INDEX.md           ← mapa całego workspace
├── .mcp.json          ← Playwright MCP (automatyzacja przeglądarki)
│
├── agents/
│   └── AGENT-TEMPLATE.md    ← szablon nowego agenta
│
├── skills/
│   ├── INDEX.md             ← lista wszystkich skilli
│   └── example-skill/
│       └── SKILL.md         ← szablon nowego skilla
│
├── knowledge/               ← wiedza domenowa (lazy loading)
│
├── logs/
│   └── activity-log.md      ← auto-dokumentacja działań
│
└── projects/
    └── example-project/
        └── ROOM.md          ← stan sub-projektu / klienta
```

---

## Jak zacząć (5 kroków)

### Krok 1 — Sklonuj lub użyj jako template
```bash
git clone https://github.com/Marcin1406/AI-Agent-Template.git MojProjekt
cd MojProjekt
```

### Krok 2 — Zdefiniuj agentów

Odpowiedz na 3 pytania:
1. **Co chcę zautomatyzować?** (np. "tworzenie i publikację artykułów na bloga")
2. **Jakie są etapy tego procesu?** (np. research → pisanie → edycja → publikacja)
3. **Kto odpowiada za każdy etap?** (np. RESEARCHER → WRITER → EDITOR → PUBLISHER)

Każdy etap = jeden agent. Skopiuj `agents/AGENT-TEMPLATE.md` tyle razy ile masz etapów.

### Krok 3 — Wypełnij CLAUDE.md

Uzupełnij:
- Tabelę agentów (kto, co robi, jaki plik)
- Routing table (jakie słowa kluczowe kierują do jakiego agenta)
- Pipeline (kolejność agentów)

### Krok 4 — Wypełnij MEMORY.md i USER.md

- `MEMORY.md` — kontekst projektu, zasady, historia
- `USER.md` — kim jesteś, jak chcesz żeby agent z tobą rozmawiał

### Krok 5 — Uruchom Claude Code

```bash
claude
```

Napisz pierwsze zadanie. SUPERVISOR przejmie, zadeleguje do właściwego agenta, wróci z wynikiem.

---

## Kluczowe koncepcje

### Routing table (CLAUDE.md)

Serce systemu. Słowa kluczowe w wiadomości → właściwy agent.

```markdown
| Trigger | Agent | Załaduj |
|---|---|---|
| "research", "analiza", "dane" | RESEARCHER | agents/RESEARCHER.md |
| "napisz", "treść", "artykuł" | WRITER | agents/WRITER.md |
```

### Lazy loading (warstwy L1–L6)

Nie ładuj wszystkiego na raz — to marnuje tokeny. Ładuj tylko to co potrzebne:
- **L1** (zawsze): CLAUDE.md + MEMORY.md + INDEX.md (~1800 tokenów)
- **L2** (gdy trigger): agents/[nazwa].md (~500-700 tokenów)
- **L3-L6** (na żądanie): skills, knowledge, projects

### Single responsibility

Każdy agent robi **jedną rzecz**. Jeśli agent ma dwie różne odpowiedzialności → rozdziel go na dwa.

### Zasada ZERO TOLERANCJI

Wbudowana w `CLAUDE.md`. Żaden agent nie może halucynować, zgadywać ani zmyślać linków. Każdy fakt musi mieć źródło.

---

## Dodawanie nowego agenta

```bash
cp agents/AGENT-TEMPLATE.md agents/MÓJAGENT.md
```

Wypełnij pola w `AGENT-TEMPLATE.md`:
- Tożsamość (co robi, co nie robi)
- Input wymagany
- Proces krok po kroku
- Format wyjściowy
- Reguły pracy

Dodaj do routing table w `CLAUDE.md` i tabeli agentów w `INDEX.md`.

---

## Dodawanie nowego skilla

```bash
cp -r skills/example-skill skills/mój-skill
```

Skill = procedura wielokrotnego użytku wywoływana przez agenta.  
Dobry skill ma: triggery, konkretny proces, format wyjściowy, "Avoid" i opcjonalny prompt gotowy.

---

## MCP (Playwright) — automatyzacja przeglądarki

Plik `.mcp.json` konfiguruje Playwright MCP — pozwala Claude Code otwierać przeglądarkę i klikać.

Wymagania:
```bash
node --version   # wymagane 18+
npx @playwright/mcp@latest --version
```

Użycie: powiedz Claude Code `"otwórz [strona] i [akcja]"` — agent widzi stronę i działa.

---

## Inspiracja i metodologia

Projekt oparty na metodologii **VGM AI Agent Hub** stworzonej przez **Mateusza Wapę** (@slavicboyyy).

Kluczowe zasady VGM które implementuje ten template:
- CLAUDE.md jako mózg agenta z routing table
- Separacja MEMORY.md (projekt) i USER.md (użytkownik)
- Single responsibility per agent
- Lazy loading przez warstwy L1–L6
- Auto-dokumentacja w logs/
- Skills jako moduły wielokrotnego użytku

---

## Licencja

MIT — używaj, modyfikuj, sprzedawaj. Atrybucja mile widziana.

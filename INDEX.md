# INDEX.md — mapa workspace [PROJECT NAME]

> Jeden ekran, wszystko widać.

---

## Zespół agentów

```
SUPERVISOR  → CLAUDE.md              ← zawsze aktywny
[AGENT_1]   → agents/[AGENT_1].md   ← trigger: [słowa kluczowe]
[AGENT_2]   → agents/[AGENT_2].md   ← trigger: [słowa kluczowe]
[AGENT_3]   → agents/[AGENT_3].md   ← trigger: [słowa kluczowe]
```

**Pipeline:**
```
[AGENT_1] → [AGENT_2] → [AGENT_3]
```

---

## Warstwy danych (lazy loading)

```
L1 (core):    CLAUDE.md, MEMORY.md, INDEX.md           ← zawsze (~1800 tokenów)
L2 (agent):   agents/<nazwa>.md                        ← gdy trigger agenta (+500–700)
L3 (projekt): projects/<nazwa>/ROOM.md                 ← gdy aktywny sub-projekt (+600)
L4 (skill):   skills/<nazwa>/SKILL.md                  ← gdy trigger skilla (+800)
L5 (wiedza):  knowledge/<nazwa>.md                     ← gdy trigger wiedzy (+400–600)
L6 (logi):    logs/<nazwa>.md                          ← gdy analiza historii
```

---

## Agenci

| Agent | Zakres | Plik |
|---|---|---|
| SUPERVISOR | Koordynacja, routing | [CLAUDE.md](CLAUDE.md) |
| [AGENT_1] | [Zakres] | [agents/[AGENT_1].md](agents/[AGENT_1].md) |
| [AGENT_2] | [Zakres] | [agents/[AGENT_2].md](agents/[AGENT_2].md) |
| [AGENT_3] | [Zakres] | [agents/[AGENT_3].md](agents/[AGENT_3].md) |

---

## Skille

| Skill | Trigger | Prompt gotowy | Plik |
|---|---|---|---|
| [nazwa] | "[trigger]" | tak/nie | [skills/nazwa/SKILL.md](skills/nazwa/SKILL.md) |

---

## Sub-projekty / Klienci

| Nazwa | Status | Plik |
|---|---|---|
| [Projekt A] | aktywny | [projects/projekt-a/ROOM.md](projects/projekt-a/ROOM.md) |

---

## Wiedza bazowa

| Plik | Zawartość |
|---|---|
| [knowledge/rules.md](knowledge/rules.md) | Zasady domenowe projektu |

> Załaduj tylko gdy trigger: [lista triggerów]

---

## Logi

| Plik | Zawartość |
|---|---|
| [logs/activity-log.md](logs/activity-log.md) | Historia działań, wyniki, wzorce |

---

## Token budget

| Warstwa | ~Tokeny | Kiedy |
|---|---|---|
| CLAUDE.md | ~400 | zawsze |
| MEMORY.md | ~500 | zawsze |
| INDEX.md | ~600 | zawsze |
| agents/*.md (1) | ~500–700 | gdy trigger agenta |
| ROOM.md (1) | ~600 | gdy aktywny projekt |
| SKILL.md (1) | ~800 | gdy trigger skilla |
| knowledge/*.md (1) | ~400–600 | gdy trigger wiedzy |
| **Razem na starcie** | **~1800** | bez agenta |
| **Razem z 1 agentem** | **~2400** | typowa sesja |
| **Razem z agentem + skill** | **~3200** | pełny pipeline |

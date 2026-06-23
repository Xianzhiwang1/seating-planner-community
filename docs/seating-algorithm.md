# Showcase: Rule-aware seating generation

> This is an illustrative excerpt cherry-picked from the Seating Planner
> documentation to showcase how the app works. It is simplified for clarity and
> may differ from the current private source. Licensed under
> [MIT](../LICENSE).

The heart of the planner is `generateSeatingWithRules`. It takes a roster, a
desired layout, and a list of rules, and returns the tables with seats filled
in — honouring every constraint it can within a fixed time budget.

## Signature

```ts
export function generateSeatingWithRules(
  people: Person[],
  config: { tables: { type: TableType; count: number; capacity: number }[] },
  rules: Rule[],
  existingTables?: Table[],
): Table[]
```

| Parameter | Purpose |
| --- | --- |
| `people` | Students to seat. |
| `config` | Tables to create — type, count, capacity. |
| `rules` | Active seating constraints. |
| `existingTables` | Currently displayed tables, when re-shuffling. Preserves the user's drag-arranged positions and keeps retrying until a *different* arrangement is found. |

## How it places students

Placement runs in priority order:

1. **Groups (must-sit-together).** Built via union-find, shuffled, then sorted by
   descending size so the largest groups get first pick of tables that fit them.
2. **Priority students** (`sitNearInstructor`). They prefer near-instruction
   tables but fall back to regular tables.
3. **Regular students.** Round out the remaining seats.

Each placement honours `cannot_sit_together` and `should_sit_together` rules.

## Accept or retry

```ts
if (didPlaceAllSeatableStudents && !hasRuleViolations(tables, rules)) {
  if (!existingTables || !isSameSeating(tables, existingTables)) {
    return tables                  // ← happy path
  }
  bestAttempt ??= tables           // valid but identical: keep trying
}
```

## Guard rails

Two cheap guards keep abusive inputs from hurting the browser tab:

```ts
// Pre-flight: reject oversized inputs immediately.
if (people.length > MAX_STUDENTS) return existingTables ?? []
if (totalTableCount > MAX_TABLES) return existingTables ?? []

// Wall-clock budget: give up rather than freeze the tab.
if (Date.now() - startTime > timeBudgetMs) break  // timeBudgetMs = 3000
```

If the algorithm hits the attempt cap (200) or the 3-second budget, it returns
the best valid attempt found, or an unconstrained fallback so the UI always has
something to render.

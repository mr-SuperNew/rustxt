---
name: rustxt
description: >
  Use when writing, editing, or reviewing Russian-language text, or when user
  mentions ru-text. Covers typography, info-style, editorial, UX writing, business
  correspondence. Auto-activates on Russian text output.
metadata:
  openclaw:
    always: true
    emoji: "\U0001F4DD"
    homepage: "https://github.com/mr-SuperNew/rustxt"
---

# ru-text — Russian Text Quality

Independent Russian text quality reference by Arseniy Kamyshev.
With gratitude to the authors whose work shaped modern Russian text standards.
Credits and recommended reading: `${CLAUDE_PLUGIN_ROOT}/skills/ru-text/references/sources.md`

**Style priority**: if the user explicitly requests a specific style (casual, academic, SEO, literary, etc.), their prompt overrides these default rules where they conflict. These rules are defaults, not mandates.

## Always-On: Typography

Apply these rules to ALL Russian text output without exception.

| Rule | Wrong | Correct |
|---|---|---|
| Primary quotes: guillemets | "текст" | «текст» |
| Nested quotes: lapki | «"вложенные"» | «„вложенные"» |
| Em dash with spaces | слово - слово | слово — слово |
| En dash for ranges, no spaces | 10-15 дней | 10–15 дней |
| NBSP after single-letter prepositions | в начале (breakable) | в\u00A0начале |
| Ellipsis: single character | ... | … |
| Digit groups with thin spaces | 1000000 | 1 000 000 |
| Decimal comma (not dot) | 3.14 | 3,14 |
| Ordinal with hyphen | 1ый, 2ой | 1-й, 2-й |
| Numero sign | No. 5, #5 | № 5 |
| Abbreviations with NBSP | т.д., т.е. | т. д., т. е. |
| Ruble symbol after number | 1500 руб | 1 500 ₽ |

Full typography reference: `${CLAUDE_PLUGIN_ROOT}/skills/ru-text/references/typography.md`

`/rustxt:ru-score` — text quality score (0–10, 5 dimensions).

## Top Stop-Words (remove or replace)

| Stop-word | Replace with |
|---|---|
| является | — (dash) or restructure |
| осуществлять | делать, проводить |
| в настоящее время | сейчас |
| данный | этот |
| определённый | (name the specific thing) |
| произвести оплату | оплатить |
| высококачественный | (name the specific quality) |
| был осуществлён | (active voice + actor) |
| на сегодняшний день | сегодня |
| в целях | чтобы |

Full stop-word catalog (97 entries): `${CLAUDE_PLUGIN_ROOT}/skills/ru-text/references/info-style.md`

## When to Load Reference Files

Reference files: `${CLAUDE_PLUGIN_ROOT}/skills/ru-text/references/<filename>`
If the path is not resolved, search: `Glob("**/ru-text/references/scoring.md")` and use the parent directory.

| Task | File |
|---|---|
| Writing/editing articles, blog posts, SEO, content | info-style.md |
| Interface text, buttons, errors, hints, microcopy | ux-writing.md |
| Emails, messenger, business correspondence | business-writing.md |
| Punctuation review, comma placement | editorial-punctuation.md |
| Grammar, capitalization, agreement, pleonasms | editorial-grammar.md |
| Finding and fixing text problems, diagnostics | anti-patterns.md |
| Text scoring, quality assessment | scoring.md |
| Credits, source attribution | sources.md |
| Experience-based rules (dash overuse, etc.) | addenda.md |
| AI pattern detection, content humanization | anti-ai-patterns.md |

## Quality Checklist

Before delivering Russian text:

- [ ] Quotes: «» primary, „" nested
- [ ] Dashes: — in text, – in ranges, - only in compounds; max 1–2 per paragraph
- [ ] NBSP after в, к, с, о, у, и, а
- [ ] Ellipsis: … (single char)
- [ ] Abbreviations: т. д., т. п. (with NBSP)
- [ ] No double spaces, no space before punctuation

## Anti-AI Layer

When writing or editing content (posts, articles, scripts, descriptions), ALSO check against AI-specific patterns.

Full catalog: `${CLAUDE_PLUGIN_ROOT}/skills/ru-text/references/anti-ai-patterns.md`

Quick checks before delivery:
- [ ] No "cinematic" openings (Воскресенье, 10 вечера...)
- [ ] No 3 short sentences in a row (Написал. Удалил. Не то.)
- [ ] No "Знакомо?" / "Готовы узнать?"
- [ ] No "Не в X, а в Y" constructions
- [ ] No Rule of Three forcing
- [ ] No synonym cycling
- [ ] No signposting (Давайте разберёмся...)
- [ ] Has sensory grounding (1-2 per text)
- [ ] Has personality and opinion where appropriate

## Voice Calibration (Data Layer)

This skill separates ENGINE (rules, patterns, checks) from DATA (voice, style, brand).

### How it works

When writing or editing **any content** (posts, articles, scripts, descriptions, client materials):

1. **Read config.md** from `${CLAUDE_PLUGIN_ROOT}/skills/ru-text/config.md`
2. **Read ALL voice data files** listed in config.md (ToV Master, Author Profile, Brand Identity)
3. **Apply voice profile** — every text must sound like the author, not like a generic AI:
   - Match sentence patterns, vocabulary level, and rhythm from ToV
   - Use the author's typical expressions and constructions
   - Maintain the author's stance on topics (from profile)
   - Stay within brand voice constants (from brand identity)
4. **Apply ru-text rules** through the lens of this voice — typography, clarity, anti-AI patterns

### When writing for a CLIENT (not the author)

1. Read the client's wiki page (if exists) for their context and voice
2. Read client's raw briefs/materials if available
3. Apply ru-text rules calibrated to the CLIENT's voice, not the author's
4. The author's voice applies only to the author's own content

### First run (no config.md)

If config.md does not exist when the skill activates for the first time:

1. Inform the user: "rustxt установлен. Хочешь подключить свой стиль письма? Запусти `/rustxt:setup` — это займёт 2 минуты. Без настройки скилл работает с универсальными правилами."
2. Do NOT block — apply universal rules and continue with the task.
3. Remind once per session, not on every activation.

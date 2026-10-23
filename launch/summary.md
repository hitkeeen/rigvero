# Rigvero — пакет запуска (для владельца)

Содержимое: описание для GitHub About, три варианта поста-анонса и чек-лист перед публикацией. Жёсткое правило: **нигде не утверждаем, что функциональность уже работает**; продукт не написан, релизов нет.

---

## 1. Описание для GitHub About (EN, ≤350 символов)

**Вариант A (рекомендуется, 207 символов):**

```
Rigvero - a planned open-source Blender add-on for VRChat avatar preparation: inspect the rig, plan changes, apply them to a copy, review a before/after report. Inspired by CATS. Early stage, no release yet.
```

**Вариант B (короткий, 154 символа):**

```
Inspect. Plan. Apply. A planned Blender add-on for careful VRChat avatar prep, with a report before you commit. MIT. Pre-release, nothing to download yet.
```

---

## 2. Посты-анонсы (EN)

### Вариант 1 — Reddit, r/VRChat

**Заголовок:** I'm planning "Rigvero" — an avatar-prep Blender add-on that shows what it will change before it touches your rig (announcement, no release yet)

**Текст:**

> One-click "Fix Model" tools made avatar preparation accessible to people who will never learn rigging — that is real value, and CATS defined the category. The trade-off is that you don't know what the button did until it has already done it. The classic case is documented in CATS [issue #236](https://github.com/absolute-quantum/cats-blender-plugin/issues/236): the automated fix *"also removes the neck bone if it works"*. Documented follow-up cases: [#357](https://github.com/absolute-quantum/cats-blender-plugin/issues/357) — a VRoid preparation broken by Fix Model; [#645](https://github.com/absolute-quantum/cats-blender-plugin/issues/645) — *"Fix model turns it white"*, author links the result to Combine Materials; [#665](https://github.com/absolute-quantum/cats-blender-plugin/issues/665) — translating blend shapes broke the animations that used them, plus a request for a rename export table.
>
> I'm starting work on **Rigvero**, a Blender add-on planned around a different loop: **Inspect → Plan → Apply**. Analyze the model, show the plan, mark risky steps; apply runs on a copy, keeps the original untouched, and produces a before/after report. Planned MVP: compatibility preflight with a declared, tested Blender version matrix; the plan/apply workflow; a PC/Mobile budget validator with honest limits (what is an error, what is a risk, what requires Unity-side checks); and an offline rename ledger so renamed bones can be mapped back.
>
> **Honesty corner:** this is an announcement, not a release. There is no code, no alpha, no screenshots of a working UI, and no release date. I'm sharing the plan early on purpose — if you have lost work to automated fixes, or you think this plan is overengineered or under-scoped, that is exactly the feedback I need right now. Once the repo's Discussions are open, please use them.

### Вариант 2 — Reddit, r/blender

**Заголовок:** Rigvero (planned Blender add-on): inspect, plan, apply — avatar prep with a report instead of one-click hope (pre-release)

**Текст:**

> VRChat avatar prep in Blender means renaming bones, merging weights, deleting "useless" bones and squeezing textures under a budget. Existing one-click tools automate this but don't show their work — the documented classic case is CATS [#236](https://github.com/absolute-quantum/cats-blender-plugin/issues/236): the automated fix *"also removes the neck bone if it works"* (see also [#645](https://github.com/absolute-quantum/cats-blender-plugin/issues/645): *"Fix model turns it white"*).
>
> **Rigvero** is a planned open-source add-on (MIT) that restructures the workflow: **Inspect** (analyze rig, shape keys, materials, textures) → **Plan** (a readable change plan separating errors, risks and recommendations) → **Apply** (on a copy, with invariant checks between stages and a before/after report). Planned target is current Blender 4.x; the planned MVP also includes a PC/Mobile budget validator and an offline rename ledger with CSV export for restoring references.
>
> **Disclaimer:** pre-release. No code, no alpha, no date — nothing to try yet. I'm posting early to collect criticism of the plan itself. If you prepare avatars (for VRChat or anything else): which step of your current pipeline scares you most?

### Вариант 3 — Hacker News (текстовый пост)

**Заголовок:** Rigvero: a verify-first approach to Blender avatar prep (announcement, nothing to try yet)

**Текст:**

> Automated "fix model" tools for VRChat avatar preparation compress hours of rigging into a button — and decide on the user's behalf what gets deleted, merged or renamed. [Issue #236](https://github.com/absolute-quantum/cats-blender-plugin/issues/236) of the original CATS plugin is the canonical example: the fix *"also removes the neck bone if it works"*.
>
> **Rigvero** is a planned open-source Blender add-on built around three phases: Inspect, Plan, Apply. The technically interesting parts: (1) all transformations run on a copy of the scene data with invariant checks between stages, so failures don't leave half-processed models; (2) platform budgets come from a versioned rules file that separates hard limits from heuristics and marks what can only be validated inside Unity; (3) an offline rename ledger — a reversible name map with collision detection — replaces a cloud translation dependency.
>
> Not a Show HN: there is no release yet, not even an alpha, and no date. Feedback on the approach and scope is what I'm after — particularly from people who have been burned by one-click pipelines.

---

## 3. Чек-лист владельца перед публикацией

- [ ] **Имя:** создать GitHub org/user `Rigvero`; проверить домены и товарные знаки (WIPO/EUIPO/USPTO). Поиск в brand.md — не юридическая проверка.
- [ ] **Репозиторий:** создать до постов; включить Discussions; подготовить issue-шаблоны («feedback on plan» и «problem report»).
- [ ] **README:** прогнать поиск по словам *works, supports, guaranteed, will fix, removes* — всё планируемое должно иметь пометку planned/roadmap.
- [ ] **LICENSE:** файл MIT (© 2026 Rigvero contributors) добавлен — он лицензирует публикуемые материалы проекта (документацию, сайт); код появится с первой сборкой под MIT, не создавая впечатления, что код уже доступен.
- [ ] **Наследие CATS:** не переносить supporters.json, аватарки патронов, имя «CATS» и кот-лого; не публиковать чужие персональные данные.
- [ ] **NeoNeko:** код не переносим: старый GitHub-репозиторий NeoNeko обозначен GPL-3.0, в текущей ветке main на Forgejo лицензия MIT © 2026 NeoNeko (проверено по LICENSE-файлу) — перед любым заимствованием проверяем лицензию конкретной версии и её зависимостей; в текстах упомянут уважительно.
- [ ] **Ссылки:** проверить, что ссылки на issues CATS открываются (сейчас — зеркало absolute-quantum; при необходимости заменить на оригинал michaeldegroot).
- [ ] **Визуал:** скриншоты/видео не публиковать до реального UI; макеты не выдавать за работающий интерфейс.
- [ ] **About:** после финальной правки пересчитать длину (лимит 350 символов).
- [ ] **Метрики:** не добавлять счётчики звёзд/пользователей, «trusted by», обещания «guaranteed upload» и гарантированного FPS.
- [ ] **Публикация:** выпускать по одному каналу за раз; первые сутки отвечать честно: «релиза ещё нет, план открыт для критики».
- [ ] **Теги:** Watch/Star — единственный призыв к действию до первого релиза.

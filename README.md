# Rigvero

![License: MIT](https://img.shields.io/badge/License-MIT-blue)
![Planned targets: Windows | Linux | macOS](https://img.shields.io/badge/Planned%20targets-Windows%20%7C%20Linux%20%7C%20macOS-lightgrey)
![Blender](https://img.shields.io/badge/Blender-4.x%20%28planned%20target%29-orange)

**Prepare your avatar. Keep control.**  
*Know what changes before you apply.*

Rigvero is a planned open-source Blender add-on for preparing VRChat avatars. The idea behind it is simple: before anything in your scene is modified, the add-on should tell you what it found, what it intends to change, and what it will leave alone. You review the plan, risky steps require your explicit confirmation, processing targets a copy of your data, and you get a before/after report — so that avatar preparation stops being an act of faith.

> ⚠️ **Rigvero is at the idea/design stage. There are no releases, and nothing described on this page works today.** Every feature below is *planned*. See [Status](#status).

## The problem

Preparing a model for VRChat usually means fixing a rig you did not build: translating dozens of Japanese bone names, merging weights, deleting leftover physics objects, cutting triangles and squeezing texture memory into platform budgets. Existing tools — above all the CATS Blender Plugin — made this accessible through one-click automation, and that was a genuine contribution. But automation without visibility cuts both ways:

- **Fixes can silently remove things you wanted to keep.** In [issue #236](https://github.com/absolute-quantum/cats-blender-plugin/issues/236), a user reports that the automated fix *"also removes the neck bone if it works."* When a single button decides what counts as "useless", you usually find out after the damage is done.
- **Documented damage from fixes and renames.** [#357](https://github.com/absolute-quantum/cats-blender-plugin/issues/357) describes a VRoid preparation broken by Fix Model; [#645](https://github.com/absolute-quantum/cats-blender-plugin/issues/645) ("Fix model turns it white") reports whitened materials, with the author linking the result to Combine Materials; [#665](https://github.com/absolute-quantum/cats-blender-plugin/issues/665) reports that translating blend shapes breaks the animations that use them — and asks for a rename export table.
- **Quest preparation can stall on the toolchain.** [#691](https://github.com/absolute-quantum/cats-blender-plugin/issues/691) describes missing textures and atlas/Material Combiner problems while preparing an avatar for Quest. The budget numbers Rigvero plans to validate against are not user anecdotes but VRChat's documented limits: [avatar performance ranking system](https://creators.vrchat.com/avatars/avatar-performance-ranking-system/), [Android/Quest content limitations](https://creators.vrchat.com/platforms/android/quest-content-limitations/), [avatar size limits](https://creators.vrchat.com/avatars/avatar-size-limits/).

The cost of an automated mistake falls entirely on the user. Rigvero's planned answer is to make the tool show its work *before* touching anything.

## What makes Rigvero different (planned)

The planned core is a loop: **Inspect → Plan → Apply**.

1. **Inspect** — analyze the imported model: rig type, bone chains, shape keys, materials, textures; list detected issues and what the tool considers safe or risky to change.
2. **Plan** — present the proposed changes as a readable plan, separating errors, risks, recommendations, and things that can only be verified in Unity / VRChat SDK.
3. **Apply** — execute the plan **on a copy** of the data, keep the original untouched, and produce a before/after report; invariant checks run after each stage, so a failure does not leave a half-processed model behind.

None of this exists yet. It is the product hypothesis this project will be built — or dropped — against.

## Features

The full feature plan, with IDs and acceptance criteria, is tracked in [docs/FEATURES.md](docs/FEATURES.md). The split below reflects current priorities.

### Planned core (MVP)

- **Compatibility Preflight** (F051) — verify the Blender version and dependencies *before* the scene is touched; an explicit, tested matrix of supported versions instead of vague "3.x/4.x/5.x" claims.
- **Inspect → Plan → Apply** (F052) — the loop described above, replacing the one-click "fix everything" model: explicit confirmation for bone deletion, weight merging, material merging and renaming; protection for custom bones, physics chains and shape keys.
- **Platform Budget Validator** (F053) — PC and Mobile profiles with versioned rules; the add-on shows *which* object exceeds a budget and what a fix is expected to change — and labels what still requires Unity-side verification.
- **Offline Rename Ledger** (F054) — a curated offline dictionary instead of a cloud translation dependency; a stable, reversible original→new name map with collision detection and CSV export, so references can be restored.

### Roadmap (after MVP)

- **Dependency Diagnostics** (F055) — pre-flight checks for importers, texture files and configured backends; error messages that say what happened, what stayed unchanged, and what to do next.
- **Atlas & Face Preservation Review** (F056) — preview of materials/UV before optimization, detection of missing textures, and a comparison pass that protects visemes, eyelids and facial shape keys.
- **SDK3 / PhysBones Handoff** (F057) — a manifest for a Unity-side editor package: stable identifiers, the rename map, bone chains; PhysBone checks against the real SDK3 scene. Exploratory.
- **Reproducible Platform Variants** (F058) — one source model, saved PC and Mobile processing recipes, separate output collections and reports with consistent naming. Exploratory.
- **Long term** — the broader workflow familiar to CATS users: multi-format import (MMD, XPS, FBX, VRM), smart decimation, visemes, eye tracking, baking. Part of the vision; none of it is implemented.

## Status

- **No releases. No downloads. No working code published yet.** Nothing in this README describes functioning software.
- Feature IDs, priorities and acceptance criteria are being written down *before* code, so the plan can be criticized early and changed cheaply.
- If the problems above sound familiar — or you believe this approach is wrong — that feedback is most useful *now*. Once the repository's Discussions are open, please use them.

## Concept preview

No screenshots yet — the addon does not exist yet. The site shows a labeled concept UI (see [site/index.html](site/index.html)): sample data, explicitly marked "Concept UI — not final". It illustrates the planned Inspect report; it is not a working interface.

## Install

Rigvero will be available with the first release, as a downloadable add-on archive with an explicit list of supported Blender versions. Until then, there is nothing to install:

- **Watch** the repository to be notified about the first alpha.
- **Star** it if you want to follow development.

## FAQ

### How is Rigvero different from CATS?

[CATS](https://github.com/michaeldegroot/cats-blender-plugin) pioneered one-click avatar preparation and defined the category. But its development stopped years ago, and it has not caught up with current Blender releases. Rigvero is planned as a new codebase, not a fork: the "fix everything with one button" model is deliberately replaced by Inspect → Plan → Apply, work on a copy, and reporting.

### How is it different from NeoNeko's fork?

[NeoNeko's Cats-Blender-Plugin](https://git.neoneko.org/NeoNeko/Cats-Blender-Plugin) is an actively maintained fork of CATS with SDK3-aware workflows; development has moved to the team's own Forgejo instance, and the [GitHub repository](https://github.com/teamneoneko/Cats-Blender-Plugin) is officially no longer maintained. If it works for you, use it. Rigvero's planned difference is in the interaction model (plan / confirm / roll back / report) rather than in adding more buttons. Note also: the old NeoNeko GitHub repository is marked GPL-3.0, while the current `main` branch on Forgejo is MIT © 2026 NeoNeko (verified against the LICENSE file); We do not reuse NeoNeko code; before any future reuse, we will check the license of the specific version and its dependencies.

### Will it be free?

Yes — planned to be free and open source under the MIT license.

### Will it support Quest / mobile avatars?

The plan includes mobile profiles with honest limits: what is a hard error, what is a hidden risk, what is only a recommendation, and what must be verified in Unity. The add-on will not promise a "guaranteed upload" — some checks are simply impossible from inside Blender.

### When is the release?

No date yet. The MVP scope is being defined first; releases will follow when the acceptance criteria for that scope actually pass.

### Can I help?

Later — with feedback and test models. Right now, the most useful contribution is criticism of the plan itself: scope, priorities, and anything that reads like overpromising.

## Roadmap

| Phase | Focus | Scope | Status |
|---|---|---|---|
| 0 | Foundations | Architecture and repo setup; supported-Blender matrix; Inspect → Plan → Apply design | planned |
| 1 | MVP core | F051–F054 (preflight, plan/apply, budget validator, rename ledger) | planned |
| 2 | Confidence & UX | F055–F056 (diagnostics, atlas/face review) | planned |
| 3 | Integration | F057–F058 (Unity handoff, platform variants) | planned, exploratory |

Phases describe scope, not dates. There is no release date yet.

## Credits & License

- **License:** MIT © 2026 Rigvero contributors — see the [LICENSE](LICENSE) file. It covers the project's published content (documentation, launch materials, this site); the add-on code does not exist yet and will appear with the first build, under MIT.
- **[CATS Blender Plugin](https://github.com/michaeldegroot/cats-blender-plugin)** by Michael Degroot (GiveMeAllYourCats) and contributors, MIT — the original project that inspired Rigvero. Without CATS, this plan would not exist.
- **NeoNeko and contributors** of the [maintained CATS fork](https://git.neoneko.org/NeoNeko/Cats-Blender-Plugin) — for keeping the toolchain alive through the SDK3 transition. Development has moved to Forgejo; the team's GitHub repository is officially no longer maintained.
- **[Tuxedo Blender Plugin](https://github.com/feilen/tuxedo-blender-plugin)** — prior art in multi-platform baking.

*Trademark notice: Blender is a registered trademark of the Blender Foundation. VRChat is a trademark of VRChat Inc. Rigvero is an independent project and is not affiliated with, endorsed by, or sponsored by either.*

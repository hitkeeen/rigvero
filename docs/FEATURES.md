# Feature Reference (planned)

This page is the canonical list of Rigvero's planned features. IDs follow the project's feature inventory; **"CATS ref"** points to the original [CATS Blender Plugin](https://github.com/michaeldegroot/cats-blender-plugin) feature that the idea comes from (IDs F001–F050; its issue tracker is mirrored at [absolute-quantum/cats-blender-plugin](https://github.com/absolute-quantum/cats-blender-plugin), where the linked issues live) or marks the feature as **new**.

> ⚠️ **Everything on this page is planned. Nothing is implemented.** IDs exist to make the plan reviewable — not to imply shipped functionality. There are no releases yet.

## Planned core (MVP)

The MVP targets the four blockers that keep users from trusting automated avatar preparation at all.

### F051 — Compatibility Preflight
Checks the Blender version and required dependencies *before* the scene is modified, and reports which operations are supported. Backed by an explicitly declared, tested version matrix instead of vague "3.x/4.x/5.x" claims; unsupported versions get a clear refusal, not a broken install. **CATS ref:** new (CATS only had hard version gates at startup, no pre-mutation report).

### F052 — Inspect → Plan → Apply
Analyzes the model and proposes a fix plan before touching anything; applies changes to a copy of the data, requires explicit confirmation for risky steps (bone deletion, weight/material merges, renaming), protects custom bones, physics chains and shape keys, and produces a before/after report with invariant checks between stages. **CATS ref:** reimagines F003–F004 (Fix Model / Fix Model Settings) as a staged, verifiable process. Documented one-click damage: [#236](https://github.com/absolute-quantum/cats-blender-plugin/issues/236) — the fix *"also removes the neck bone if it works"*; [#357](https://github.com/absolute-quantum/cats-blender-plugin/issues/357) — a VRoid preparation broken by Fix Model.

### F053 — Platform Budget Validator
PC and Mobile profiles driven by versioned rules with a recorded source and date; separates hard errors from hidden risks, recommendations, and items that can only be verified in Unity. Names the specific object that exceeds a budget and the expected effect of a fix, instead of a single opaque score. **CATS ref:** new; reworks the idea behind F030 (static triangle presets, incl. the outdated "Quest (5000)") and F040 (Quest baking) with up-to-date budgets.

### F054 — Offline Rename Ledger
An offline curated dictionary (plus authored English MMD names) with collision detection and a stable, reversible original→new rename map, exportable to CSV so references can be restored after re-import. Network translation only as an explicitly enabled backend whose failure never blocks the workflow. **CATS ref:** reworks F041 (Translate Entities), which depended on an unofficial Google Translate client. Motivating report: [#665](https://github.com/absolute-quantum/cats-blender-plugin/issues/665) — *"If one translates blend shapes, animations which make use of it will be broken"* — with a request to export a rename table.

## Roadmap (after MVP)

### F055 — Dependency Diagnostics
Pre-flight diagnostics for importers, texture file availability and configured backends, run before work starts. Errors follow the pattern "what happened → what stayed unchanged → what to do next", with a copyable, sanitized technical report (versions, stage, traceback — no model content). **CATS ref:** new.

### F056 — Atlas & Face Preservation Review
Preview of materials and UVs before optimization is applied, warnings for missing textures and overlaps, and a result-vs-original comparison that protects visemes, eyelids and key facial shape keys. Replaces the mandatory third-party atlas dependency with a swappable backend or built-in implementation. **CATS ref:** reworks F035–F037 (Texture Atlas / Combine Materials / Texture Material Ops) and the face-priority parts of F040 (Bake). Documented trouble with the current atlas/combine workflow: [#691](https://github.com/absolute-quantum/cats-blender-plugin/issues/691) — missing textures and atlas/Material Combiner problems while preparing a Quest avatar; [#645](https://github.com/absolute-quantum/cats-blender-plugin/issues/645) — *"Fix model turns it white"*, author links the result to Combine Materials.

### F057 — SDK3 / PhysBones Handoff
Prepares safe bone chains and a manifest for a Unity-side editor package — stable identifiers, the rename map, expected materials — that validates real SDK3 components and PhysBone budgets against the actual Unity scene. Dynamic Bone migration goes through the VRChat SDK with a backup, not an "FBX conversion". **CATS ref:** reworks F039 (Root Bone Parenting for legacy Dynamic Bones); SDK3-aware mapping extends F032–F033 (Eye Tracking).

### F058 — Reproducible Platform Variants
One source model, saved PC and Mobile processing recipes, and separate output collections with reports and consistent naming — so updating an avatar does not repeat every manual step, and PC/Mobile variants stay in sync. **CATS ref:** reworks F040 (Bake System with Desktop/Quest presets).

## From the original CATS inventory

Most capabilities of the original CATS (F001–F050 in the source inventory) — multi-format import/export, decimation, visemes, eye tracking, merging, translation UI and more — remain part of the long-term vision and will be re-planned individually. Decisions already made:

| CATS ID | Decision |
|---|---|
| F003–F004 | Not carried over as-is: replaced by F052, a staged process instead of a monolithic one-click fix |
| F013 | "No vertex weights" does not mean "useless": physics chains and user exceptions must survive deletion logic (see [#236](https://github.com/absolute-quantum/cats-blender-plugin/issues/236)) |
| F015 | No silent constraint deletion; constraints require bake or explicit removal instead of a blanket claim |
| F030 | The "Quest (5000)" preset is outdated; budgets come from versioned rules (see F053) |
| F041 | Replaced by F054: offline dictionary + optional providers + reversible rename map |
| F043 | The auto-updater requires a rework; not part of the MVP |
| F046–F047 | Patron lists, donor avatars and CATS branding are not carried over |
| F049 | The FBX exporter monkey-patch needs an audit; reimplemented only if reproducibly necessary |
| F050 | Dead code (unregistered Copy Protection panel) is not carried over and will not be advertised |

**License note:** the old NeoNeko GitHub repository is marked GPL-3.0, while the current `main` branch on the team's Forgejo instance is MIT © 2026 NeoNeko (verified against the LICENSE file); We do not reuse NeoNeko code; before any future reuse, we will check the license of the specific version and its dependencies.

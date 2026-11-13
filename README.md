# Injustice Lab v0.2 — Team and Statistics Research Sandbox

**Static website for GitHub Pages.** Mobile upload package, using the **repository-root** layout your existing GitHub Actions workflow already deploys.

## Installation / upgrading an existing repository

Extract this ZIP and upload/replace these five files in the **root of the existing repository**:

- `index.html`
- `app.js`
- `catalog.js`
- `styles.css`
- `README.md`

**Keep your current `.github/workflows/deploy.yml` untouched**. It should already use `actions/upload-pages-artifact` with `path: .`. Pushing to `main` triggers deployment. Do not upload the ZIP itself as a GitHub Pages website; upload the five extracted files.

**Before upgrading:** If you have configured your own builds in v0.1, open the deployed site, go to **Data Studio → Export all data JSON**, and save the backup. Browser-based data lives in localStorage, not your GitHub repository. The new version migrates existing in-browser teams and saved builds. It resets legacy guessed ownership entries to screenshot-audited `Owned`, `Not owned`, or `Unknown`; custom records and user-authored passive/tag descriptions are preserved when flagged as user-verified. You can correct ownership directly on library cards.

## What changed in v0.2

1. **144-character reference dataset**, including rarity, Level 1 base damage and health, and maximum promotion, imported from the existing `Injustice_Mobile_Character_Stat_Database.xlsx` research workbook.
2. **87 unique gear families and 1,914 fusion/evolution stages** from the existing `Injustice_Mobile_Gear_Progression_Database_RESEARCH_UPDATED.xlsx` research workbook. Some old catalogue aliases still exist internally to preserve saved-build IDs; the picker displays one entry per family.
3. **Calculated stats** instead of asking for manual numbers only. Per character: Elite promotion, level, up to +300 damage or health base augmentation, personal 10% support enhancements, and up to 25% global support-card bonuses. Manual override remains available for observed stats.
4. **Stat Explorer** compares every legal promotion for any of the 144 cards, including non-linear Metal promotions and the Gold Elite IV damage/health multiplier discrepancy. Level 1–50 formulas are workbook-backed. Level 51–60 for eligible E7+ non-Metals is explicitly labelled as a published Breakthrough extension, not workbook-sourced; Metals stop at level 50.
5. **Promotion impact estimates** show how each next Elite upgrade would affect the approximate weighted Multiplayer team-power value at current levels and modifiers.
6. **Ownership corrected:** 73 character entries are explicitly marked owned based on historical screenshots and conversation, 6 are known future targets, and 65 remain unknown. An absent card is never inferred to be unowned without evidence. Individual status can be changed inside the card library; the website cannot automatically inspect the game account.
7. **Character progress metadata** includes certain photographed Elite and level states. The date is historic; adjust if your account has progressed since.
8. **Gear stage selector:** selecting a piece lets you inspect stage-specific gear text at Unevolved +0 through Evolved +10 where that source has a stage entry. The scoring engine does not yet perform exact stage-by-stage combat damage calculations.
9. Data persists in the browser. Saved builds, JSON import/export, modes, gear uniqueness checks and synergy notes remain available.

## Research formulas

Let `B` be base damage or health; `A` be the optional augment of that stat; `L` the level multiplier; `E` promotion multiplier; `S` the combined support percentage.

`Displayed stat = floor( (B + A) × L × E × (1 + S/100) )`

Damage level multiplier: Level 1 = 1.0; Levels 2–10 add 0.20 each; Levels 11–30 add 0.10 each; Levels 31–50 add 0.05 each (Level 50 = 5.8). For Breakthrough Levels 51–60, continuing +0.05 each yields 6.3 at 60.

Health level multiplier: starts at 1.0; increases by 0.20 per level (Level 50 = 10.8; Level 60 = 12.8). This is the card statistic, **not** effective in-battle health with gear, passives or shields.

Gold promotions: E0 ×1, E1 ×1.5, E2 ×2, E3 ×3, E4 ×3.5 damage / ×3.6 health, E5 ×4, E6 ×4.5, E7 ×5, E8 ×5.5, E9 ×6, E10 ×6.5. Metals: E0 ×1, E1 ×1.2, E2 ×1.5, E3 ×2.19, E4 ×2.41, E5 ×2.70, E6 ×3.08, E7 ×3.57. Other rarities follow the workbook tables.

*Note:* game/wiki display rounding may differ by ±1 in edge cases; unusual support effects and combat multipliers are outside this specific formula. For an exact account comparison, use the builder's **Manual** stat mode.

Approximate MP weighted team power: `0.6 × (highest Damage+Health) + 0.3 × (middle) + 0.1 × (lowest)`. This is a documented community model, **not officially confirmed matchmaking code**. It cannot predict true win rate or account for every team-selection edge case.

## Limitations and priorities for next iterations

- Passive descriptions and tags are well-developed for familiar builds but **not exhaustive for all 144 playable cards**; records without individually verified passives are explicitly identified as not yet audited.
- The 1,914 gear stage entries are research-derived tables; **don't treat every per-stage figure as an independently tested combat result**.
- A chosen fusion stage updates the displayed researched effects, not the heuristic grade's raw damage math.
- Only screenshots and explicitly reported holdings are treated as confirmed ownership. The site is offline-first; no game-account API exists here.
- Passive triggers, AI defence behaviour, blocking, stuns, DOT stack logic, gear proc probabilities and special animations are not yet executed by a battle simulator. Grade is theorycrafting guidance only.
- Full combat model, validated battle replays, per-gear proc modelling, Survivor round scaling and a tested AI opponent remain subsequent work.

## Core sources / research provenance

- User-owned character research workbook `Injustice_Mobile_Character_Stat_Database.xlsx` (144 playable character records and level/promotion matrices).
- User-owned gear research workbook `Injustice_Mobile_Gear_Progression_Database_RESEARCH_UPDATED.xlsx` (87 families, 1,914 gear stages, model limitations).
- https://injustice-mobile.fandom.com/wiki/Level
- https://injustice-mobile.fandom.com/wiki/Promotion
- https://injustice-mobile.fandom.com/wiki/Damage
- https://injustice-mobile.fandom.com/wiki/Health
- https://www.reddit.com/r/InjusticeMobile/ (community matchmaking research; formula requires ongoing validation).

**Independent community research tool, not affiliated with WB Games or NetherRealm Studios.**

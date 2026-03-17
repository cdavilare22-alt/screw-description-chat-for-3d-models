# Fusion 360 Speed Tricks (Intermediate, Real-World Modeling)

This guide is for users who can model parts already but want faster edits and fewer rebuild headaches.

## Core Mindset for Speed

- Model for change, not just for first completion.
- If a "simple change" feels hard, the driving feature/parameter is probably in the wrong place.
- Keep design intent in sketches, parameters, and early timeline features.

## 1) Start with a Stable Skeleton

- Use one or two master sketches for critical dimensions (overall size, key hole centers, mounting pattern).
- Constrain sketches fully so edits are predictable.
- Reference origin planes/axes early; avoid depending on temporary edges whenever possible.

Why this is faster:

- You edit a few dimensions and many downstream features update automatically.

## 2) Drive Repeated Sizes with User Parameters

Use parameters for anything likely to change:

- Wall thickness
- Hole diameter and hole spacing
- Boss diameter/height
- Nut trap size/depth
- Clearance offsets

Practical pattern:

- Keep a small parameter set (`Base_Length`, `Bolt_Dia`, `Hole_Pitch`, `Wall_Thk`).
- Build features from those parameters only.
- Avoid hard-coded values in later timeline features.

## 3) Use Feature Patterns Instead of Copying Geometry

- Use sketch patterns or feature patterns for holes, slots, and repeating bosses.
- Prefer patterning one clean seed feature over creating many independent features.

Why this is faster:

- One edit to seed geometry updates the full pattern.

## 4) Edit with the Right Tool (Common Time Saver)

- `Press Pull` for quick offset/thickness updates.
- `Move/Copy` for controlled repositioning when design intent allows.
- `Replace Face` when you need a face to match another surface without rebuilding many features.
- `Split Body` + `Combine` for controlled geometry surgery.

Rule:

- If edits are frequent, rebuild with stronger design intent instead of stacking one-off fixes.

## 5) Timeline Discipline (Prevents Rework)

- Name important features (`Base Extrude`, `Hole Pattern`, `Mount Bosses`).
- Group related operations when possible (sketch -> hole -> pattern).
- Use timeline rollback to insert features at the correct historical point.

Why this is faster:

- You can find and edit the right feature immediately instead of hunting.

## 6) Robust References (Avoid Broken Features)

- Prefer references to origin planes, master sketches, and stable construction geometry.
- Avoid dimensioning to fillet/chamfer edges that may disappear when topology changes.
- Add fillets/chamfers later in timeline when possible.

## 7) Components vs Bodies (When to Split)

- Use separate components for real assemblies or reusable parts.
- Use joints for motion/fit checks rather than ad-hoc body moves.
- Keep single-part concepts as one component until reuse/assembly demands separation.

## 8) Fast Change Playbook (When You Are Stuck)

1. Identify which dimension should own the change.
2. Find that dimension in parameters or earliest responsible sketch.
3. Edit there first.
4. If update fails, inspect first failed timeline feature and repair upstream references.
5. If model fights back repeatedly, refactor: create a clean driving sketch and repoint dependent features.

## 9) High-Value Checks Before Finalizing

- Toggle section analysis to verify wall thickness and clearances.
- Suppress cosmetic fillets/chamfers temporarily during heavy edits.
- Confirm hole/fastener sizes against your reference tables before release.

## 10) Practical "Faster Tomorrow" Habits

- Build a personal template with your common parameters and naming style.
- Save reusable feature sequences (mount boss, nut trap, clearance hole stack).
- After each project, note one edit that was painful and convert it into a reusable pattern.

# sum-like-it-hot

**sum-like-it-hot** is a journal-first cooking & baking application for conscious people who love to bake (and cook) but want to stay aware of what's actually in their food. Write your recipes naturally, let the AI do the measuring and nutrition math, log every bake over time, and adapt any recipe to your dietary needs... allowing to do it without the app ever turning into a preachy diet tracker.

---

## Why it exists

Most recipe apps are either cozy notebooks with no numbers, or clinical calorie trackers with no soul. sum-like-it-hot has it both!:

- **Cozy on the surface**: your recipes, your handwritten notes, a soft nutrition summary.
- **Data-driven one tap down**: full gram-by-gram breakdown, macros, sugar callouts, and allergen flags.

The "conscious" part comes from **clarity, not coaching**. You see exactly what's in your bake — it never judges you or pushes fitness goals.

---

## The five pillars

### 1. Recipe Box
Your collection of reusable recipes. Paste a recipe in plain text — *"2 cups flour, 1 stick butter, 3 eggs..."* — and the AI:
- Parses it into structured ingredients
- Converts everything to **grams** (handling cups/sticks/units → weight)
- Lets you **confirm or correct** before saving
- Computes nutrition for the whole batch, **per 100g**, and **per serving**

### 2. Journal
The heart of the app. Each recipe can have many **bakes** — the times you actually made it.
- Log a bake with a date, freeform notes, and optional quick tags (*"too dense," "perfect," "oven ran hot," "swap next time"*)
- Flip back through your history and watch yourself improve
- One recipe → many bakes over time

### 3. Nutrition
Objective, factual, layered.
- A quiet summary chip on top (*"~210 cal/slice · 18g sugar"*)
- A full gram/macro table underneath (calories, protein, carbs, fat, sugar)
- Automatic **allergen flags** (gluten, dairy, eggs, nuts)
- A neutral, non-personalized reference where helpful (*"FDA suggests ~50g added sugar/day"*)

### 4. Adapt
Re-engineer any recipe to fit a dietary need — *"make this vegan,"* *"gluten-free,"* *"lower the sugar."*
- The AI proposes **explicit swaps** (*"3 eggs → 3 flax eggs"*) with the reasoning and impact
- Shows a **side-by-side nutrition diff** (original vs. adapted)
- Each swap carries a confidence label: **reliable** / **may affect texture** / **experimental**
- Saved as a **new linked variant** — your original is never overwritten

### 5. Portion-from-Target
The reverse calculation. Name a limit, get a real portion.
- *"I want to stay under 25g of sugar — how much can I eat?"*
- → *"1 cookie keeps you at ~17g; 2 puts you at ~34g."*
- Works for any nutrient (calories, fat, sugar) and answers in **cuttable, average person terms** — counts, fractions of the batch, or grams

---

## Data model

```
Recipe  (reusable master)
 ├─ ingredients (parsed → grams)
 ├─ steps
 ├─ servings / yield (e.g. "makes 24 cookies")
 ├─ computed nutrition (batch / per 100g / per serving)
 └─ variants → linked adapted recipes (vegan, GF, ...)

Bake  (journal entry — a time you made a recipe)
 ├─ date
 ├─ notes (freeform) + optional tags
 ├─ → points to a Recipe version
 └─ optional serving override (e.g. "cut into 16 this time")
```

- A **Recipe** is the canonical, reusable thing in your recipe box.
- A **Bake** is one journal entry — a time you made it.
- Per-bake ingredient tweaks live as **notes** by default; recompute is opt-in.

---

## How the engine works

Everything runs on a single **gram-based nutrition engine**, which is why the features hang together:

1. **Parse** free text → structured ingredients
2. **Convert** volumes/units → grams (using ingredient density data)
3. **Look up** nutrition per ingredient → sum the batch
4. **Divide** by servings or per 100g for any view
5. **Invert** the math for portion-from-target

Pillars 3 → 5 are all just different questions asked of the same gram math.

---

## Status

Early development: vision locked, building v1.

**v1 scope:** Recipe Box · Journal · Nutrition · Adapt · Portion-from-Target

**Later:** one-tap "recalculate this bake with my changes," keto/low-carb adaptations, photo recipe import, recipe sharing.

---

## Getting started

> Setup instructions will be added as the stack is scaffolded.

```bash
git clone https://github.com/ahernandez41/sum-like-it-hot.git
cd sum-like-it-hot
```

---

## License

See [LICENSE](LICENSE).

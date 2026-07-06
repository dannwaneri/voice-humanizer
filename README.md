# voice-humanizer

A Claude Code skill that checks your writing against *your own voice*, not generic AI-pattern rules.

The [humanizer by Siqi Chen](https://github.com/blader/humanizer) catches generic AI tells. This does something different: it calibrates to a specific author's voice using their published work as a corpus, then flags drift from that voice alongside the standard AI pattern check.

---

## What it does

**For drafts:**
- Voice drift flags (with rewrites in your register)
- Specificity audit (every unanchored claim, with required substitution)
- AI pattern check (weighted below voice drift)
- Comment stacking detection (attribution lists that aren't building toward a point)

**For incoming comments:**
- Authenticity score (0–3): specific citation + personal experience + real question
- Synthetic praise detection
- Response length recommendation

**For your own replies:**
- Three-step engagement check: locate what's new → extend it → redirect
- Voice drift flags
- Tic detection

---

## Example

Here's voice-humanizer catching drift a generic humanizer would miss.

**Before (draft):**

> Skills in Claude Code are stored across three locations. Understanding
> the sync behavior helps you avoid unexpected issues. The install
> directory holds runtime files, the manifest cache stores metadata, and
> your git repo is the source of truth.

**Flag:**

> Voice drift — three-item list where your corpus compresses to two.
> "Understanding X helps you avoid Y" is the signpost-before-the-move
> construction (#33) — your corpus states the failure, not the promise.
> Parallel three-clause structure ("A holds B, C stores D, E is F")
> shows uniform investment (#36) where your corpus is uneven.
>
> No AI pattern fires hard. Grammar's clean. But it doesn't sound like you.

**After:**

> Skills live in three places: the install directory (runtime files),
> the manifest cache (metadata), the git repo (source of truth). Edit
> one and forget the others, next sync clobbers you. Ask me how I know.

A generic humanizer would pass the Before. Voice-humanizer caught it because the corpus knew this author compresses lists, states failures instead of announcing help, and closes on lived experience. That's the difference.

---

## Install

```bash
mkdir -p ~/.claude/skills
git clone https://github.com/dannwaneri/voice-humanizer.git ~/.claude/skills/voice-humanizer
```

Then replace `CORPUS.md` with your own writing. See `SETUP.md` for full instructions.

---

## The key idea

Generic humanizers check for patterns to avoid. This one checks for patterns to *match* — your specific cadences, the kinds of specificity you reach for, what good writing in your voice actually sounds like vs what Claude-flavored-you sounds like.

The corpus is private (`.gitignore`). The skill and structure are public.

---

Built for Claude Code. Claude desktop users see SETUP.md for manual usage. Inspired by [blader/humanizer](https://github.com/blader/humanizer).
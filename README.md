# GroupDNA — WhatsApp Group Chat Analyzer

**Author:** <Your Name> (<Roll Number>)
**Batch:** <Your Batch>
**Project:** Week 1 Minor Project, The Unlox Academy

## What this is

GroupDNA reads a raw WhatsApp chat export (`.txt`) and produces a full
personality-and-activity analytics report for the group — busiest day/hour,
a NumPy-powered hour-of-day activity heatmap, top group vocabulary, response
speed, longest silent streaks, and a personality archetype for every member
(Spammer, Group Mom, Night Owl, Storyteller, Drama Queen, Ghost, Comedian,
Question Master — plus one invented bonus archetype, **The Deadline Warrior**).

Run on the provided dataset (`hostel_bois.txt`, 6 participants, 60 days,
3,174 real messages), it correctly identifies:

- **Rahul** → The Spammer (avg burst of 4.5 back-to-back messages)
- **Priya** → The Group Mom (highest count of caring/check-in keywords)
- **Aman** → The Night Owl (79.8% of messages between 11 PM–5 AM)
- **Karan** → The Storyteller (avg 57 words/message) *and* the bonus
  Deadline Warrior (39.4% of messages mention exams/deadlines/placements)
- **Neha** → The Drama Queen (63.3% ALL-CAPS / double-exclamation messages)
- **Vikas** → The Ghost (73.3% of days silent, including an 11-day streak)

## Screenshot

<!-- Paste a screenshot of your final report output here, e.g.: -->
<!-- ![GroupDNA report output](screenshot.png) -->

## Constraints — what this project deliberately does NOT use

This was built using only Python fundamentals, as a discipline exercise —
the goal was to prove the analysis doesn't need heavier libraries.

**Used:** core Python (strings, lists, dicts, sets, tuples, loops,
conditionals, functions, f-strings, comprehensions, `sorted(key=...)`),
NumPy (`np.zeros`, indexing, slicing, aggregation), `open()`/file reading,
and `datetime.strptime` / `timedelta` for timestamp parsing only.

**Deliberately avoided:** pandas, matplotlib/seaborn/plotly,
`collections.Counter`/`defaultdict`, `re` (regex), any pre-built chat
analyzer or AI/ML library. All counting, tokenizing, and pattern detection
is done with plain dictionaries and string methods.

## How the parser handles messy real-world data

- **System messages** (group created, member added, description changed —
  no colon after the sender name) → skipped from analysis, counted separately
- **`<Media omitted>`** → counted as a message sent, excluded from word
  frequency / message-length stats, tracked in its own counter
- **`This message was deleted`** → tracked in its own per-person counter
- **Multi-line messages** → a line not starting with a `DD/MM/YY` timestamp
  is treated as a continuation of the previous message
- **Empty lines** → skipped silently

## How the archetypes are assigned (avoiding duplicate labels)

Each of the 8 core archetypes has a scoring function and the threshold rule
from the project brief. Archetypes are assigned in priority order (the six
primary archetypes first, then the two fallback ones): for each archetype,
whichever *unassigned* person scores highest — and clears that archetype's
threshold — gets it, then is removed from the pool. This guarantees every
person gets exactly one label and prevents two people from claiming the same
archetype. The bonus 9th archetype (Deadline Warrior) is reported separately
alongside a person's main archetype rather than competing for the same slot.

## How to run it

1. Open `GroupDNA_<YourName>_<RollNumber>.ipynb` in Google Colab
2. Upload `hostel_bois.txt` to the Colab session (sidebar → folder icon →
   upload), or place it in the same folder if running locally
3. Run all cells top to bottom (Runtime → Run all)
4. The final formatted report prints at the bottom of the notebook

## Repo contents

- `GroupDNA_<YourName>_<RollNumber>.ipynb` — the notebook
- `hostel_bois.txt` — the provided dataset
- `README.md` — this file

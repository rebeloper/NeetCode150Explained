# NeetCode150Explained Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build a Swift-only, GitHub-Wiki-based curriculum covering Big-O, 12 core data structures, 17 interview patterns, and all 150 NeetCode 150 problems, styled after SwiftConcurrencyExplained.

**Architecture:** Main repo (`NeetCode150Explained`) holds only `README.md` + `LICENSE`. A separate wiki git repo (`NeetCode150Explained.wiki`) holds every chapter as a numbered Markdown page (`NN-—-Title.md`) with `Home.md` as the master index. No compiled Swift package — all code is illustrative, embedded in Markdown code fences.

**Tech Stack:** Markdown, GitHub Wiki (git-backed), Swift code fences (illustrative only, not compiled).

## Global Constraints

- Wiki-only code: every Swift code sample lives inside a fenced ```swift block in a wiki page. No Xcode project, no Swift Package, nothing compiled or CI-tested.
- Filename convention: `NN-—-Title-With-Dashes.md` (two-digit zero-padded number, em dash `—` surrounded by single dashes, exactly matching the reference repo's convention, e.g. `02-—-Thread-vs-Task.md`).
- Numbering is sequential and global across the whole wiki (no per-section restart).
- `Home.md` groups pages under emoji section headers, in reading order, and every new page gets a link added to `Home.md` in the same commit that adds the page.
- Every chapter cross-links to at least one other chapter it depends on (Problem → Pattern/Data-Structure, Pattern → Data-Structure where relevant) using a relative wiki link: `[Title](./NN-—-Title.md)`.
- Every batch of pages is committed to the wiki repo as its own commit before moving to the next task.
- Tone/format matches the reference repo: conversational, 🍽️/🧠/📊/💻/🧸/⚠️/✅ section markers (see Chapter Template below), analogies, ASCII diagrams.

## Chapter Template (shared by all writing tasks)

Every chapter is a Markdown file with these sections, in this order. Emoji headers are literal — copy them exactly.

**Big-O chapter (only 1 page, Task 3):**
```
## 🍽️ Intuition
## 🧠 What It Means In Swift
## 📊 Growth Rate Table          (table: O(1)...O(2^n), each row: a tiny Swift snippet)
## 🧭 How To Eyeball Big-O       (practical checklist for reading unfamiliar code)
## 🧸 Memory Sentence
## ✅ Check Your Understanding
```

**Data Structure chapter (Task 4, 12 pages):**
```
## 🍽️ Intuition
## 🧠 What It Is & When To Reach For It
## 📊 ASCII Diagram
## 💻 Swift Implementation        (hand-rolled type, or note re: Array/Dictionary/etc.)
## ⏱️ Core Operations & Big-O     (table: operation | Big-O | why)
## 🧸 Memory Sentence
## ✅ Check Your Understanding
```

**Pattern chapter (Task 5, 17 pages):**
```
## 🍽️ Intuition
## 🚩 Recognition Signal          (what in a problem statement tells you to use this)
## 📊 ASCII Diagram
## 💻 Generic Swift Template      (reusable skeleton function/algorithm shape)
## 🧩 Worked Example               (one full problem solved with this pattern)
## 🧸 Memory Sentence
## ✅ Check Your Understanding
```

**Problem chapter (Tasks 6-23, 150 pages):**
```
## 🍽️ Intuition
## 🚩 Pattern-Recognition Cue     (what in THIS problem's phrasing signals the pattern)
## 🐢 Brute Force                 (Swift code + Big-O)
## 🚀 Optimal                     (Swift code + Big-O)
## 🔑 The Key Insight             (why brute force -> optimal works)
## 🔗 Related Chapters            (links to Data Structure(s) / Pattern(s) used)
## 🧸 Memory Sentence
## ✅ Check Your Understanding
```

**Structural acceptance check (run after drafting any chapter, before committing):**
```bash
FILE="path/to/NN-—-Title.md"
grep -c '^## ' "$FILE"          # matches the section count for that chapter type
grep -c '```swift' "$FILE"      # at least 1 (Big-O/DS/Pattern) or 2 (Problem: brute+optimal)
grep -c '\[.*\](\./[0-9].*\.md)' "$FILE"   # at least 1 cross-link (Pattern/Problem chapters)
```
Expected: counts match the template above; 0 means a section or link was skipped — fix before committing.

---

### Task 1: Repo & Wiki Scaffolding

**Files:**
- Create: `README.md`
- Create: `LICENSE`
- Create (in separate wiki repo, cloned as sibling dir `../NeetCode150Explained.wiki`): `Home.md`

**Interfaces:**
- Produces: `Home.md` section headers that every later task appends entries under: `## 🧮 Foundations`, `## 🧱 Data Structures`, `## 🧩 Patterns`, `## 🎯 NeetCode 150`.

- [ ] **Step 1: Create the main repo README**

Write `README.md`:
```markdown
# NeetCode150Explained 🎯

Ace [NeetCode 150](https://neetcode.io/roadmap) by understanding it, not memorizing it — explained entirely in **Swift**.

This isn't just 150 solutions. It's:
- 🧮 **Big-O** — the vocabulary you need first
- 🧱 **Data Structures** — the building blocks
- 🧩 **Patterns** — the recognizable shapes that show up in *any* interview question, not just these 150
- 🎯 **NeetCode 150** — every problem, brute force → optimal, tied back to the pattern and data structure it uses

Perfect for:
- Swift developers prepping for coding interviews who don't want to context-switch to Python/Java
- Anyone who's grinded LeetCode without a system and wants the *why*, not just 150 memorized answers
- Engineers who want to recognize "oh, this is a sliding window problem" in a question they've never seen

👉 **[Start here — the Wiki](../../wiki)**

Styled after [SwiftConcurrencyExplained](https://github.com/rebeloper/SwiftConcurrencyExplained).

## License

MIT — see [LICENSE](./LICENSE).
```

- [ ] **Step 2: Add an MIT LICENSE**

Write `LICENSE` with standard MIT text, copyright holder `rebeloper`, year 2026.

- [ ] **Step 3: Commit the main repo scaffolding**

```bash
git add README.md LICENSE
git commit -m "Scaffold README and LICENSE"
```

- [ ] **Step 4: Create and clone the wiki repo**

GitHub Wikis exist once the repo has at least one wiki edit made via the web UI, or once you push a first commit to the `<repo>.wiki.git` remote. Confirm with the user that the wiki is enabled on the GitHub repo (Settings → Features → Wikis) and that `NeetCode150Explained` exists on GitHub before this step — this is the first action that touches the actual GitHub repo (not just the local directory), so pause and confirm with the user before creating/pushing to it.

```bash
cd ..
git clone https://github.com/rebeloper/NeetCode150Explained.wiki.git NeetCode150Explained.wiki
cd NeetCode150Explained.wiki
```

- [ ] **Step 5: Create the Home.md skeleton**

Write `Home.md` (in the wiki repo):
```markdown
This tutorial walks through Data Structures & Algorithms in a carefully structured progression — entirely in Swift:

## 🧮 Foundations

## 🧱 Data Structures

## 🧩 Patterns

## 🎯 NeetCode 150

---

By following this path, you'll go from:

👉 "I memorized 150 answers 😵"
to
👉 "I recognize the pattern before I finish reading the problem 💡"
```

- [ ] **Step 6: Commit the wiki skeleton**

```bash
git add Home.md
git commit -m "Scaffold wiki Home page"
git push
```

---

### Task 2: Content Inventory (150 problem titles per category)

**Files:**
- Create: `docs/superpowers/plans/problem-inventory.md` (in the main repo — a planning artifact, not a wiki page)

**Interfaces:**
- Consumes: the 18 NeetCode category names from the design spec (`docs/superpowers/specs/2026-07-12-neetcode150-explained-design.md`, section 2).
- Produces: for every category, an ordered list of exact problem titles with LeetCode difficulty, and the final wiki chapter number assigned to each (continuing the sequence after Data Structures + Patterns). Tasks 6-23 consume this file directly.

- [ ] **Step 1: Gather the current NeetCode 150 list**

Live scraping of `neetcode.io/roadmap` and `leetcode.com/problem-list/plakya4j/` failed during design (JS-rendered page, 403 respectively). Try, in order, until one succeeds:
```bash
curl -sL -A "Mozilla/5.0" https://neetcode.io/api/roadmap-data  # or similar API endpoint — inspect neetcode.io's network tab / public API first
```
Fall back to cross-referencing 2-3 independent, well-known public sources that mirror the list (e.g. community GitHub repos explicitly titled "neetcode-150" with a checklist README) via WebFetch, and reconcile any discrepancies by majority match across sources. Do not invent problem titles — every title must be confirmed by at least one fetched source.

- [ ] **Step 2: Write the inventory file**

Format, one section per category, in NeetCode's order:
```markdown
# NeetCode 150 — Problem Inventory

Numbering continues from Task 5 (Patterns). Data Structures = 02-13, Patterns = 14-30.
Problems start at 31.

## Arrays & Hashing (31-...)
31. Contains Duplicate (Easy)
32. Valid Anagram (Easy)
...

## Two Pointers (...)
...

[continue for all 18 categories, ending with Bit Manipulation]
```

- [ ] **Step 3: Verify the count**

```bash
grep -cE '^[0-9]+\.' docs/superpowers/plans/problem-inventory.md
```
Expected: `150`. If not 150, find the missing/extra category and fix before proceeding — do not round or approximate.

- [ ] **Step 4: Commit**

```bash
git add docs/superpowers/plans/problem-inventory.md
git commit -m "Add verified NeetCode 150 problem inventory with chapter numbering"
```

---

### Task 3: Big-O Chapter

**Files:**
- Create (wiki repo): `01-—-Big-O-Notation.md`
- Modify (wiki repo): `Home.md`

**Interfaces:**
- Consumes: Chapter Template → Big-O chapter shape (above).
- Produces: `01-—-Big-O-Notation.md`, the page every later chapter's Big-O sections implicitly assume the reader has read.

- [ ] **Step 1: Draft `01-—-Big-O-Notation.md`**

Follow the Big-O chapter template exactly (all 6 section headers). The Growth Rate Table must cover, at minimum: O(1), O(log n), O(n), O(n log n), O(n²), O(2ⁿ), each with a 3-8 line Swift snippet that visibly demonstrates that complexity (e.g. O(1): array subscript; O(n²): nested loop over the same array).

- [ ] **Step 2: Run the structural acceptance check**

```bash
FILE="01-—-Big-O-Notation.md"
grep -c '^## ' "$FILE"      # expect 6
grep -c '```swift' "$FILE"  # expect >= 6 (one per growth rate row, minimum)
```

- [ ] **Step 3: Add the entry to Home.md**

Under `## 🧮 Foundations`, add:
```markdown
1. [Big-O Notation](./01-—-Big-O-Notation.md)
```

- [ ] **Step 4: Commit**

```bash
git add "01-—-Big-O-Notation.md" Home.md
git commit -m "Add Big-O Notation chapter"
git push
```

---

### Task 4: Data Structures Batch (12 chapters)

**Files:** (wiki repo, all `Create`)
- `02-—-Arrays-and-Strings.md`
- `03-—-Hash-Maps-and-Hash-Sets.md`
- `04-—-Linked-Lists.md`
- `05-—-Stacks.md`
- `06-—-Queues-and-Deques.md`
- `07-—-Binary-Trees.md`
- `08-—-Binary-Search-Trees.md`
- `09-—-Heaps-and-Priority-Queues.md`
- `10-—-Tries.md`
- `11-—-Graphs.md`
- `12-—-Union-Find.md`
- `13-—-Segment-and-Fenwick-Trees.md`
- Modify: `Home.md`

**Interfaces:**
- Consumes: Chapter Template → Data Structure chapter shape; links back to `01-—-Big-O-Notation.md` for every Big-O reference.
- Produces: chapters 02-13, which Task 5 (Patterns) and Tasks 6-23 (Problems) link back to by exact filename above.

- [ ] **Step 1: Draft all 12 chapters**

For each file above, follow the Data Structure chapter template exactly. Each `⏱️ Core Operations & Big-O` table must link its complexity claims back to `01-—-Big-O-Notation.md`. Where Swift's standard library already provides the structure (Array, Dictionary, Set), the `💻 Swift Implementation` section shows the stdlib usage *and* a hand-rolled minimal version (e.g. a `Stack<T>` wrapper over `[T]`), since interviews often ask for both.

- [ ] **Step 2: Run the structural acceptance check on all 12 files**

```bash
for f in "02-—-Arrays-and-Strings.md" "03-—-Hash-Maps-and-Hash-Sets.md" "04-—-Linked-Lists.md" \
         "05-—-Stacks.md" "06-—-Queues-and-Deques.md" "07-—-Binary-Trees.md" \
         "08-—-Binary-Search-Trees.md" "09-—-Heaps-and-Priority-Queues.md" "10-—-Tries.md" \
         "11-—-Graphs.md" "12-—-Union-Find.md" "13-—-Segment-and-Fenwick-Trees.md"; do
  echo "$f: $(grep -c '^## ' "$f") sections, $(grep -c '```swift' "$f") swift blocks"
done
```
Expected: every file reports 7 sections (template has 7 headers) and >= 1 swift block.

- [ ] **Step 3: Add all 12 entries to Home.md**

Under `## 🧱 Data Structures`, add numbered links 1-12 in the same order as the file list above.

- [ ] **Step 4: Commit**

```bash
git add 0[2-9]-—-*.md 1[0-3]-—-*.md Home.md
git commit -m "Add Data Structures section (12 chapters)"
git push
```

---

### Task 5: Patterns Batch (17 chapters)

**Files:** (wiki repo, all `Create`)
- `14-—-Two-Pointers.md`
- `15-—-Sliding-Window.md`
- `16-—-Fast-and-Slow-Pointers.md`
- `17-—-Binary-Search.md`
- `18-—-DFS-and-Backtracking.md`
- `19-—-BFS.md`
- `20-—-Topological-Sort.md`
- `21-—-Union-Find-Pattern.md`
- `22-—-Monotonic-Stack.md`
- `23-—-Prefix-Sum.md`
- `24-—-Merge-Intervals.md`
- `25-—-Top-K-and-Heap-Pattern.md`
- `26-—-1D-Dynamic-Programming.md`
- `27-—-2D-Dynamic-Programming.md`
- `28-—-Greedy.md`
- `29-—-Matrix-Traversal.md`
- `30-—-Bit-Manipulation-Tricks.md`
- Modify: `Home.md`

**Interfaces:**
- Consumes: Chapter Template → Pattern chapter shape; each pattern links back to the Data Structure chapter(s) it's built on (e.g. `21-—-Union-Find-Pattern.md` links to `12-—-Union-Find.md`; `25-—-Top-K-and-Heap-Pattern.md` links to `09-—-Heaps-and-Priority-Queues.md`).
- Produces: chapters 14-30, which Tasks 6-23 (Problems) link back to by exact filename above.

- [ ] **Step 1: Draft all 17 chapters**

For each file above, follow the Pattern chapter template exactly. The `🚩 Recognition Signal` section is the highest-value section in the whole project — it must give 2-4 concrete phrasings/constraints from real problem statements that signal this pattern (e.g. for Sliding Window: "contiguous subarray/substring" + "longest/shortest/max/min" in the same sentence).

- [ ] **Step 2: Run the structural acceptance check on all 17 files**

```bash
for f in 14-—-*.md 15-—-*.md 16-—-*.md 17-—-*.md 18-—-*.md 19-—-*.md 20-—-*.md \
         21-—-*.md 22-—-*.md 23-—-*.md 24-—-*.md 25-—-*.md 26-—-*.md 27-—-*.md \
         28-—-*.md 29-—-*.md 30-—-*.md; do
  echo "$f: $(grep -c '^## ' "$f") sections, $(grep -c '```swift' "$f") swift blocks"
done
```
Expected: every file reports 7 sections and >= 2 swift blocks (template + worked example).

- [ ] **Step 3: Add all 17 entries to Home.md**

Under `## 🧩 Patterns`, add numbered links 1-17 in the same order as the file list above.

- [ ] **Step 4: Commit**

```bash
git add 1[4-9]-—-*.md 2[0-9]-—-*.md 30-—-*.md Home.md
git commit -m "Add Patterns section (17 chapters)"
git push
```

---

### Task 6-23: NeetCode 150 Problem Batches (one task per category, 18 tasks)

This task shape repeats identically for each of the 18 NeetCode categories, in NeetCode's order: Arrays & Hashing, Two Pointers, Sliding Window, Stack, Binary Search, Linked List, Trees, Tries, Heap/Priority Queue, Backtracking, Graphs, Advanced Graphs, 1-D DP, 2-D DP, Greedy, Intervals, Math & Geometry, Bit Manipulation. Do not start a category task until `problem-inventory.md` (Task 2) has confirmed titles and chapter numbers for that category.

**Files:** (wiki repo)
- Create: one `NN-—-Problem-Title.md` per problem in the category, using the exact numbers and titles recorded in `docs/superpowers/plans/problem-inventory.md` for that category.
- Modify: `Home.md`

**Interfaces:**
- Consumes: Chapter Template → Problem chapter shape; `problem-inventory.md` for exact titles/numbers; chapters 02-30 (Data Structures + Patterns) for the `🔗 Related Chapters` links.
- Produces: one wiki page per problem, cross-linked into the Data Structure/Pattern it uses.

- [ ] **Step 1: Draft every chapter in the category**

For each problem, follow the Problem chapter template exactly. `🐢 Brute Force` and `🚀 Optimal` must both be complete, syntactically valid Swift functions (not fragments) solving the actual stated problem — not pseudocode. `🔗 Related Chapters` must link to at least one Data Structure chapter and at least one Pattern chapter by their real filenames from Tasks 4-5.

- [ ] **Step 2: Run the structural acceptance check on every file in the category**

```bash
for f in <category's files>; do
  echo "$f: $(grep -c '^## ' "$f") sections, $(grep -c '```swift' "$f") swift blocks, $(grep -c '\[.*\](\./[0-9].*\.md)' "$f") cross-links"
done
```
Expected: every file reports 8 sections (Problem template has 8 headers: 🍽️🚩🐢🚀🔑🔗🧸✅), >= 2 swift blocks (brute force + optimal), >= 2 cross-links (1 Data Structure + 1 Pattern minimum).

- [ ] **Step 3: Add all entries to Home.md**

Under `## 🎯 NeetCode 150`, add (or reuse, on the first problem task) a `### <Category Name>` subheading, then numbered links for every problem in that category, in the order recorded in `problem-inventory.md`.

- [ ] **Step 4: Commit**

```bash
git add <category's files> Home.md
git commit -m "Add <Category Name> problems"
git push
```

---

## Self-Review Notes

- **Spec coverage:** §1 architecture → Task 1. §2 content inventory → Tasks 2-23 (Big-O explicit in Task 3; DS/Patterns enumerated exactly from the spec's own lists in Tasks 4-5; Problems deferred to inventory per spec's explicit non-goal, resolved in Task 2). §3 templates → Chapter Template section, one per chapter type. §4 build order/phasing → task ordering (1→2→3→4→5→6-23) and per-category/per-section batching with commits between each.
- **Placeholder scan:** No TBD/TODO. The one deliberately deferred item (exact 150 titles) is the spec's own explicit non-goal, resolved by Task 2 before any problem chapter is written — not left vague at execution time.
- **Type/name consistency:** Filenames referenced by later tasks (Data Structure and Pattern chapter names in Tasks 4-5) are used identically in Task 6-23's `🔗 Related Chapters` instructions. `Home.md` section headers defined in Task 1 (`🧮 Foundations`, `🧱 Data Structures`, `🧩 Patterns`, `🎯 NeetCode 150`) are the exact headers every later task appends under.

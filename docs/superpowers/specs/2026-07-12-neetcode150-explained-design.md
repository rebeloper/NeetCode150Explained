# NeetCode150Explained — Design

## Purpose

A Swift-only companion to NeetCode 150 that teaches not just the 150 problems, but the underlying data structures and interview-recognizable patterns, so the reader can generalize to any DSA interview question — not just the ones they memorized. Styled after [SwiftConcurrencyExplained](https://github.com/rebeloper/SwiftConcurrencyExplained), but with substantially more code per chapter.

## Reference style (from SwiftConcurrencyExplained)

Confirmed by cloning `SwiftConcurrencyExplained.wiki.git` and reading actual chapter files (not just the README):

- Each chapter is a numbered wiki page (`NN-—-Title.md`), grouped into themed sections with emoji headers, indexed from `Home.md`.
- Chapter skeleton: 🍽️ **Intuition** (real-world analogy) → 🧠 **What It Means** (technical explanation) → 📊 **ASCII Diagram** → 💻 **Code Example** → 🧸 **Memory Sentence** → ⚠️ **Analogy Limit** → ✅ **Check Your Understanding**.
- Tone: conversational, encouraging, demystifying rather than authoritative. Chapters are short (2-4 min read) in the reference; ours will be longer since the brief calls for "a lot more code."

## 1. Repo / Wiki architecture

- **Main repo** (`NeetCode150Explained`): `README.md` + `LICENSE` only. README mirrors the reference's pitch/tone: short intro, "Perfect for" bullets, a table of contents linking into wiki pages, grouped by the 3 sections below.
- **Wiki** (`NeetCode150Explained.wiki`, a separate git repo, cloned locally alongside the main repo so both can be authored the same way): holds every chapter as its own numbered Markdown page (`NN-—-Title.md`), numbered sequentially across all sections. `Home.md` is the master index, grouped into the sections below with emoji headers, same as the reference.
- No Swift Package, no compiled/testable code. All code lives as embedded Swift code blocks directly in wiki pages — illustrative, not compiled or CI-verified (explicit tradeoff, chosen for lower authoring overhead over the reference repo's own approach).

## 2. Content inventory (sections, in reading order)

0. **Big-O Notation & Complexity Analysis** (1 chapter) — prerequisite vocabulary for everything else.

1. **Data Structures** — Arrays & Strings, Hash Maps & Hash Sets, Linked Lists (singly/doubly), Stacks, Queues & Deques, Binary Trees, Binary Search Trees, Heaps / Priority Queues, Tries, Graphs (adjacency list/matrix), Union-Find (Disjoint Set), Segment/Fenwick Trees (bonus — covers the advanced-graph/interval problems that benefit from them).

2. **Patterns** — the interview-recognition catalog: Two Pointers, Sliding Window, Fast & Slow Pointers, Binary Search (incl. binary-search-on-the-answer), DFS / Backtracking, BFS, Topological Sort, Union-Find pattern, Monotonic Stack, Prefix Sum, Merge Intervals, Top-K / Heap pattern, 1-D DP, 2-D DP, Greedy, Matrix Traversal, Bit Manipulation tricks.

3. **NeetCode 150** — grouped into NeetCode's own 18 roadmap categories, in NeetCode's order: Arrays & Hashing, Two Pointers, Sliding Window, Stack, Binary Search, Linked List, Trees, Tries, Heap/Priority Queue, Backtracking, Graphs, Advanced Graphs, 1-D DP, 2-D DP, Greedy, Intervals, Math & Geometry, Bit Manipulation. Each problem chapter links back to the specific Data Structure(s) and Pattern(s) it draws on.

The exact 150 problem titles per category are **not enumerated in this spec** — live scraping of neetcode.io/roadmap and the LeetCode problem list failed during design (JS-rendered / 403). Confirming the current, correct list is the first task in the implementation plan, not a guess made here.

Total scope: 1 + ~13 + ~17 + 150 ≈ **181 wiki pages**.

## 3. Chapter templates

**Big-O chapter** (1 page): intuition analogy for growth rates → table of common complexities, each with a tiny Swift example → a practical "how to eyeball the Big-O of code in front of you" cheat sheet → check-your-understanding.

**Data Structure chapter:** intuition/analogy → what it is & when to reach for it → ASCII diagram → Swift implementation (or a note that `Array`/`Dictionary`/etc. already provide it, with when to still hand-roll one) → core operations with Big-O for each → memory sentence → check-your-understanding.

**Pattern chapter:** intuition/analogy → the recognizable "signal" in a problem statement that tells you this pattern applies → ASCII diagram of the mechanic → a generic reusable Swift template/skeleton for the pattern → one fully worked example problem → memory sentence → check-your-understanding.

**Problem chapter** (150 of these): intuition/analogy tied to the problem → pattern-recognition cue (what in the phrasing signals this pattern) → brute-force Swift solution + Big-O → optimal Swift solution + Big-O → the key insight that gets you from brute-force to optimal → links to the Data Structure/Pattern chapters it uses → memory sentence → check-your-understanding.

## 4. Build order & phasing

Given ~181 pages, this cannot be a single implementation pass:

1. **Content-inventory step** (first task): pull the current, accurate 150 problem titles for each of the 18 NeetCode categories.
2. **Build order:** Big-O → Data Structures → Patterns → NeetCode 150 (category by category, in NeetCode's own order). Foundations come first because problem chapters link back into them.
3. **Batching:** Data Structures as one batch, Patterns as one batch, then each NeetCode category (8-12 problems) as its own batch. `Home.md` is updated incrementally after each batch. Each batch is committed to the wiki repo separately so progress is never lost mid-way.
4. Work spans many sessions — implementation uses plan/execute with review checkpoints between batches rather than one uninterruptible run.

## Explicit non-goals

- No compiled/testable Swift Package — code is illustrative wiki markdown only.
- No enumeration of exact LeetCode problem titles in this spec (deferred to implementation's content-inventory step).
- No interleaving of DS/Patterns with problems — the three sections stay as separate, stable reference blocks.

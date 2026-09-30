# The Unofficial Guide

Saba Salem — campus_life corpus

> **This file is your submission.** Fill it in as you go — most sections get
> written during the milestone that produces them, not at the end.
>
> How the starter works, and every command you'll need, is in `RUNNING.md`.
> Leave that file alone.
>
> **Paste everything as text.** No screenshots, no video. A typed table gets
> full credit; a picture of the same table gets none.
>
> Delete these instruction blocks as you replace them. The `<!-- -->` comments
> are notes to you and don't show up when the page renders — you can leave them
> or remove them.

---

# Unit 1

## What This Does

This system answers questions about campus life — things like course
add/drop policies, dining dollars, financial aid quirks, and housing —
using a corpus of 88 short student-life posts. It retrieves the most
relevant post(s) for a question and generates a grounded answer that
names its source.


## Chunking Strategy

Chunk size: One full document per chunk (no fixed character limit).

Overlap: None.

My corpus contains 88 short student-life posts, with a maximum length of 549 characters and an average length of 317 characters. Since each post already expresses a complete, self-contained thought, keeping each document as one chunk preserves the full context. Splitting posts by character count could cut a useful sentence in half without providing any benefit, so no overlap is needed.

## Sample Chunks



**Chunk 1** — source: `admin_add_drop_deadline.txt#0` — produced by: `chunker.py::split_documents`

```
On the add/drop deadline

You can add a course through the end of the second week. Dropping is a longer window — through the end of week six — but a drop after week two shows as a W on your transcript. Nothing anywhere on the registrar's site says this plainly, and students find out from each other.
```


**Chunk 2** — source: `course_biol_160.txt#0` — produced by: `chunker.py::split_documents`

```BIOL 160 Cell Biology

I lived here my sophomore year. Format is lecture three times a week with a weekly lab. Assessment: four unit tests and a cumulative final. Not curved.

Expect 9 to 11 hours a week, the heaviest first-year course by reputation.

The one piece of advice: the unit tests come fast, roughly every three weeks; falling behind once is very hard to recover from.
```


**Chunk 3** — source: `course_hist_118_workload.txt#0` — produced by: `chunker.py::split_documents`

```Workload for HIST 118 Modern World History

People keep asking so: a lot of reading, about 120 pages a week, but no problem sets. That's real time, not optimistic time.

It's front-loaded — the first month is heavier than the rest, partly because you're learning the format.
```


**Chunk 4** — source: `dining_pellew_dining_hall_followup.txt#0` — produced by: `chunker.py::split_documents`

```Re: Pellew Dining Hall

Adding to what people have said about Pellew Dining Hall. The wait figure of 12 to 18 minutes at peak matches what I've seen. If you're trying to eat between classes, go before 11:45 and it's a different building entirely.

Also worth saying: the furthest hall from anywhere, next to the athletics centre. Nobody tells you this at orientation.
```


**Chunk 5** — source: `housing_innisfree_hall.txt#0` — produced by: `chunker.py::split_documents`
```Innisfree Hall — what it's actually like

Transferred in last year, so take this with a grain of salt. Built 1991, renovated 2022. Rooms are doubles arranged as pairs sharing one bathroom between two rooms.

The good: the shared-bathroom-between-two-rooms arrangement is the best compromise on campus.

The bad: no air conditioning, which matters for the first three weeks of September.

Laundry costs $1.75 wash, $1.75 dry, app-based. On noise: moderate; the building is L-shaped and the short wing is much quieter.
```

## Sample Answer

<!-- One complete question and answer, pasted as text, with the source line
     visible. Milestone 4. -->

**Question:**
What happens to unused dining dollars at the end of spring?

**Answer:**
```
Whatever dining dollars are left in May (at the end of the spring semester)
disappear; they do not roll over to the following autumn.

Source: admin_dining_dollars.txt
```
**My relevance cutoff:** 0.6

I kept the starter's default of 0.6. My five in-corpus questions all scored
between 0.244 and 0.388, and my five out-of-scope questions all scored
between 0.825 and 0.934 — a clean gap of more than 0.4 with no overlap
between the two groups. 0.6 sits safely in the middle of that gap.

| Question | In corpus? | Best distance |
|---|---|---|
| Can I add a course after the first week of the semester? | Yes | 0.388 |
| What happens to unused dining dollars at the end of spring? | Yes | 0.255 |
| What is the deadline for dropping a class without getting a W? | Yes | 0.264 |
| How late can I drop a class? | Yes | 0.371 |
| Do work-study earnings count against financial aid? | Yes | 0.244 |
| What is the capital of Mongolia? | No | 0.825 |
| How do I change the oil in a diesel engine? | No | 0.934 |
| Who won the 1994 World Cup? | No | 0.886 |
| What is the recommended dosage of ibuprofen for a headache? | No | 0.844 |
| How do I write a for loop in Rust? | No | 0.896 |
## How I Used AI

<!-- Two specific moments. For each: what you asked for, what came back, and
     what you changed about it.

     "I asked Claude to write the chunking function from my notes. It ignored
     the overlap, so I added that myself" is the level of detail we're after.
     "I used AI to help me code" is not.

     Milestone 5. -->

**I asked Claude for help fixing a pip install error with chroma-hnswlib. It first suggested a --no-deps workaround, but the real fix was installing Microsoft C++ Build Tools, since the exact pinned version had no prebuilt Windows wheel available.**

**I initially assumed my venv path itself was wrong when packages installed successfully but test.py still couldn't import them. The actual cause was that plain pip was resolving to a different Python install than my venv's — switching to python -m pip fixed it.**

<!-- ── Stretch features ─────────────────────────────────────────────────────
     Doing one? Say so here BEFORE you start. A feature this README never
     claims earns nothing.
     ───────────────────────────────────────────────────────────────────────── -->

---

# Unit 2

<!-- These sections get ADDED to what's already above. Don't delete or rewrite
     unit 1 — the point is that someone can see what you said before you knew
     how it went. -->

## Run Log — Before

<!-- Your five criteria, three runs each. `python run_eval.py --label before`
     runs the questions, puts the OUT_OF_SCOPE ones through the gate, and
     writes it all into results/ for you. Targets come from criteria.md; the
     verdict column is your call.

     Criterion 3 is measured in one deterministic pass rather than three, so
     the same number goes in all three run columns. That's correct, not lazy.

     Milestone 1. -->

| Criterion | Target | Run 1 | Run 2 | Run 3 | Verdict |
|---|---|---|---|---|---|
| 1. Retrieved chunk contains the answer | 4 of 5 | 5/5 | 5/5 | 5/5 | MET |
| 2. Every answer names a source | 5 of 5 | 5/5 | 5/5 | 5/5 | MET |
| 3. Gate stops out-of-corpus questions | 4 of 5 | 5/5 | 5/5 | 5/5 | MET |

     
     
### Can I add a course after the first week of the semester? — run 1

- Best distance: 0.3881 (passed the gate)
- Sources retrieved: admin_add_drop_deadline.txt, admin_declaring_a_major.txt, admin_pass_fail_option.txt, advising_registration.txt, course_cs_340.txt

Yes, you can add a course through the end of the second week.

Source: admin_add_drop_deadline.txt


### Can I add a course after the first week of the semester? — run 2

- Best distance: 0.3881 (passed the gate)
- Sources retrieved: admin_add_drop_deadline.txt, admin_declaring_a_major.txt, admin_pass_fail_option.txt, advising_registration.txt, course_cs_340.txt

Yes, you can add a course through the end of the second week.

Source: admin_add_drop_deadline.txt


### Can I add a course after the first week of the semester? — run 3

- Best distance: 0.3881 (passed the gate)
- Sources retrieved: admin_add_drop_deadline.txt, admin_declaring_a_major.txt, admin_pass_fail_option.txt, advising_registration.txt, course_cs_340.txt

Yes, you can add a course through the end of the second week.

Source: admin_add_drop_deadline.txt


### What happens to unused dining dollars at the end of spring? — run 1

- Best distance: 0.2550 (passed the gate)
- Sources retrieved: admin_dining_dollars.txt, admin_meal_plan_changes.txt, dining_halden_hall.txt, dining_north_kitchen.txt, dining_the_atrium.txt

Whatever dining dollars are left in May (at the end of spring) disappear and do not roll over to the following autumn.

Source: admin_dining_dollars.txt


### What happens to unused dining dollars at the end of spring? — run 2

- Best distance: 0.2550 (passed the gate)
- Sources retrieved: admin_dining_dollars.txt, admin_meal_plan_changes.txt, dining_halden_hall.txt, dining_north_kitchen.txt, dining_the_atrium.txt

Whatever is left in May disappears (it does not roll over from the spring to the following autumn).

Source: admin_dining_dollars.txt


### What happens to unused dining dollars at the end of spring? — run 3

- Best distance: 0.2550 (passed the gate)
- Sources retrieved: admin_dining_dollars.txt, admin_meal_plan_changes.txt, dining_halden_hall.txt, dining_north_kitchen.txt, dining_the_atrium.txt

Whatever dining dollars are left in May (at the end of the spring semester) disappear; they do not roll over to the following autumn (admin_dining_dollars.txt).

## Verdicts

| # | Criterion | Verdict | How I decided |
|---|---|---|---|
| 1 | Retrieved chunks contain the answer | MET | All 5 questions had the correct fact present in the retrieved chunks, across all 3 runs (5/5 every time, target was 4/5). |
| 2 | Every answer names a source | MET | Every single answer across all 3 runs cited its source file (5/5 every time, target was 5/5). |
| 3 | Gate stops out-of-corpus questions | MET | The gate refused 5 of 5 out-of-scope questions (target was 4/5). |
| 4 | Something about your chunks | MET | All 5 sample chunks read as complete, self-contained posts with nothing cut off. |
| 5 | Correct source attribution | MET | Every answer's cited source file matched the actual topic of the question. |

## Diagnoses

I missed nothing, all 5 criteria came out MET across all 3 runs. That likely means my targets were set safely rather than my system being flawless.

Criterion 1 is the one I'd tighten. My 5 test questions are all simple, single-fact lookups on clearly distinct topics (add/drop, dining dollars,
work-study), so retrieval never had to distinguish between similar-sounding posts. A harder test would include a question where two different posts discuss related topics - e.g. two different dorms both mentioning laundry costs - so retrieval actually has to pick the right one apart from a close competitor, not just find "the one post about X" when there's only one post about X in the whole corpus.

## The Improvement

**What I changed:**

I lowered `CHUNK_SIZE` in `config.py` from its original value to 150 characters and temporarily switched `split_documents` in `chunker.py` to call `fallback_split` instead of my own one-post-per-chunk strategy. This forced posts that used to be one whole chunk to split into multiple small fragments (88 documents became 972 chunks, average 116 characters, some as short as 1 character).

**Why I picked it:**

In Milestone 3 (Unit 2), I diagnosed criterion 1 as the least-tested of my five criteria, since my original chunker keeps every post whole and never has to prove it can handle fragmented context. I wanted to test what happens if that assumption is forced to break.

### Run Log — After

| Criterion | Target | Run 1 | Run 2 | Run 3 | Verdict |
|---|---|---|---|---|---|
| 1. Retrieved chunk contains the answer | 4 of 5 | 5/5 | 5/5 | 5/5 | MET |
| 2. Every answer names a source | 5 of 5 | 5/5 | 5/5 | 5/5 | MET |
| 3. Gate stops out-of-corpus questions | 4 of 5 | 5/5 | 5/5 | 5/5 | MET |

All five in-corpus questions still passed the gate (distances 0.206–0.373, still under the 0.6 cutoff) and the gate still refused all 5 out-of-scope questions. On the surface, every criterion still shows MET.

But reading the actual generated text tells a different story. On "What is the deadline for dropping a class without getting a W?", run 1 produced this:
   Based on the documents provided, you can add a course through the end of
   the second week, and dropping through that same time frame (the end of
   week two) avoids showing a "W" on your transcript, as drops after week
   two show a "W" through the end of week six.
Compare that to the same question in the "before" run: a clean, single sentence citing the correct deadline. This "after" answer conflates the add-course deadline with the drop deadline and reads confusingly — a real comprehension failure that the aggregate numbers don't capture. Runs 2 and 3 of the same question came out clean, so this failure appeared in only 1 of 3 runs, on 1 of 5 questions.

I also noticed source diversity dropped. Before, the dining-dollars question retrieved 5 distinct source files; after, only 2. The
work-study question went from 5 distinct files to just 1. With 972 small chunks instead of 88, several of the top-5 retrieved chunks now often come from the *same* file, crowding out other documents that might have added useful context.

**Did it help?**

No. The pass/fail numbers stayed the same, but this wasn't a real improvement — it introduced a genuine coherence failure in 1 of 3 runs and reduced the diversity of sources retrieved per question, for no measurable benefit. I reverted `chunker.py` and `config.py` back to my original one-post-per-chunk strategy, which is the version reflected in the rest of this repository.

## What's Still Broken

Officially, nothing — all 5 criteria are MET. But my Milestone 4 experiment surfaced a real, unlabeled weakness: when chunks get small and numerous, answer coherence can degrade even while every named criterion still passes. None of my 5 criteria would have caught that failure, since it doesn't show up in distance scores or in whether a source was named. If I continued, I'd add a sixth criterion specifically testing answer coherence/consistency across repeated runs of the same question, not just whether the right fact is present.

## What I'd Do Differently

I'd tighten criterion 1 to specifically include at least one question about two related-but-distinct topics (e.g. two different dorms, or two different deadlines), since my current 5 questions are all clearly separated topics that never forced retrieval to discriminate between close competitors. I'd also add a criterion about answer coherence, since my Milestone 4 experiment showed a system can pass every existing criterion while still occasionally producing a confused, conflated answer.
# Acceptance criteria — The Unofficial Guide

Five criteria that say what "working" means for this system, written in unit 1
**before** any results existed.

An acceptance criterion names a target: a number, a count, a rate, or something
a person could plainly observe. *"Retrieval works"* is an opinion. *"For at
least 4 of my 5 test questions, the top results include a chunk containing the
answer"* is a criterion.

Under each one, write a sentence or two on **why that target** and not a
stricter or looser one. A reason that says something about your corpus or your
pipeline earns credit; *"80% seemed reasonable"* does not.

> Missing your own targets next unit costs you nothing. Setting a target so
> easy you can't miss it does.

---

## 1. Retrieved chunks contain the answer

For at least 4 of my 5 test questions, the retrieved chunks include one that
contains the answer.

**Why this target:**
My five questions are directly based on information covered in my corpus. Each question focuses on a specific fact, such as the add/drop deadlines, work-study and financial aid, declaring a major, or dining dollars. Because these topics are explicitly discussed in the documents, I expect at least four of the five questions to retrieve a chunk containing the information needed to answer the question.
---

## 2. Every answer names a source

Every answer the system produces names at least one source document.

**Why this target:**
I expect every answer to name at least one source because my questions are all about information contained in my corpus. The system is designed to retrieve relevant documents before generating an answer, so each answer should be supported by one of those documents. This should be achievable as long as the retrieval step finds a relevant chunk for each question and the answer-generation step includes the source information.

---

## 3. The relevance gate stops out-of-corpus questions

When I ask a question my documents clearly don't cover, the relevance gate
stops it and the system returns "I don't have enough information about that" —
in at least 4 of 5 tries.

<!-- The five questions are the ones in `OUT_OF_SCOPE` at the bottom of
     `questions.py`, and `run_eval.py` puts them through the gate and writes
     what happened into your run log. Swap them for your own if you'd rather —
     just keep five of them, or the "4 of 5" above has nothing to be 4 of. -->

**Why this target:**
<!-- What did your distances look like when you set the cutoff in Milestone 4?
     Was there a clean gap, or did the two groups overlap? -->

---

## 4. Something about your chunks

At least 4 of the first 5 chunks in the run log contain one complete campus-life post, with no sentence cut off at the start or end.

Why this target:

My corpus contains 88 short student-life posts about topics such as dining dollars, course add/drop policies, financial aid, and housing. Since these posts are relatively short, I expect each chunk to contain a complete post rather than splitting important information across multiple chunks. I chose 4 out of 5 because some posts may be longer or contain more information than others, making them harder to fit into a single chunk.





---

## 5. Correct Source Attribution

At least 4 of 5 test answers cite the correct source document that contains the information used in the answer.

Why this target:

My campus-life corpus contains 88 student-life posts covering different topics, so the system needs to identify the correct source rather than simply naming any document. I chose 4 out of 5 because some posts may discuss similar topics, making it harder for the system to identify the exact source every time.


**Why this target:**



---

<!-- ─────────────────────────────────────────────────────────────────────────
     UNIT 2 — read this before you change anything above.

     If a criterion turns out to be BROKEN rather than merely unmet, you can
     revise it, and that earns credit. But never delete or edit the original
     line. Add the revision underneath it, like this:

         ## 1. Retrieved chunks contain the answer

         For at least 4 of my 5 test questions, the retrieved chunks include
         one that contains the answer.

         **Why this target:** ...

         > **Revised in unit 2:** For at least 4 of 5 questions, the top three
         > results contain the answer.
         >
         > **Why revised:** I couldn't judge "the chunks include one that
         > contains the answer" the same way twice — I scored two questions
         > differently on Monday than on Wednesday. The new version is
         > something I can actually check.

     That's a revision because the criterion couldn't be MEASURED.

     Lowering a target because you missed it is not a revision, and it costs
     you the point:

         ✗ "I said 4 of 5 but got 2 of 5, so 2 of 5 is more realistic."

     A number you missed stays where it is, gets diagnosed, and gets a fix
     attempted. That's where the points are.

     The whole reason the originals stay visible is so someone can see what you
     said before you knew the answer.
     ───────────────────────────────────────────────────────────────────────── -->

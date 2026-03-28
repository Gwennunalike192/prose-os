# 🏗️ Architecture — How the 17-Stage ProseOS Pipeline Works

ProseOS is a linear state machine designed to mimic a high-end editorial department. By decomposing the writing process into 17 atomic stages, the system maintains **architectural control** over long-form content, preventing the "vague drift" common in single-prompt AI outputs.

---

## 🗺️ Pipeline Overview

ProseOS breaks essay generation into 17 discrete, quality-controlled stages. Each stage has a single responsibility, clear inputs/outputs, and built-in validation.

```text
TOPIC INPUT
    ↓
① Duplicate Check
    ↓
② Insight Generator
    ↓
③ Thesis Architect
    ↓
④ Hook Writer
    ↓
⑤ Writer Part 1
    ↓
⑥ Writer Part 2
    ↓
⑦ Word Count Gate          ⚠️ Quality Gate (no API)
    ↓
⑧ Fact Checker (Part 1)
    ↓
⑨ Fact Checker (Part 2)
    ↓
⑩ Merge Sections            ⚠️ Logic only
    ↓
⑪ Voice Architect (Part 1)
    ↓
⑫ Voice Architect (Part 2)
    ↓
⑬ Link Injector             ⚠️ Logic only
    ↓
⑭ Blog Formatter
    ↓
⑮ SEO Generator
    ↓
⑯ Image Prompt Architect
    ↓
⑰ Final Editor              ⚠️ Creates Google Doc
    ↓
PUBLISHED GOOGLE DOC + METADATA
````

-----


---

## Stage-by-Stage Breakdown

### ① Duplicate Check

**Purpose:** Prevent redundant essays by detecting topic overlap.  
**Method:** Scans the **Memory** sheet for 40%+ keyword overlap with previously published topics.  
**API Cost:** 0 (pure logic)

**Why it exists:** Saves API credits and maintains a clean content archive.

**Common Output:**  
- `DUPLICATE WARNING` → Topic overlaps with an existing essay.  
**Fix:** Change the angle or manually set Agent to "Insight Generator" and run Force Rerun.

---

### ② Insight Generator

**Purpose:** Generate foundational, non-obvious ideas before writing begins.  
**Output:** 3 high-value insights + 2 observable behavioral/cultural patterns.  
**API Cost:** 1 call

**Why it exists:** Ensures the essay has depth and originality rather than generic content.

**Failure Mode:** Malformed response (missing `INSIGHTS:` or `PATTERNS:` labels).  
**Fix:** Force Rerun.

---

### ③ Thesis Architect

**Purpose:** Synthesize insights into a single, strong, tension-filled thesis statement.  
**Output:** 1–2 sentence thesis.  
**API Cost:** 1 call

**Note:** If you manually enter content in the **Thesis** column, this stage is automatically skipped.

---

### ④ Hook Writer

**Purpose:** Craft a compelling opening paragraph (60–90 words).  
**Rules:** Start with a concrete observation, create curiosity, do **not** state the thesis directly.  
**API Cost:** 1 call

---

### ⑤ Writer Part 1 & ⑥ Writer Part 2

**Purpose:** Generate the full essay in two parts to avoid truncation issues common with long outputs.

- **Part 1** (~800 words): Opens the essay, includes answer capsule, and builds the argument. Ends with `<<<CONTINUES>>>`.
- **Part 2** (~800 words): Continues directly from Part 1, fully develops the thesis, and ends with a memorable insight. Ends with `<<<COMPLETE>>>`.

**API Cost:** 2 calls

**Why split?** Improves reliability and allows better quality control between sections.

---

### ⑦ Word Count Gate ⚠️

**Purpose:** Quality control gate (no API call).  
**Checks:**
- Section 1 ≥ 300 words
- Section 2 ≥ 300 words
- Total essay ≥ 1000 words

**If it fails:** Set Agent back to "Writer Part 1" and Force Rerun.

---

### ⑧–⑨ Fact Checker (Part 1 & Part 2)

**Purpose:** Verify factual accuracy while preserving voice and structure.  
**Behavior:** Only rewrites incorrect or unverifiable claims.  
**API Cost:** 2 calls (can be skipped via "Skip Fact-Check" column)

**Recommendation:** Skip for well-known or opinion-based topics to save cost.

---

### ⑩ Merge Sections ⚠️

**Purpose:** Combine Part 1 and Part 2 into a single `Final Essay` column.  
**API Cost:** 0 (logic only)

---

### ⑪–⑫ Voice Architect (Part 1 & Part 2)

**Purpose:** Polish the prose — improve rhythm, clarity, specificity, and memorability.  
**Key Note:** This stage is **optional**.  

**Recommendation:** Skip Voice Architect (`RECOMMEND_SKIP_VOICE = true` or set "Skip Voice = Yes"). Most users find the marginal improvement not worth the extra 2 API calls.

**API Cost:** 2 calls (skippable)

---

### ⑬ Link Injector ⚠️

**Purpose:** Prepare internal linking suggestions from the **Published Links** sheet and list authority domains.  
**API Cost:** 0 (logic only)  
**Output:** Stores context in the **Notes** column for easy manual review.

---

### ⑭ Blog Formatter

**Purpose:** Convert plain prose into a well-structured blog post with H1, H2s, pull-quotes, and lists.  
**API Cost:** 1 call

---

### ⑮ SEO Generator

**Purpose:** Generate SEO metadata including best title, meta description, slug, and FAQs.  
**API Cost:** 1 call

---

### ⑯ Image Prompt Architect

**Purpose:** Generate 3 high-quality editorial image prompts (Hero, Section-focused, Anchor) in a conceptual style.  
**API Cost:** 1 call

**Usage:** Copy prompts into Gemini.app (free tier works).

---

### ⑰ Final Editor ⚠️

**Purpose:** Create a professionally formatted Google Doc with the essay and SEO metadata.  
**API Cost:** 0 (logic + Google Docs API)

**Output:** A clean, publication-ready Google Document.

---

## Cost Summary

| Mode                        | API Calls | Approx. Time | Use Case                     |
|----------------------------|-----------|--------------|------------------------------|
| Full Pipeline              | 11–13     | 2–3 minutes  | Maximum quality              |
| Skip Voice (Recommended)   | 9–11      | ~2 minutes   | Best balance                 |
| Skip Fact + Voice          | 7–9       | 90–120 sec   | Speed & cost optimization    |

---

## Quality Gates (No API Cost)

- **Word Count Gate**
- **Merge Sections**
- **Final Editor**

These gates act as safety checkpoints. If any fail, the pipeline pauses with a clear recovery suggestion.

---

## Error Recovery Guidelines

1. Check the **Usage Log** column for specific suggestions.
2. Set the **Agent** column back to the failed stage.
3. Click **Force Rerun**.
4. Most transient errors (truncation, malformed output) resolve on retry.

**Persistent issues?**  
- Try a shorter or more focused topic  
- Refine your `STYLE_PROFILE`  
- Skip optional stages (Voice / Fact Check)

---

**Next:** See `VOICE_PROFILE_EXAMPLE.md` for guidance on customizing your voice.

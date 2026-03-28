# ⚡ Quick Reference — ProseOS Pipeline Cheat Sheet

A high-level overview for daily operations. Bookmark this page.

---

## 🚀 60-Second Setup

1. Copy the Google Sheet Template.
2. Go to **Extensions → Apps Script**, delete default code, and paste `scripts/pipeline.gs`.
3. Go to **Project Settings** (gear icon) → **Script Properties** → Add:
   - **Property**: `GEMINI_API_KEY`
   - **Value**: Your API key from [ai.google.dev](https://ai.google.dev)
4. Customize `STYLE_PROFILE` and `VOICE_PROFILE` at the top of the script.
5. Add a topic in the **Dashboard** tab (Row 2).
6. Click **Awesomengers → Run Pipeline**.

---

## 🏗️ The 17-Stage Pipeline
① Duplicate Check → ② Insight Generator → ③ Thesis Architect → ④ Hook Writer
↓
⑤ Writer Part 1 → ⑥ Writer Part 2 → ⑦ Word Count Gate (Quality Gate)
↓
⑧ Fact Checker 1 → ⑨ Fact Checker 2 → ⑩ Merge Sections
↓
⑪ Voice Architect 1 → ⑫ Voice Architect 2 → ⑬ Link Injector
↓
⑭ Blog Formatter → ⑮ SEO Generator → ⑯ Image Prompt Architect
↓
⑰ Final Editor → Published Google Doc

---

## 🚦 Status Meanings

| Status            | Meaning                                      |
|-------------------|----------------------------------------------|
| **Pending**       | Ready to process                             |
| **Processing**    | Currently running                            |
| **Ready**         | Complete — Google Doc generated              |
| **Ready - Review**| Complete but requires manual approval        |
| **Error**         | Failed — check Usage Log                     |
| **Quota Wait**    | API limit hit — wait for reset               |
| **Content Fail**  | Quality gate failed                          |

---

## Essential Menu Commands

| Command                        | When to Use                                      |
|--------------------------------|--------------------------------------------------|
| **Run Pipeline**               | Process next Pending row                         |
| **Force Rerun**                | Retry failed, Ready, or Content Fail rows        |
| **Resume Quota Wait Rows**     | After quota reset (~1:30 AM IST)                 |
| **Discover Trending Ideas**    | Generate 5 new essay ideas from Reddit/HN        |
| **Approve Ideas to Dashboard** | Move approved ideas from Idea Bank               |
| **Archive Finished Articles**  | Move Ready articles to Memory sheet              |
| **Color-Code Dashboard**       | Visual color coding by status                    |

---

## 💰 API Cost & Optimization

| Scenario                    | API Calls | Approx. Time | Recommendation          |
|-----------------------------|-----------|--------------|-------------------------|
| Full Pipeline               | 11–13     | 2–3 min      | Maximum quality         |
| **Skip Voice** (Recommended)| 9–11      | ~2 min       | **Best balance**        |
| Skip Fact + Voice           | 7–9       | 90–120 sec   | Speed & cost saving     |

**Pro Tip:** Use the **Skip Fact-Check** and **Skip Voice** columns in Dashboard to save up to 4 API calls per essay.

---

## 🛠️ Common Errors & Quick Fixes

| Error                              | Cause                        | Quick Fix                                      |
|------------------------------------|------------------------------|------------------------------------------------|
| Quota exceeded (429)               | Daily limit hit              | Wait → Resume Quota Wait Rows                  |
| DUPLICATE WARNING                  | Topic too similar            | Change angle or force "Insight Generator"      |
| TRUNCATION                         | Response cut off             | Set Agent back → Force Rerun                   |
| CONTENT FAIL                       | Malformed output             | Force Rerun on that stage                      |
| GEMINI_API_KEY not found           | Key not set                  | Add in Project Settings → Script Properties    |

---

## 🦾 Manual Intervention (Co-Writing)

You can edit columns manually. After editing, set the **Agent** to the next logical stage and click **Force Rerun**.

- Edit **Thesis** → Set Agent to `Hook Writer`
- Edit **Hook** → Set Agent to `Writer Part 1`
- Edit **Section 1** → Set Agent to `Voice Architect (Part 1)`
- Edit **Section 2** → Set Agent to `Voice Architect (Part 2)`

---

## 📄 Documentation Index

- [`scripts/pipeline.gs`](scripts/pipeline.gs) — Main engine
- [`docs/SETUP.md`](docs/SETUP.md) — Step-by-step onboarding (start here)
- [`docs/ARCHITECTURE.md`](docs/ARCHITECTURE.md) — Detailed stage breakdown
- [`docs/VOICE_PROFILE_EXAMPLE.md`](docs/VOICE_PROFILE_EXAMPLE.md) — How to engineer your voice
- [`docs/ERROR_RECOVERY.md`](docs/ERROR_RECOVERY.md) — Full troubleshooting guide
- [`README.md`](README.md) — Project overview

---

**Pro Tip:**  
The quality of your output depends **90%** on how well you define `STYLE_PROFILE`.  
Spend time refining it — the pipeline will amplify a good voice definition.

---

**Questions?**  
Check `ERROR_RECOVERY.md` first, then open a GitHub issue.

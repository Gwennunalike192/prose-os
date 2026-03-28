# 🛠️ Error Recovery — Troubleshooting Guide

The ProseOS pipeline is designed to **fail gracefully**. When something goes wrong, the pipeline halts, turns the dashboard row **Red**, and provides a diagnostic fix in the **Usage Log** column.

---

## 🚨 Common Critical Errors

### ❌ "Quota exceeded (429)"
**What it means:** You've hit Gemini's daily API limit (free tier allows ~20 calls per day).  
**When it happens:** Usually during the 2nd or 3rd full essay run in a 24-hour period.  
**How to fix:**
1. Wait for the quota reset (usually around 1:30 AM IST / midnight UTC).
2. Go to **Awesomengers → Resume Quota Wait Rows**.
3. Click **Run Pipeline** again.

### ❌ "DUPLICATE WARNING: Overlaps with..."
**What it means:** Semantic memory detected that this topic (40%+ keyword overlap) exists in your `Memory` sheet.  
**How to fix:**
- **Recommended:** Pivot the angle. Instead of "Why X is good," try "The hidden danger of X."
- **Force Override:** Set the **Agent** column to `Insight Generator` and click **Force Rerun** to bypass the check.

### ❌ "TRUNCATION: Section 1 only [X] words"
**What it means:** Gemini stopped writing mid-sentence or hit a token limit before finishing the section.  
**How to fix:**
1. Set the **Agent** back to the failed stage (e.g., `Writer Part 1`).
2. Click **Force Rerun**. Retrying usually resolves this instantly.

---

## 🖋️ Content & Logic Failures

| Error Message | Cause | Resolution |
| :--- | :--- | :--- |
| **"INSIGHTS/PATTERNS missing"** | Malformed API response. | Trigger **Force Rerun** on the Insight stage. |
| **"No ## headings produced"** | Essay returned as wall of text. | Rerun **Blog Formatter** or add H2s manually. |
| **"Voice P1 inserted headings"** | `VOICE_PROFILE` logic leak. | Ensure your Profile forbids Markdown headings. |
| **"Marker missing"** | Missing hand-off tokens. | Manually add `<<<CONTINUES>>>` and Force Rerun. |

---

## ⚙️ Configuration Issues

### ❌ "GEMINI_API_KEY not found"
**How to fix:** Go to **Extensions → Apps Script** > **Gear Icon** (Project Settings) > **Script Properties**. Ensure the key is named exactly `GEMINI_API_KEY`.

### ❌ "Dashboard sheet missing" / "Missing required column"
**How to fix:** - Ensure your tab is named exactly **`Dashboard`** (case-sensitive).
- Verify all 19 headers match the order in `docs/SETUP.md`.

### ❌ "Weekly limit of 5 articles reached"
**How to fix:** This is a safety gate to protect free-tier users. To remove it, edit the `WEEKLY_LIMIT` constant at the top of your script.

---

## 🦾 Manual Recovery (Power User Mode)

ProseOS is **state-aware**. If a stage fails and you think you can do a better job than the AI, you can intervene:

1. **Edit Directly:** Manually write the `Thesis`, `Hook`, or `Section` in its respective column.
2. **Shift State:** Change the **Agent** column to the *next* logical step in the pipeline.
3. **Resume:** Click **Force Rerun**. The system will use your manual entry as the "source of truth" and continue.

---

## 📈 Performance & Prevention

- **Save Calls:** Use `Skip Fact-Check` and `Skip Voice` flags in the Dashboard.
- **Stable Topics:** LLMs work best with clear, high-intent topics. Avoid extremely abstract one-word topics.
- **Archive Often:** Regularly run **Awesomengers → Archive Finished Articles** to keep your duplicate detection engine sharp.

---

**Still Stuck?** Open a **GitHub Issue** with the topic name and a copy of your **Usage Log** (never share your API key).

See also: [`SETUP.md`](docs/SETUP.md) | [`ARCHITECTURE.md`](docs/ARCHITECTURE.md)

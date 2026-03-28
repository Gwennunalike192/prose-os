# ProseOS Setup Guide

**Time to completion:** ~15 minutes

### Prerequisites
- Google Account
- Gemini API Key (from [ai.google.dev](https://ai.google.dev))

---

### Phase 1: Create the Google Sheet

1. Create a new Google Sheet and name it something like "ProseOS - Content Pipeline".
2. Create these 5 tabs:

   | Tab Name           | Purpose                              |
   |--------------------|--------------------------------------|
   | **Dashboard**      | Main control center                  |
   | **Idea Bank**      | Store raw ideas                      |
   | **Memory**         | Prevents duplicate essays            |
   | **Published Links**| Internal linking database            |
   | **Pipeline Health**| Auto-generated status overview       |

3. In the **Dashboard** tab, add these column headers in Row 1 (make them bold):

   `Topic`, `Status`, `Agent`, `Insight`, `Pattern`, `Thesis`, `Hook`, `Section 1`, `Section 2`, `Final Essay`, `Metadata`, `Doc Link`, `Skip Fact-Check`, `Skip Voice`, `Manual Review`, `Notes`, `Published Date`, `Usage Log`, `Priority`

---

### Phase 2: Deploy the Code

1. In your Google Sheet, go to **Extensions → Apps Script**.
2. Delete all default code in `Code.gs`.
3. Paste the full code from **`scripts/pipeline.gs`**.
4. Click the **gear icon** (Project Settings).
5. Go to **Script Properties** → **Add Script Property**:
   - **Property**: `GEMINI_API_KEY`
   - **Value**: Your Gemini API key
6. Click **Save**.

---

### Phase 3: Customize Your Voice

Open `scripts/pipeline.gs` and edit the two constants at the top:

- `STYLE_PROFILE` — Defines how the **writer** creates content
- `VOICE_PROFILE` — Defines how the **editor** sharpens the prose

**Tip:** Start with the examples in `docs/VOICE_PROFILE_EXAMPLE.md` and customize them to match your unique voice.

---

### Phase 4: Run Your First Essay

1. Refresh the Google Sheet. You should see the **Awesomengers** menu.
2. In **Dashboard**, enter a test topic in Row 2 under the **Topic** column.
3. Go to **Awesomengers → Run Pipeline**.
4. Monitor the **Status** and **Agent** columns as it progresses.
5. When complete, a Google Doc link will appear in the **Doc Link** column.

---

### Cost-Saving Tip

We recommend keeping `RECOMMEND_SKIP_VOICE = true` (default).  
The Voice Architect stage provides only marginal improvement for most users but costs extra API calls. You can always do a quick manual review in the final Google Doc.

---

### Troubleshooting

- **Menu not showing?** Refresh the sheet and wait 10 seconds.
- **429 Quota Error?** Wait for the daily reset or use "Force Rerun".
- **Truncated output?** Set the Agent back to the failed stage and rerun.
- **Output doesn't match your voice?** Refine `STYLE_PROFILE` and `VOICE_PROFILE`.

---

**Next:**  
→ [VOICE_PROFILE_EXAMPLE.md](VOICE_PROFILE_EXAMPLE.md) — How to define your writing voice  
→ [ARCHITECTURE.md](ARCHITECTURE.md) — How the 17-stage pipeline works

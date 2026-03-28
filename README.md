# ProseOS — AI Essay Pipeline

**Production-grade AI pipeline for high-quality long-form essays.**

ProseOS is a complete 17-stage AI essay generation system built with Google Apps Script and Gemini. It turns raw topics into polished, voice-consistent, SEO-ready blog posts and essays — perfect for writers who want depth and quality instead of generic AI output.

### Why ProseOS?

While most AI writing tools rely on a single prompt, ProseOS applies software engineering principles to content creation with strict quality gates, voice preservation, and editorial control.

**Key Capabilities:**
- 17-stage orchestrated pipeline with built-in validation
- Deep voice consistency through dedicated STYLE and VOICE profiles
- Fact-checking, word count gates, and smart error recovery
- Automatic SEO metadata, blog formatting, and image prompts
- Trending idea discovery from Reddit and Hacker News

### Who It's For (Use Cases)

ProseOS is designed for serious content creators who publish regularly:

- **Substack & Newsletter Writers** — Generate 2–5 high-quality essays per week while keeping your unique voice
- **Indie Bloggers & SEO Content Creators** — Produce long-form articles optimized for search and reader engagement
- **Thought Leaders & Experts** — Turn complex ideas into clear, structured essays with proper fact-checking
- **Content Teams** — Maintain brand voice across multiple writers using customizable profiles
- **AI Power Users** — Run a reliable, cost-effective pipeline on Gemini’s free tier (2–3 essays/week)

### Core Features

- **Quality-First Architecture**: Duplicate detection, fact-check passes, voice sharpening, and word count gates
- **Voice Preservation**: Separate writing and editing stages so output sounds like you, not generic AI
- **Production Output**: Professional Google Docs with clean formatting, SEO metadata (titles, meta descriptions, FAQs), internal linking, and 3 custom image prompts per essay
- **Smart Tooling**: Color-coded dashboard, pipeline health monitor, auto-archiving, and quota management
- **Idea Engine**: Automated trending topic discovery to fuel your editorial calendar

### Quick Start (Under 10 Minutes)

1. Copy the [Google Sheet template](https://docs.google.com/spreadsheets/d/1NUT5usAcT0njhbh4LQdxhG9-ree069HlvR6KcL6Uj9A/edit?usp=sharing)
2. Open **Extensions → Apps Script** and paste the full script
3. Add your `GEMINI_API_KEY` in Script Properties
4. Customize `STYLE_PROFILE` and `VOICE_PROFILE` (most important step for voice accuracy)
5. Add a topic in the Dashboard and run **Awesomengers → Run Pipeline**

The system will advance through all 17 stages and deliver a ready-to-publish Google Doc.

### Tech Stack

- Google Apps Script + Google Sheets
- Gemini 2.5 Flash (easy to swap model)
- Google Docs for final output

---

**Built for writers who demand control and quality from AI.**

If you're tired of generic AI essays and want a true pipeline that respects your voice, star ⭐ this repo.

### Next Steps

- [Full Setup Guide](docs/SETUP.md)
- [Voice Customization Guide](docs/VOICE_PROFILE_EXAMPLE.md)
- [Pipeline Architecture](docs/ARCHITECTURE.md)
- [Error Recovery & Troubleshooting](docs/ERROR_RECOVERY.md)

Contributions, issues, and feature requests are welcome.

**Keywords**: AI essay generator, AI long-form writing, Google Apps Script Gemini, voice consistent AI content, automated essay pipeline, AI content pipeline for bloggers

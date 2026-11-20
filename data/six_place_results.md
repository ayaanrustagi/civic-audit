# Citizen Portal accuracy: six-place follow-up (redacted public copy)
*Draft, Nov 20, 2026. All verdicts are AI judgments that Ayaan has not reviewed yet. Numbers come from `study_results.json` (in this folder) (final run Nov 20, about 10:05 AM CT).*

## Results (articles only: headline, dek and first paragraph)

| Place | Size | Articles | Claims | First checker "contradicted" | Confirmed errors (Major/Minor) | Articles with ≥1 Major error [95% CI] |
|---|---|---|---|---|---|---|
| Seattle City Council (budget committee) | large | 30 | 309 | 9.7% | 12 (10/2) | 7/30 = 23.3% [11.8–40.9] |
| Columbus City Council | large | 18 | 205 | 7.8% | 10 (0/10) | 0/18 = 0.0% [0.0–17.6] |
| Wells, ME Select Board and Planning Board | small | 25 | 278 | 9.4% | 31 (9/22) | 4/25 = 16.0% [6.4–34.7] |
| Nephi, UT City Council | small | 13 | 125 | 31.2% | 14 (2/12) | 1/13 = 7.7% [1.4–33.3] |
| **Large places combined** | | 48 | 514 | 8.9% | 22 (10/12) | 7/48 = 14.6% [7.2–27.2] |
| **Small places combined** | | 38 | 403 | 16.1% | 45 (11/34) | 5/38 = 13.2% [5.8–27.3] |
| Newport, NH Board of Selectmen (document-based, reported separately) | small | 28 | 320 | 5.3% | 2 (0/2) | 0/28 = 0.0% [0.0–12.1] |
| Leander (first study), for reference | | 79 | 928 | 10.0% | 66 (14/52) | 10/79 = 12.7% [7.0–21.8] |

- **Small minus large, articles with a Major error:** −1.4 points, 95% CI −16.0 to +14.5 (Newcombe, articles treated as independent). No difference shown.
- **Small minus large, articles with any confirmed error:** +15.0 points, 95% CI −4.9 to +33.9. Also not significant.
- **Confirmed errors per claim** (95% bootstrap over articles):
  - Seattle 3.9% (1.5–6.4)
  - Columbus 4.9% (1.0–9.7)
  - Wells 11.2% (5.5–17.3)
  - Nephi 11.2% (3.6–19.9)
  - Newport 0.6% (0.0–1.6)
- **Newport (document-based arm):** 2 Minor errors in 320 claims, and no Majors.
  - One body sentence folds a separate bridge-redecking request into the trails grant application.
  - One headline says election staffing was "finalized" when one poll worker was still unconfirmed.
  - Its first checker flagged 17 claims. Grok judged most of them supported or unclear. For example, the Little League agreement, the resignation and the rate scenarios were all in the minutes, but the checker's trimmed evidence missed them.
  - Articles written from the minutes themselves were far more accurate than the recording-based articles. That is consistent with most errors in the other places being transcription slips (names, numbers) and "discussed vs. acted".
- Nashville was dropped (see PLACES.md). Newport is not pooled: its Citizen Portal articles are written from the posted minutes, not from a recording.

## What the errors look like
- **Seattle (10 Major):**
  - Mostly headlines or sentences saying the Council or committee "advanced", "funded" or "approved" a budget proposal. The minutes record only that an information item was heard or discussed.
  - Also one dollar figure: "$500,000" where the official proposal packet says $175,000.
  - Also one proposal sponsor credited to staff instead of the councilmember.
- **Columbus:** 10 Minor items: name spellings, dates, and one borderline wording about whose budget it was. No Majors.
- **Wells (9 Major):**
  - "sidewalk" where the minutes say "site walk" (4 claims, one article);
  - "lot 10" for the 10th occupancy;
  - a 4-0-1 vote reported as unanimous;
  - an applicant given the wrong first name (3 claims).
  - Minor items are mostly name spellings from the OCR'd minutes.
- **Nephi (2 Major):**
  - One article gives the two young wrestlers recognized by the mayor the wrong surname (the dek and the body; names withheld).
  - Minor items:
    - the mayor's surname misspelled ("Sealy" for Seely);
    - "Roof Theatre" for the Ruth Theater;
    - "Neagle Heights" for Nebo Heights (3 claims);
    - a bid of $682,882 instead of $682,822;
    - a "CU3" zone that the minutes don't mention (they discuss CU1/CU2);
    - a grant of "up to $135,000" written as $135,000;
    - three separate rezonings described as parcels on one downtown block.
  - Nephi's first checker flagged 31% of claims, the most of any place, but many flags were wrong. For example, it said the noise ordinance was "only introduced", but the minutes record a roll-call vote approving it. It also treated "voice vote" as contradicted where the minutes just say "4-0".

## Methods note: which models ran where
- **Articles and records:**
  - Articles are logged-out Citizen Portal pages.
  - Records are official minutes and agendas (Legistar for Seattle and Columbus; town PDFs elsewhere; Wells OCR'd on the box), plus YouTube auto-captions where available.
- **Pipeline:** claims → first check → second check (every flagged article group plus a seeded 25% of the rest, seed 20261116).
- **Columbus and Wells:** claims by Codex; first check GPT-6.1 Terra (high reasoning); second check GPT-6 Astra; full evidence.
- **Seattle:**
  - Claims: 5 jobs on Gemini 3.8 Flash high, 3 on Flash medium and 1 on Claude Sonnet 4.6, all via the Antigravity (agy) CLI.
  - First check: 289 claims by Claude Sonnet 4.6 via agy (full evidence) and 20 by Gemini 3.8 Flash high (trimmed evidence).
  - Second check: Gemini 3.8 Flash high (trimmed).
- **Nephi:** claims, first check and second check all on Gemini 3.8 Flash high via agy, with trimmed evidence.
- **Newport:**
  - Claims: 3 jobs on Claude Sonnet (Claude Code CLI) and 5 on Gemini 3.8 Flash high.
  - First and second check: Gemini 3.8 Flash high via agy, trimmed evidence.
- **Trimmed evidence** means the top 5 passages by BM25 (3 from documents, 2 from the transcript), capped at about 4,500 characters per prompt. This was introduced to cut usage after the Codex and Claude limits were hit.
- **Independence:** where both checkers are the same model (Gemini Flash high: Nephi, Newport and Seattle's 20 trimmed claims), the second check is less independent than in Leander.
- **Reference review (all places):** done by Grok (AI reference reviewer). It covers every claim either checker called contradicted, plus a seeded sample of 10 claims both checkers called supported (seed 20261118).
  - Grok used the Leander rubric:
    - Major means it misstates an official action, vote or procedure; a number is off by more than 25%; or it names the wrong person.
    - "Contradicted" requires an official record to say otherwise. Caption-only differences count as unclear.
  - Every record quote was verified verbatim against the record text by `grok_apply.py`.
- **Seattle reference review:** for Seattle, Grok also read the official Legistar budget-proposal packets (council events 6769 and 6770). The machine checkers did not see these.
- **Reviewer agreement:** Grok's labels match the earlier Claude Sonnet reference labels on 21/27 verdicts in Columbus and 40/49 in Wells. Grok rated Columbus's one Claude "Major" as Minor (borderline), which is why Columbus now has 0 Majors.
- **Codex** was turned off mid-study at Ayaan's request. **Claude** was used only while its limits allowed.

## Caveats
- Small samples: 13 to 30 articles per place. Every interval above is wide.
- No human review yet. Grok is the reference reviewer, and the severity labels are provisional until Ayaan checks the queue.
- Wells minutes are OCR'd and Seattle's minutes are thin. Name and "action vs. discussion" errors depend on how complete the record is.
- Seattle covers one budget-committee season. Wells spans Jan 2025 to Oct 2026. The other places cover a few 2026 meetings.
- Models varied by place (see the methods note), so per-place differences partly reflect the checkers. The confirmed-error counts all come from the same reference reviewer.

## Usage (from `usage_report.py`, CLI log `data/parsed/cli_usage.jsonl`; covers the Seattle, Nephi and Newport runs after Codex was turned off)
| Place | Calls (ok) | Input tokens | Output tokens (of which thinking) |
|---|---|---|---|
| Seattle | 152 (63) | 1,109,301 | 2,117,861 (2,004,006) |
| Nephi | 77 (30) | 580,722 | 1,129,472 (1,088,064) |
| Newport | 88 (53) | 758,817 | 1,505,028 (1,403,697) |
| **All agy** | 298 (145) | 2,469,112 | 4,739,276 (4,496,037) |
| **All Claude Code CLI** | 23 (4) | 8 (plus about 11k cache-creation tokens per call) | 13,466 |

- Failed calls were mostly agy timeouts, stream interruptions and the Nov 19 transient "model not recognized" errors.
- 18 of the Claude calls were connection resets.
- These totals include 4 test calls.
- Codex usage for Columbus and Wells is reported in INTERIM.md.

Names of members of the public and of students are withheld in this file.

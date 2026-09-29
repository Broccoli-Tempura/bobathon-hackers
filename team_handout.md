# THE MERIDIAN PROBLEM
## Team handout · 5-hour build challenge · Bobathon @ HSG · Build with IBM Bob

> **DISCLAIMER: THIS CASE IS FICTION.** **Everything in this case is invented.** Halcyon Systems, Kestrel Labs, MERIDIAN and all the people in it do not exist. Real places such as St. Gallen are used in a fictitious manner. Any resemblance to actual persons, living or dead, or to actual companies or events, is coincidental. **What is real: the rules, the clock and the scoring.**

---

## YOUR JOB, IN ONE SENTENCE

Tells us **who** took the model, **how sure** it is, and **where** every piece of its reasoning came from.

---

## THE CASE

Halcyon Systems, St. Gallen, built **MERIDIAN**, an AI model that predicts which battery chemistries will work in the lab. It is right 1 time in 9; the rest of the industry manages 1 in 400.

One weekend in October 2025, someone copied the model onto a portable drive and left the building with it. They used the one window when nothing was recording: audit logging was switched off **on purpose**, from **21:00 Friday 10 October to 06:00 Saturday 11 October**, for a datacenter migration (ticket INFRA-2291). About forty people knew the window was coming. There are no cameras on the engineering floor, and the door badge record is useless.

About a month later, a rival lab, Kestrel Labs, published a paper. Their model produced one of twenty impossible materials that Halcyon had hidden in its own training data as a watermark. So the theft is certain. The thief is not.

The investigator, Nadia Arslan, interviewed the eight people who could have done it and collected every export she could get: from Halcyon, the card issuer and the building's landlord. There was too much for one person to check, so she handed the whole file to you, exactly as she received it.

---

## WHAT YOU GET

One zip, `meridian_case_bundle.zip`, about **210,000 words** in nine formats. Start with its `README.md`.

| Path | What it is | Format |
|---|---|---|
| `investigator_notebook.md` | The investigator's working notes | Markdown |
| `interviews/` | 8 interviews + 2 follow-ups, automatic transcripts, not proofread | Text |
| `forensic_summary_bakalian.pdf` | Forensic examination of the storage the copy ran on | PDF |
| `witness_statement_okada_scan.pdf` | Handwritten witness statement | Scanned PDF (image only) |
| `evidence_photos/` | Two photos taken during the investigation | JPEG |
| `slack_export/` | Chat workspace export: users, channels, one file per channel per day | JSON |
| `email_export.mbox` | ~650 emails, some in German and Italian | mbox |
| `jira_export.json` | ~300 tickets with comments | JSON |
| `calendars/` | 12 calendars from two different calendar apps | iCalendar (.ics) |
| `helpdesk_and_facilities.md` | IT and building tickets | Markdown |
| `expense_reports.md` | Expense claims and claim detail | Markdown |
| `card_feed_q4.csv` | Corporate card transactions from the card issuer | CSV |
| `garage_barrier_log.csv` | The landlord's garage number-plate log | CSV (German) |
| `parking_permits.xlsx` | Parking permit list | Excel |
| `meeting_notes.md` | 1:1s, all-hands, board readouts | Markdown |
| `kestrel_diligence_log.md` | Takeover-talks request log and data-room access | Markdown |

Nobody has sorted or cleaned it. The systems disagree on names, date formats and time zones, and not every clock was right. Some evidence exists only in the scanned statement and the photos; you will need OCR or a model that can read images to use it, but the case can be solved without them.

---

## THE TRAP

Ask an AI assistant who did it and you may well get a name. What you won't get is why the other seven are innocent, and that is most of the score. Some people in this case **seem to know things only the thief could know**. For some of them, the innocent explanation is in a different file, in a different format, thousands of messages away.

Flagging suspicious people and stopping there misses the hardest part. Saying *"three people looked suspicious; two are explained by X and Y; here is the one that isn't"* is doing what we ask.

**What one finding looks like** (a real example from the bundle):

| | |
|---|---|
| Suspicion | `interviews/interview_07_kurt_steiner.txt:11`: Kurt Steiner confirms he was in the building on the Sunday, and he has admin accounts on most systems. |
| Paperwork | `slack_export/general/2025-10-12.json:5`: `"text": "office is beautifully quiet on a sunday"`, posted from his user ID (see `slack_export/users.json`) |
| Judgement | The record puts him there on Sunday; the copy happened Friday night. Weight: low. Lowered, not cleared. |

---

## WHAT YOU HAND IN

One repository per team. The one thing we score automatically is **`verdict.json`**, in exactly this format:

```json
{
  "team": "your-team-name",
  "culprit": "Full Name",
  "confidence": 0.65,
  "suspects": [
    {
      "name": "Full Name",
      "verdict": "culprit | cleared | unresolved",
      "reasoning": "one or two sentences",
      "evidence": [
        {"claim": "what this shows", "source": "slack_export/general/2025-10-12.json:5",
         "quote": "office is beautifully quiet on a sunday"}
      ]
    }
  ]
}
```

Start from `verdict_template.json` (blank, all eight suspects already listed). `verdict_example.json` shows the same format filled in — with different names, so it's a format example, not an answer.

- All eight suspects appear in `suspects`.
- `source` is the path inside the bundle plus where to look:
  - text files (`.md` `.txt` `.json` `.csv` `.mbox` `.ics`): `path:line` or `path:start-end`, line numbers as received;
  - PDFs: `file.pdf:page`, e.g. `forensic_summary_bakalian.pdf:1`;
  - the spreadsheet: `parking_permits.xlsx:row`, the Excel row number;
  - photos: just the file, e.g. `evidence_photos/whiteboard_room_2F-3.jpg`.
- `quote` is copied exactly from that line, page, row or photo. We check every quote automatically; a quote that isn't there counts against you.

Alongside `verdict.json`, hand in the code that produced it and a short README covering how to run it and anything you typed into the code after reading it yourself (see Rules, below).

---

## SCORING

Half the points come from a script that checks your `verdict.json` against the case files. The other half come from the judges during your pitch.

**The script (50 points)**

| | |
|---|---|
| **The right name**, with both misleading suspects correctly explained. | **20** |
| **A source for every claim.** Every claim points to a file, a line and the exact quote, and the quote is really there. | **15** |
| **Handling uncertainty.** An honest confidence number, all eight suspects judged, innocent people cleared with evidence. | **15** |

**The judges (50 points).** Each judge scores seven criteria from 1 to 5 on their own; the scores are averaged across judges and scaled to 50.

| Criterion | The judges ask |
|---|---|
| **Problem** | What is the problem, and why does it matter? |
| **Design** | What thought went into the design and user experience? Can an investigator check each claim and see the doubt? |
| **Develop** | What thought went into developing it with Bob? Bob inside the system, its answers checked. |
| **Test** | How was it tested? Quotes verified, traps tried, repeat runs. |
| **Deploy** | How would it be taken live, and what are the next steps? |
| **Demo** | A functioning solution shown live, making the case with evidence. A terminal can score full marks; a UI earns nothing on its own. |
| **Time** | Did you stay within the 5 minutes? |

**Bonus (10 points, on top).** Anything extra your team proposes beyond what's asked, for example how you'd stop this from happening again. Judged the same way, scored 0 to 10 directly, added on top so the total can reach 110.

The judges then compare their top three to pick the winner, announced at 17:30.

A lucky guess with nothing behind it gets 10 of the script's 50. The wrong name from a careful system that cites its sources, knows how sure it is and shows it well can still finish near the top.

---

## RULES

1. **Chat is only a lead.** Anything Bob tells you in a chat window is a suggestion. If your system cannot find it in the bundle, you do not have it.
2. **Say what you typed in.** You may read the files. If you read something and type it into your code as evidence, list it in the README. Typing in the eight names is fine; they are given. Typing in *"X overheard it"* is evidence. Undeclared evidence scores zero for "a source for every claim" and "the right name".
3. **One team, one repo, five hours.** The clock pauses for lunch.

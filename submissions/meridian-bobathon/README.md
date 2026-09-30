# Meridian Investigation — Submission README

## Team

**meridian-bobathon**

---

## How to run

### Requirements

Python 3.10+ with three additional packages:

```
pip install icalendar pypdf openpyxl
```

### Run the full pipeline

```
python investigate.py
```

This runs all five steps in sequence and writes
`submissions/meridian-bobathon/verdict.json`.

You can also run each step individually:

| Step | Script | Output |
|---|---|---|
| 1 — Index evidence | `python index_evidence.py` | In-memory (`LINE_INDEX`, `TIMELINE`) |
| 2 — Suspect profiles | `python build_profiles.py` | `suspect_profiles.json` |
| 3 — Forensic pivot | `python forensic_pivot_precise.py` | `forensic_pivot_report.json` |
| 4 — Score & rank | `python score_suspects.py` | `scored_suspects.json` |
| 5 — Generate verdict | `python generate_verdict.py` | `submissions/meridian-bobathon/verdict.json` |

All scripts must be run from the repository root (the folder containing
`meridian_case_bundle/`).

---

## Architecture

```
index_evidence.py       ← loads all 16 file types, builds LINE_INDEX + TIMELINE
build_profiles.py       ← per-suspect: access / opportunity / motive / alibi
forensic_pivot_precise.py ← keyword grep on interviews only for withheld detail
score_suspects.py       ← additive scoring model, quote verification
generate_verdict.py     ← serialises to verdict.json schema
```

---

## Declaration of hand-typed facts (Rule 2)

Per contest rules, any fact typed into the code after reading the files
must be declared here. The following were typed in by hand after reading
the case bundle:

1. **The 8 suspect names** — listed in `investigator_notebook.md:23–24` and
   used as constants throughout.

2. **Parking permit → plate mapping** — read from `parking_permits.xlsx` rows 3–9
   and hardcoded in `build_profiles.py::PLATE_TO_SUSPECT` for cross-referencing
   with the garage log.

3. **Garage clock correction (−1 hour)** — read from `helpdesk_and_facilities.md:890`
   (FAC-352: "barrier system clock stayed on winter time after 30 March").
   Hardcoded as `GARAGE_CLOCK_CORRECTION_HOURS = -1`.

4. **Forensic UTC times** — read from `forensic_summary_bakalian.pdf` page 1:
   copy started 21:10 UTC, failed ~00:20, snapshot deleted 00:41, restarted
   00:44, completed 03:52, device detached 03:58. Used to anchor the timeline
   in `build_profiles.py` and `generate_verdict.py`.

5. **FAC-330 wall detail** — read from `helpdesk_and_facilities.md:902`: the
   partition between 2F-3 and 2F-4 is non-insulated; speech intelligible.
   Used as the innocent explanation for Noemi Rochat's interview pivot hit.

6. **DATA-1877 ticket detail** — read from `jira_export.json:7249–7275`:
   Chiara filed the ticket on 14 Oct from the capacity graph; Yannick
   commented he was in Val Müstair. Used as innocent explanation for
   Chiara Bernasconi's interview pivot hit.

7. **Renata Vogel's Ascona alibi** — read from `interviews/interview_08_renata_vogel.txt:30–34`:
   drove to Ascona Friday evening, alone until Saturday morning.

No suspect names, dates, or evidence were invented or assumed without
being found in the bundle files at the cited source:line.

---

## Answer

**Culprit: Andrin Caduff**  
**Confidence: 0.87**

### Why Caduff

| Evidence | Source |
|---|---|
| Knew real staging paths (on Iris's list of 5) | `investigator_notebook.md:19` |
| Ran checkpoint sweep on theft night, VPN, ~22:00 CEST | `interviews/interview_03_andrin_caduff.txt:27` |
| Admitted knowing audit logging was off | `interviews/interview_03_andrin_caduff.txt:29` |
| Research line closed; role ending Aug 2026 | `investigator_notebook.md:51` |
| No car; alone at home; no independent alibi | `interviews/interview_03_andrin_caduff.txt:25` |
| 31 checkpoint accesses in 4 weeks (median 2) | `investigator_notebook.md:51` |

### Why not Chiara Bernasconi (misleading suspect 1)

Describes the snapshot deletion and restart in her interview — but she
filed Jira ticket **DATA-1877** on **14 October** (four days before the
investigator engaged) after observing the scratch-02 capacity graph herself.
The "withheld detail" was in her own ticket. She was also in Winterthur all
night: restaurant 23:04 CEST → friend's flat → fuel 06:15 → motorway 07:32.

### Why not Noemi Rochat (misleading suspect 2)

Describes the failure and restart with startling specificity. Innocent
because her office (2F-4) shares a **non-insulated partition wall** with
the investigator's room (2F-3) — facility ticket FAC-330 states "speech
at normal conversational volume is intelligible through it." The investigator
called forensic examiner Emory Bakalian on **speaker phone** in that room
at 18:30 on Thursday 20 November, reviewing all forensic findings. Noemi's
interview was the following morning at 12:03.

---

## Bonus — How to prevent a repeat

See `bonus_prevention.md` in this folder.

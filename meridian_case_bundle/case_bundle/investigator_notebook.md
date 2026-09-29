# Notebook · N. Arslan · Halcyon engagement
*Working notes. Typed up from handwritten pages each evening. Not a report.*

---

## Fri 14.11.2025

- Engaged by W. Pryce (board) by phone, 08:10. Conditions: fast, discreet, not the police. Kestrel preprint went up Tue 11.11.
- Met the four people Halcyon has cleared to know why I'm here: Dov Halperin (CEO), W. Pryce, June Okada (office manager, logistics only), Dessie Moran (finance, for records access).
- June gave me a room on the second floor. Small, no window. She mentioned a ticket about the wall. Didn't follow up.
- Background, as told to me by Dov:
  - MERIDIAN: materials model, proposals work ~1 in 9 in the lab vs ~1 in 400 industry. The company rests on it.
  - Weights, training corpus and probably the recipe are out. Proof: Kestrel's model generated one of the 20 impossible phases Iris seeded into the training data in 2023 (watermark).
  - Migration weekend (autumn holidays, office closed Mon 13.10). Audit collector stopped on purpose, **Fri 10.10 21:00 → Sat 11.10 06:00**, ticket INFRA-2291. SIEM cold tier pointed at the same backend, so no copy. ~40 people knew the window (ticket, #eng-infra, standup).
  - Iris's decoy programme: 11 fake checkpoint bundles, more attractive than the real ones, beacon on open. None opened. The real ones were taken. → whoever did this knew which were real.

## Sat 15.11.2025

- Who could know which artifacts were real:
  - Iris's list of 5 (Iris, Dov, Lukas, Andrin, Yannick). Dov was in Tel Aviv 8–16.10 (mother's 80th, 40+ guests, photographer). Out.
  - Board pack, Feb: Iris briefed the decoy programme, 4 slides, one of them the real/decoy mapping by path. **Distribution list: get it from the email, not from memory.**
  - Confluence page "Storage Integrity Controls (WIP)", written by Yannick in March, permissioned to eng-all. Page analytics: 16 views, 9 distinct accounts.
- Crossed with: could find the real staging path, and within reach of St. Gallen that weekend → 8 names:
  Renata Vogel, Lukas Hofer, Iris Ammann, Andrin Caduff, Yannick Favre, Chiara Bernasconi, Noemi Rochat, Kurt Steiner.

## Sun 16.11.2025 · what survived

- Audit logs: none (by design). SIEM: none.
- Badge readers (landlord system): street entrance + lift lobby only. 11 entries over the 4 days, 9 of them the cleaning contractor. Alley freight door propped most of Saturday for a catering delivery to the ground-floor tenant. Badge record worth nothing.
- Cameras on the engineering floor: none. Refused by the board twice (Iris asked).
- The one thing that kept its own records: **scratch-02**, the fast non-redundant array used for bulk copies. Not part of the migration, never wired to the audit pipeline. Image sent to E. Bakalian (Winterthur) for analysis.

## Mon 17.11.2025

- 14:00 debrief with Emory at his office in Winterthur. His written summary is attached (forensic_summary_bakalian.pdf). He works in UTC. Converted:
  - copy job onto an attached external device started **23:10 Fri**, ran ~3h, **failed partway** (~40%), target full: bundles decompress on write;
  - **02:41 Sat**: old snapshot deleted on the destination to make room (~9 TB free-space jump);
  - job **restarted from the beginning**, completed **05:52 Sat**, eight minutes before logging came back.
- **WITHHOLD ALL OF IT.** Failure, snapshot, restart, the hours. Nobody at Halcyon hears any of it before the interviews. Emory has agreed. Dov gets told after all eight are done, Friday 21.11 evening. Board the week after.

## Tue 18.11.2025 · prep

- Interviews off-site (Rosenbergstrasse), two days, 90 min apart, booked by June as "process interviews related to the migration". Nobody told why.
  - Thu 20.11: Vogel 09:00 · Hofer 10:30 · Caduff 12:00 · Ammann 13:30
  - Fri 21.11: Favre 09:00 · Bernasconi 10:30 · Rochat 12:00 · Steiner 13:30
- Each asked not to discuss. Different exit route. Nobody is told the forensic findings.
- Suspect sheets (what I know going in), alphabetical:
  - **Ammann** (Head of Security): designed decoys and watermarks, signed off INFRA-2291. ~CHF 210k personal debt.
  - **Bernasconi** (Director Data Eng): owns the corpus pipelines. Internal review of ~CHF 41k expenses open since late September.
  - **Caduff** (Principal Research Eng): research line closed in the September replan, role ends August. 31 checkpoint accesses in 4 weeks, median 2.
  - **Favre** (Infra Eng): built the scratch arrays; wrote the Confluence page. Says he was away.
  - **Hofer** (VP Eng): built the pipeline. Passed over for CTO in August (board decision). In the building Saturday afternoon (incident).
  - **Rochat** (Head of Product): leaving in spring to start a company ("orthogonal"). Read the Confluence page once.
  - **Steiner** (Chief Scientist, co-founder): admin accounts nobody reviewed, passwords in a notebook. In the building on the Sunday.
  - **Vogel** (Chief of Staff): ran the Kestrel acquisition process Feb–Jun, day-to-day counterpart for 120 days. Not technical, says so often.

## Thu 20.11.2025 / Fri 21.11.2025 · interviews

- Transcripts from TranscribeDesk in the interviews folder. Not proofread; speaker labels unreliable.
- Short notes after each:
  - Ammann: folder with finances and boarding passes. Lisbon.
  - Bernasconi: volunteered DATA-1877 before I asked anything.
  - Caduff: very direct. The paper. No car.
  - Favre: volunteered the Confluence page and the moonlighting, unprompted.
  - Hofer: angry, then precise. Architecture explained well. Friday evening: "a dog".
  - Rochat: theories. Was in the building Friday until ~22:30 by her own account.
  - Steiner: charming, no times for anything.
  - Vogel: helpful, long on the data room and Kestrel. Mentioned the May approach from Aubert herself.
- Thu 20.11, 18:30: back in my room (2F-3). Called Emory on speaker to go through the day against his findings. Forty minutes.
- Dov briefed 19:30 Friday after the last interview.

## Mon 24.11.2025 → Fri 28.11.2025 · follow-ups

- Lukas confirms Andrin's retrospective access (follow-up 01). Never put in writing.
- Iris's folder: care home, cancelled policy, litigation with a Zurich firm, statements. Every franc accounted for. Lisbon: flights, hotel, photographer's timestamped raw files. Verified.
- CTO decision: board-driven, Dov resisted for six weeks and lost (per W. Pryce).
- Kestrel: found the May thread (Aubert → Vogel, "continuing role"), forwarded to Dov within the hour. Reads clean.
- Access: the data room service accounts were never revoked (SEC-419). One export role broader than intended since April.
- The other ~40 who knew the window: none knew which bundles were real. Two in the building that weekend: cleaning supervisor; Priya Raghunathan (Sunday backfill, 4 h, nothing else).
- June follow-up (02). Asked June for the parking permit list and the landlord's garage barrier log. Asked Dessie for card-feed data behind Q4 claims.
- Received: permit list (26.11), card feed (27.11). Garage log from the landlord arrived Mon 01.12. Not yet gone through.

## Tue 02.12.2025 · handover

- Met Dov and W. Pryce. I have eight interviews, follow-ups, and everything the company could export: chat, tickets, calendars, email, expenses, card feed, the diligence log, facilities, the garage log, the permit list. Not summaries. As received.
- I can't hold all of it in my head at once and see the one line in one system that changes the meaning of one line in an interview. Asked for technical specialists.
- Handing over everything exactly as received. No name until it can be pointed to on a page.

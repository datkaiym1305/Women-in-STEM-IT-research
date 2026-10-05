# Women in STEM/IT in Kyrgyzstan – reproducible analysis package

## Contents
| Path | What it is |
|---|---|
| `analysis.py` | The whole analysis: cleaning → codebook → tests → tables → figures |
| `data/survey_clean_anonymized.xlsx` | Cleaned data (sheet `data`), `codebook`, and `free_text_REVIEW_NAMES` |
| `data/specialty_coding.csv` | STEM / non-STEM coding of each respondent's specialty. **Edit `manual_code` (1/0) and re-run** |
| `results/results_tables.xlsx` | 16 result sheets + a README sheet explaining every test |
| `results/run_log.txt` | Row counts, parsing notes, software versions |
| `figures/fig1…fig7.png` | Charts (English labels; edit the label dictionaries in the script to translate) |

## How to reproduce
```
pip install -r requirements.txt
python analysis.py path/to/raw_google_forms_export.xlsx .
```
The raw export is **not** included because its last column contains Telegram/WhatsApp contacts. Keep it out of anything you share.

## Before you use any number – 5 checks
1. **Likert anchors.** The script assumes 1 = strongly disagree … 5 = strongly agree. Confirm in your Google Form (also what 1–5 mean for family finances and religiosity).
2. **STEM coding.** Open `data/specialty_coding.csv`, review rows with `needs_review = 1`, fill `manual_code`, re-run. All RQ1 "STEM field" results depend on it.
3. **Free text.** Sheet `free_text_REVIEW_NAMES` may contain names of real people. Remove or replace them before quoting or sharing.
4. **"Top-3" question.** 15 respondents ticked more than 3 measures. They are kept as given; state this in Methods or restrict to ≤3 as a sensitivity check.
5. **Minors.** 13 respondents are under 18. Confirm your consent/ethics arrangements (see AAPOR code: https://aapor.org/standards-and-ethics).

## Methods used (with sources)
- Likert items treated as ordinal: medians, percentages, Mann–Whitney, Spearman (Sullivan & Artino 2013, https://pmc.ncbi.nlm.nih.gov/articles/PMC3886444).
- Small counts → Fisher's exact test instead of chi-square (https://www.r-bloggers.com/2020/01/fishers-exact-test-in-r-independence-test-for-a-small-sample/amp/).
- 39 tests in sheet 5 → Holm adjustment reported next to raw p-values (Holm 1979; implemented in `holm()`).
- Cronbach's alpha for candidate scales (Tavakol & Dennick 2011, https://pmc.ncbi.nlm.nih.gov/articles/PMC4205511).
- Open-ended answers: reflexive thematic analysis (Braun & Clarke 2006) – not automated here; do it manually.
- Report structure: IMRaD (https://libguides.umn.edu/StructureResearchPaper).

## Limits you must state in the paper
Non-random, self-selected sample (n = 61); small subgroups (15 IT/STEM workers, 10 with a role model, 18 with a mentor); retrospective self-report; some items answered by schoolgirls and adults alike; associations only, and some may run in reverse (e.g. olympiad participation → "teachers suggested olympiads"). Perceived effectiveness of interventions (RQ3) is opinion, not evidence of effect – use the literature for that.

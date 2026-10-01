 Online Learning Engagement and Academic Performance

> **Learning analytics research proposal — Version 0.1**
>
> This document describes a proposed dataset. No data have been collected, and no findings or ethics approvals are claimed. All procedures and sample sizes below are planned.

## Overview

This study will examine how participation in an online undergraduate course relates to final exam performance. Learning management system (LMS) activity will be combined with baseline knowledge and final exam scores to explore engagement patterns that could inform teaching support.

**Research question:** How are active learning days, resource viewing, discussion participation, and timely assignment submission associated with final exam scores after accounting for baseline knowledge?

**Hypothesis:** More consistent participation and a higher on-time submission rate will be associated with higher final exam scores. This observational study will assess associations, not establish causation.

## Contents

- [Study metadata](#study-metadata)
- [Metadata standard](#metadata-standard)
- [Collection plan](#collection-plan)
- [Dataset structure](#dataset-structure)
- [Data dictionary](#data-dictionary)
- [Data preparation and quality](#data-preparation-and-quality)
- [Analysis and limitations](#analysis-and-limitations)
- [Ethics and access](#ethics-and-access)
- [Citation](#citation)
- [Assignment reflection](#assignment-reflection)

## Study metadata

| Field | Description |
|---|---|
| Title | Online Learning Engagement and Academic Performance |
| Researcher | [haoquan wang] |
| Institution | Columbia University, New York, New York, US |
| Contact | [hw3162@tc.columbia.edu] |
| ORCID | https://orcid.org/0009-0002-5783-3655 |
| Subject | Education; learning analytics; online learning |
| Keywords | LMS, student engagement, academic performance, higher education |
| Design | Observational study of one course cohort |
| Population | Students aged 18 or older enrolled in one selected online undergraduate course |
| Planned sample | Approximately 100 consenting students; actual participation may differ |
| Collection period | One 12-week teaching period; exact dates to be confirmed |
| Unit of analysis | One student in one course |
| Language | English |
| File format | CSV, UTF-8 encoding, comma-separated, with a header row |
| Version | 0.1 — proposal |
| Updated | 2026-09-28 |

## Sample data

This project is currently at the proposal stage. The five synthetic records below illustrate the planned dataset structure. They do not represent real students or research findings. The planned sample is approximately 100 consenting students, and the observation period is 12 weeks (84 days).

Each row represents one student in one course. Student identifiers are fictional research codes.

| student_id | baseline_score | active_days | resource_views | discussion_posts | assignments_due | on_time_submissions | on_time_rate | final_exam_score |
|---|---|---|---|---|---|---|---|---|
| S0001 | 65.00 | 52 | 180 | 14 | 10 | 9 | 90.00 | 82.00 |
| S0002 | 78.00 | 38 | 125 | 8 | 10 | 8 | 80.00 | 85.00 |
| S0003 | 54.00 | 61 | 240 | 20 | 10 | 10 | 100.00 | 76.00 |
| S0004 | 72.00 | 27 | 88 | 0 | 10 | 6 | 60.00 | 79.00 |
| S0005 | NA | 45 | 156 | 11 | 8 | 7 | 87.50 | NA |

### Interpretation

- Assessment scores and submission rates are percentages ranging from 0 to 100.
- `active_days` counts distinct days with qualifying LMS activity and cannot exceed 84.
- `resource_views` and `discussion_posts` count activity during the observation period.
- `assignments_due` excludes optional or waived assignments, so the number may vary between students.
- `on_time_rate` is calculated as `100 × on_time_submissions / assignments_due`.
- `NA` indicates missing or unavailable information. A zero indicates an observed value of zero.
- For S0005, seven on-time submissions out of eight required assignments produce an on-time rate of 87.50%.

These examples demonstrate the proposed format and calculation rules only. No conclusions about student learning or academic performance should be drawn from these synthetic records.
## Metadata standard

**Selected standard: Data Documentation Initiative — DDI-Codebook (DDI-C).**

DDI-Codebook supports descriptions of individual datasets, including their purpose, provenance, collection methods, files, variables, and access conditions. It suits this educational study because readers need both study context and precise definitions of student-level measures. See the [DDI-Codebook overview](https://ddialliance.org/ddi-codebook).

This README organizes human-readable metadata using DDI-Codebook concepts. It is not a schema-validated DDI XML file and does not claim formal DDI conformance.

| Documentation area | README coverage |
|---|---|
| Study description | Overview, metadata, and collection plan |
| File description | Dataset structure and file format |
| Variable description | Data dictionary, units, codes, and derivations |
| Processing and provenance | Data preparation and quality |
| Access and use | Ethics, access, and citation |

## Collection plan

1. Obtain institutional permissions and required ethics review before recruitment or access to student records.
2. Invite eligible students in one course to participate voluntarily. Participation will not affect grades.
3. Administer a baseline knowledge assessment before teaching begins.
4. Obtain authorized LMS activity and assignment exports for the teaching period and retrieve final exam scores after grading.
5. Replace institutional identifiers with random research identifiers and link records in a restricted environment.
6. Produce one summary row per consenting student. Retain records with missing outcomes in the documented dataset and disclose exclusions for each analysis.

The study will use a convenience sample. The observation window will cover 84 consecutive days from the official course start. Exact timestamps and the course timezone must be recorded before extraction. Activity outside this window will be excluded; final exam grades may be retrieved later.

## Dataset structure

Each row in the planned `student_engagement.csv` will represent one student. The unique key will be `student_id`. The dataset has not yet been created.

| File | Status | Purpose |
|---|---|---|
| `README.md` | Available | Proposal metadata and data dictionary |
| `student_engagement.csv` | Planned; restricted | Student-level engagement and assessment data |
| `processing_log.md` | Planned | Sources, extraction dates, transformations, and exclusions |

Raw logs, consent records, and the identifier linkage file will be held separately under restricted access and will not be uploaded to GitHub.

## Data dictionary

These are proposed columns, to be checked against the selected LMS before collection. Following [OSF guidance](https://help.osf.io/article/217-how-to-make-a-data-dictionary), the dictionary includes exact names, readable labels, units, allowed values, and definitions.

| Variable | Readable label | Type | Unit / allowed values | Definition and source | Missing rule |
|---|---|---|---|---|---|
| `student_id` | Research student identifier | String | Unique code, e.g., `S0001` | Random identifier assigned during preparation; not an institutional student number | Required |
| `baseline_score` | Baseline knowledge score | Decimal | Percent, 0–100 | Pre-course assessment points earned / possible points × 100 | `NA` if unavailable |
| `active_days` | Days with LMS activity | Integer | Days, 0–84 | Distinct course-local dates with a resource view, discussion contribution, or assignment submission | `NA` if logging coverage is incomplete |
| `resource_views` | Course resource views | Integer | Events, 0 or greater | Recorded views of course pages or learning files during the window; repeat views count after duplicate export records are removed | `NA` if unavailable or incompletely logged |
| `discussion_posts` | Discussion contributions | Integer | Posts, 0 or greater | New discussion threads and replies authored during the window | `NA` if unavailable or incompletely logged |
| `assignments_due` | Required assignments due | Integer | Assignments, 0 or greater | Required assignments with a student-specific deadline inside the window; excludes optional and waived work | `NA` if requirements are unknown |
| `on_time_submissions` | Assignments submitted on time | Integer | Assignments, 0–`assignments_due` | Required assignments first validly submitted by the applicable deadline, including approved extensions; maximum one count per assignment | `NA` if deadlines or records are incomplete |
| `on_time_rate` | On-time submission rate | Decimal | Percent, 0–100 | `100 * on_time_submissions / assignments_due` | `NA` if denominator is zero or either input is missing |
| `final_exam_score` | Final exam score | Decimal | Percent, 0–100 | Official final exam points earned / possible points × 100 | `NA` for absence or unavailable score; zero only for an actual recorded zero |

**Conventions:** `NA` means unavailable or undefined. Zero means an observed zero, never missing data. Numeric values will not contain percent symbols. Derived percentages will be calculated without intermediate rounding and stored to two decimal places. Records with missing identifiers will be held for investigation.

## Data preparation and quality

- Record export sources, extraction times, observation timestamps, timezone, and source column mappings.
- Remove duplicate exported events using stable event IDs when available. If absent, document and review an alternative matching rule before deleting duplicates.
- Filter to consenting students, the selected course, and the observation window.
- Aggregate by research identifier and join assessments using the restricted linkage file. Investigate unmatched records.
- Check unique student identifiers, numeric types, allowed ranges, and missing values.
- Verify that on-time submissions do not exceed assignments due and recalculate submission rates from their inputs.
- Check logging coverage before interpreting absent activity as zero. Mark uncertain coverage as missing.
- Retain legitimate extreme values; record corrections of verified errors in the processing log.
- Report actual row counts, missingness, and exclusions after collection. No quality-check results are available yet.

## Analysis and limitations

Planned analysis includes descriptive summaries, missing-data summaries, scatterplots, and multiple linear regression. Final exam score will be the outcome; baseline score, active days, resource views, discussion posts, and on-time rate will be candidate predictors. The counts used to derive on-time rate will not also enter the same model as interchangeable predictors.

Model assumptions and overlap among engagement measures will be assessed. Model complexity will depend on the available sample. Complete-case analysis may be used if missingness is limited and defensible; any alternative approach will be documented. Results will include effect estimates and uncertainty.

LMS activity is an imperfect indicator of learning: students may study offline, and repeated views may reflect difficulty. Motivation and other unmeasured factors may affect both engagement and grades. A single-course convenience sample limits generalization. No causal claims or findings are available at the proposal stage.

## Ethics and access

**Current availability:** Documentation only. No research data are available.

Educational records require careful handling. Research identifiers provide pseudonymization, not guaranteed anonymity. Direct identifiers and linkage keys will be separated from analytical data, with access limited to authorized researchers.

Consent, withdrawal procedures, storage safeguards, retention periods, and sharing conditions will be finalized through institutional review. Approval has not yet been obtained. Student-level records will not be published on GitHub. Any future public release will require appropriate authorization and disclosure review.

**License:** No data license has been assigned. The author will select a documentation license before publication. Public visibility alone does not establish permission to reuse student records.


## Assignment reflection

### Which metadata standard did you choose and why?

DDI-Codebook was selected because the study needs descriptions of its purpose, collection methods, dataset structure, variables, and access restrictions. Its study-level and variable-level concepts provide a useful framework for understanding and reusing educational research data. This README is informed by those concepts rather than being a formal DDI XML implementation.

### Which template or software did you use?

This draft was prepared with VS code assistance from OpenAI Codex in Markdown. Its organization draws on [Make a README](https://www.makeareadme.com/), with a research-specific dictionary informed by [OSF guidance](https://help.osf.io/article/217-how-to-make-a-data-dictionary). GitHub is the intended publishing platform.


### What was the most challenging part, and how did you overcome it?

[Complete this paragraph after editing so it reflects your actual experience. Possible topics include defining engagement consistently, distinguishing missing values from zeros, formatting the dictionary, or distinguishing planned procedures from completed work. Describe the specific difficulty, what you did, and what improved.]

## References

- [DDI Alliance: DDI-Codebook](https://ddialliance.org/ddi-codebook)
- [OSF: How to Make a Data Dictionary](https://help.osf.io/article/217-how-to-make-a-data-dictionary)
- [Make a README](https://www.makeareadme.com/)
- [ORCID registration](https://orcid.org/register)

## Version history

| Version | Date | Change |
|---|---|---|
| 0.1 | 2026-09-28 | Initial proposal documentation; no data collected |

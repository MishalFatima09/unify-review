# UNIFY Case Review: annotation site for external reviewers

A static page for industry engineers to label the 15 pilot cases blind. Nothing to install: all the code is embedded in the page, and progress is saved in the reviewer's browser. When they finish, they download a CSV and send it to you.

## Try it now
Unzip and double-click `index.html`. It works offline (fonts fall back to system fonts).

## Put it on GitHub Pages (about 5 minutes)
GitHub Pages needs a **public** repo on a free account, so use a new repo, not the team repo.

1. On GitHub: **New repository** → name it e.g. `unify-review` → **Public** → Create.
2. **Add file → Upload files** → drag in `index.html` and `cases.js` → Commit.
3. **Settings → Pages** → Source: *Deploy from a branch* → Branch: `main`, folder `/ (root)` → Save.
4. After a minute the link appears at the top of that page: `https://<your-username>.github.io/unify-review/`. Send that link to reviewers.

The repo contains only code from three MIT-licensed open-source projects plus the case descriptions. It does **not** contain the answer key, case origins or anyone's labels. Never upload `docs/dataset/_constructor_only/` or the annotation sheets.

## What reviewers send back
A file named `unify_annotations_<name>_<date>.csv`, in the same format as `docs/dataset/05_raw_annotations/`, plus three extra columns: role, years of experience and `annotator_type=external`.

1. Save each one as `docs/dataset/05_raw_annotations/external_<initials>.csv`.
2. Compare any two reviewers:
   ```
   python docs/dataset/tools/agreement.py docs/dataset/05_raw_annotations/external_ab.csv docs/dataset/05_raw_annotations/external_cd.csv
   ```
3. Report the external round **separately** from the internal pilot (Abdullah and Haaniah).

## Regenerating `cases.js`
Only if the cases change: `python tools/build_data.py <dataset_dir> <case_trees_dir> cases.js`. The script refuses to write the file if any label or origin wording leaks into it.

## Notes for the report
- The site shows the same evidence as the case packets: criterion, diff (base → evaluated head), test results, candidate snippets and events. It doesn't link to the GitHub commit for cases with a head patch, because that commit shows different code from what's being judged.
- The guide condenses annotation manual v1, including rules R1 and R2, into four rules. Record the manual version as `v1-web`.
- Time per case is measured automatically while the tab is visible.

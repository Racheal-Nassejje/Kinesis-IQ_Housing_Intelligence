# Kinesis-IQ Housing Intelligence (Pod 4)

Projects 7 and 8: Landlord Asset Management and Displacement Tactics; Renter and Buyer Stock Transition.

## What this project does

We combine City of Toronto open data (Landlord and Tenant Board eviction cases, 311 complaints, building permits and short-term rental registrations) and group the records by ward. We turn them into rates per 1,000 addresses so wards of different sizes can be compared. We test whether complaints and permits help predict the next month's eviction rate, and whether a simple early warning flag would have caught rising pressure in June and July. Hits and misses are reported, and the limits are stated.

## Repository contents

| File | Purpose |
|------|---------|
| `Project-Description.md` | Project overview, data sources, privacy rules, and team |
| `MEASURES.md` | Abstract measure definitions (M1 to M15) |
| `.gitignore` | Stops secrets and raw data from being pushed |
| `pod4_housing_analysis.ipynb` | Analysis notebook (to be added after group agreement) |
| `etl/` | Loading scripts for the events database (to be added) |

## Data sources

| Source | Shared in this repo? | Notes |
|--------|----------------------|-------|
| 311 complaints | Yes, once loaded | Ward recorded for most requests; 13 have "Unknown ward" |
| Building permits (2026) | Yes, once loaded | Filtered to applications filed in 2026 |
| Short-term rental registrations | Yes, once loaded | Single snapshot, no date or status column |
| Landlord and Tenant Board cases | Masked version only | Raw file stays private; names and unit numbers removed after group agreement |
| Address points | Not committed | Downloaded from the open data portal |

## Privacy rules

- The raw LTB file is never committed or shared.
- The database password and keys stay in a local `.env` file, which is ignored by Git.
- Only masked files go into the repo, and only after the group agrees.
- Personal email addresses are not written in the repo.

## Limits

- PDF text extraction and named-entity recognition (NER) on LTB PDFs are not done.
- Address points stand in for homes, so rates are per 1,000 addresses, not per household.
- The short-term rental list has no status column, so it may include operators who are no longer approved.
- The Spadina-Fort York operator count (2,101) is derived as the City total minus the other 24 wards.

## Team

| Team member |
| --- |
| Racheal Nassejje (coordinator) |
| Abdimalik Ali Ahmed |
| Benjamin Tutua Samuel |
| Arinda Deogracious |
| Kandolo Rabbi Raphael |
| Baboucarr A Bobb |

## How to run

1. Open the shared data folder: [Pod 4 Share](https://drive.google.com/drive/folders/1-QtNbyyQFh04hf6fxEVVXr1ghXZ-wcyD?usp=sharing). Add it to your Drive with "Add shortcut to Drive", then open `pod4_housing_analysis.ipynb` from the folder in Colab.

1. Open `pod4_housing_analysis.ipynb` in Google Colab from the Pod 4 Share folder (Add shortcut to Drive first, so the files stay current).
2. Run the cell that connects Google Drive (`drive.mount`) and approve the sign-in.
3. Run the cells from the top to the bottom, skipping any cell marked "COORDINATOR ONLY". Those cells connect to the database and are not needed to reproduce the results.
4. The eviction data comes from `ltb_counts_by_ward_month.csv` in the DATASETS folder. It holds ward, month, order type and counts only.
5. If a path error appears, check that the Pod 4 Share folder is in your My Drive under the same name.



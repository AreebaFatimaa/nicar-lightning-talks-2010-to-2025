## NICAR Lightning Talks (2010-2025)

I was inspired by Christine Zhang's compilation of all the NICAR lightning talks till 2019:

https://source.opennews.org/articles/nine-years-nicar-lightning-talks-and-cats/

And decided to follow up on her work.

The dataset used for this project is curated by hand. I found archived links announcing the talks in 2019, 2020, and 2021. I added the names of the speakers, their gender, and other details by searching for them manually and checking out their LinkedIn profiles. Then I classified each talk manually to fit into themes.

---

## Project structure

```
lightningtalks_clean.csv   — Source dataset (161 talks, hand-labeled themes)
data_processing.ipynb      — Jupyter notebook that maps themes and exports CSVs
index.html                 — Scrollytelling webpage with D3.js visualization
cover.png                  — Cover image for the webpage
output/                    — All generated CSV files
  themes_summary.csv       — Pivot table (year x 15 theme categories)
  gender_by_year.csv       — M/F counts per year
  all_talks_classified.csv — Full dataset with mapped category column
  theme_trends_analysis.txt— Written analysis of trends over the years
  [15 per-theme CSVs]      — One CSV per theme (year, count) for Datawrapper
```
---

## Step-by-step process

### 1. Data collection
- Compiled all NICAR lightning talks from 2018-2025 by hand, and used Christine Zhang's dataset for the ones before it
- Sources: IRE archived schedules, speaker LinkedIn profiles
- Recorded: year, title, speaker, org, gender (M/F), location, international status, description of the talk
- Saved as `lightningtalks_clean.csv` (161 rows)

### 2. Theme labeling
- Manually assigned a theme tag to every talk based on its title and description
- Resulted in 70+ granular labels (e.g. "Python", "FOIA", "Satire, Storytime", "Data Viz")
- Some talks had comma-separated multi-tags
- Storytime: This is where data journalists shared stories about their personal experiences. Marraiges, drinking habits, stories which were killed, and those which survived. 

### 3. Theme mapping (data_processing.ipynb)
- Defined 15 broad theme categories:
  1. AI & Machine Learning
  2. Accessibility & Design
  3. Climate & Environment
  4. Data Analysis & Statistics
  5. Data Habits
  6. Data Visualization & Charts
  7. Elections & Politics
  8. FOIA & Public Records
  9. Humor & Satire
  10. Investigations & Accountability
  11. Mapping & Geospatial
  12. Newsroom Culture & Career
  13. Programming & Tools
  14. Scraping & Data Collection
  15. Storytime

## 4. For the ScrollyTelling bit, I got my friend Claude Code to help me out! 
- Built a dictionary (`THEME_MAP`) mapping every raw theme string to one of these 15 categories
- For comma-separated themes, used the primary/first tag to decide the category
- Applied the mapping with `df['theme'].map(THEME_MAP)`
- Built a scroll-driven D3.js visualization embedded in the article
- Step 0: All 161 talks shown as colored circles grouped by theme
- Steps 1-4: Highlights specific themes while dimming others (Programming, Data Viz, Newsroom Culture, FOIA/Storytime)
- Step 5: Circles animate into year-based columns showing distribution over time
- Includes a Datawrapper iframe for the gender breakdown chart
- Sticky chart stays in view while narrative text cards scroll over it

### 5. CSV export (data_processing.ipynb)
- Generated one CSV per theme with columns `year, count` 
- Generated `themes_summary.csv` — a pivot table with all 15 themes as columns
- Generated `gender_by_year.csv` — M/F counts per year
- All files saved to the `output/` folder, ready for Datawrapper import, in case you want to create your own visualizations

### 6. Trend analysis for traditions over the years
  - Programming & Tools dominated 2010-2012, then declined
  - Newsroom Culture & Career surged in 2018-2019
  - Storytime became the late-era staple (2020-2025)
  - FOIA surges in cycles correlated with less transparent administrations
  - AI adoption has been slow and cautious
  - Data Habits is the most consistent theme across all years

---

## Dependencies

- Python 3
- pandas
- Jupyter
- Black coffee

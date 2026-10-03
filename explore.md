# My Little Pony Transcript Exploration

## 1. How big is the dataset?
- Commands used:
  - `wc -l clean_dialog.csv`
  - `ls -lh clean_dialog.csv`
- Results:
  - Total line count: 36,860 lines (1 header line + 36,859 dialogue lines).
  - File size: 4.7 MB.

## 2. What's the structure of the data?
- Command: `head -n 2 clean_dialog.csv`
- The file has 4 columns:
  - `title`: episode name
  - `writer`: episode writer
  - `pony`: who is speaking the line
  - `dialog`: what they say

## How many episodes does it cover?
- Command: `csvtool col 1 clean_dialog.csv | tail -n +2 | sort -u | wc -l`
- It covers 197 unique episodes.

## Unexpected aspect of the dataset
- Command: `csvtool col 3 clean_dialog.csv | grep " and " | head -n 5`
- In the pony column, sometimes multiple ponies are listed as talking together
(like "Narrator and Twilight Sparkle" or "Twilight Sparkle and Rainbow Dash").
If you just grep for an individual pony name,
you'll miss these lines where they speak at the same time.

## Speaker frequency
- Total lines (all characters): `csvtool col 3 clean_dialog.csv | tail -n +2 | wc -l` → 36,859
- Per pony: `csvtool col 3 clean_dialog.csv | grep -x "Twilight Sparkle" | wc -l` (repeated for each pony)
- Percent: count / 36,859 × 100 (computed with awk)
- Results are in Line_percentages.csv

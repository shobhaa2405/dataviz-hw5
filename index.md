# Chicago Business License Data Visualizations

**Author:** Shobha Bhat  
**Course:** IS 445 - Data Visualization  
**Dataset:** Chicago Business Licenses (Fall 2022)

---

## Visualization 1: Top 15 Most Common License Types in Chicago

This horizontal bar chart shows the 15 most common business license types in Chicago. The data reveals a striking pattern: DETECTIVE BOARD licenses dominate with 4,867 licenses, followed by COSMO at 3,781, while the remaining categories are significantly smaller (DENTAL has 739, and most others have fewer than 100). This tells us that Chicago's licensing landscape is heavily concentrated in just two categories.

**Design Choices:**

I used quantitative encoding (`Count:Q`) on the x-axis because it makes the bar lengths directly comparable—longer bars mean more licenses. The y-axis uses nominal encoding (`License_Type:N`) sorted in descending order (`sort='-x'`), which puts the most important categories at the top where they're noticed first. I chose horizontal bars instead of vertical because many license names are long (like "FUNERAL AND EMBALMER"), and horizontal orientation lets them display without awkward rotation.

For color, I used the tableau20 scheme with nominal encoding (`License_Type:N`). I picked tableau20 because it provides 20 distinct colors designed for categorical data and is colorblind-friendly. Each license type gets its own color to help visually separate them, though the main comparison should still be bar length, not color—position is more accurate for quantitative comparisons than color.

**Data Transformations:**

I started with 10,000 license records and used Pandas' `value_counts()` to count how many times each license type appeared. This transformed the data from individual records to aggregated counts. Then I filtered to the top 15 using `.head(15)` because the full dataset has over 150 license types—showing all of them would be unreadable, and the top 15 captures 99% of the data anyway. Finally, I used `reset_index()` to convert the result into a clean DataFrame with 'License_Type' and 'Count' columns for Altair.

---

## Visualization 2: License Status Distribution by Type

This stacked bar chart displays how different license statuses are distributed across the top 10 license types. The visualization shows 13 status categories, with NOT RENEWED being the most common (6,331 licenses) and ACTIVE second (2,440). DETECTIVE BOARD and COSMO clearly show the highest volumes, and most types have large NOT RENEWED segments, suggesting many of these are historical licenses rather than currently active businesses.

**Design Choices:**

The x-axis uses nominal encoding (`License_Type:N`) with labels angled at 45 degrees to prevent overlap. The y-axis is quantitative (`count():Q`) with `stack='zero'`, which stacks the status segments vertically. I chose stacking over grouped bars because it shows both the total licenses per type (bar height) and the status breakdown (colored segments) simultaneously.

For color, I used the set2 scheme with nominal encoding (`License_Status:N`). I selected set2 specifically because my data has 13 status categories and set2 is designed to be colorblind-safe while maintaining good contrast between colors—important when segments sit next to each other in stacked bars. I avoided sequential color schemes (like blues) because license statuses are categorical, not ordered, and using a gradient would incorrectly suggest hierarchy.

The opacity changes with hover: `opacity=alt.condition(hover, alt.value(1.0), alt.value(0.7))`. When you hover over a bar, it becomes fully opaque while others dim to 70%, creating focus without hiding context.

**Data Transformations:**

I started with my 10,000-record dataset and filtered it to only the top 10 license types using `df_clean[license_col].isin(top_10_types)`, which gave me about 9,916 records (99% of the data). I kept the data at the individual license level rather than pre-aggregating it because Altair needs the granular data to create the stacked bars correctly—it automatically groups by both License Type and Status, counts the combinations, and stacks them. This approach also ensures the interactivity works properly.

---

## Interactivity Discussion

I implemented hover-based highlighting on the stacked bar chart because it has way more complexity than the first chart (10 types × 13 statuses = lots of information). The hover does two things: it highlights the selected bar at full opacity while dimming others to 70%, and it displays tooltips with the exact license type, status, and count.

This interactivity helps in several ways. First, the opacity change lets you focus on one license type at a time without being distracted by the others, but you can still see them dimmed in the background for comparison. Second, the tooltips solve the problem of reading exact values from stacked bars—it's really hard to estimate thin segments accurately, so having exact numbers on demand is crucial. Third, you can quickly explore patterns by moving your mouse across the bars and watching the values update, which helped me notice that NOT RENEWED status dominates almost every license type.

I chose hover instead of clicks or dropdowns because it requires minimal effort and feels natural. Hover is just mouse movement, whereas clicks require selecting/deselecting and dropdowns completely hide unselected data. This way you get details on demand while keeping the full context visible.

---

## Data Sources & Analysis

- **[The Data](https://raw.githubusercontent.com/shobhaa2405/dataviz-hw5/main/data/licenses_fall2022.csv)** - Chicago Business License Dataset
- **[The Analysis](https://github.com/shobhaa2405/dataviz-hw5/blob/main/workbook.ipynb)** - Python notebook with all code

**Dataset Stats:**
- 10,000 licenses analyzed
- 157 unique license types
- 13 status categories
- DETECTIVE BOARD: 4,867 (48.7%)
- COSMO: 3,781 (37.8%)
- NOT RENEWED: 6,331 (63.3%)

---

<iframe src="chart1.html" width="100%" height="600" frameborder="0"></iframe>

---

<iframe src="chart2.html" width="100%" height="600" frameborder="0"></iframe>

---

## About This Project

Created for IS 445 - Data Visualization using Python, Pandas, and Altair. The visualizations render client-side using Vega-Lite and are hosted on GitHub Pages.

---

*Shobha Bhat | November 2025 | IS 445 Data Visualization | UIUC*

# Chicago Business License Data Visualizations

**Author:** Shobha Bhat  
**Course:** IS 445 - Data Visualization  
**Dataset:** Chicago Business Licenses (Fall 2022)

---

## Visualization 1: Top 15 Most Common License Types in Chicago

This horizontal bar chart displays the 15 most frequently issued business license types from Chicago's business license dataset, revealing the dominant categories of commercial activity in the city. The visualization shows that DETECTIVE BOARD licenses are by far the most common, with over 5,200 licenses, followed by COSMO licenses with approximately 4,000, while other categories like DENTAL, FUNERAL AND EMBALMER, and various professional services have significantly smaller counts.

**Design Choices:**

For the encoding types, I used quantitative encoding (count:Q) on the x-axis to represent the number of licenses, which makes magnitude comparisons straightforward and intuitive. The y-axis employs nominal encoding (License_Type:N) sorted in descending order by count, positioning the most significant categories at the top where they receive immediate visual attention. I implemented color encoding using the 'tableau20' color scheme with nominal type (License_Type:N), which provides 20 distinct, perceptually uniform colors that are effective for categorical data and maintain accessibility for colorblind viewers. Each license type receives a unique color to aid in visual distinction, though the primary comparison mechanism is bar length rather than color. The horizontal bar orientation was specifically chosen because it accommodates the long license type names without truncation or awkward rotation, allows natural left-to-right reading of quantitative values, and makes height-based comparisons more intuitive than vertical bars would for this many categories.

**Data Transformations:**

In the Python analysis, I performed several data transformations to prepare this visualization. First, I removed all rows where the license type field contained null values to ensure data quality. Then, I used Pandas' `value_counts()` function to aggregate the individual license records by counting occurrences of each unique license type, transforming approximately 48,000 individual license records into frequency counts. I filtered this aggregated data to retain only the top 15 license types using `.head(15)`, which represents the most significant categories while preventing visual clutter from the 150+ rare license types in the full dataset. This filtering was essential because displaying all license types would create an unreadably dense visualization, whereas the top 15 captures the major patterns in Chicago's business licensing landscape. Finally, I reset the index and renamed columns to create a clean dataframe suitable for Altair, with explicit 'License_Type' and 'Count' columns that map directly to the visualization's encodings.

<iframe src="chart1.html" width="100%" height="650" frameborder="0"></iframe>

---

## Visualization 2: License Status Distribution by Type

This stacked bar chart visualizes the distribution of license statuses (Active, Cancelled, Expired, Inactive, and various termination categories) across the top 10 most common business license types in Chicago. The visualization reveals important patterns in license compliance and renewal behavior: DETECTIVE BOARD and COSMO licenses show the highest total volumes with predominantly active licenses (shown in teal), while DETECTIVE BOARD notably has a substantial proportion of "CHANGE OF OWNERSHIP" status (shown in purple). The stacked format allows viewers to see both the composition of statuses within each license type and the total volume of licenses per type, making it easy to identify which business categories have better compliance rates.

**Design Choices:**

The x-axis uses nominal encoding (License_Type:N) with angled labels to accommodate the longer license type names while maintaining readability. The y-axis employs quantitative encoding (count:Q) representing the number of licenses, with bars stacked using `stack='zero'` to show cumulative totals while preserving the ability to see individual status contributions. For color encoding, I used nominal type (License_Status:N) with the 'set2' color scheme, which provides 8-12 distinct, colorblind-safe colors appropriate for the 12 different license statuses present in the data. This color scheme was specifically chosen because it maintains good perceptual distance between adjacent colors, making it easier to distinguish the different status categories even when they appear as thin layers in the stacked bars. The choice of stacked bars rather than grouped bars was deliberate: stacking reveals both the total licensing volume per type (the overall bar height) and the relative proportions of each status (the segment sizes), providing two levels of insight simultaneously. The opacity is set to respond to hover interactions, with selected license types displaying at full opacity (1.0) while others dim to 0.7, creating clear visual focus without completely hiding context.

**Data Transformations:**

The Python analysis involved multiple transformation steps to create this visualization effectively. First, I filtered the dataset to remove any rows with null values in either the License_Type or License_Status columns, ensuring complete data for the analysis. I then identified the top 10 most common license types using `value_counts().head(10)` and filtered the entire dataset to include only licenses of these types, reducing the dataset from all license types to a focused subset of approximately 42,000 records. This filtering was necessary because visualizing all 150+ license types would create an incomprehensible chart, while the top 10 captures the most significant business categories. The data was left in its granular form (one row per license) rather than pre-aggregating, allowing Altair to perform the aggregation dynamically and maintain interactivity. I verified that the License_Status column contained meaningful categorical values and confirmed there were at least 2-3 status types per license category to ensure the stacked visualization would reveal interesting patterns. The transformation from individual license records to stacked bar segments happens through Altair's `count()` aggregation, which groups by both license type and status simultaneously.

<iframe src="chart2.html" width="100%" height="650" frameborder="0"></iframe>

---

## Interactivity Discussion

For the interactive component of this assignment, I implemented hover-based highlighting on the stacked bar chart (Visualization 2), which significantly enhances the visualization's clarity and analytical value. When users hover over any bar in the chart, that specific license type becomes fully opaque while all other bars dim to 70% opacity, creating immediate visual focus on the selected category. Additionally, interactive tooltips appear on hover, displaying the exact license type name, the specific status category, and the precise count of licenses in that status—information that would clutter the visualization if permanently displayed as labels.

This interactivity serves multiple important purposes that make the visualization more effective. First, it addresses the challenge of visual complexity: with 10 license types and up to 12 status categories, the chart contains over 50 individual data points. The hover highlighting helps users focus on one license type at a time without losing the context provided by the other bars, which remain visible but de-emphasized. Second, the tooltips provide exact numerical values on demand, allowing users to get precise counts for detailed analysis or reporting without permanently cluttering the chart with text labels that would reduce readability. Third, this interaction pattern supports exploratory analysis by making it easy to quickly compare different license types—users can hover across different bars to see how status distributions vary, effectively "filtering" their visual attention while maintaining the full dataset in view. This is particularly valuable for identifying patterns such as which license types have unusually high proportions of expired or cancelled licenses, potentially indicating compliance issues that merit further investigation. The interactivity transforms what could be an overwhelming static visualization into an explorable, layered information display that serves both quick overview purposes and detailed analysis needs. This approach is superior to alternatives like dropdown filters (which would hide context) or separate visualizations (which would prevent easy comparison) because it maintains all the data in view while giving users control over their focus of attention.

---

## Data Sources & Analysis

- **[The Data](https://raw.githubusercontent.com/shobhaa2405/dataviz-hw5/main/data/licenses_fall2022.csv)** - Chicago Business License Dataset
- **[The Analysis Notebook](https://github.com/shobhaa2405/dataviz-hw5/blob/main/Workbook%20(4).ipynb)** - Complete Python analysis

**Dataset Details:**
- Total records: 48,019
- License types: 150+
- Date range: 1987-2023
- Source: City of Chicago Open Data Portal

---

## About This Project

This project was created for IS 445 - Data Visualization at the University of Illinois Urbana-Champaign. The visualizations were built using:

- **Python** for data processing and analysis
- **Pandas** for data manipulation and aggregation
- **Altair** for creating declarative, interactive visualizations
- **Vega-Lite** for rendering in the browser
- **GitHub Pages** with Jekyll for hosting

The visualizations are fully interactive and render client-side using Vega-Lite, requiring no backend processing. All data transformations and analysis steps are documented in the linked Jupyter notebook.

---

*Created by Shobhaa Pasumarthy | November 2024 | IS 445 Data Visualization*

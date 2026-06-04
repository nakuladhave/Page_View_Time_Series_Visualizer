# 📈 Page View Time Series Visualizer

A Python-based time-series analysis project that explores **1,300+ days of freeCodeCamp forum traffic data (May 2016 – Dec 2019)** using trend analysis, seasonal decomposition, and multi-chart visualization.

---

## 📌 Project Overview

This project analyzes daily page view data from the freeCodeCamp forum to detect long-term growth trends, monthly seasonality patterns, and year-over-year changes. It produces a **3-chart dashboard** — line plot, bar plot, and box plots — enabling multi-dimensional KPI tracking and executive-level trend visualization.

These techniques are foundational to **AI forecasting pipelines**, **web analytics reporting**, and **business intelligence dashboards**.

---

## 📊 Dataset

- **Source:** [freeCodeCamp Forum Page Views Dataset](https://raw.githubusercontent.com/freeCodeCamp/boilerplate-page-view-time-series-visualizer/main/fcc-forum-pageviews.csv)
- **Coverage:** May 2016 – December 2019 (1,300+ daily records)

| Column | Description |
|--------|-------------|
| `date` | Date of measurement (parsed as DatetimeIndex) |
| `value` | Daily page view count |

---

## 🔧 Tech Stack

| Library | Purpose |
|---------|---------|
| Python 3 | Core language |
| Pandas | Data loading, cleaning, groupby, resampling |
| Matplotlib | Line plot and bar chart generation |
| Seaborn | Box plot visualization |

---

## 📁 Project Structure

```
page-view-time-series-visualizer/
│
├── page_view_time_series_visualizer.py   # Main script with all 3 plot functions
├── line_plot.png                         # Daily trend line chart
├── bar_plot.png                          # Monthly average bar chart by year
├── box_plot.png                          # Year-wise and month-wise box plots
└── README.md
```

---

## 🚀 How to Run

### Option A — Google Colab (Recommended)
Dataset loads directly from GitHub — no file upload needed.

### Option B — Local
```bash
# 1. Clone the repo
git clone https://github.com/nakuladhave/Page_View_Time_Series_Visualizer.git
cd Page_View_Time_Series_Visualizer

# 2. Install dependencies
pip install pandas matplotlib seaborn

# 3. Run
python page_view_time_series_visualizer.py
```

---

## 🧹 Data Cleaning

```python
lower_quantile = df['value'].quantile(0.025)
upper_quantile = df['value'].quantile(0.975)
df = df[(df['value'] >= lower_quantile) & (df['value'] <= upper_quantile)]
```

Top and bottom 2.5% of page view values removed to eliminate outliers (traffic spikes and anomalies), ensuring cleaner trend analysis.

---

## 📈 Visualizations

### 1. Line Plot — Daily Trend
```python
ax.plot(df.index, df['value'], color='red', linewidth=1)
ax.set_title('Daily freeCodeCamp Forum Page Views 5/2016-12/2019')
```
Plots raw daily page views over the full date range. Reveals the **overall upward growth trend** in forum traffic from 2016 to 2019.

---

### 2. Bar Plot — Monthly Averages by Year
```python
df_bar['year'] = df_bar.index.year
df_bar['month'] = df_bar.index.month_name()
df_bar_grouped = df_bar.groupby(['year','month'])['value'].mean().unstack()
df_bar_grouped = df_bar_grouped[months_order]  # Jan–Dec ordered
df_bar_grouped.plot(kind='bar', figsize=(15,7))
```
Groups data by year and month, calculates average page views per month, and plots a grouped bar chart. Months are ordered January–December for clean readability. Reveals **year-over-year growth** and **intra-year seasonal patterns**.

---

### 3. Box Plots — Trend & Seasonality
```python
# Year-wise
sns.boxplot(x='year', y='value', data=df_box, ax=axes[0])

# Month-wise (sorted Jan–Dec using month_num)
df_box = df_box.sort_values('month_num')
sns.boxplot(x='month', y='value', data=df_box, ax=axes[1])
```
Two side-by-side box plots:
- **Year-wise** — shows median page views increasing each year (long-term trend)
- **Month-wise** — reveals seasonal distribution shifts across months (seasonality detection)

Months sorted correctly Jan–Dec using `month_num` to avoid alphabetical ordering.

---

## 🔍 Key Findings

- Forum page views show a **consistent upward trend** from 2016 to 2019
- **Year-wise box plot** confirms rising median values year over year
- **Month-wise box plot** reveals higher traffic in certain months — indicating seasonal usage patterns
- Post-2018 data shows notably higher page view volumes compared to 2016–2017 baseline

---

## 🎯 Skills Demonstrated

- Time-series data loading with `parse_dates` and `index_col`
- Quantile-based outlier removal for cleaner trend analysis
- `groupby` + `unstack()` for pivot-style aggregation
- Controlled month ordering using `month_name()` + custom sort list
- Multi-chart figure layout with `plt.subplots(1,2)`
- Seaborn box plots for distribution and seasonality analysis

---

## 📜 Certification Context

Completed as part of the **freeCodeCamp Data Analysis with Python** certification — one of 5 required industry-standard projects.

🔗 [freeCodeCamp Certification](https://www.freecodecamp.org/certification/nakuladhave/data-analysis-with-python-v7)

---

## 👤 Author

**Nakul Adhave**
📧 nakuladhave@gmail.com
🔗 [LinkedIn](https://linkedin.com/in/nakul-adhave-a82294330)
💻 [GitHub](https://github.com/nakuladhave)

---

## 📄 License

This project is open source under the [MIT License](LICENSE).

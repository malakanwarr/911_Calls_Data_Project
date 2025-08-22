# 🚨 911 Calls Capstone Project

This project analyzes **911 emergency call data** from [Kaggle](https://www.kaggle.com/mchirico/montcoalert).  
The dataset provides insights into **emergency call patterns** across categories such as **EMS, Fire, and Traffic**.  
We use **pandas, matplotlib, seaborn, and numpy** to clean, analyze, and visualize the data.

---

## 📂 Dataset Overview

The dataset contains the following fields:

- **lat** : Latitude  
- **lng** : Longitude  
- **desc** : Description of the Emergency Call  
- **zip** : Zipcode  
- **title** : Title of the call (includes category like EMS, Fire, or Traffic)  
- **timeStamp** : Date & time of the call (`YYYY-MM-DD HH:MM:SS`)  
- **twp** : Township  
- **addr** : Address  
- **e** : Dummy variable (always 1)  

---

## 🛠️ Tools & Libraries

- **Python**  
- **NumPy, Pandas** → Data handling  
- **Matplotlib, Seaborn** → Visualization  

---

## 📊 Exploratory Data Analysis

### Top Zipcodes & Townships
- Most 911 calls came from **Zipcode 19401** and **Township LOWER MERION**.

### Reasons for 911 Calls
- Extracted a new column **Reason** (EMS, Fire, Traffic).  
- Most common reasons:
  - **EMS**: ~48,000  
  - **Traffic**: ~35,000  
  - **Fire**: ~15,000  

📌 Visualization:
```python
sns.countplot(x='Reason', data=df, palette='viridis')
```

## 🕒 Time Series Analysis

Converted timeStamp into datetime objects.

Created new columns: Hour, Month, Day of Week.

Mapped days as: 0=Mon, 1=Tue, …, 6=Sun.

## 📌 Call distribution by Day of Week & Reason:
```python
sns.countplot(x='Day of Week', hue='Reason', data=df, palette='viridis')
```

## 📌 Call distribution by Month & Reason:
```python
sns.countplot(x='Month', hue='Reason', data=df, palette='viridis')
```

## 📈 Trend Analysis

Grouped by Month to observe call volume trends.

Applied linear regression fit using seaborn’s lmplot.
```python
byMonth = df.groupby('Month').count()
sns.lmplot(data=byMonth.reset_index(), x='Month', y='twp')
```

Extracted a Date column to visualize daily call trends.

📌 Example:
```python
df.groupby('Date').count()['twp'].plot()
```

Also created separate daily plots for EMS, Fire, and Traffic calls.

## 🔥 Heatmaps & Clustermaps

To explore call density by time:

Grouped by Day of Week & Hour → Heatmap of call activity across the week.

Grouped by Day of Week & Month → Seasonal call density.

📌 Example:
```python
dt = df.groupby(['Day of Week','Hour']).count()['Reason'].unstack()
sns.heatmap(dt, cmap='viridis')
sns.clustermap(dt, cmap='viridis')
```
## 📌 Key Insights

- EMS calls dominate the dataset, followed by Traffic and Fire.

- Weekdays (especially Mon & Fri) have higher call volumes.

- Call frequency shows seasonal variation across months.

- Heatmaps reveal peak emergency hours in mornings and evenings.

## 🚀 How to Run

Clone this repository:
```bash
git clone https://github.com/yourusername/911-calls-analysis.git
cd 911-calls-analysis
```

## Install dependencies:
```bash
pip install -r requirements.txt
```

## Run the Jupyter Notebook:

jupyter notebook 911_Calls_Project.ipynb

## 📌 Future Improvements

- Incorporate geospatial analysis (plot calls on a map).

- Explore time-series forecasting of call volumes.

- Use machine learning to predict call type based on features.

✨ Built with Python, Pandas, Seaborn, and curiosity.

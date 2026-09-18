# FUTURE_DS_03 — Marketing Funnel & Conversion Performance Analysis

**Track:** Data Science & Analytics (DS) — Task 3
**Author:** _<your name>_
**Tools used:** Python (pandas, matplotlib, seaborn), SQL (SQLite), Jupyter Notebook

---

## 📌 Task

Analyze marketing funnel data to identify conversion drop-offs, channel performance, and
opportunities to improve lead-to-customer conversion.

**Deliverable:** A funnel performance dashboard/analysis report with key drop-off insights and
actionable recommendations to improve conversions.

## 🗂️ Repository Structure

```
FUTURE_DS_03/
├── data/
│   └── funnel_events.csv                  # 1,440-row daily channel-level funnel dataset
├── notebooks/
│   └── 01_funnel_conversion_analysis.ipynb # full analysis, step by step, with charts + narrative
├── sql/
│   ├── schema.sql                         # table definition
│   ├── analysis_queries.sql               # 8 business-question SQL queries
│   └── funnel.db                          # SQLite database preloaded with the dataset
├── src/
│   ├── generate_data.py                   # synthetic data generator (documents all assumptions)
│   ├── analysis.py                        # reusable analysis functions
│   └── dashboard.py                       # builds the static dashboard image below
├── images/
│   └── funnel_conversion_dashboard.png    # one-page visual dashboard (see below)
└── README.md
```

## 📊 Dashboard

![Marketing Funnel & Conversion Dashboard](images/funnel_conversion_dashboard.png)

## 🧾 Dataset

Since no client dataset was provided for this task, a **realistic synthetic dataset** was
generated (`src/generate_data.py`): 240 days of daily funnel activity (Impression → Click →
Lead → Signup → Customer) across **6 acquisition channels** (Paid Search, Paid Social, Organic
Search, Email, Referral, Direct), 3 devices, and 5 regions.

- Each channel has its own realistic, documented stage-to-stage conversion rates and cost
  structure (e.g. Paid Social has high reach but low conversion and high CPM; Referral has low
  volume but very high conversion and no media cost).
- Includes daily spend so **Customer Acquisition Cost (CAC)** can be computed per channel.
- All modeling assumptions are documented as comments in `generate_data.py`.

> To use this project with real data, replace `data/funnel_events.csv` with your own file
> matching the schema in `sql/schema.sql`, then re-run the notebook/scripts.

## 🔎 Methodology

1. **Data generation / ingestion** — `src/generate_data.py`
2. **Funnel & channel analysis** — `notebooks/01_funnel_conversion_analysis.ipynb`
   - Overall funnel shape and stage-to-stage conversion rates
   - Biggest drop-off points
   - Channel performance ranking (conversion rate, CAC)
   - Conversion rate trend over time
   - Device and region breakdowns
3. **SQL layer** — `sql/analysis_queries.sql` reproduces the funnel KPIs, channel ranking, and
   drop-off analysis directly in SQL against `sql/funnel.db`.
4. **Dashboard** — `src/dashboard.py` renders the full one-page dashboard image above.

## 💡 Key Findings

- Overall Impression→Customer conversion is **~0.28%**; the **Click→Lead** step (~70%
  drop-off) is the highest-leverage optimization point after natural top-of-funnel loss.
- **Referral** and **Direct** are the most efficient channels — highest conversion rate, $0
  direct acquisition cost.
- **Paid Social** drives the most impressions but has the **lowest conversion rate** and
  **highest CAC (~$48/customer)** — a volume channel, not an efficiency channel.
- **Paid Search** is a solid middle ground: real cost (~$7 CAC) with healthy conversion and
  strong volume.
- **Mobile** converts better than Desktop or Tablet despite carrying the most traffic.
- Conversion rate has been **flat month-over-month** while volume grew — efficiency, not just
  reach, is the next growth lever.

## ✅ Recommendations

1. **Reallocate a portion of Paid Social spend** toward Paid Search/Email, or improve Paid
   Social's audience targeting and creative before scaling further.
2. **Prioritize Click→Lead optimization** (landing pages, form length, page speed) — the
   single biggest addressable drop-off.
3. **Invest in referral mechanics** — it's already the highest-converting, zero-CAC channel.
4. **Protect and refine the mobile experience**, which already out-converts other devices.
5. **Set a CVR-improvement goal**, not just a volume goal, for next quarter.

## ▶️ How to Run

```bash
# 1. Install dependencies
pip install pandas numpy matplotlib seaborn

# 2. Regenerate the dataset (optional — funnel_events.csv is already included)
python src/generate_data.py

# 3. Run the analysis
python src/analysis.py

# 4. Rebuild the dashboard image
python src/dashboard.py

# 5. Or open the full notebook
jupyter notebook notebooks/01_funnel_conversion_analysis.ipynb

# 6. Run SQL queries directly
sqlite3 sql/funnel.db < sql/analysis_queries.sql
```

## 🧠 Skills Demonstrated

Funnel analysis · Conversion metrics · Growth analytics · Customer Acquisition Cost (CAC)
analysis · SQL querying · Data visualization · Performance optimization

---

*Part of the Data Science & Analytics track — Task 3. See also: [FUTURE_DS_02 — Customer
Retention & Churn Analysis](../FUTURE_DS_02).*

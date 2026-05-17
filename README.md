# Evaluating E-Commerce Recommendation Systems via A/B Testing

## 📌 Project Overview
This project performs a rigorous end-to-end evaluation of an A/B test launched by an international online store. The test, named `recommender_system_test`, aimed to determine if implementing an improved recommendation system impacts user conversion through a multi-stage funnel within 14 days of registration.

The pipeline covers programmatic data cleaning, validation of test design flaws, exploratory data analysis (EDA), and proportion hypothesis testing ($Z$-test).

## 📊 Technical Specifications & Business Targets
*   **Test Name:** `recommender_system_test`
*   **Target Audience:** 15% of new users from the EU region
*   **Sample Groups:** 
    *   **Group A (Control):** Legacy user experience
    *   **Group B (Variant):** New payment funnel + upgraded recommendation system
*   **Experiment Duration:** December 07, 2020 – January 01, 2021 (User acquisition stopped Dec 21, 2020)
*   **Success Metrics:** Expected minimum **10% increase** in conversion at each funnel stage within 14 days of user signup:
    $$\text{Login} \longrightarrow \text{Product Page} \longrightarrow \text{Product Cart} \longrightarrow \text{Purchase}$$
*   **Target Sample Size:** 6,000 participants

---

## 🛠️ Tech Stack & Methodology
*   **Languages & Environment:** Python 3, Jupyter Notebooks
*   **Data Manipulation:** Pandas, NumPy
*   **Statistical Analysis:** SciPy (Stats), Statsmodels (`proportions_ztest`)
*   **Data Visualization:** Matplotlib, Seaborn, Plotly Express/Graph Objects

---

## 📈 Analytical Workflow & Data Validation

### 1. Data Cleaning & Integrity Audits
*   **Data Type Management:** Programmatically cast raw features to unified `datetime` standards.
*   **Missing Value Strategy:** Discovered 363,447 missing values in the event `details` column. Evaluated against business rules to deduce that empty elements indicate non-purchase actions (e.g., logins, page loads), allowing a clean programmatic fill of `0` without distorting the data distribution.
*   **Experiment Pollution Control:** Identified that **6.1% of participants** were cross-pollinated across conflicting experiment groups. To protect experiment integrity, these users were dropped. 
*   **Cohort Filtering:** Strictly filtered for users matching the target region (`EU`) and limited actions to events occurring within a **14-day cohort window** from each specific user's signup timestamp.

### 2. Exploratory Data Analysis (EDA) Insights
*   **Sample Imbalance:** The experiment suffered a massive design skew. Instead of a standard 50/50 or balanced layout, **Group A contained 75% of users**, while **Group B was severely starved at 25%**. 
*   **Sample Size Deficiency:** The active sample only yielded **2,787 valid users**, falling short of the required 6,000-user power threshold.
*   **Funnel Anomalies:** While overall conversion from login to purchase stood at 30%, a unique user path was found: purchase events outstripped cart additions. This indicates the existence of an accelerated "Buy Now" feature bypassing the cart setup.
*   **Seasonality Effects:** Activity spiked violently on **December 21st**, heavily driven by late holiday shopping traffic rather than isolated test feature engagement.

### 3. Hypothesis Testing ($Z$-Test)
Proportions were evaluated across all funnel events using a two-sided Z-test ($\alpha = 0.05$).

*   **Null Hypothesis ($H_0$):** There is no statistically significant difference in conversion proportions between Group A (Control) and Group B (Variant).
*   **Alternative Hypothesis ($H_1$):** There is a statistically significant difference in conversion proportions between Group A and Group B.

---

## 🔑 Key Findings & Results
*   **Funnel Breakdown:** Group B (the new system) **underperformed** relative to the control group across critical stages and completely missed the targeted 10% lift.
*   **Statistical Outcomes:** 
    *   **Login & Product Cart:** Failed to reject $H_0$. No statistically measurable variance.
    *   **Product Page & Purchase:** Rejected $H_0$. A statistically significant negative conversion regression occurred in Group B.

## 🚀 Business Recommendations
1.  **Do Not Deploy Variant B:** The new recommendation system fails to deliver positive uplift and shows a statistical drop in user movement to product pages.
2.  **Discard and Rerun the Experiment:** The test parameters were fundamentally compromised due to heavy group imbalance (75/25), missing sample targets by over 50%, and data collection cutting off abruptly on Dec 29 instead of Jan 01. 
3.  **Account for Seasonality:** Future tests should avoid overlapping major global shopping events like Christmas unless specifically tracking holiday promotions.
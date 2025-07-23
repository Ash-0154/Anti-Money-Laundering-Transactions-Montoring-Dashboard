# Anti-Money Laundering (AML) Transaction Monitoring Dashboard

## 🗂️ Introduction

This project introduces an end-to-end Anti-Money Laundering Transaction Monitoring Dashboard designed to detect, investigate, and visualize suspicious financial activity. The solution leverages Power BI and IBM’s synthetic AML dataset to simulate realistic scenarios involving anomalous transactions, high-risk merchants and customers, and peak risk periods.

- **Objective:**  
  Monitor and analyze financial transactions to detect potential money laundering, including unusual patterns, high-risk entities, and periods of heightened activity among customers, merchants, and banks.

- **Key Highlights:**  
  - Innovative use of dynamic KPIs for total suspicious activity, flagged entities, and risk distribution.
  - Drillthrough pages offering in-depth breakdowns for merchants and banks.
  - Time-based trends to surface suspicious behavior patterns.
  - Advanced Power BI features: interactive tooltips, dynamic navigation, and star schema modeling.

- **Built With:**  
  Power BI Desktop, IBM synthetic AML CSV datasets, DAX, and Star Schema modeling principles.

## 📂 Dataset Source

- **IBM Watsonx Synthetic AML Dataset (CSV format; Available in Kaggle)**
- **Files Used:**
  - `transactions_HI.csv`, `transactions_LI.csv`
  - `patterns_HI.csv`, `patterns_LI.csv`
  - `amounts_HI.csv`, `amounts_LI.csv`

## 🏗️ Data Modeling Steps

- **Merged Transactions & Patterns**
  - The `patterns` tables contained all columns of `transactions`, plus additional pattern-specific fields.
  - Both High Intensity (HI) and Low Intensity (LI) transaction and pattern datasets were merged to create a single consolidated fact table: `FactTransactions`.

- **Combined Account Details**
  - HI and LI versions of the `amounts` table were merged to produce a unified `DimAccount` dimension table.

- **Created Date Table**
  - An independent `DimDate` dimension was created, containing a complete date hierarchy.
  - The `TransactionDate` field in `FactTransactions` is related to the `DateKey` in `DimDate`.

- **Dual Roleplaying Dimension**
  - `DimAccount` was duplicated to serve as both `DimAccount_From` and `DimAccount_To`, representing both sender and receiver contexts.
  - Each dimension was appropriately linked to `FactTransactions` to model transaction origin and destination.

- **Schema Design**
  - The entire model is structured as a classic **Star Schema**:
    - **Fact Table:** `FactTransactions`
    - **Dimensions:** `DimDate`, `DimAccount_From`, `DimAccount_To`

## 📊 Report Pages & Navigation

### 1. **Introduction Page**

- **Purpose:**  
  Sets the report objective, data source, and navigational links for user guidance.
- **Contents:**
  - Clear project goal (transaction monitoring for AML)
  - Features list, including datasets, visual features, and navigation overview
  - At-a-glance explanation of how to use the report and what insights each section delivers
  - Visual navigation buttons for each main analysis page

<img width="584" height="331" alt="intro page" src="https://github.com/user-attachments/assets/74348d77-07de-411d-92df-fb9a6fb7c80b" />

### 2. **Executive Overview**

- **Purpose:**  
  Provides high-level KPIs and trend insights into overall suspicious activity, laundering percentages, and behavioral patterns.
- **Features:**
  - KPI cards (Total Transactions, Suspicious %, High-Risk Count)
  - Transaction trends by time and entities
  - Heatmap comparison by payment type and bank
  - Global slicers for quick filtering

<img width="596" height="337" alt="pg 1" src="https://github.com/user-attachments/assets/57066d09-db19-477b-9ffb-ef279c5aa847" />

### 3. **Merchant Risk Profile**

- **Purpose:**  
  Flags high-risk merchants, analyzes laundering trends, and enables drillthrough for detailed merchant investigation.
- **Features:**
  - KPIs for merchant-level risk
  - Suspicious activity breakdowns
  - Top merchants ranked by suspicious value/count
  - Filters by currency/pattern/type

<img width="591" height="341" alt="pg 2" src="https://github.com/user-attachments/assets/567171d3-f4f9-4a10-92a0-ae6954bc6932" />

### 4. **Time-Based Suspicious Activity Analysis**

- **Purpose:**  
  Surfaces risk by analyzing activity across days/hours to highlight vulnerable periods.
- **Features:**
  - KPIs for peak hour, weekend laundering rate, daily suspicious average
  - Charts showing suspicious activity distribution
  - Flexible filters and date/time controls

<img width="593" height="338" alt="pg 3" src="https://github.com/user-attachments/assets/65744ab3-df00-4a8e-90a0-ad6d7583a186" />

### 5. **Customer Risk Profile**

- **Purpose:**  
  Profiles customer activity, exposing high-risk senders and behavioral trends.
- **Features:**
  - KPIs and visualizations for customer-centric suspicious metrics
  - Distribution and concentration analysis by entity/size/type
  - Dynamic filters for custom review

<img width="591" height="338" alt="pg 4" src="https://github.com/user-attachments/assets/dcb6b9e7-3c71-4bce-898f-ad81d53673e9" />

### 6. **Laundering Risk Summary & What-If Analysis**

- **Purpose:**  
  Models systemic risk, offers “what-if” scenario analysis, and highlights risk concentration by channel/institution.
- **Features:**
  - KPIs for weighted suspicious volume and high-risk participants
  - Sliders for interactive scenario simulation
  - Pie/bar charts for breakdowns by payment format and bank

<img width="592" height="338" alt="pg 5" src="https://github.com/user-attachments/assets/490f8ea2-9a08-466e-850f-3cc938f2f82c" />

## 🔍 Drillthrough Pages

### Merchant Drillthrough

When a merchant is selected from  a page (eg.Merchant Risk Profile), users can drill through to a detailed analytics page focused solely on that merchant’s activities.

- **Merchant KPIs:**
  - Total transaction amount
  - Suspicious transaction count and percent
  - Average suspicious transaction value
- **Transaction Classification:** Charts showing transaction size by laundering classification.
- **Suspicious Activity Trends:** Time series showing suspicious transactions over time.
- **Detailed Transaction Table:** Filterable and sortable transaction records for the merchant.
- **Filters:** Payment format, pattern type, currency.

<img width="587" height="338" alt="merchant drillthrough og" src="https://github.com/user-attachments/assets/330884c0-ebb1-4da0-97b0-c429af294492" />

<img width="590" height="331" alt="merchant risk profile drillthrough" src="https://github.com/user-attachments/assets/d1685557-fc90-4163-b469-14cb6d42db30" />

<img width="586" height="335" alt="specific merchant" src="https://github.com/user-attachments/assets/4474308a-afc5-49cf-80e1-a6e0a9941554" />

### Bank Drillthrough (From Laundering Risk Summary Page)

On selecting a bank from a page (eg.Laundering Risk Summary), users can drill through to a bank-specific report detailing laundering risk at the institution level.

- **Bank KPIs:**
  - Total transaction volume
  - Total suspicious volume
  - Number of flagged customers
  - Average suspicious amount per customer
- **Heatmaps:** Temporal distribution of suspicious transactions by day and hour.
- **Behavioral Radar:** Visualization of sender account patterns like FAN-IN, STACK, CYCLE.
- **Filters:** Payment format, transaction bucket, currency.
- **Navigation:** Back to summary or drill further into customers or merchants.

<img width="587" height="337" alt="bank drillthrough og" src="https://github.com/user-attachments/assets/505fd66a-5f0d-43d8-b38c-b1582d772273" />

<img width="599" height="335" alt="laundering risk drillthrough for bank" src="https://github.com/user-attachments/assets/a62f6880-6d4a-4180-81d2-aeff621737ae" />

<img width="588" height="337" alt="specific bank" src="https://github.com/user-attachments/assets/8c4ec21e-21f1-406f-8f09-7acc92bce932" />

## 🧩 Advanced Power BI Features Demonstrated

- Drillthrough capability for in-depth data exploration
- Custom tooltips on KPIs and visuals for on-demand explanations
  
  <img width="683" height="360" alt="kpi tooltip eg" src="https://github.com/user-attachments/assets/8782d7b2-1338-413c-847d-ca814f3fbbd5" />

  <img width="689" height="337" alt="visual tooltip eg" src="https://github.com/user-attachments/assets/43f13286-c3ba-48f5-9898-f4b1d5723fd1" />

- Interactive bookmarks enabling scenario analysis and navigation

  <img width="588" height="335" alt="pg 1 insights" src="https://github.com/user-attachments/assets/8971e149-78cf-4da9-b0a7-0c86b8ab1e80" />

- Dynamic slicers providing flexible, instant data filtering
- Roleplaying dimensions modeling sender and receiver perspectives
- Clean, consistent design supporting accessibility and usability

## ⚙️ Interactivity & User Experience

| Feature                | Description                                                                             |
|------------------------|-----------------------------------------------------------------------------------------|
| Global Navigation Bar  | Jump to any report page instantly                                                       |
| Back/Next Buttons      | Sequential navigation between pages                                                     |
| Drillthroughs          | Detailed views for merchants and banks                                                  |
| Tooltips (KPI, Visual) | Mouseover explanations enhancing context                                                |
| Question Mark Icon     | Opens a dedicated explanation page per report                                           |
| Dynamic Slicers        | Slicing on entity, payment, pattern, currency, time                                     |
| What-If Slicers        | Interactive sliders for scenario analysis/filtering—adjust sensitivity thresholds       |
|                        | (e.g., laundering suspicion weights, transaction volumes) and instantly visualize       |
|                        | the impact across all relevant charts and KPIs                                          |

## 📥 How to Use

1. Use the navigation bar to select any report page.
2. Review KPIs and interact with visuals, using tooltips for more context.
3. Hover or click on the question mark in the top-left to access detailed page explanations.
4. Use Back and Next buttons for sequential page flow.
5. Drillthrough from summary pages (merchants or banks) to detailed entity profiles.
6. Explore filters and bookmarks for tailored scenario analysis.

## 👩‍💼 Author

Ashika S S  
July 2025

## ✨ Acknowledgments

- IBM Watsonx Synthetic AML Dataset  
- A live website version of this dashboard is hosted on my university’s internal portal (vit.ac.in) and is accessible only to VIT community members due to network restrictions. Please refer to the included screenshots and documentation in this repository for a full demonstration of dashboard features and interactivity.
- This dashboard is for demonstration and educational purposes only. No real financial data is present.





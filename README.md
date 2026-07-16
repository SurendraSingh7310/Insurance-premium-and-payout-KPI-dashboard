# Insurance-premium-and-payout-KPI-dashboard
Insurance Premium and Payout KPI Dashboard

📊 **Project Overview**
This repository contains a comprehensive Power BI dashboard designed for an insurance provider to track policy performance, premium collections, and agent productivity. The dashboard provides executive and operational views into financial KPIs, demographic distributions, and long-term return on investment (ROI) metrics.

🎯 **Key Performance Indicators (KPIs)**
The dashboard tracks the following high-level metrics at a glance:  
Total Policies: 1.816K active policies.  
Total Annual Premium: 556.13M.  
Total Premium Amount: 5.56bn.  
Total Premium Paid: 2.27bn.  
Total Premium Payable: 3.30bn.  
Underwriting Expense: 9.50M.  

📈 **Dashboard Features & Visualizations**
The report is highly interactive, featuring multiple slicers to filter data by Policy Type, Policy Name, Sales Agent, Year, State, and Tenure (5 or 10 years). 

Key visual insights include:
Financial Trending: Dual-axis charts comparing the Sum of Total Premium Paid, Sum of Total Premium Payable, and the Average Annualized ROI (%) over time (spanning forecasts up to 2032).  
Geographic Distribution: Bar charts highlighting top-performing states, led by Uttar Pradesh (70.43M), Delhi (69.88M), and Sikkim (51.84M).  
Agent Performance: Treemaps and stacked bar charts detailing premium collections by agents such as Divij Malhotra, Baiju Singh, and Biju Issac.  
Customer Demographics: Visuals breaking down annual premiums by customer occupation, highlighting top segments like Theatre stage and Medical tech professionals.  
Detailed Customer Ledger: A granular table view providing line-by-line customer data, including Policy Holder Name (e.g., Amira Kade, Prerak Chaudhari), Premium Duration, Sum Assured, and Maturity Amounts.  

**⚙️ Technical Architecture1.** 
Data Transformation (Power Query)
Before rendering the visuals, the raw data undergoes rigorous cleaning and transformation within Power Query. The standard process applied in this project includes:
Data Extraction & Profiling: Connecting to the raw data sources (e.g., SQL databases, Excel, or CSV) and evaluating data quality.
Data Cleansing: Handling missing values, standardizing text fields (like standardizing state names or policy types), and ensuring accurate data types for financial figures (Currency) and dates.
Custom Column Creation: Calculating derived metrics, such as identifying the remaining premium payable by subtracting "Total Premium Paid" from "Total Premium Amount".  
Schema Optimization: Structuring the data into a Star Schema, separating Fact tables (transactions, premiums paid) from Dimension tables (Customers, Sales Agents, Geography, Dates) to optimize the DAX engine's performance.

2. Row-Level Security (RLS) ImplementationTo ensure data privacy and organizational compliance, this dashboard utilizes Dynamic Row-Level Security (RLS). This ensures that users only see the data they are authorized to view based on their corporate hierarchy.
3. 
4. How RLS is structured in this dashboard:5.
6. Hierarchical Data Model: The dataset explicitly contains an organizational hierarchy mapping the Sales Agent to a Regional Manager and a Zonal Manager. For example, Sales Agent Divij Malhotra reports to Regional Manager Ananya Sharma, who reports to Zonal Manager Rohit Kapoor.
7. Email Mapping: The data model includes specific email columns (Agent Mail, RM Mail, ZM Mail) to facilitate dynamic filtering.
8. DAX Security Roles: In Power BI Desktop, roles are created (e.g., "Agent", "Regional Manager") using DAX filters. A standard dynamic RLS DAX filter uses the USERPRINCIPALNAME() function. For example, the Agent role would have a filter on the employee table like: [Agent Mail] = USERPRINCIPALNAME().
9. Power BI Service Assignment: Once published to the Power BI Service, users (or Azure Active Directory Security Groups) are assigned to these roles. When a Zonal Manager logs in, the RLS dynamically filters the entire dashboard to show only the aggregated performance of their subordinate Regional Managers and Sales Agents.

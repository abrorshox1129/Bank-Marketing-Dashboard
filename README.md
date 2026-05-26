# Bank Marketing Dashboard - Data Dictionary

## Overview
This document describes all fields, tables, and metrics used in the Bank Marketing Dashboard.

---

## 📋 Core Tables

### 1. **CUSTOMERS** Table
Customer demographic and profile information.

| Field Name | Data Type | Description | Example |
|------------|-----------|-------------|---------|
| customer_id | Integer | Unique customer identifier | 1001 |
| age | Integer | Customer age in years | 35 |
| age_group | Text | Age category (18-25, 26-35, 36-45, 46-55, 55+) | 26-35 |
| education | Text | Education level (primary, secondary, tertiary, unknown) | tertiary |
| marital_status | Text | Marital status (single, married, divorced) | married |
| job | Text | Job category | management |
| balance | Decimal | Account balance in currency units | 1500.50 |
| balance_category | Text | Balance tier (Young, Old, Poor, Safely) | Young |
| housing_loan | Boolean | Has housing loan (Yes/No) | Yes |
| personal_loan | Boolean | Has personal loan (Yes/No) | No |
| contact_type | Text | Preferred contact method (cellular, telephone, email) | email |
| day_of_week | Text | Last contact day (Monday-Sunday) | Thursday |
| month | Text | Last contact month | May |

### 2. **DEPOSITS** Table
Customer deposit account information.

| Field Name | Data Type | Description | Example |
|------------|-----------|-------------|---------|
| deposit_id | Integer | Unique deposit identifier | 5001 |
| customer_id | Integer | Foreign key to CUSTOMERS table | 1001 |
| deposit_date | Date | Date deposit account opened | 2026-05-15 |
| deposit_amount | Decimal | Initial deposit amount | 5000.00 |
| deposit_type | Text | Type of deposit (savings, fixed-term, etc.) | savings |
| interest_rate | Decimal | Interest rate percentage | 4.5 |
| has_converted | Boolean | Customer made deposit (Yes/No) | Yes |

### 3. **CAMPAIGNS** Table
Marketing campaign execution details.

| Field Name | Data Type | Description | Example |
|------------|-----------|-------------|---------|
| campaign_id | Integer | Unique campaign identifier | C001 |
| customer_id | Integer | Foreign key to CUSTOMERS table | 1001 |
| campaign_start_date | Date | Campaign start date | 2026-04-01 |
| campaign_duration_seconds | Integer | Campaign duration in seconds | 250 |
| duration_group | Text | Duration category (0-300s, 301-900s, 901-1000s, 1001+s) | 0-300s |
| campaign_contacts | Integer | Number of contacts during campaign | 3 |
| campaign_outcome | Text | Campaign result (success, failure, other) | success |
| contact_method | Text | Method used (cellular, telephone, email) | email |
| campaign_nationality | Text | Campaign nationality classification | success |
| campaign_group | Text | Campaign group classification | 1 to ... |
| previous_contacts | Integer | Previous campaign contacts | 0 |

---

## 📊 Calculated Fields & Measures

### Key Performance Indicators (KPIs)

| Measure Name | Formula | Description |
|-------------|---------|-------------|
| **Total Customers** | COUNT(Customers[customer_id]) | Total number of customers |
| **Total Deposit Holders** | COUNTIF(Deposits[has_converted], TRUE) | Number of customers with deposits |
| **Conversion Rate %** | (Deposit Holders / Total Customers) × 100 | Percentage of customers who opened deposits |
| **Average Balance** | AVERAGE(Customers[balance]) | Mean account balance |
| **Total Deposits Value** | SUM(Deposits[deposit_amount]) | Total value of all deposits |
| **Campaign Success Rate** | COUNTIF(Campaigns[outcome], "success") / COUNT(Campaigns) × 100 | Percentage of successful campaigns |
| **Average Contact Duration** | AVERAGE(Campaigns[campaign_duration_seconds]) | Mean campaign duration in seconds |

### Conversion Metrics

| Metric | Definition | Usage |
|--------|-----------|-------|
| **Conversion by Education** | Deposit conversion % for each education level | Identify high-value segments |
| **Conversion by Age Group** | Deposit conversion % by age category | Demographic targeting |
| **Conversion by Marital Status** | Deposit conversion % by marital status | Life stage analysis |
| **Conversion by Balance Category** | Deposit conversion % by balance tier | Financial capacity analysis |
| **Conversion by Duration** | Campaign success % by duration group | Campaign optimization |
| **Conversion by Contact Method** | Success % by contact channel | Channel effectiveness |

---

## 🎯 Dashboard Dimensions

### Education Levels
- **Primary** - Elementary education
- **Secondary** - Middle/High school
- **Tertiary** - College/University
- **Unknown** - Education not specified

### Age Groups
- **18-25** - Young professionals
- **26-35** - Mid-career professionals
- **36-45** - Senior professionals
- **46-55** - Pre-retirement
- **55+** - Retirement age

### Marital Status
- **Single** - Never married
- **Married** - Legally married
- **Divorced** - Previously married

### Job Categories
- Management
- Technician
- Services
- Admin
- Retired
- Blue-collar
- Unemployed
- Entrepreneur
- Student
- Housemaid
- Unknown

### Balance Categories
- **Young** - Young customers with growing balances
- **Old** - Established customers with higher balances
- **Poor** - Customers with lower balances
- **Safely** - Stable customers with secure balances

### Contact Methods
- **Cellular** - Mobile phone
- **Telephone** - Landline phone
- **Email** - Electronic mail

### Campaign Duration Groups
- **0-300s** - Very short campaigns (< 5 minutes)
- **301-900s** - Short campaigns (5-15 minutes)
- **901-1000s** - Medium campaigns (15-17 minutes)
- **1001+s** - Long campaigns (> 17 minutes)

### Campaign Outcomes
- **Success** - Customer opened deposit
- **Failure** - Customer declined
- **Other** - Unclear/pending result

---

## 📈 Data Quality Notes

### Missing Values Handling
- Unknown education/job/contact type coded as "unknown"
- Null balances treated as 0
- Missing campaign data excluded from campaign analysis

### Data Validation Rules
- Age must be between 18-120
- Balance cannot be negative
- Duration must be positive integer
- Customer IDs must be unique
- Dates must be valid and within range

### Data Update Frequency
- Customer data: Monthly
- Campaign data: Real-time
- Deposit data: Daily
- Overall dashboard: Weekly refresh

---

## 🔍 Analysis Categories

### Customer Segmentation
- **By Education**: Identify knowledge-level targeting
- **By Age**: Life stage and career progression
- **By Balance**: Financial capacity and tier targeting
- **By Marital Status**: Life event-based targeting

### Campaign Optimization
- **Duration Analysis**: Find optimal campaign length
- **Contact Method**: Identify preferred channels
- **Frequency Impact**: Measure contact repetition effects
- **Nationality Patterns**: Geographic performance

### Conversion Drivers
- **Education Impact**: Tertiary shows 54% conversion
- **Age Effect**: Middle-aged (36-55) show strong conversion
- **Balance Correlation**: Higher balance correlates with conversion
- **Housing Credit**: Significant predictor of deposit opening

---

## 💡 Common Calculations

### Conversion Rate by Segment
```
Conversions in Segment / Total Customers in Segment × 100
```

### Campaign Effectiveness Score
```
(Success Rate × Duration × Contact Frequency) / 100
```

### Customer Lifetime Value
```
(Deposit Amount × Interest Rate × Years) - Acquisition Cost
```

### Churn Prediction Risk
```
Inactivity Days / Average Contact Frequency
```

---

## 📚 Data Sources

- **Primary Source**: Bank customer database
- **Campaign Data**: Marketing automation platform
- **Deposit Records**: Core banking system
- **Customer Demographics**: CRM system

---

## 🔐 Data Privacy & Compliance

- All data is anonymized (no real names)
- Customer IDs are hashed
- Complies with GDPR and banking regulations
- Regular data audits conducted
- Secure storage and access controls

---

## 📞 Questions?

For questions about specific fields or data:
- Check the README.md for overview
- Review the CONTRIBUTING.md for update procedures
- Open an Issue on GitHub
- Contact the data governance team

---

**Last Updated**: May 7, 2026
**Data Dictionary Version**: 1.0.0

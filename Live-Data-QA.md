<img width="130" alt="Screenshot 2024-09-10 at 11 42 36 AM" src="https://github.com/user-attachments/assets/076ded8b-63a2-45cc-821c-ca109fc7e6a2">

# Data QA - Code Challenge

The main objective of this assignment is measuring test engineering skills.

---

## Requirements and Output

### Challenge One:  
**e-Commerce Highest Customer Revenue**

e-commerce marketing analytics, they need to find the customer who generated the most revenue for them during **July 2021**.  

Revenue rules:  

- **type=BUY** → transaction amount is potential revenue.  
- **type=SELL** → Mart collects a 10% fee (0.1 * amount).  
- **status=COMPLETED** → transaction is included.  
- **status=PENDING** → transaction is ignored.  
- **status=CANCELED** → 1% of the transaction amount is *deducted* from revenue.  

**Columns to report**:  
- `customer`  
- `buy` → number of BUY transactions  
- `sell` → number of SELL transactions  
- `completed` → number of COMPLETED transactions  
- `pending` → number of PENDING transactions  
- `canceled` → number of CANCELED transactions  
- `total` → calculated revenue, rounded to 2 decimals (show trailing zeros)  

---

#### Schema

**transactions**

| name     | type         | description                |
|----------|--------------|----------------------------|
| dt       | VARCHAR(19)  | Transaction timestamp      |
| customer | VARCHAR(64)  | Customer email address     |
| type     | VARCHAR(4)   | Transaction type (BUY/SELL)|
| amount   | DECIMAL(5,2) | Transaction amount         |
| status   | VARCHAR(9)   | Transaction status         |

---

#### Sample Data

**transactions**

| dt                  | customer                  | type | amount | status     |
|---------------------|---------------------------|------|--------|------------|
| 2021-07-18 03:13:37 | stapenden1@google.de      | BUY  | 95.90  | COMPLETED  |
| 2021-07-09 09:56:13 | jpeddersen6@virginia.edu  | BUY  | 34.37  | CANCELED   |
| 2021-07-13 01:12:15 | rclaypole0@qq.com         | BUY  | 79.27  | COMPLETED  |
| 2021-07-05 02:12:53 | asmithin4@elegantthemes.com | SELL | 23.80  | PENDING    |
| 2021-06-21 13:50:29 | bhaddeston2@mapquest.com  | BUY  | 89.55  | COMPLETED  |
| 2021-06-28 08:09:02 | cpalek8@yahoo.com         | SELL | 64.45  | CANCELED   |
| 2021-07-23 07:07:29 | rclaypole0@qq.com         | BUY  | 19.92  | COMPLETED  |
| 2021-07-03 15:20:54 | rclaypole0@qq.com         | SELL | 51.30  | COMPLETED  |
| 2021-07-13 18:05:55 | stapenden1@google.de      | SELL | 86.29  | COMPLETED  |
| ...                 | ...                       | ...  | ...    | ...        |

---

### Challenge Two:  
**Antivirus Detection Rates**

An organization uses multiple antivirus software across its computer systems. A query needs to be developed to analyze the detection rate of each software based on scan reports.  

**Requirements**:  
- Return all antivirus software whose most recent scan reported **>10 detections**.  
- Columns:  
  - `title` → product title  
  - `last_detections` → detections in the most recent scan  
  - `change_in_detections` → difference vs. previous scan  
- Order by `last_detections` (DESC), then `title` (ASC).  

---
#### Clarification

- **Most recent scan** = the row with the **maximum `dt`** per software.  
- **Previous scan** = the row with the **next maximum `dt`** (immediately before the most recent one).  
- If a software has **only one scan record**, exclude it from the results.

#### Schema

**softwares**

| name | type        | constraint  | description                       |
|------|-------------|-------------|-----------------------------------|
| id   | INT         | PRIMARY KEY | Antivirus software ID             |
| title| VARCHAR(255)| UNIQUE      | Product title of the antivirus    |

**scans**

| name        | type       | constraint                  | description              |
|-------------|------------|-----------------------------|--------------------------|
| software_id | INT        | FOREIGN KEY → softwares.id  | Antivirus software ID    |
| dt          | VARCHAR(19)|                             | Scan datetime            |
| detections  | INT        |                             | Number of detections     |

### softwares

| id | title        |
|----|--------------|
| 1  | SecureShield |
| 2  | DefenderPro  |
| 3  | SafeGuard    |

### scans

| software_id | dt                  | detections |
|-------------|---------------------|------------|
| 1           | 2023-06-26 03:51:52 | 4          |
| 1           | 2023-07-03 22:28:37 | 8          |
| 1           | 2023-07-10 05:51:31 | 2          |
| 1           | 2023-07-11 20:49:45 | 12         |
| 1           | 2023-07-24 00:21:44 | 13         |
| 1           | 2023-07-24 07:35:17 | 9          |
| 1           | 2023-07-25 10:56:12 | 2          |
| 1           | 2023-07-26 15:12:36 | 12         |
| 2           | 2023-07-02 20:06:09 | 17         |
| 2           | 2023-07-21 10:03:18 | 13         |
| 2           | 2023-07-24 10:15:22 | 6          |
| 2           | 2023-07-27 15:10:20 | 18         |
| 2           | 2023-08-04 08:54:55 | 3          |
| 2           | 2023-08-06 15:21:06 | 4          |
| 2           | 2023-08-07 16:41:19 | 8          |
| 3           | 2023-07-06 07:06:48 | 3          |
| 3           | 2023-07-13 00:28:19 | 2          |
| 3           | 2023-07-15 04:19:28 | 20         |
| 3           | 2023-07-19 21:06:56 | 8          |
| 3           | 2023-07-21 07:22:24 | 9          |


---


### Challenge Three:  
**Insurance Risk Analysis**

An insurance company analyzes the risk of applicants before issuing policies.  

Monthly premiums:  
- Term Life / Whole Life → **$100**  
- Health → **$400**  
- Endowment → **$500**  

Payout rules (as % of yearly collected premium):  

| Insurance Type | Low Risk | Medium Risk | High Risk |
|----------------|----------|-------------|-----------|
| Term Life      | 10%      | 8.5%        | 7%        |
| Whole Life     | 10%      | 8.5%        | 7%        |
| Health         | 2%       | 1.5%        | 1%        |
| Endowment      | 15%      | 12%         | 10%       |


You are given a table **`users`** with the following schema:

| Column         | Type     | Description                                                   |
|----------------|----------|---------------------------------------------------------------|
| user_id        | INTEGER  | Unique identifier of the user                                 |
| insurance_type | VARCHAR  | Type of insurance (e.g., Term Life, Health, Whole Life, Endowment) |
| risk           | VARCHAR  | Risk level (Low, Medium, High)                                |

---

## Sample Data

| user_id | insurance_type | risk   |
|---------|----------------|--------|
| 6697    | Term Life      | Medium |
| 4084    | Term Life      | Medium |
| 3053    | Health         | Medium |
| 2716    | Term Life      | Medium |
| 3130    | Health         | Medium |
| 4146    | Whole Life     | Low    |
| 5875    | Health         | Low    |
| 8747    | Whole Life     | High   |
| 2095    | Term Life      | Medium |
| 8374    | Term Life      | High   |
| 6014    | Whole Life     | High   |
| 6546    | Endowment      | High   |
| 4533    | Term Life      | Low    |
| 7174    | Health         | Low    |
| 4470    | Health         | Medium |
| 1364    | Whole Life     | Low    |
| 4293    | Health         | High   |
| 7062    | Health         | Medium |
| 6839    | Term Life      | Medium |
| 9596    | Health         | Low    |

---

**Task**:  
- Calculate insured amount per user.  
- Round to nearest integer.  
- Return columns: `user_id`, `insurance_type`, `risk`, `insured_amount`.  
- Order by `user_id`.  

---

## What we are looking for:

A query we can **trust**! ✅  

Passing execution does not automatically mean correctness — queries must return the exact expected output.

Your SQL code should be:  
- **Accurate** → produces the right results.  
- **Reliable** → works on different valid datasets.  
- **Clear** → easy to read and understand.  

---

## Important Notes for Delivery:

- Deliver the challenge as a **public Git repository** (GitHub/Bitbucket preferred).  
- **Quality > completeness**. Don’t implement everything at the cost of messy code.  
- Even if you can’t finish, submit your work.  

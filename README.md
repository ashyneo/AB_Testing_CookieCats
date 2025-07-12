# Cookie Cats A/B Testing: Does Gate Placement Affect Player Retention?

This project is an A/B testing analysis on Cookie cats mobile game to evaluate whether moving the first gate from level 30 (control) to level 40 (exp) impacts player retention using hypothesis testing, confidence interval, and practical significance insights.

## 📌 Problem Statement

Cookie Cats is a popular mobile puzzle game where players can progress through levels and encounter 'gates' that slow progress unless unlocked. The games developers want to know:

> **Does moving the first game from level 30 (control) to level 40 (experimental) improve player retention?**

To answer this, I conducted a **2-sample, 2 tailed Z-test** to determine whether the gate position made any statistical and practically significant difference on **Day 1 and Day 7 player retention.**

---

## 🧠 Game Mechanics and Understanding the User Journey
In Cookie Cats, the first few levels act as a learning curve before players hit their first 'gate', a friction point that may impact motivation. Understanding this progression helped define **player retention** as the success metric. If players leave before or after the gate, it may indicate how disruptive or engaging the gate placement is.

---

## The Success Metric 🎯: Player Retention

The business aims to **Retain players over time.** Hence, I measured:
- **Day 1 Retention**: Did the player return the day after installing?
- **Day 7 Retention**: Did the player return 7 days later?

---

## 🧪 Hypothesis Testing

Two hypotheses were tested:

- **Hypothesis 1 (Day 1 Retention)**:  
  - **H₀**: No difference in Day 1 retention between Gate 30 and Gate 40  
  - **H₁**: There is a difference in Day 1 retention between Gate 30 and Gate 40

- **Hypothesis 2 (Day 7 Retention)**:  
  - **H₀**: No difference in Day 7 retention between Gate 30 and Gate 40  
  - **H₁**: There is a difference in Day 7 retention between Gate 30 and Gate 40

---

## Dataset Overview

This dataset was sourced from [Kaggle](https://www.kaggle.com/datasets/mursideyarkin/mobile-games-ab-testing-cookie-cats) and contains **90,189** player records with the following key columns:
| Column          | Description                                                |
|-----------------|------------------------------------------------------------|
| `userid`        | Unique identifier for each player                          |
| `version`       | A/B group: `gate_30` (control) or `gate_40` (test)         |
| `sum_gamerounds`| Total number of game rounds played within 14 days         |
| `retention_1`   | 1 if player returned on Day 1, else 0                      |
| `retention_7`   | 1 if player returned on Day 7, else 0                      |

> For full data dictionary and preprocessing steps, please refer to my [notebook](https://github.com/ashyneo/AB_Testing_CookieCats/blob/031f50d2b036d6495092344eb88983f096e10174/AB%20Testing%20Marketing%20(Which%20Is%20better)-5.ipynb).

---

## Analysis & Key Findings 

### ✅ Sanity Checks – A/A Test

Before testing, I validated that players were randomly and fairly split:

- Created A1 (n=22,337) and A2 (n=22,363) from control group.

<img width="218" height="64" alt="image" src="https://github.com/user-attachments/assets/29d755d0-1ec7-4ab3-a0eb-cc0ce4037971" />

  
- **Chi-Square Test Result**:
  - Chi-square = 3.0408, p-value = 0.0812
  - ✅ No significant difference → groups are homogeneous and unbiased.

<img width="156" height="39" alt="image" src="https://github.com/user-attachments/assets/9c131e6d-3640-41d7-adb8-6f533099a290" />

---

### 📊 Retention Distribution

- **Bar charts** were used to visualize total retained vs. not retained users for each version.
- **Day 1 retention** is higher across both groups, while **Day 7 retention drops notably**.
- However, Gate 30 vs Gate 40 differences appear subtle. I will proceed with the AB testing to find out.
<img width="893" height="507" alt="image" src="https://github.com/user-attachments/assets/4a2d4810-3fee-4223-9278-2c124ba821aa" />


<img width="923" height="504" alt="image" src="https://github.com/user-attachments/assets/f16f5a7b-9ea6-4c27-9b10-809daa4c9d77" />


---
### 🎮 Game Rounds Behavior

Plotted `sum_gamerounds` revealed:
- Most players play very few rounds; ~5,000 played only once.
- There is a sharp early **churn**.
- A small long-tail could mean **hardcore, engaged users** who played 100+ rounds.
- Indicates that **player engagement declines naturally** over time, this could outline that there are factors more important than gate positioning later.

<img width="893" height="517" alt="image" src="https://github.com/user-attachments/assets/fcdf660f-bd6a-4ea4-ace0-b402ff033456" />


--- 
## 📐 Statistical Testing Assumptions

- I used a **2-sample Z-test** (Central Limit Theorem applies with n > 30)
- Assumptions:
  - α = 0.05 (5% Type I error)
  - MDE (Minimum Detectable Effect) = **10%**

## 📈 A/B Test Results

### Day 1 Retention:
- **p-value**: 0.074
- **Result**: ❌ *No statistically significant difference*  
- **Conclusion**: The gate change had **no real impact** on short-term player engagement.

### ✅ Day 7 Retention:
- **p-value**: 0.002 ✅ *Statistically significant*
- **95% Confidence Interval**: [-0.013, -0.003]
- **Minimum Detectable Effect (MDE)**: 10%
- **Result**: ❌ *Not practically significant*
- **Conclusion**: While Gate 40 underperforms slightly in retention, the drop is **small (0.3%–1.3%)** and not large enough to justify a change from a business perspective.

---

## 📉 Gaussian Plot (Rejection Region)

To provide a visual view of Day 7's **standard normal distribution** result:

<img width="538" height="412" alt="image" src="https://github.com/user-attachments/assets/387551c7-4510-431d-9fdc-97a7e10acb59" />

- **Z-test statistic = 3.16** (green dashed line)
- Red tails = rejection region
- The test statistic **falls well into the rejection region**, showing **strong evidence** that there is a difference between Gate 30 and Gate 40's retention rates.

*Note: While the Gaussian distribution plot confirms strong statistical significance for Day 7 retention (As the test statistic falls well into the rejection region), this does not imply practical significance. As mentioned earlier, the 95% confidence interval was (-0.013, -0.003), and my MDE was set at 10%.*

*Since the observed difference falls below my practical threshold, I can conclude that the difference though statistically real, is too small to warrant a product change based solely on retention.*

---

## 💡 Conclusion & Recommendations

From both a **statistical and business perspective**, **Gate 40 does not bring meaningful improvements** to retention. Reverting the gate may not be worthwhile unless:

- Developers believe even a 0.3–1.3% retention drop is impactful at scale  
- Product stakeholders are willing to invest engineering effort for a small gain

Moreover, game data shows that **player engagement tends to decline naturally with more rounds**, possibly due to fatigue, difficulty spikes, or lack of rewards. These may play a larger role in retention rather than focusing on gate placement alone.

> **Recommendation**: Consider scrapping the gate 40 idea and **reiterating core gameplay mechanics**. For example, consider reward systems, level pacing, or difficulty curves, as these may have stronger influence on long-term retention.

---

## 🛠️ Tools Used

- Python, Pandas, NumPy
- Matplotlib, Seaborn
- Scipy for statistical testing

---

## References
Yarkin, M. (2021). Mobile games A/B testing - Cookie Cats [Dataset]. Kaggle. https://www.kaggle.com/datasets/mursideyarkin/mobile-games-ab-testing-cookie-cats (Originally from DataCamp; reuploaded by Murside Yarkin on Kaggle.)



# 🍽️ Restaurant Business Analysis — EDA & Visualization

_Analyzing restaurant success of User Engagement and Success Metrics decisions using SQL and Python._

---

## 📌 Table of Contents
- <a href="#overview">Project Overview</a>
- <a href="#Problem Statement">Problem Statement</a>
- <a href="#dataset">Dataset</a>
- <a href="#tools--technologies">Tools & Technologies</a>
- <a href="#project-structure">Project Structure</a>
- <a href="#data-cleaning--preparation">Data Cleaning & Preparation</a>
- <a href="#research-questions--key-findings">Research Questions & Key Findings</a>
- <a href="#how-to-run-this-project">How to Run This Project</a>
- <a href="#final-recommendations">Conclusion</a>
- <a href="#author--contact">Author & Contact</a>

---
<h2><a class="anchor" id="overview"></a>📌 Project Overview</h2>

- This project performs Exploratory Data Analysis (EDA) and Data Visualization on the Yelp dataset, focusing exclusively on the restaurant industry.
- The analysis explores how reviews, check-ins, tips, and ratings influence restaurant success and customer engagement.

---
<h2><a class="anchor" id="Problem Statement"></a>🎯 Problem Statement</h2>

- In a competitive market like the restaurant industry, understanding the factors that drive business success is crucial.
- This project investigates the relationship between user engagement (reviews, tips, check-ins) and business success metrics (review count, ratings) for restaurants.

---
<h2><a class="anchor" id="dataset"></a>Dataset</h2>

- Multiple JSON files located in `/data/` folder (user, review, business, checkins, tip)
- Summary table created from ingested data and used for analysis
- We does not add data folder because data set is in large size.

---

<h2><a class="anchor" id="tools--technologies"></a>Tools & Technologies</h2>

- SQL (Common Table Expressions, Joins, Filtering)
- Python (Pandas, Matplotlib, Seaborn, SciPy)
- GitHub

---
<h2><a class="anchor" id="project-structure"></a>Project Structure</h2>

```
restaurant-business-analysis/
│
├── README.md
├── .gitignore
├── requirements.txt
├── Restaurant Business Report.pdf
│
├── notebooks/                  # Jupyter notebooks
│   ├── database_creation.ipynb
│   ├── restaurant_business_analysis.ipynb
│
```

---
<h2><a class="anchor" id="data-cleaning--preparation"></a>Data Cleaning & Preparation</h2>

1. The Data Cleaning by SQL query:
```python
pd.read_sql_query("""
    select business_id, review_count
    from business
    where lower(categories) like '%restaurant%' and is_open=1
""", conn)

```

**Column Selection**
- business_id: Unique identifier for each business, necessary for linking to other tables (e.g., reviews/tips).
- review_count: Number of reviews for each business, a core metric for business engagement and popularity.

**Negative or Zero Values Detected:**
- The main goal is to filter for relevant records, ensuring the analysis focuses solely on open restaurants with available review counts.

**Filtering Conditions**
- lower(categories) like '%restaurant%': This condition:
	- Converts the categories column to lowercase (for case-insensitive matching).
	- Selects businesses whose category contains the word "restaurant" anywhere in its value.
- is_open=1: This ensures only businesses that are currently open (active) are selected, excluding closed/defunct locations.

**Result Set**
- The output is a cleaned DataFrame with two columns: business_id and review_count.
- Only rows meeting both filter conditions are included, reducing noise and focusing the EDA on active restaurants only.


---

---
<h2><a class="anchor" id="research-questions--key-findings"></a>🔍 Research Questions & Key Findings</h2>

**Restaurant Count & Reviews**
- Number of restaurants analyzed: 150,346
- Average reviews per restaurant: ~104
- Review count range: 5 (min) to 7,568 (max)
-  Average rating: 3.52
- Median rating: 3.5

**Top Chains (by Reviews)**
| Restaurant | Reviews | Avg Rating |
| :--- | :---: | ---: |
| McDonald's | 16,490 | 1.87 |
| Chipotle Mexican Grill | 9,071 | 2.38 |
| Taco Bell | 8,017	 | 2.14 |
| Chick-fil-A | 7,687 | 3.38 |
| First Watch | 6,761 | 3.88 |
| Panera Bread | 6,613 | 2.66 |
| Buffalo Wild Wings | 6,483 | 2.34 |
| Domino's Pizza | 6,091 | 2.29 |
| Wendy's | 5930 | 2.03 |
| Chili's | 5,744 | 2.51 |

Large chains have high review counts but generally low average ratings.

**Highest Rated Restaurants**
| Name | Reviews | Avg Rating |
| :--- | :---: | ---: |
| ā café | 48 | 5.0 |
| two birds cafe | 77 | 5.0 |
| the brewers cabinet production | 13 | 5.0 |

Small restaurants often achieve perfect ratings, though with fewer reviews.

**User Engagement**
- Correlation coefficients:
	- Review vs. Check-ins: 0.63
	- Review vs. Tips: 0.77
	-  Check-ins vs. Tips: 0.77

	Higher reviews strongly link to more tips and check-ins, showing overall engagement channels are connected.

**High vs. Low Rated Restaurants**
| Category | Avg Review | Avg Tip | Avg Tip |
| :--- | :---: | ---: | ---: |
| High-rated | 72.3 | 10.2 | 122.1 |
| Low-rated | 42.1 | 6.5 | 88.9 |

High-rated restaurants drive more reviews, tips, and check-ins.

**City-Level Highlights**
| City | Restaurant Count | Total Reviews | Avg Rating | Success Score |
| :--- | :---: | ---: | ---: | ---: |
| Philadelphia | 3,001 | 175,487 | 3.53 | 42.65 |
| Tampa | 1,715 | 104,376 | 3.57 | 41.27 |
| Indianapolis | 1,701 | 92,639 | 3.41 | 39.02 |
| Tucson | 1,419 | 91,613 | 3.39 | 38.69 |
| Nashville | 1,404 | 87,070 | 3.49 | 39.74 |

Philadelphia leads in restaurant density, reviews, and business success.

**Temporal Trends**
- Review & tip volumes have grown year-over-year, peaking around 2018-2019.:
	- December 2018: 27,871 reviews, 2,535 tips
	- December 2020: 18,858 reviews, 1,543 tips
	-  December 2021: 21,872 reviews, 1,085 tips

Recent years show a dip, likely reflecting pandemic effects.

**User Contribution**
| User Type | Count | Reviews |
| :--- | :---: | ---: |
| Elite | 91,198 | 20,484,441 |
| Non-Elite | 1,896,699 | 26,021,235 |

Elite users are few but contribute a large share of detailed reviews.

---

---
<h2><a class="anchor" id="how-to-run-this-project"></a>How to Run This Project</h2>

1. Clone the repository:
```bash
git clone https://github.com/your-username/restaurant-business-analysis.git
cd restaurant-business-analysis

```
2. Open and run notebooks:
```
   jupyter notebook Analysis_Review.ipynb
```


---
<h2><a class="anchor" id="final-recommendations"></a>📌 Conclusion</h2>

The project reveals that in the Yelp data, user engagement metrics (reviews, tips, check-ins) are strongly interconnected and serve as meaningful indicators of restaurant success. High-quality restaurants tend to attract more active customer participation. Geographic and temporal factors influence engagement dynamics, with elite users playing a crucial role in review volume and depth. These insights can help stakeholders make informed decisions and strategies in the competitive restaurant industry.

---
<h2><a class="anchor" id="author--contact"></a>Author & Contact</h2>

**Ashutosh Kalaskar**  
Data Analyst  
📧 Email: kalaskarashu@gmail.com

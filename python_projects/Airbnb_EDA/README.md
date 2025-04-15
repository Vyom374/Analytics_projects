# 🏠 Airbnb NYC Exploratory Data Analysis (EDA)

## 🛏️ What is Airbnb?

**Airbnb** is an online marketplace that connects people looking to rent out their homes (hosts) with those looking for accommodations (guests). It allows travelers to book short-term stays in apartments, houses, shared rooms, or even unique locations like boats or treehouses.

It operates globally and provides an alternative to traditional hotels, often offering a more local, affordable, and flexible experience.

---

## 📊 Airbnb Dataset Column Descriptions

| Column Name                    | Description                                                                 |
|-------------------------------|-----------------------------------------------------------------------------|
| **id**                         | Unique identifier for each listing                                         |
| **name**                       | Title of the listing                                                       |
| **host_id**                    | Unique ID of the host                                                      |
| **host_name**                  | Name of the host                                                           |
| **neighbourhood_group**       | Borough or main area of the listing (e.g., Manhattan, Brooklyn)            |
| **neighbourhood**             | Specific neighborhood within the borough                                   |
| **latitude**                   | Geographical latitude of the property                                      |
| **longitude**                  | Geographical longitude of the property                                     |
| **room_type**                  | Type of room listed (entire home, private room, shared room, etc.)         |
| **price**                      | Price of the listing in USD                                                |
| **minimum_nights**            | Minimum number of nights required for booking                              |
| **number_of_reviews**         | Total number of reviews received                                           |
| **last_review**               | Date of the most recent review                                             |
| **reviews_per_month**         | Average number of reviews per month                                        |
| **calculated_host_listings_count** | Number of listings the host has                                       |
| **availability_365**          | Number of days the listing is available in a year                          |
| **license**                   | Whether the listing is officially licensed or not                          |
| **rating**                    | Average rating of the listing                                              |
| **bedrooms**                  | Number of bedrooms                                                         |
| **beds**                      | Number of beds available                                                   |
| **bath**                      | Number of bathrooms                                                        |

---

## 🎯 Objective

The goal of this project is to:

1. Analyze **room types, prices, and availability** across different neighborhoods.
2. Understand **host behavior** and listing patterns.
3. Detect potential **outliers** in prices.
4. Provide recommendations for guests and hosts based on insights.

---

## 🧰 Steps Followed

### 1. 🧹 Data Cleaning

- Removed unwanted non-ASCII characters from the `name` column and split it for better analysis.
- Filled null values in `price` with the **median**.
- Dropped records with missing or null values in other columns.
- Removed extreme outliers (e.g., listings with prices over $100k).

---

### 2. 📊 Exploratory Data Analysis (EDA)

#### Room Type Distribution
- Visualized room types using bar plots.
- Found that **Entire home/apt** is the most common.

#### Neighborhood Group Insights
- Analyzed price variations by borough.
- **Manhattan** had the highest average prices.

#### Availability Trends
- Created heatmaps to show correlations between:
  - `price`, `availability_365`, `number_of_reviews`, `beds`.

#### Price Distribution
- Most listings priced between **$50–$300**.
- Used histograms to detect skewness and boxplots for outliers.

---

### 3. 📈 Data Visualization

- **Pairplot**: Visualized relationships between features.
- **Heatmap**: Checked correlations among numerical features.
- **Boxplots & Histograms**: Used to identify outliers and skewness.
- **Bar Charts**: Showed distribution of room types and neighborhoods.

---

## 📈 Insights from Univariate & Bivariate Analysis

### 💸 Price Distribution
- Majority of listings are priced between **$50–$300**.
- **Private and shared rooms** are significantly cheaper.

---

### 🏨 Room Type Analysis
- **Entire homes/apartments** dominate.
- **Private rooms** cater to budget travelers.
- **Hotel and shared rooms** are minimal.

---

### 🗺️ Neighbourhood Group Distribution
- Top 3 boroughs by listing count:
  1. Manhattan
  2. Brooklyn
  3. Queens
- **Manhattan** is the most premium in terms of pricing and volume.

---

### 🔁 Availability Analysis
- Most listings are available **200–365 days** a year.
- Entire homes are generally available more than other types.

---

### 🏘️ Neighbourhood-Level Insights
- Most active neighborhoods are in **central Manhattan and Brooklyn** — high tourist density areas.

---

### ⭐ Review Count & Popularity
- Listings with **moderate pricing** tend to get more reviews.
- **High-priced** listings often have fewer reviews — possibly targeting a niche market.

---

## 🧾 Airbnb EDA Summary: Actionable Insights

### 👤 For Guests / Tourists

- **Private rooms** are great for budget travel in premium locations.
- Choose listings in **Manhattan and Brooklyn** for accessibility and quality.
- Look for **highly reviewed** listings for better experiences.

---

### 🏠 For Hosts

- Focus on **Manhattan and Brooklyn** for higher booking potential.
- Offering **entire homes** leads to better returns and higher demand.
- Optimize pricing — being slightly below the borough average attracts more guests.
- There's room for **hotel-style offerings** with the right pricing strategy.

---

## ✅ Conclusion

This project provides a comprehensive overview of the Airbnb landscape in NYC using EDA techniques. We extracted meaningful insights about room types, pricing, availability, and review behavior — helping both guests and hosts make informed decisions.

In the future, this project can be extended using **predictive modeling** to forecast prices, estimate demand, or optimize booking strategies.

---


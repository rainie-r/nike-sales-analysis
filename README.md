# Nike Sales Analysis

A business analytics project using a public Kaggle dataset to look at sales performance across products, regions, retailers, and sales channels.

## Project Overview

I built this as a portfolio project to practice a full analytics workflow, starting from a messy-ish raw dataset and working through to actual findings I could defend. The goal wasn't just to make charts, it was to understand the data well enough to know what it can and can't tell me about the business.

## Business Problem

I approached this like I was prepping a sales performance review, trying to answer:
- Which products and regions actually drive revenue
- Whether products with high unit sales are also the highest revenue earners
- How average selling price differs across products and channels
- Whether there's anything off in the data that needs to be flagged before anyone draws conclusions from it

## Dataset & Disclaimer

Dataset is from Kaggle: [krishnavamsis/nike-sales](https://www.kaggle.com/datasets/krishnavamsis/nike-sales). 9,360 transaction rows, Jan 2020 to Dec 2021, US regions only.

**This is not official Nike data.** It's a public dataset used here as a business case to practice analytics, nothing in this project should be read as a statement about Nike's real sales.

## Tools Used

- **Excel** – first pass at profiling the data, checking it manually, building some quick pivot tables
- **Python (Pandas, NumPy, Matplotlib, Seaborn)** – the actual cleaning and analysis, plus the charts
- **GitHub** – putting it all together

I'd originally planned to add a Power BI dashboard too. Didn't end up happening, more on that under Limitations.

## Analytical Approach

1. Started in Excel: checked for missing values, duplicates, and whether the categories (region, retailer, etc.) were spelled consistently
2. Built a `Calculated Sales` column (Price × Units) and compared it to the recorded `Total Sales`. This is where things got interesting, a huge chunk of rows didn't match
3. Moved to Python to rebuild that check in code (so it's reproducible) and actually dig into why the mismatch was happening, plus built out KPI tables, checked a correlation, and looked at the data across product, region, retailer, and time
4. Made six charts to cover the revenue breakdowns, the trend over time, and the data quality issue
5. Wrote up findings as Finding / Evidence / Business Meaning / Potential Action, trying to keep observations separate from my own interpretation of them

## Key Findings

**1. Revenue isn't riding on one hero product.**
It takes the top 4 of 6 product categories to reach 80% of total revenue. Men's Street Footwear, the single biggest category, is still only 23.2% of revenue. So the portfolio is spread out, not dependent on one bestseller.

**2. West is the strongest region, and not just by luck in one category.**
West leads overall revenue (26.99%) and it leads in almost every row when you break revenue down by product and region together. It's not one product line carrying the whole region.

**3. Total Sales probably includes a discount that isn't recorded anywhere else, mostly in Online and Outlet.**
79.65% of rows have a Total Sales value that doesn't match Price × Units. The mismatch rate is 90.5% for Online and 81.9% for Outlet, versus 46.2% for In-store. A lot of these mismatches cluster around a suspiciously consistent ~90% reduction, which feels specific enough that it's worth asking whoever owns this data about, rather than just assuming it's a normal discount.

**4. The jump in revenue from 2020 to 2021 is probably just a data coverage gap, not real growth.**
2020 only has 1,302 recorded transactions, 2021 has 8,058. Amazon has zero transactions recorded in 2020 at all. So this reads more like an artifact of how the data was collected than an actual growth story.

**5. Price and volume don't move together much.**
Correlation between Price per Unit and Units Sold is 0.27. Higher priced items aren't really selling in noticeably lower volumes here.

*Findings 3 and 4 are my interpretation of the pattern, not confirmed facts, I don't have access to whoever actually owns this data to verify either one.*

## Business Recommendations

- Don't put all the marketing or inventory focus on one product category. The top four all matter, not just the number one.
- Worth digging into what West is doing differently, since whatever's working there might be repeatable in a weaker region like the Midwest.
- The Total Sales discrepancy should be flagged as a known limitation anywhere this dataset gets used. If this were a real internal dataset, the next step would be asking the data owner directly whether it's a discount field that just isn't exposed.
- Don't present the 2021 revenue increase as growth without mentioning that the transaction counts between the two years are very different. That caveat changes the story.

## Project Limitations

- I originally planned to build a Power BI dashboard for this. Power BI Desktop doesn't run natively on Mac, so I tried building it on a borrowed Windows laptop and ran into enough technical friction (trackpad precision issues, the laptop shutting down mid-session) that I decided it wasn't worth pushing further given the time I had. The six Python charts cover most of what a dashboard would have shown anyway.
- No cost or margin column in this dataset, so everything here is about revenue, not profit.
- No customer-level data, so there's nothing here about repeat purchases or customer behavior.
- The Total Sales discrepancy and the 2020 vs 2021 transaction gap are both my best interpretation of the pattern. I don't have access to the original data source to confirm either one for certain.

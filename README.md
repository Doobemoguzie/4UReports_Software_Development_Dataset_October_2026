# Software Delivery Quality Dashboard

A three-page Power BI report for the ZoomCharts 4U Reports Challenge. The data is 643 software releases from 2024 and 2025, and the question I ended up chasing was simple: when releases go wrong, where does it cost the most?


## Why I opened with the money

The dataset comes with seven benchmarks, and five of them are missed. I could have built the whole report around that list, but "incidents per release is 0.34 against a target of 0.30" doesn't make anyone want to act on it. $2.95M does, so that's the first number on page one. I think people react to money faster than they react to a ratio.

## What I found

65.5% of releases shipped on or before the planned date. The target is 90%, and no quarter in the two years got above 70.3%. The late ones ran 4.1 days over on average, against a 3-day target.

The downtime cost comes to an estimated $2.95M, and it's lumpy. Only 146 of the 643 releases had any downtime at all. Five modules make up 61% of the total, and one release, R-0201 on BillingPro Invoicing, cost roughly $206K by itself. Four teams (Atlas, Beacon, Titan and Nimbus) hold 76% of it, and Beacon turns up five times in the ten costliest releases.

On testing, I expected more tests to mean fewer production defects. The data didn't give me that. Teams that run more tests per feature have slightly more defects per feature, with a correlation of about 0.25 across the 15 teams. That's weak, and I wouldn't build a recommendation on it. One possible reason is that teams test harder on riskier work, but this data can't show that either way.

Bug fixes are about a fifth of all work items (1,267 of 6,226), roughly two per release.

## The three pages

Overview has the seven KPI cards against their targets, the cost headline, cost by module, and a quarterly chart with a selector for five different measures. The target line disappears for downtime cost, since it's the one measure with no benchmark.

Quality and teams is a 15-team scorecard sorted by cost, a bubble chart of tests against defects per feature, and the bug fix numbers. The bubble and bar charts drill from team to product down to modules.

Incidents and cost is a drill-through page. Right-click a team or product on the first two pages and it opens on the ten costliest releases for that selection, with the release details underneath.

Every page has an Info button that explains how the numbers are calculated.

## Where I got stuck

Resolution time is easy to get wrong. 77% of releases have no incidents and are stored as 0 hours, so averaging the column gives 0.7 hours, which passes the 2-hour target. Weight it by incident count and it's 3.2 hours, which doesn't.

Counting rows in the release items table gives 6,226 "features". The real number is 4,959, because 1,267 of those rows are bug fixes.

I wanted rounded pills for met and missed in the team table. Every time I've tried images in a Power BI table the rows stretch, so I dropped the idea and used a filled circle for missed and an open circle for met. It isn't what I pictured, but it reads fine without colour.

The metric selector on the quarterly chart threw a composite key error when I read the parameter's name column. Reading the order column instead fixed it. My "most frequent team in the top ten" measure also returned the wrong team for a while. It says Beacon now, which is right.

## Things I chose not to claim

I considered a product-level scorecard and dropped it. There are 123 team and product pairs, the median has 4 releases, and 53% have fewer than 5. With three releases, a single one moves a rate by 33 points. Product detail stays on the charts, where the release count is visible.

I didn't call delivery "improving" either. 2025 opens with the best quarter in the data (70.3%) and closes with the worst (60.9%).

## What I'm not sure about

The cost is an estimate. It rests on the per-minute rates in the DowntimeCost sheet, so I use it to compare modules and teams, not to quote a loss.

Eight quarters is not enough to call a trend, and each quarter only has 68 to 92 releases.



The benchmarks come from the challenge's own sheet. The data also stops at December 2025.

## How the numbers are built

- Rates are total over total, not averages of per-release percentages.
- Resolution hours are weighted by incident count. Automated and test failure rates are weighted by tests executed.
- Cost is downtime minutes times the module's cost per minute.
- Features come from the Feature rows in the release items table, which match the features column for all 643 releases.

## Power BI Report Access

* [Click to download Power BI file](/Onyz%20Data%202026-10%20Power%20BI%20Representation.pbix)

## Built with

Power BI Desktop, ZoomCharts Drill Down visuals and DAX. The source is the challenge workbook, Software_Delivery_Quality_challenge_dataset.xlsx.


##  Author

**Doobem**  
Data Analyst  

- LinkedIn: [doobemoguzie](https://www.linkedin.com/in/prosper-oguzie-54a706336) 
- GitHub: [Doobemoguzie](https://github.com/Doobemoguzie)
- Contact: [Prosperoguzie379@gmail.com](prosperoguzie379@gmail.com)

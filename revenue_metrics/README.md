# Revenue Metrics Analysis
A SQL + Tableau project that tracks monthly revenue health for a mobile gaming platform — from raw payment transactions to an interactive dashboard with key subscription metrics.

**[View Tableau Dashboard](https://public.tableau.com/views/FinalProject_17344587814450/Finalinformation?:language=en-US&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link)**

## Tech Stack
- **PostgreSQL** — data preparation and metric calculation
- **Tableau Public** — metric calculation, visualization and dashboard

## Data Sources
| Table | Key Fields |
|---|---|
| `project.games_payments` | user_id, game_name, payment_date, revenue_amount_usd |
| `project.games_paid_users` | user_id, language, has_older_device_model, age |

---

## SQL Structure
The query is built as three CTEs:
1. **`payment_summary`** — aggregates payments per user, game, and month
2. **`payment_with_months`** — adds previous/next calendar months and lag/lead revenue values using window functions
3. **`metrics`** — applies CASE logic to classify each user-month record into one of the revenue metric categories
The final SELECT joins with `games_paid_users` to enrich the output with user attributes (language, age, device model), then sorts by `user_id`, `game_name`, `payment_month`.

### Metrics calculated in SQL
| Metric | Description |
|---|---|
| **New MRR** | Revenue from users making their first payment |
| **Expansion Revenue** | Revenue increase from existing users compared to previous month |
| **Contraction Revenue** | Revenue decrease from existing users compared to previous month |
| **Churned Revenue** | Revenue lost from users who stopped paying |
| **Churn Month** | The month a user is considered churned |

---

## Dashboard
### Metrics calculated in Tableau
| Metric | Description |
|---|---|
| **MRR** | Total Monthly Recurring Revenue |
| **ARPPU** | Average Revenue Per Paid User |
| **New Paid Users** | Users with first-ever payment in the month |
| **Churned Users** | Users who did not pay in the following month |
| **Churn Rate** | Share of churned users out of total paid users |
| **Revenue Churn Rate** | Share of lost revenue out of total MRR |
| **LT** | Average customer lifetime in months |
| **LTV** | Total revenue expected from a user over their lifetime |

The Tableau dashboard has 7 visualizations, all filterable by **age**, **language**, and **month**:
1. **MRR vs Paid Users** — total recurring revenue alongside user count over time
2. **ARPPU** — average revenue per paid user by month
3. **New MRR vs New Paid Users** — growth from newly acquired users
4. **Churned Revenue & Churned Users** — revenue and user loss trends
5. **Churn Rate & Revenue Churn Rate** — retention health over time
6. **Expansion MRR & Contraction MRR** — upsell vs downsell dynamics
7. **LTV & LT** — lifetime value and lifetime duration trends

---

## Use Cases
- **Product teams** — identify which months had the highest churn and correlate with product changes or game updates
- **Marketing teams** — segment revenue metrics by language or age group to evaluate campaign effectiveness
- **Finance teams** — monitor MRR composition (new, expansion, contraction, churned) for revenue forecasting
- **Game managers** — compare revenue health across different games in the portfolio
- **Analysts** — use the SQL as a base template for subscription-style revenue reporting in other domains



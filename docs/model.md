# Transaction and analytical model rules

## Transaction contract

`tbl_transactions` contains Date, Type, Amount, From Account, To Account, Category, Merchant, Note, and Entry Status. Amount is a positive whole-number VND value. Merchant and Note are optional.

| Type | Direction | Category | Analytical effect |
|---|---|---|---|
| Income | To one asset account | An Income category | Income and asset increase |
| Expense | From one asset or liability | An Expense category | Spending increases; asset decreases or debt increases |
| Refund | To one asset or liability | Original Expense category | Net spending decreases; asset increases or debt decreases |
| Transfer | From and To different tracked accounts | Blank | Changes natural balances; excluded from income/spending |
| Allocation | From or To one asset | Savings & Investment | From is gross contribution; To is allocation return |
| Adjustment | Exactly one side | Blank | Corrects a natural balance; excluded from income/spending |

Borrowing and credit-card repayments use Transfer. They are not income or expense. Fees and interest are Expense transactions. Allocations leave or re-enter the tracked assets; the destination investment balance is not tracked in this demo.

`tbl_accounts` holds Account Name, Institution, Account Type, Account Class, Opening Balance, Opening Date, Credit Limit, Active, and the formula-driven Current Balance. `tbl_categories` provides type/classification mapping. `tbl_monthly_plan` holds month, category, and planned VND amount.

## Natural balances

Asset balance = opening balance + To amounts − From amounts.

Liability balance = opening debt + From amounts − To amounts. Debt is positive when owed. Excel restricts transactions to on/after the opening date in each account balance calculation. Power Query adds one opening ledger row per account, filters each transaction side to on/after that account's opening date, and signs it using the same asset/liability convention. Transactions before an account opens may still be valid for the flow KPIs, but are excluded from that account balance in both Excel and Power BI. Enter an opening date for each named account; the Power Query fallback for a missing date is the demo start date, 1 September 2026.

## Power Query and model

`WorkbookSource` opens the workbook once. Raw queries select the four named tables. `ValidTransactions` trims text, converts dates/amounts defensively, and accepts only positive transactions with `Entry Status = OK`. Refresh-time transaction keys depend on workbook row order, rather than serving as permanent externally stable identifiers.

- `FactTransactions`: validated Income, Expense, Refund and Allocation rows for flow KPIs (8 rows in this demo). Transfers and Adjustments affect the movement ledger only.
- `FactAccountMovements`: signed opening and From/To ledger rows.
- `FactMonthlyPlan`: category/month targets and budgets.
- `DimAccount`, `DimCategory`, `DimDate`: account, category, and calendar dimensions.
- `_Measures`: explicit cash-flow, allocation, budget, and balance measures.

The report uses dimension filters and cumulative balances through the selected date. The workbook balances reflect all valid entered rows since account opening; changing its selected month affects the flow KPIs and budget view, not the account balances.

## Measure definitions

- Total Income: Income transactions.
- Gross Expense: Expense transactions.
- Total Refund: Refund transactions.
- Net Expense: Gross Expense − Total Refund.
- Monthly Surplus: Total Income − Net Expense, before allocation.
- Allocation Contribution: gross outbound Allocation, with returns reported separately through balances.
- Allocation Target: plan values for Allocation categories.
- Allocation Target %: contribution / target.
- Expense Budget: plan values for Expense categories only.
- Budget Variance: Net Expense − Expense Budget; negative indicates under budget.
- Account Balance: cumulative natural ledger balance to the latest selected date.
- Tracked Liquid Assets: natural asset balances.
- Outstanding Debt: natural liability balances.
- Tracked Net Position: liquid assets − debt.

Definitions and source expressions are editable in the TMDL files. See Microsoft's [PBIP overview](https://learn.microsoft.com/en-us/power-bi/developer/projects/projects-overview) for project/cache management.

# Synthetic demo fixture

All figures, accounts, merchants, and notes are fictional. Each row uses a different date from 1 to 12 September 2026. Opening balances at 1 September: Bank 1,000,000 VND, Wallet 100,000 VND, Credit Card debt 0 VND. The fictional card limit is 2,000,000 VND.

| # | Type | From | To | Amount (VND) | Purpose |
|---:|---|---|---|---:|---|
| 1 | Income | | Bank | 3,000,000 | Synthetic salary |
| 2 | Expense | Bank | | 500,000 | Groceries & Essentials |
| 3 | Expense | Credit Card | | 200,000 | Shopping |
| 4 | Transfer | Bank | Credit Card | 100,000 | Card repayment |
| 5 | Transfer | Bank | Wallet | 50,000 | Wallet funding |
| 6 | Refund | | Credit Card | 20,000 | Shopping refund |
| 7 | Allocation | Bank | | 400,000 | Savings & Investment contribution |
| 8 | Allocation | | Bank | 100,000 | Allocation return |
| 9 | Transfer | Credit Card | Bank | 30,000 | Borrowing |
| 10 | Expense | Credit Card | | 10,000 | Fees & Interest |
| 11 | Refund | | Bank | 50,000 | Groceries refund |
| 12 | Adjustment | | Wallet | 5,000 | Balance correction |

Expense budgets: Groceries & Essentials 600,000, Shopping 250,000, Fees & Interest 50,000 VND. The separate Savings & Investment target is 500,000 VND.

## Expected September results

| Metric | Expected |
|---|---:|
| Bank | 3,130,000 VND |
| Wallet | 155,000 VND |
| Outstanding Debt | 120,000 VND |
| Tracked Liquid Assets | 3,285,000 VND |
| Tracked Net Position | 3,165,000 VND |
| Total Income | 3,000,000 VND |
| Gross Expense | 710,000 VND |
| Total Refund | 70,000 VND |
| Net Expense | 640,000 VND |
| Monthly Surplus | 2,360,000 VND |
| Allocation Contribution | 400,000 VND |
| Allocation Target | 500,000 VND |
| Allocation Target % | 80% |
| Expense Budget | 900,000 VND |
| Budget Variance | −260,000 VND |

These are fixture controls, not real financial results. Native Excel checks also test invalid-row exclusion and input-driven recalculation, restoring this exact fixture before saving.

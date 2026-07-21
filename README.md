# Financial Tracker v3.4 Multi-Project

## Update included

This version updates FI Upload actuals logic to support dynamic input file structures.

Required FI upload columns, in any order:

- Project
- Employee/Supplier
- Item Date
- Quantity
- UOM

Mapping:

- Project → Actuals Code
- Employee/Supplier → Actuals Name
- Item Date → Actuals Week calculated from Dashboard Start Date
- Quantity → number of hours
- UOM → must contain `Hours`

Calculation:

```text
Actual Days = total Quantity hours per Project + Employee/Supplier + Week / 8
```

Rows where UOM does not contain `Hours` are skipped and reported in the FI Upload reconciliation.

Invoice-locked actuals cells are still protected and skipped during FI Upload.

## Deployment

Replace the existing `index.html` in the FTracker GitHub repository with this `index.html`, commit to main, and allow GitHub Pages to redeploy.

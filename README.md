# Financial Tracker v3.6 Multi-Project

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


## v3.6 Location-aware actuals conversion

This version adds a required `Location` field to Forecast and FI Actuals uploads. Allowed values are:

- `IND` — FI Upload converts hours to days using 9 hours per day.
- `ANZ` — FI Upload converts hours to days using 8 hours per day.

Forecast upload required columns include: `Stream`, `Role`, `Code`, `Name`, `Location`, `Day Rate`, and `W1...Wn`.

FI Upload required columns include: `Project`, `Employee/Supplier`, `Item Date`, `Quantity`, `UOM`, and `Location`. `UOM` must contain `Hours`; `Quantity` is treated as hours and converted to days based on `Location`.

Deploy `index.html` to the FTracker repository. Keep both templates in the same folder as `index.html` if you want users to download clean upload templates.


## v3.6 changes
- Forecast upload template removes unused columns: Baseline Location, Actual Location, City, Total Days EAC, Total Revenue EAC and Revenue Variance.
- Forecast upload retains Location with allowed values IND and ANZ.
- FI Upload accepts Project, Employee/Supplier, Item Date, Quantity and UOM as required dynamic headers.
- FI Upload uses Location when provided; otherwise it derives Location from the loaded Forecast/Actuals row using Project + Employee/Supplier.
- Hours-to-days conversion: IND = Quantity / 9; ANZ = Quantity / 8.
- Rows with UOM not containing Hours are skipped. Rows where Location cannot be provided or derived are skipped and shown in reconciliation.

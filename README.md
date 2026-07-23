# Financial Tracker v3.7 Multi-Project

Replace the existing `index.html` in the FTracker GitHub repository with this version.

## FI Upload sequence

For each Project + Employee/Supplier + project week group:

1. Sum positive values in the `Days` column.
2. If the Days total is zero or absent, sum `Quantity` rows whose `UOM` contains `Hours`.
3. Convert hours to days using Location: ANZ = 8 hours/day; IND = 9 hours/day.
4. If both Days and Hours exist, Days is authoritative and Hours is used only for reconciliation cross-checking.

Column order is dynamic. Required keys are Project, Employee/Supplier and Item Date, plus Days and/or Quantity with UOM.

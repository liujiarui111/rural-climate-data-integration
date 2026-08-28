# Excel integration workflow

This document records the logic used in the workbook without exposing restricted row-level data.

## 1. Construct a record key

Each panel row receives a readable year-province-village identifier:

```excel
=D1751&"-"&E1751&"-"&F1751
```

Where:

- column D = year;
- column E = province code; and
- column F = village code.

## 2. Match geographic attributes

Geographic attributes were retrieved from the existing reference rows by matching both province code and village code:

```excel
=XLOOKUP(
  1,
  ($B$4:$B$1750=E1751)*($C$4:$C$1750=F1751),
  $G$4:$G$1750,
  "UNMATCHED"
)
```

The return range was changed for each target field, including province name, original village label, administrative levels, longitude, latitude, and village name.

## 3. Preserve auditability

- Keep the original records on a separate sheet.
- Append historical rows only on the expanded sheet.
- Use `UNMATCHED` rather than a plausible-looking substitute when no key is found.
- Review duplicate province-village combinations before accepting a match.
- Reconcile row counts by year after all formulas are populated.

## 4. Recommended production enhancement

For a future version, create a dedicated lookup table with one row per unique province-village key, validate duplicates, and use Power Query to append yearly files. This would make refreshes easier and reduce repeated formulas.


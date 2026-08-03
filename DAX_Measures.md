# DAX Measures — DePaul Applications Dashboard

All measures live in a dedicated `_Measures` table inside the Power BI data model.
Table name in Power BI: `Cleaned Data`

---

## Core Measures

### Total Applications
```dax
Total Applications = COUNTROWS('Cleaned Data')
```

### Call Log Coverage
```dax
Call Log Coverage =
DIVIDE(
  CALCULATE(COUNTROWS('Cleaned Data'), 'Cleaned Data'[Has_Call_Log]="Yes"),
  [Total Applications]
)
```

### Admitted Call Coverage
```dax
Admitted Call Coverage =
CALCULATE([Call Log Coverage], 'Cleaned Data'[Admit_Status]="Admitted")
```

### Non-Admit Call Coverage
```dax
Non-Admit Call Coverage =
CALCULATE([Call Log Coverage], 'Cleaned Data'[Admit_Status]="Not Admitted")
```

### Transcript Stall Rate
```dax
Transcript Stall Rate =
DIVIDE(
  CALCULATE(COUNTROWS('Cleaned Data'),
    'Cleaned Data'[Outcome_1] IN {
      "Missing 0 Transcript (NOT Study Group)",
      "Missing >1 Transcript (NOT Study Group)"
    }),
  CALCULATE(COUNTROWS('Cleaned Data'),
    NOT(ISBLANK('Cleaned Data'[Outcome_1])))
)
```

### Evaluation Completion Rate
```dax
Evaluation Completion Rate =
DIVIDE(
  CALCULATE(COUNTROWS('Cleaned Data'),
    'Cleaned Data'[Comments]="Evaluation Completed"),
  [Total Applications]
)
```

---

## Calculated Columns

### Has_Call_Log
```dax
Has_Call_Log =
IF(
  ISBLANK('Cleaned Data'[Outcome_1]) || 'Cleaned Data'[Outcome_1] = "N/A",
  "No",
  "Yes"
)
```
> Note: Outcome_1 uses literal "N/A" text in some rows, not a true blank — both conditions are required.

### Has_Admit_Date
```dax
Has_Admit_Date =
IF(ISBLANK('Cleaned Data'[Admit_Date]), "No", "Yes")
```

### Admit_Status
```dax
Admit_Status =
IF('Cleaned Data'[Has_Admit_Date] = "Yes", "Admitted", "Not Admitted")
```

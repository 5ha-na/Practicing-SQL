# Data Cleaning Flowchart on SQL

```mermaid
flowchart TD
    A[Raw Data Table] --> B[To inspect data, Run\nSELECT *\nFROM table\nLIMIT 100;]
    B --> C[Check for NULL values\nSELECT COUNT * - COUNT col AS nulls\nFROM table;]
    C --> D{Choose NULL handling}
    
    D -->|Option 1| E[Delete rows with NULLs\nDELETE\nFROM table\nWHERE col IS NULL;]
    D -->|Option 2| F[Fill NULLs with default\nUPDATE table\nSET col = 'Unknown'\nWHERE col IS NULL;]
    D -->|Option 3| G[Fill NULLs with average\nUPDATE table\nSET col = SELECT AVGcol FROM table \nWHERE col IS NUL]
    
    E --> H[Remove duplicate records]
    F --> H
    G --> H
    
    H --> I[Standardize text case and trim]
    I --> J[Convert to correct data types\nALTER TABLE table\nALTER COLUMN date TYPE DATE\nUSING date::DATE;]
    J --> K[Delete irrelevant records\nDELETE FROM table\nWHERE status = 'test';]
    K --> L[Add derived columns]
    L --> M[Add data validation rules]
    M --> N[Final Clean Table]
```
| Step | SQL Command Example |
|------|---------------------|
| 1. Raw Table | `SELECT * FROM raw_table;` |
| 2. Inspect Data | `SELECT * FROM table LIMIT 100;` |
| 3. Find NULLs | `SELECT COUNT(*) - COUNT(col) AS nulls FROM table;` |
| 4. Handle NULLs | `DELETE WHERE col IS NULL;` or `UPDATE SET col = 'Unknown';` |
| 5. Remove Duplicates | `DELETE FROM table USING (SELECT ... ROW_NUMBER() OVER(...))` |
| 6. Standardize Text | `UPDATE table SET name = UPPER(TRIM(name));` |
| 7. Convert Data Types | `ALTER TABLE table ALTER COLUMN date TYPE DATE;` |
| 8. Filter Rows | `DELETE FROM table WHERE status = 'test';` |
| 9. Add Calculated Columns | `ALTER TABLE table ADD COLUMN full_name TEXT;` |
| 10. Apply Constraints | `ALTER TABLE table ADD CHECK (age >= 0);` |

<!-- Vehicle Registry Dataset (500,000 rows)

Schema:

* vin (String)
* model (String)
* mfg_year (Integer)
* fuel_type (String)
* base_kmpl (Float)

Edge Cases Included:

1. Missing VIN values
2. Invalid VIN length (< 5 characters)
3. Null / empty model names
4. Manufacturing year anomalies:

   * Null values
   * Negative values
   * Future years (> current year)
   * Non-integer values (e.g., 'abcd')
   * Unrealistic values (e.g., 0, 3000)
5. Fuel type anomalies:

   * Null / empty
   * Invalid strings like 'UNKNOWN$$$', 'WATER', '123'
6. base_kmpl anomalies:

   * Null values
   * Negative values (e.g., -5)
   * Zero values (0)
   * Non-numeric values (e.g., 'ten')
   * Extremely high or unrealistic values
7. Duplicate patterns may exist
8. Mixed valid and invalid fields within the same row
9. Whitespace-only strings in text fields

Corrupted Data Strategy:

* Rows with invalid VIN (null or length < 5) → reject
* Invalid mfg_year → cast or mark as invalid
* Unknown fuel types → map to 'UNKNOWN'
* Null model → fill with 'UNKNOWN_MODEL'
* Invalid base_kmpl → cast to float or mark as null
* Negative or zero base_kmpl → treat as invalid

Purpose:

* Helps simulate real-world dirty data pipelines
* Useful for building bronze → silver → gold cleaning logic
* Enables testing of data validation and transformation rules
* Suitable for PySpark, AWS Glue, and ETL pipeline development -->



Vehicle Registry Dataset (200,000 rows)

Schema:

* vin (String)
* model (String)
* mfg_year (Integer)
* fuel_type (String)

Edge Cases Included:

1. Missing VIN values
2. Invalid VIN length (< 5 characters)
3. Null / empty model names
4. Manufacturing year anomalies:

   * Null values
   * Negative values
   * Future years (> current year)
   * Non-integer values (e.g., 'abcd')
   * Unrealistic values (e.g., 0, 3000)
5. Fuel type anomalies:

   * Null / empty
   * Invalid strings like 'UNKNOWN$$$', 'WATER', '123'
6. Duplicate patterns may exist
7. Mixed valid and invalid fields within the same row
8. Whitespace-only strings in text fields

Corrupted Data Strategy:

* Rows with invalid VIN (null or length < 5) → reject
* Invalid mfg_year → cast or mark as invalid
* Unknown fuel types → map to 'UNKNOWN'
* Null model → fill with 'UNKNOWN_MODEL'

Purpose:

* Master dimension table for vehicles
* Helps simulate real-world dirty data pipelines
* Useful for building bronze → silver → gold cleaning logic
* Join base for all other datasets

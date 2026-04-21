Vehicle Assignment Dataset (200,000 rows)

Schema:

* vin (String)
* driver_id (String)
* start_timestamp (Unix Timestamp)
* end_timestamp (Unix Timestamp / Null)
* daily_rate (Float)
* region (String)

Frequency:

* Daily at 00:00 UTC (Incremental)

Edge Cases Included:

1. Missing VIN values
2. Invalid VIN length (< 5 characters)
3. Invalid driver_id formats (null, missing prefix, numeric only)
4. Timestamp anomalies:

   * Null values
   * Negative timestamps
   * Non-numeric values (e.g., 'abcd')
   * end_timestamp earlier than start_timestamp
5. Overlapping driver assignments for same VIN
6. Missing end_timestamp for active drivers
7. daily_rate anomalies:

   * Null values
   * Negative values
   * Zero values
   * Non-numeric values (e.g., 'ten')
8. Region anomalies:

   * Null / empty
   * Invalid strings like 'UNKNOWN$$$'

Corrupted Data Strategy:

* Invalid VIN → reject
* Invalid timestamps → convert or mark invalid
* end_timestamp < start_timestamp → flag inconsistency
* Invalid driver_id → map to 'UNKNOWN_DRIVER'
* Invalid daily_rate → cast or mark null
* Invalid region → map to 'UNKNOWN'

Data Handling:

* Convert Unix timestamps to date format
* Ensure continuity of driver assignments per VIN
* Resolve overlapping assignments

Purpose:

* Tracks driver transitions and cost per vehicle
* Useful for driver performance and utilization analysis
* Supports incremental ETL pipelines

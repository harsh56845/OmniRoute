Maintenance Schedules Dataset (200,000 rows)

Schema:

* vin (String)
* service_date (Date)
* service_type (String)

Frequency:

* Yearly / Scheduled events

Edge Cases Included:

1. Missing VIN values
2. Invalid VIN format
3. service_date anomalies:

   * Null values
   * Invalid date formats
   * Future or unrealistic dates
4. service_type anomalies:

   * Null / empty
   * Invalid strings like 'UNKNOWN$$$'
5. Duplicate maintenance records
6. Multiple services on same date
7. Missing service_type

Corrupted Data Strategy:

* Invalid VIN → reject
* Invalid dates → cast or mark invalid
* Missing service_type → fill with 'UNKNOWN_SERVICE'

Purpose:

* Represents vehicle downtime
* Helps calculate availability and utilization
* Supports maintenance analytics in data pipelines

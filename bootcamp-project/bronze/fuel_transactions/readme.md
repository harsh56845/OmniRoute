Fuel Transactions Dataset (200,000 rows)

Schema:

* transaction_id (String)
* vin (String)
* fuel_liters (Float)
* odometer_reading (Float)
* timestamp (UTC)

Frequency:

* Daily at 07:00 UTC

Edge Cases Included:

1. Missing VIN values
2. Invalid transaction_id
3. fuel_liters anomalies:

   * Null values
   * Negative values
   * Non-numeric values (e.g., 'ten')
4. odometer_reading anomalies:

   * Negative values
   * Sudden drops (rollback)
   * Unrealistic jumps
5. Timestamp anomalies:

   * Null values
   * Invalid format
6. Duplicate transactions

Corrupted Data Strategy:

* Invalid VIN → reject
* Invalid fuel values → cast or mark null
* Odometer rollback → flag anomaly
* Invalid timestamp → convert or discard

Purpose:

* Used to calculate fuel efficiency
* Enables cost and performance analysis
* Supports KPI like km/l and fuel consumption trends

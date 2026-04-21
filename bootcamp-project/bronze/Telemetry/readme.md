Telemetry Stream Dataset (200,000 records)

Schema:

* vin (String)
* driver_id (String)
* speed (Integer)
* lat (Float)
* long (Float)
* event_timestamp (Unix Timestamp)

Frequency:

* Real-time (Kafka Stream)

Edge Cases Included:

1. Missing VIN or driver_id
2. Invalid VIN format (short length, null, empty)
3. Invalid driver_id formats (null, numeric-only, missing prefix)
4. Speed anomalies:

   * Negative values
   * Extremely high speeds (> 150, e.g., 200, 999)
   * Sudden spikes in speed
5. Location anomalies:

   * Invalid latitude/longitude values (e.g., 999, -999)
   * Out-of-bound coordinates
   * Null location values
6. Timestamp anomalies:

   * Null values
   * Negative timestamps
   * Non-numeric values (e.g., 'abcd')
7. Missing fields in JSON objects
8. Duplicate or repeated events
9. Mixed valid and corrupted fields in the same record

Corrupted Data Strategy:

* Invalid VIN → discard record
* Invalid driver_id → map to 'UNKNOWN_DRIVER'
* Invalid coordinates → flag as anomaly
* Speed > threshold → trigger safety alert
* Invalid timestamp → cast or discard
* Missing fields → mark record as incomplete

Purpose:

* Simulates real-time vehicle telemetry data
* Enables safety monitoring and alert generation
* Supports streaming analytics (Kafka + Spark)
* Used for detecting overspeeding and risky driving behavior

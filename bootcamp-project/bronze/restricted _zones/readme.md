Restricted Zones Dataset (5,000 records)

Schema:

* zone_name (String)
* min_lat (Float)
* max_lat (Float)
* min_long (Float)
* max_long (Float)

Frequency:

* Static / Updated on demand

Edge Cases Included:

1. Missing zone_name
2. Invalid zone names (null, empty, 'UNKNOWN$$$')
3. Coordinate anomalies:

   * Null values
   * Invalid latitude/longitude (e.g., 999, -999)
   * Out-of-bound coordinates
4. Boundary issues:

   * min_lat > max_lat
   * min_long > max_long
5. Overlapping zones
6. Duplicate zones
7. Incomplete zone definitions
8. Extremely large or unrealistic geographic ranges

Corrupted Data Strategy:

* Invalid coordinates → reject or flag
* Incorrect boundaries → swap or mark invalid
* Missing zone_name → assign 'UNKNOWN_ZONE'
* Overlapping zones → allow but flag for review
* Duplicate zones → deduplicate in processing

Purpose:

* Defines geofenced restricted areas
* Used for safety strike detection when vehicles enter restricted zones
* Supports geospatial analytics and rule-based alerting
* Works with telemetry stream for real-time monitoring

# Redis TimeSeries


is the space efficiency and higher speed a dedicated solution can bring over a generic database.


the writing load is much higher than the reading load

Example IOT Sensors, send data routinely but querying them usually occurs at lower rate.


RedisTimeSeries has features / advantages over others:

* High volume inserts, low latency reads
* Query by start time and end-time
* Aggregated queries (Min, Max, Avg, Sum, Range, Count, First, Last) for any time bucket
* Configurable maximum retention period
* Downsampling/Compaction
* automatically updated aggregated timeseries
* Secondary index - each time series has labels (field value pairs) which will allows to query by labels

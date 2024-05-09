# MicroServo

MicroServo, is an overall dataset for analyzing operation problems such as anomaly detection, failure classification, root cause analysis, etc.

## Quick Start
The MicroServo dataset consists of three days of data collected from the MicroServo platform. The fault scenarios include Pod failure, CPU and Memory stress, and faults related to network and HTTP types. It also provides the ground truth of fault injection.

### Metric
MicroServo includes 15 container-level metrics and 10 service-level metrics, each stored in separate CSV files. The format for these files is as follows: (timestamp, cmdb_id, kpi_name, value), where each line represents a value sampled from all instances of a service. The sampling frequency is set at 60 second.

| timestamp   | cmdb_id   | kpi_name   | value   |
| ----------- | -------   | -------   | -------   |
| 1715124412  | observe.cartservice-0 | container_memory_cache | 30363648 |

- timestamp: the time of data collection: 10-bit timestamp
- cmdb_id: node name and instance name
- kpi_name: metric name
- value: value of metric at the timestamp

### Trace
The traces in MicroServo is stored in a CSV format, capturing the intricate web of service requests. The CSV file is meticulously structured with columns that consist of: (timestamp, cmdb_id, span_id, trace_id, duration, type,
status_code, operation_name, parent_span).

| timestamp   | cmdb_id   | span_id   | trace_id   | duration   | type   | status_code   | operation_name   | parent_span   |
| ----------- | --------   | -------   | -------   | -------   | -------   | -------   | -------   | -------   |
| 1711036800122210  | frontend-0 | 6ced3c24a24da73e | 6ced3c24a24da73ead6eb3325d860ea4 | 11199 | request | 0 | /hipstershop.FrontendService/ProductGrpc	| 6ced3c24a24da73e

- timestamp: 16-bit of time record
- cmdb_id: the identifier of the specific service instance participating in the trace
- span_id: the unique identifier for the current service invocation within the trace
- trace_id: overarching identifier that aggregates all related spans for a full transaction across the system
- duration: the execution time (milliseconds) for the individual trace,
- type: protocol, such as gRPC or HTTPS
- status_code: the response status for the invocation
- operation_name: the method of operation
- parent_span: ID of the preceding request in the call hierarchy

### Log
The logs within MicroServo are preserved in a CSV file. Each row in the CSV file corresponds to an individual log entry, representing a singular event or state captured by the microservice’s logging system. And the format of the CSV file is composed of the following columns: (log_id, timestamp, date, cmdb_id, value). 

| log_id   | timestamp   | date   | cmdb_id   | message   |
| ----------- | -------   | -------   | -------   | -------   |
| v-UeFo8BSpQAhE0cMNiy  | 1714060800 | 2024-04-25T16:00:00.237Z | shippingservice-0 | level:debug,message:gathering metrics |

- log_id: the identifier of log entry
- timestamp: 10-bit of time record
- date: string of time record with the form YYYY-MM-DD hh:mm:ss
- cmdb_id: the identifier of the microservice instance from which the log was generated. 
- value: the actual message content of the log entry.

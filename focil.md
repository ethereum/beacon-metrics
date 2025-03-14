# FOCIL Metrics

The following metrics are proposed to be added to clients for FOCIL monitoring. This list is open for discussion. Each client has the opportunity to contribute to it by suggesting additions or disputing existing metrics.

| Name | Metric type | Usage | Sample collection event |
|--------------------------------------------|-------------|-------------------------------------------------------------|----------------------|
| `beacon_inclusion_list_size_bytes_total`            | Counter   | Byte size of the inclusion list  |      |
| `beacon_validated_inclusion_list_total`           | Counter   | Number of validated inclusion lists |      |
| `beacon_inclusion_list_validation_time_milliseconds `  | Histogram | Total time to validate inclusion list  |  |
| `beacon_get_inclusion_list_v1_total`           | Counter   | Number of requested inclusion lists |      |
| `beacon_get_inclusion_list_v1_latency_milliseconds `  | Histogram | RPC latency for getInclusionListV1 |  |
| `beacon_update_payload_with_inclusion_list_total`  | Counter   | Count the number of execution payloads with inclusion lists |    |
| `beacon_update_payload_with_inclusion_list_v1_latency_milliseconds`  | Histogram | RPC latency for updatePayloadWithInclusionListV1   |   |
| `beacon_inclusion_list_submitted_for_rpc_total`  | Counter   | Number of inclusion lists submitted for rpc |     |


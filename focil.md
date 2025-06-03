# FOCIL Metrics

The following metrics are proposed to be added to clients for FOCIL monitoring. This list is open for discussion. Each client has the opportunity to contribute to it by suggesting additions or disputing existing metrics.

| Name | Metric type | Usage | Sample collection event |
|--------------------------------------------|-------------|-------------------------------------------------------------|----------------------|
| `beacon_inclusion_lists_size_bytes_total`            | Counter   | Byte size of the inclusion list  |      |
| `beacon_inclusion_lists_validated_total`           | Counter   | Number of validated inclusion lists |      |
| `beacon_inclusion_lists_validation_time_seconds`  | Histogram | Time to validate inclusion list  |  |
| `beacon_get_inclusion_list_v1_total`           | Counter   | Number of getInclusionListV1 requests |      |
| `beacon_get_inclusion_list_v1_latency_seconds`  | Histogram | Latency for getInclusionListV1 |  |
| `beacon_update_payload_with_inclusion_list_v1_total`  | Counter   | Number of updatePayloadWithInclusionListV1 requests |    |
| `beacon_update_payload_with_inclusion_list_v1_latency_seconds`  | Histogram | Latency for updatePayloadWithInclusionListV1   |   |
| `beacon_inclusion_lists_submitted_for_rpc_total`  | Counter   | Number of inclusion lists submitted for RPC |     |
| `beacon_inclusion_lists_cached_total`  | Counter   | Number of cached inclusion lists in slot N-1 |     |


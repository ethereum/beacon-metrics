# FOCIL Metrics

The following metrics are proposed to be added to clients for FOCIL monitoring. This list is open for discussion. Each client has the opportunity to contribute to it by suggesting additions or disputing existing metrics.

| Name | Metric type | Usage | Sample collection event | Labels | Buckets |
|------|-------------|-------|-------------------------|--------|---------|
| `beacon_inclusion_lists_valid_total`| Counter | Total number of valid inclusion lists | On inclusion list validation | **source:** gossip, api | |
| `beacon_inclusion_lists_invalid_total`| Counter | Total number of invalid inclusion lists | On inclusion list validation | **source**: gossip, api; **reason**: unknown, [REJECT/IGNORE from specs](https://github.com/ethereum/consensus-specs/blob/master/specs/_features/eip7805/p2p-interface.md#inclusion_list) | |
| `beacon_inclusion_lists_valid_size_bytes_total`| Counter | Total size of valid inclusion lists in bytes  | On inclusion list validation | | |
| `beacon_inclusion_lists_invalid_size_bytes_total`| Counter | Total size of invalid inclusion lists in bytes  | On inclusion list validation | | |
| `beacon_inclusion_lists_validation_time_seconds`| Histogram | Time taken to validate inclusion lists | On inclusion list validation | **source**: gossip, api | 0.1, 0.25, 0.5, 0.75, 1, 2 |
| `beacon_inclusion_lists_received_total`| Counter | Total number of received inclusion lists | On receiving inclusion list | **source**: gossip, api | |
| `beacon_inclusion_list_transactions_received_total`| Counter | Total number of transactions in received inclusion lists | On receiving inclusion list | **source**: gossip, api | |
| `beacon_inclusion_lists_published_total`| Counter | Total number of published inclusion lists | On publishing inclusion list | | |
| `beacon_inclusion_lists_arrival_time_seconds`| Histogram | Inclusion list arrival time since the beginning of slot | On receiving inclusion list | | 0, 1, 2, 3, 4, 6, 8, 9, 10, 11, 12 |
| `beacon_inclusion_lists_equivocating_total`| Counter | Total number of equivocating inclusion lists | Fork-choice `on_inclusion_list` | | |
| `beacon_inclusion_list_unsatisfied_blocks_total`| Counter | Total number of unsatisfied inclusion list blocks | Fork-choice `on_block` | | |
| `beacon_inclusion_list_transactions_sent_to_payload_total`| Counter | Total number of inclusion list transactions sent to payload | On `notify_new_payload` | | |
| `beacon_engine_getInclusionListV1_requests_total`| Counter | Total number of engine_getInclusionListV1 requests sent | On `engine_getInclusionListV1` | | |
| `beacon_engine_getInclusionListV1_requests_duration_seconds`| Histogram | Duration of engine_getInclusionListV1 requests| On `engine_getInclusionListV1` | | 0.005, 0.01, 0.025, 0.05, 0.075, 0.1, 0.5 |

## Clients implementations

| Metric | Grandine | Lighthouse | Lodestar | Nimbus | Prysm | Teku |
|--------|----------|------------|----------|--------|-------|------|
| `beacon_inclusion_lists_valid_total`| □ | □ | ✅ | □ | □ | □ |
| `beacon_inclusion_lists_invalid_total`| □ | □ | ✅ | □ | □ | □ |
| `beacon_inclusion_lists_valid_size_bytes_total`| □ | □ | ✅ | □ | □ | □ |
| `beacon_inclusion_lists_invalid_size_bytes_total`| □ | □ | ✅ | □ | □ | □ |
| `beacon_inclusion_lists_validation_time_seconds`| □ | □ | ✅ | □ | □ | □ |
| `beacon_inclusion_lists_received_total`| □ | □ | ✅ | □ | □ | □ |
| `beacon_inclusion_list_transactions_received_total`| □ | □ | ✅ | □ | □ | □ |
| `beacon_inclusion_lists_published_total`| □ | □ | ✅ | □ | □ | □ |
| `beacon_inclusion_lists_arrival_time_seconds`| □ | □ | ✅ | □ | □ | □ |
| `beacon_inclusion_lists_equivocating_total`| □ | □ | ✅ | □ | □ | □ |
| `beacon_inclusion_list_unsatisfied_blocks_total`| □ | □ | ✅ | □ | □ | □ |
| `beacon_inclusion_list_transactions_sent_to_payload_total`| □ | □ | ✅ | □ | □ | □ |
| `beacon_engine_getInclusionListV1_requests_total`| □ | □ | ✅ | □ | □ | □ |
| `beacon_engine_getInclusionListV1_requests_duration_seconds`| □ | □ | ✅ | □ | □ | □ |
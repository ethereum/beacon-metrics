# Execution Layer Metrics

- [Beacon Chain Metrics](#beacon-chain-metrics)
    - [Slot](#slot)
    - [Epoch](#epoch)
- [Validator Metrics](#validator-metrics)
    - [Validators](#validators)
    - [Attestations](#attestations)
- [Fork-choice Metrics](#fork-choice-metrics)
    - [Reorgs](#reorgs)
- [Network Metrics](#network-metrics)
    - [ReqResp](#reqresp)
    - [Gossip](#gossip)
    - [Beacon API](#beacon-api)
    - [Peers](#peers)    


## Beacon Chain Metrics

### Slot

| Name | Type | Usage | Sample collection event | Grandine | Lighthouse | Lodestar | Nimbus | Prysm | Teku |
|--------|-------|-------|-------------------------|----------|------------|----------|--------|-------|------|
| `beacon_head_slot` | Gauge | Latest slot of the beacon chain | On fork choice | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |


### Epoch

| Name | Type | Usage | Sample collection event | Grandine | Lighthouse | Lodestar | Nimbus | Prysm | Teku |
|--------|-------|-------|-------------------------|----------|------------|----------|--------|-------|------|
| `beacon_finalized_epoch`                   | Gauge       | Current finalized epoch                                     | On epoch transition  | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| `beacon_current_justified_epoch`           | Gauge       | Current justified epoch                                     | On epoch transition  | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| `beacon_previous_justified_epoch`          | Gauge       | Current previously justified epoch                          | On epoch transition  | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |

## Validator Metrics

### Validators

| Name | Type | Usage | Sample collection event | Grandine | Lighthouse | Lodestar | Nimbus | Prysm | Teku |
|--------|-------|-------|-------------------------|----------|------------|----------|--------|-------|------|
| `beacon_current_validators`                   | Gauge       | Number of `status="pending\|active\|exited\|withdrawable"` validators in current epoch  | On epoch transition |
| `beacon_current_active_validators`         | Gauge       | Current total active validators                             | On epoch transition  | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| `beacon_previous_validators`                  | Gauge       | Number of `status="pending\|active\|exited\|withdrawable"` validators in previous epoch | On epoch transition | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| `beacon_current_live_validators`              | Gauge       | Number of active validators that successfully included attestation on chain for current epoch     | On block  | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| `beacon_previous_live_validators`             | Gauge       | Number of active validators that successfully included attestation on chain for previous epoch    | On block  | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| `beacon_processed_deposits_total`          | Gauge       | Total number of deposits processed                          | On epoch transition  | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| `beacon_pending_deposits`                     | Gauge       | Number of pending deposits (`state.eth1_data.deposit_count - state.eth1_deposit_index`)           | On block  | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| `beacon_processed_deposits_total`             | Gauge       | Number of total deposits included on chain                                                        | On block  | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| `beacon_pending_exits`                        | Gauge       | Number of pending voluntary exits in local operation pool                                         | On slot   | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| `beacon_previous_epoch_orphaned_blocks`       | Gauge       | Number of blocks orphaned in the previous epoch                                         | On epoch transition | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| `gossipsub_mesh_peers_per_main_topic`         | Gauge       | Number of peers per gossipsub topic                                                     | On slot             | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| `beacon_attestation_delay_count`              | Histogram   | Attestation delay count, bucket size yet to be decided                                  | On epoch transition | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| `local_validator_count`                       | Gauge       | Count of the number of local validators                                                 | On slot             | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| `store_beacon_block_cache_hit_total`          | Gauge       | Total number of block cache hits                                                        | On epoch transition | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| `beacon_state_data_cache_misses_total`        | Gauge       | Total number of block cache misses                                                      | On epoch transition | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| `beacon_head_state_finalized_root`            | Gauge       | Current finalized root*                                                                 | On epoch transition | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| `beacon_previous_justified_root`              | Gauge       | Current previously justified root*                                                      | On epoch transition | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| `beacon_aggregates_received_total`            | Gauge       | Total number of aggregates received                                                     | On epoch transition | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| `beacon_block_delay_count`                    | Histogram   | Block delay count, bucket size yet to be decided                                                  | On slot   | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| `beacon_attestor_slashing_received_total`     | Gauge       | Total number of attestor slashing received                                              | On epoch transition | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| `beacon_block_proposed_total`                 | Gauge       | Total number of blocks proposed                                                         | On epoch transition | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| `beacon_processor_gossip_block_imported_total`| Gauge       | Total number of imported blocks                                                         | On epoch transition | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| `libp2p_pubsub_validation_failure_total`      | Gauge       | Number of pubsub validation messages failed                                             | On epoch transition | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| `beacon_head_state_root`                      | Gauge       | Head state root                                                                                     | On slot | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| `beacon_attestations_received_total`          | Gauge       | Total number of attestations received                                                   | On epoch transition | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| `beacon_attestor_slashing_created_total`      | Gauge       | Total number of slashing created                                                        | On epoch transition | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| `beacon_http_api_requests_total`              | Gauge       | Total number of requests to the HTTP API endpoint                                                 | On slot   | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| `beacon_http_api_successes_total`             | Gauge       | Total number of successful requests to the HTTP API endpoint                                      | On slot   | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| `beacon_sync_state`                           | Gauge       | Beacon sync state, 0 for not syncing, 1 for synced, 2 for syncing                                 | On slot   | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| `process_cpu_seconds_total`                   | Gauge       | Total CPU time in seconds                                                                         | On slot   | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| `process_max_fds`                             | Gauge       | Maximum number of file descriptors                                                                | On slot   | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |

\* All `*_root` values are converted to signed 64-bit integers utilizing the last 8 bytes interpreted as little-endian (`int.from_bytes(root[24:32], byteorder='little', signed=True)`).
    
### Attestations

| Name | Type | Usage | Sample collection event | Grandine | Lighthouse | Lodestar | Nimbus | Prysm | Teku |
|--------|-------|-------|-------------------------|----------|------------|----------|--------|-------|------|
| `beacon_attestations_published_total` | Gauge | Total number of attestations proposed | On epoch transition |

## Fork-choice Metrics

### Head

| Name | Type | Usage | Sample collection event | Grandine | Lighthouse | Lodestar | Nimbus | Prysm | Teku |
|--------|-------|-------|-------------------------|----------|------------|----------|--------|-------|------|
| `beacon_head_slot` | Gauge | Latest slot of the beacon chain | On fork choice | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |

### Reorgs
| Name | Type | Usage | Sample collection event | Grandine | Lighthouse | Lodestar | Nimbus | Prysm | Teku |
|--------|-------|-------|-------------------------|----------|------------|----------|--------|-------|------|
| `beacon_reorgs_total`                      | Counter     | Total number of chain reorganizations                       | On fork choice       | ✅ | ✅ | ✅ | ✅ | `beacon_reorgs` | ✅ |

## Network Metrics

### ReqResp

| Name | Type | Usage | Sample collection event | Grandine | Lighthouse | Lodestar | Nimbus | Prysm | Teku |
|--------|-------|-------|-------------------------|----------|------------|----------|--------|-------|------|

### Gossip

| Name | Type | Usage | Sample collection event | Grandine | Lighthouse | Lodestar | Nimbus | Prysm | Teku |
|--------|-------|-------|-------------------------|----------|------------|----------|--------|-------|------|

### Beacon API

| Name | Type | Usage | Sample collection event | Grandine | Lighthouse | Lodestar | Nimbus | Prysm | Teku |
|--------|-------|-------|-------------------------|----------|------------|----------|--------|-------|------|

### Peers

| Name | Type | Usage | Sample collection event | Grandine | Lighthouse | Lodestar | Nimbus | Prysm | Teku |
|--------|-------|-------|-------------------------|----------|------------|----------|--------|-------|------|
| `libp2p_peers` | Gauge | Tracks the total number of libp2p peers | On peer add/drop | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |

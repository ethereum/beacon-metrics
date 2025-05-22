# Beacon chain metrics

## Introduction

This specification encodes the behavior of sampling and collection of metrics by beacon chain clients.

This specification is informative, and implementations are not required to implement all recommendations.

## Metrics

This section defines a set of metrics to be sampled by beacon chain clients.

### Rationale

The metrics SHOULD behave under the guidelines set by the [Prometheus documentation](https://prometheus.io/docs/practices/instrumentation/#things-to-watch-out-for).

### Interop Metrics

The following are the minimal metrics agreed to be conformed by the various client teams. 

| Name | Metric type | Usage | Sample collection event |
|--------------------------------------------|-------------|-------------------------------------------------------------|----------------------|
| `libp2p_peers               `              | Gauge       | Tracks the total number of libp2p peers                     | On peer add/drop     |
| `beacon_head_slot`                         | Gauge       | Latest slot of the beacon chain                             | On fork choice       |
| `beacon_finalized_epoch`                   | Gauge       | Current finalized epoch                                     | On epoch transition  |
| `beacon_current_justified_epoch`           | Gauge       | Current justified epoch                                     | On epoch transition  |
| `beacon_previous_justified_epoch`          | Gauge       | Current previously justified epoch                          | On epoch transition  |
| `beacon_current_active_validators`         | Gauge       | Current total active validators                             | On epoch transition  |
| `beacon_reorgs_total`                      | Counter     | Total number of chain reorganizations                       | On fork choice       |
| `beacon_processed_deposits_total`          | Gauge       | Total number of deposits processed                          | On epoch transition  |

\* All `*_root` values are converted to signed 64-bit integers utilizing the last 8 bytes interpreted as little-endian (`int.from_bytes(root[24:32], byteorder='little', signed=True)`).

### PeerDAS Metrics

The following metrics are proposed to be added to clients for PeerDAS monitoring. This list is open for discussion. Each client has the opportunity to contribute to it by suggesting additions or disputing existing metrics.

#### Data column, kzg, custody metrics

| Name | Metric type | Usage | Sample collection event |
|--------------------------------------------|-------------|-------------------------------------------------------------|----------------------|
| `beacon_data_column_sidecar_processing_requests_total`            | Counter   | Number of data column sidecars submitted for processing                     | On data column sidecar gossip verification     |
| `beacon_data_column_sidecar_processing_successes_total`           | Counter   | Number of data column sidecars verified for gossip                         | On data column sidecar gossip verification     |
| `beacon_data_column_sidecar_gossip_verification_seconds`          | Histogram | Full runtime of data column sidecars gossip verification                   | On data column sidecar gossip verification     |
| `beacon_data_availability_reconstructed_columns_total`            | Counter   | Total count of reconstructed columns                                      | On data column kzg verification  |
| `beacon_data_availability_reconstruction_time_seconds`            | Histogram | Time taken to reconstruct columns                                      | On data column kzg verification  |
| `beacon_data_column_sidecar_computation_seconds`                  | Histogram | Time taken to compute data column sidecar, including cells, proofs and inclusion proof                |  On data column sidecar computation            |
| `beacon_data_column_sidecar_inclusion_proof_verification_seconds` | Histogram | Time taken to verify data column sidecar inclusion proof                          |  On data column sidecar inclusion proof verification  |
| `beacon_kzg_verification_data_column_single_seconds`             | Histogram | Runtime of single data column kzg verification                                 | On single data column kzg verification  |
| `beacon_kzg_verification_data_column_batch_seconds`               | Histogram | Runtime of batched data column kzg verification                                 | On batched data column kzg verification |
| `beacon_custody_groups` | Gauge | Total number of custody groups within a node | On updating custody group count |
| `beacon_custody_groups_backfilled` | Gauge | Total number of custody groups backfilled by a node | On syncing |
| `beacon_engine_getBlobsV2_requests_total` | Counter |  Total number of `engine_getBlobsV2` requests sent | On sending `engine_getBlobsV2` requests | 
| `beacon_engine_getBlobsV2_responses_total` | Counter | Total number of `engine_getBlobsV2` successful responses received | On receiving `engine_getBlobsV2` responses |
| `beacon_engine_getBlobsV2_runtime_seconds` | Histogram | Full runtime of `engine_getBlobsV2` requests | On `engine_getBlobsV2` request completion

### Additional Metrics

The following are proposed metrics to be added to clients. This list is _not_ stable and is subject to drastic changes, deletions, and additions. The additional metric list is being
discussed, we are yet to reach consensus. Ideally we would also discuss which of these values need to be counters, guages or histograms. 

| Name | Metric type | Usage | Sample collection event |
|----------------------------------------------|-------------|--------------------------------------------------------------------------------------|---------------------|
| `beacon_current_validators`                   | Gauge       | Number of `status="pending\|active\|exited\|withdrawable"` validators in current epoch  | On epoch transition |
| `beacon_previous_validators`                  | Gauge       | Number of `status="pending\|active\|exited\|withdrawable"` validators in previous epoch | On epoch transition |
| `beacon_current_live_validators`              | Gauge       | Number of active validators that successfully included attestation on chain for current epoch     | On block  |
| `beacon_previous_live_validators`             | Gauge       | Number of active validators that successfully included attestation on chain for previous epoch    | On block  |
| `beacon_pending_deposits`                     | Gauge       | Number of pending deposits (`state.eth1_data.deposit_count - state.eth1_deposit_index`)           | On block  |
| `beacon_processed_deposits_total`             | Gauge       | Number of total deposits included on chain                                                        | On block  |
| `beacon_pending_exits`                        | Gauge       | Number of pending voluntary exits in local operation pool                                         | On slot   |
| `beacon_previous_epoch_orphaned_blocks`       | Gauge       | Number of blocks orphaned in the previous epoch                                         | On epoch transition |
| `gossipsub_mesh_peers_per_main_topic`         | Gauge       | Number of peers per gossipsub topic                                                     | On slot             |
| `beacon_attestation_delay_count`              | Histogram   | Attestation delay count, bucket size yet to be decided                                  | On epoch transition |
| `local_validator_count`                       | Gauge       | Count of the number of local validators                                                 | On slot             |
| `store_beacon_block_cache_hit_total`          | Gauge       | Total number of block cache hits                                                        | On epoch transition |
| `beacon_state_data_cache_misses_total`        | Gauge       | Total number of block cache misses                                                      | On epoch transition |
| `beacon_head_state_finalized_root`            | Gauge       | Current finalized root*                                                                 | On epoch transition |
| `beacon_previous_justified_root`              | Gauge       | Current previously justified root*                                                      | On epoch transition |
| `beacon_aggregates_received_total`            | Gauge       | Total number of aggregates received                                                     | On epoch transition |                                                   
| `beacon_block_delay_count`                    | Histogram   | Block delay count, bucket size yet to be decided                                                  | On slot   |
| `beacon_attestor_slashing_received_total`     | Gauge       | Total number of attestor slashing received                                              | On epoch transition | 
| `beacon_block_proposed_total`                 | Gauge       | Total number of blocks proposed                                                         | On epoch transition | 
| `beacon_attestations_published_total`         | Gauge       | Total number of attestations proposed                                                   | On epoch transition | 
| `beacon_processor_gossip_block_imported_total`| Gauge       | Total number of imported blocks                                                         | On epoch transition | 
| `libp2p_pubsub_validation_failure_total`      | Gauge       | Number of pubsub validation messages failed                                             | On epoch transition | 
| `beacon_head_state_root`                      | Gauge       | Head state root                                                                                     | On slot | 
| `beacon_attestations_received_total`          | Gauge       | Total number of attestations received                                                   | On epoch transition |
| `beacon_attestor_slashing_created_total`      | Gauge       | Total number of slashing created                                                        | On epoch transition |
| `beacon_http_api_requests_total`              | Gauge       | Total number of requests to the HTTP API endpoint                                                 | On slot   |
| `beacon_http_api_successes_total`             | Gauge       | Total number of successful requests to the HTTP API endpoint                                      | On slot   |
| `beacon_sync_state`                           | Gauge       | Beacon sync state, 0 for not syncing, 1 for synced, 2 for syncing                                 | On slot   |
| `process_cpu_seconds_total`                   | Gauge       | Total CPU time in seconds                                                                         | On slot   |
| `process_max_fds`                             | Gauge       | Maximum number of file descriptors                                                                | On slot   |
    

### Labels

The metrics should be collected without labels unless specified. The collection process might add additional labels as metadata regarding the machine and build information.

## Prometheus metrics collection

A beacon chain client using Prometheus for metrics collection SHOULD conform to the following:

* Beacon chain clients SHOULD configure [Prometheus](https://prometheus.io/) so that it exposes metrics collection over an HTTP port.
* Beacon chain clients MAY elect to secure the HTTP endpoint by restricting network access and applying Prometheus security settings, according to Prometheus [best practices](https://prometheus.io/docs/operating/security/).
* Beacon chain clients SHOULD allow configuration flags to set the network interface and the port the Prometheus collection endpoint will be served from.
* By default, the Prometheus collection endpoint SHOULD be served from 0.0.0.0:8008.

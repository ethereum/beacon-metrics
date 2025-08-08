# EIP-7594 Metrics (PeerDAS)

## Fork Overview & Metrics Tracking Reference

| Fork Half | EIP | Metrics | Grandine | Lighthouse | Lodestar | Nimbus | Prysm | Teku |
|-----------|-----|--------- | -------- | ---------- | -------- | ------ | ----- | ---- |
| [Fulu (CL)](fusaka-cl-index.md) | [EIP-7594](https://eips.ethereum.org/EIPS/eip-7594)  | 13  | 3 | 8 | 12 | 6 | 8 | 13 |

## Metrics

### Beacon

| Metric | Usage | Sample collection event | Grandine | Lighthouse | Lodestar | Nimbus | Prysm | Teku |
|--------|-------|-------------------------|----------|------------|----------|--------|-------|------|
| `beacon_data_availability_reconstructed_columns_total` | Total count of reconstructed columns | On data column kzg verification | 📝 | ✅  | ✅ | □ | ✅  | ✅  |
| `beacon_data_availability_reconstruction_time_seconds` | Time taken to reconstruct columns | On data column kzg verification | 📝 | ✅  | ✅ | □ | ✅  | ✅ |
| `beacon_data_column_sidecar_computation_seconds` | Time taken to compute data column sidecar, including cells, proofs and inclusion proof | On data column sidecar computation | 📝 | ✅ | ✅ | ✅ | ✅ | ✅ |
| `beacon_data_column_sidecar_inclusion_proof_verification_seconds` | Time taken to verify data column sidecar inclusion proof | On data column sidecar inclusion proof verification | 📝 | ✅ | ✅ | ✅ | ✅ | ✅ |
| `beacon_kzg_verification_data_column_batch_seconds` | Runtime of batched data column kzg verification | On batched data column kzg verification | 📝 | ✅ | ✅ | ✅ | ✅ | ✅ |

### Network

#### Gossip

| Metric | Usage | Sample collection event | Grandine | Lighthouse | Lodestar | Nimbus | Prysm | Teku |
|--------|-------|-------------------------|----------|------------|----------|--------|-------|------|
| `beacon_data_column_sidecar_processing_requests_total` | Number of data column sidecars submitted for processing | On data column sidecar gossip verification | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| `beacon_data_column_sidecar_processing_successes_total` | Number of data column sidecars verified for gossip | On data column sidecar gossip verification | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| `beacon_data_column_sidecar_gossip_verification_seconds` | Full runtime of data column sidecars gossip verification | On data column sidecar gossip verification | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |

#### Req/resp

### Sync

| Metric | Type | Usage | Sample collection event | Grandine | Lighthouse | Lodestar | Nimbus | Prysm | Teku |
|--------|-------|-------|-------------------------|----------|------------|----------|--------|-------|------|
| `beacon_custody_groups` | Gauge | Total number of custody groups within a node | On updating custody group count | □ | □ | ✅ | □ | □ | ✅ |
| `beacon_custody_groups_backfilled` | Gauge | Total number of custody groups backfilled by a node | On syncing | □ | □ | □ | □ | □ | ✅ |

### Engine API

| Metric | Usage | Sample collection event | Grandine | Lighthouse | Lodestar | Nimbus | Prysm | Teku |
|--------|-------|-------------------------|----------|------------|----------|--------|-------|------|
| `beacon_engine_getBlobsV2_requests_total` | Total number of `engine_getBlobsV2` requests sent | On sending `engine_getBlobsV2` requests | □ | □ | ✅ | □ | □ | ✅ |
| `beacon_engine_getBlobsV2_responses_total` | Total number of `engine_getBlobsV2` successful responses received | On receiving `engine_getBlobsV2` responses | □ | □ | ✅ | □ | □ | ✅ |
| `beacon_engine_getBlobsV2_request_duration_seconds` | Duration of `engine_getBlobsV2` requests | On `engine_getBlobsV2` request completion | □ | □ | ✅ | □ | □ | ✅ |


**Legend**: Implementation Status
✅ - implemented
📝 - in progress, requiring adjustments
□ - not implemented

## Dashboards
- [Ethereum Package dashboard (Kurtosis)](https://github.com/ethpandaops/ethereum-package/blob/main/static_files/grafana-config/dashboards/peerdas-dashboard.json)

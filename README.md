# Ethereum Consensus Layer Metrics Repository (aka Beacon Metrics)

## Repository Purpose
This repository tracks and standardizes metrics for the Ethereum Consensus Layer (CL) beacon nodes, with a focus on Prometheus-compatible metrics to monitor protocol performance, network health, and upgrade readiness. Metrics are essential for client teams to ensure interoperability, facilitate testing, identify bottlenecks, and support research into early EIP implementations (e.g., for features like PeerDAS, shorter slots, zkEVM, EL pairing, and performance networking).  

This repository was originally created in August 2021 ahead of The Merge to propose a set of informative Prometheus metrics for beacon chain clients, including minimal interop metrics (e.g., libp2p_peers, beacon_head_slot) and additional proposals. See [metrics.md](metrics.md) for the original specification, which remains informative and non-mandatory. We are building on this foundation by standardizing metrics across clients, organizing them by protocol upgrades (hard forks and EIPs), and tracking implementation progress to enhance interoperability and testing.

- **Standardization Effort**: We are unifying metrics across CL clients and EL clients, starting with PeerDAS (EIP-7594) as part of the Fusaka upgrade. This includes a common set of significant metrics and standardized naming conventions for consistency. Clients are encouraged to implement these and track progress via linked issues/PRs.  
- **Link to Companion Repo**: For Execution Layer (EL) metrics, visit [ethereum/execution-metrics](https://github.com/ethereum/execution-metrics).  
- **Relationship to Ethereum Upgrades**: Metrics are organized by hard forks and EIPs, enabling targeted tracking for protocol changes. The primary goal is interoperability and better testing, not client benchmarking.  
- **Dashboards and Tooling**: Use [EthPandaOps](https://github.com/ethpandaops) for visualizations, including PeerDAS dashboards. Tools like [Xatu](https://github.com/ethpandaops/xatu) or [ethereum-metrics-exporter](https://github.com/ethpandaops/ethereum-metrics-exporter) can unify metrics from JSON-RPC/Beacon API, but native Prometheus metrics provide granular, feature-specific data.

## How Client Teams Should Use This Repository
To contribute to metric standardization and tracking:

- **Review and/or Propose**: Review the proposed metrics in the relevant hard fork/EIP files and/or submit proposed metrics.
- **Implement Standardized Metrics**: Implement the metrics in your client codebase, ensuring they align with the standardized names, types, and units.
- **Track Implementation**: Open a tracking issue in your client's repository to monitor implementation progress (e.g., "Implement PeerDAS metrics from beacon-metrics repo").
- **Update Implementation Status**: Update the implementation status in the relevant EIP metrics files in this repository via a PR (e.g., change status to ✅ implemented, 📝 in progress, or □ not implemented). Client teams are encouraged to open these PRs directly as progress is made.

## Hard Fork Index Table

| Fork | Epoch | Status | EIPs (SFI'd) | EIPs with Metrics |
|------|-------|--------|--------------| ------------------|
| [Fusaka (Fulu CL)](fusaka/fusaka-cl-index.md) | TBD (Late 2025) | 🚧 Testing | 13 EIPs | 1 EIP |
| Glamsterdam (Gloas CL) | TBD | 📋 Planning | TBD | TBD |

## Metric Types
Metrics in this repository (on each EIP page) are organized in tables grouped by Metric Type (e.g., Counters, Histograms, Gauges) for clarity and to align with Prometheus/OpenMetrics standards. For full details, refer to the [OpenMetrics specification](https://prometheus.io/docs/specs/om/open_metrics_spec/#metric-types).

| Type           | Description                                                                 |
|----------------|-----------------------------------------------------------------------------|
| Gauge          | Current measurements, such as bytes of memory used or items in a queue, where the absolute value is of interest. |
| Counter        | Measures discrete events, such as HTTP requests received, with focus on how quickly the value increases over time. |
| StateSet       | Represents a series of related boolean values, suitable for encoding ENUMs with multiple states that change over time. |
| Info           | Exposes textual information that should not change during process lifetime, such as application version or compiler version. |
| Histogram      | Measures distributions of discrete events, such as request latencies, with cumulative buckets and sum values. |
| GaugeHistogram | Measures current distributions, such as queue wait times, with buckets and sum values treated as gauges. |
| Summary        | Measures distributions of discrete events, used when histograms are too expensive, with count, sum, and quantiles. |
| Unknown        | Used when it is impossible to determine the types of individual metrics from 3rd party systems, with a single value. |

## License

All code and generated test vectors are public domain under [CC0](https://creativecommons.org/publicdomain/zero/1.0/).
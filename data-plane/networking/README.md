# East/west networking

[K8s-netperf](https://github.com/cloud-bulldozer/k8s-netperf) is the tool we use to orchestrate the east-west network load tests. Its execution is orchestrated by the e2e-benchmarking wrapper, network-perf-v2 using the configuration described in sm-run.yaml that orchestrates a netperf based workload in different scenarios and configurations.

Scenarios:

The test scenarios are very similar to the ones executed in regular OpenShift (baseline) using the default CNI plugin OVNKubernetes. The intention of this is to evaluate the impact of OpenShift Service Mesh by doing a baseline comparison.

Pod 2 service:

- TCP_STREAM: The stream scenarios are meant to benchmark TCP network throughput using different packet sizes
  - Message sizes: 64, 4096 and 8192
  - Streams: 1 and 2
- TCP_RR. Request/response test meant to benchmark TCP network latency
  - Message sizes: 1024

Run the test:
* OSSM in sidecar mode: `MESH_MODE=sidecar ./run.sh sm-mtls.yml`
* OSSM in ambient mode: `MESH_MODE=ambient ./run.sh sm-mtls.yml`
* OSSM in ambient mode with Waypoint: `MESH_MODE=ambient WAYPOINT=true ./run.sh sm-mtls.yml`

## Considerations

pod 2 pod fails with mTLS: https://github.com/istio/istio/issues/37431

